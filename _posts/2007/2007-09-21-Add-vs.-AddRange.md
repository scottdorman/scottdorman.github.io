---
layout: post
title: Add vs. AddRange
date: '2007-09-21 16:55:41 -05:00'
---

It was recently pointed out to me that not many developers are familiar with the [TreeNodeCollection.AddRange](http://msdn2.microsoft.com/w2s56wzs.aspx) method and how it differs from the [TreeNodeCollection.Add](http://msdn2.microsoft.com/bc9ezxke.aspx) method. Even though I am focusing specifically on the methods available through the [TreeNodeCollection](http://msdn2.microsoft.com/2667e4k1.aspx), exposed by the [TreeView.Nodes](http://msdn2.microsoft.com/3xx805ek.aspx) property, the concepts apply equally to any of the collections that expose both an Add and an AddRange method.

Looking at the MSDN documentation, [AddRange](http://msdn2.microsoft.com/w2s56wzs.aspx) "*adds an array of previously created tree nodes to the collection*" while [Add](http://msdn2.microsoft.com/bc9ezxke.aspx) "*adds a new tree node to the collection*". Continuing to look at the documentation, you will notice that [AddRange](http://msdn2.microsoft.com/w2s56wzs.aspx) can be used to "*quickly add a group of previously created [TreeNode](http://msdn2.microsoft.com/bctbxtcb.aspx) objects to the collection instead of manually adding each [TreeNode](http://msdn2.microsoft.com/bctbxtcb.aspx) to the collection using the [Add](http://msdn2.microsoft.com/bc9ezxke.aspx) method.*"

At this point, you might be asking yourself what the difference is since these definitions sounds pretty similar. If you're thoroughly confused by now, don't feel bad. The explanations given in the documentation do sound very similar and don't do an adequate job of explaining the differences between them.

The simple answer is this:

> If you are only adding a small number of nodes or adding nodes infrequently, use the [Add](http://msdn2.microsoft.com/bc9ezxke.aspx) method. However, if you need to add a large number of nodes at one time you should use [AddRange](http://msdn2.microsoft.com/w2s56wzs.aspx).

The .NET Framework was designed to provide good performance under a wide variety of situations. However, it isn't always clear how **our** design choices can impact that performance. This is one of those cases.

For example, take the process of initializing a [TreeView](http://msdn2.microsoft.com/sc9ba94b.aspx). Normally, you would create the [TreeNode](http://msdn2.microsoft.com/bctbxtcb.aspx) objects inside some sort of a loop and add each node to the tree when it was created. The following sample, although somewhat arbitrary, shows how you might accomplish this:
 
```csharp
TreeNode root = new TreeNode("Root"); 
for (int i = 0; i <= 5000; i++)
{                
    TreeNode childNode = new TreeNode("Child" + i.ToString());
    mainNode.Nodes.Add(childNode);
} 
```

This is valid code and will compile and run without any problems. However, you are causing the .NET runtime to do a lot more work than it needs to. Using [Reflector](http://www.aisto.com/roeder/dotnet/), we can see what actually ends up happening by looking at the code for the relevant [Add](http://msdn2.microsoft.com/bc9ezxke.aspx) methods:

```csharp
public virtual TreeNode Add(string text)
{
    TreeNode node = new TreeNode(text);
    this.Add(node);
    return node;
}
 
public virtual int Add(TreeNode node)
{
    return this.AddInternal(node, 0);
}
```


Now, lets take a look at the code for the [AddRange](http://msdn2.microsoft.com/w2s56wzs.aspx) method:

```csharp
public virtual void AddRange(TreeNode[] nodes)
{
    if (nodes == null)
    {
        throw new ArgumentNullException("nodes");
    }
    if (nodes.Length != 0)
    {
        TreeView treeView = this.owner.TreeView;
        if ((treeView != null) && (nodes.Length > 200))
        {
            treeView.BeginUpdate();
        }
        this.owner.Nodes.FixedIndex = this.owner.childCount;
        this.owner.EnsureCapacity(nodes.Length);
        for (int i = nodes.Length - 1; i >= 0; i--)
        {
            this.AddInternal(nodes[i], i);
        }
        this.owner.Nodes.FixedIndex = -1;
        if ((treeView != null) && (nodes.Length > 200))
        {
            treeView.EndUpdate();
        }
    }
}
```

As you can see, there is a lot more going on here. If we ignore the parameter validation we can see that the following steps are performed:

1.  A call to [TreeView.BeginUpdate](http://msdn2.microsoft.com/en-us/library/system.windows.forms.treeview.beginupdate.aspx) is made if the *nodes* array is larger than 200 items. 
2.  The FixedIndex internal property is set to the value of childCount. This is really the index of the last node in the collection. 
3.  A call to EnsureCapacity is made, which makes sure that the internal array used to hold the nodes is large enough to hold the array passed in. 
4.  The passed in array is looped through, calling AddInternal for each node in the *nodes* array. The key difference here is the integer parameter to AddInternal is the index of the node rather than 0. 
5.  The FixedIndex internal property is set to -1, which is the default value. 
6.  A call to [TreeView.EndUpdate](http://msdn2.microsoft.com/en-us/library/system.windows.forms.treeview.endupdate.aspx) is mad if the *nodes* array is larger than 200 items.

These 6 steps can be split up into two groups, with steps 1 and 6 making up one group and steps 2 - 5 making up the other group.

Steps 1 and 6 are calls to [TreeView.BeginUpdate](http://msdn2.microsoft.com/en-us/library/system.windows.forms.treeview.beginupdate.aspx) and [TreeView.EndUpdate](http://msdn2.microsoft.com/en-us/library/system.windows.forms.treeview.endupdate.aspx), respectively, and will only be called if the *nodes* array is larger than 200 objects. Because these methods will be called for you automatically, there is no need to call them yourself if you are adding more than 200 nodes. Adding less than 200 nodes, doesn't actually need the benefit provided by these calls, so you don't need them. (It shouldn't hurt the performance if you call them, but they aren't necessary). Just in case you are wondering, the [TreeView.BeginUpdate](http://msdn2.microsoft.com/en-us/library/system.windows.forms.treeview.beginupdate.aspx) call prevents the control from painting until the [TreeView.EndUpdate](http://msdn2.microsoft.com/en-us/library/system.windows.forms.treeview.endupdate.aspx) method is called. 

The second group (steps 2 - 5) are really what provide the performance improvements and are concerned with the call to AddInternal and setting the FixedIndex property. If we examine the relevant section of AddInternal, we see the following code:

```csharp
private int AddInternal(TreeNode node, int delta)
{
    ...
    node.parent = this.owner;
    int fixedIndex = this.owner.Nodes.FixedIndex;
    if (fixedIndex != -1)
    {
        node.index = fixedIndex + delta;
    }
    else
    {
        this.owner.EnsureCapacity(1);
        node.index = this.owner.childCount;
    }
    this.owner.children[node.index] = node;
    this.owner.childCount++;
    ...
    return node.index;
}
```

As we can see, AddInternal uses the FixedIndex property to decide if it should call EnsureCapacity. Looking back at the steps in the [AddRange](http://msdn2.microsoft.com/w2s56wzs.aspx) method, you should notice that EnsureCapacity has already called. You may also remember that it wasn't called by any of the [Add](http://msdn2.microsoft.com/bc9ezxke.aspx) methods.

Since [AddRange](http://msdn2.microsoft.com/w2s56wzs.aspx) sets the FixedIndex property, the index of *node* is set to FixedIndex + *delta* and then added to the internal array. However, if FixedIndex is -1 (which is the default), a call to EnsureCapacity(1) is made and then the index of *node* is set to the value of childCount. It is this call to EnsureCapacity(1) that is the key. By passing in a 1, EnsureCapacity is told to double the size of the internal array used to hold the nodes.

So, the bottom line is that each time you call [Add](http://msdn2.microsoft.com/bc9ezxke.aspx), you are doubling the size of the internal array. When you call [AddRange](http://msdn2.microsoft.com/w2s56wzs.aspx), you expand the internal array just enough to hold the additional nodes. In some cases, both methods may perform about the same but, on average, the call to [AddRange](http://msdn2.microsoft.com/w2s56wzs.aspx) will provide better performance when adding a large number of nodes.

One last thing to note about performance, which really has nothing to do with calling [Add](http://msdn2.microsoft.com/bc9ezxke.aspx) or [AddRange](http://msdn2.microsoft.com/w2s56wzs.aspx). If you set the [TreeViewNodeSorter](http://msdn2.microsoft.com/en-us/library/system.windows.forms.treeview.treeviewnodesorter.aspx) property of the [TreeView](http://msdn2.microsoft.com/sc9ba94b.aspx), each time you add a new node the tree will be resorted. Normally, this is acceptable behavior. However, if you are adding a large number of nodes (using either [Add](http://msdn2.microsoft.com/bc9ezxke.aspx) or [AddRange](http://msdn2.microsoft.com/w2s56wzs.aspx)), you should follow these steps:

1.  Make a temporary copy of the value of the [TreeViewNodeSorter](http://msdn2.microsoft.com/en-us/library/system.windows.forms.treeview.treeviewnodesorter.aspx) property.
2.  Set the [TreeViewNodeSorter](http://msdn2.microsoft.com/en-us/library/system.windows.forms.treeview.treeviewnodesorter.aspx) property to *null*.
3.  Add the nodes (using either [Add](http://msdn2.microsoft.com/bc9ezxke.aspx "Add Method") or [AddRange](http://msdn2.microsoft.com/w2s56wzs.aspx "AddRange Method")).
4.  Set the [TreeViewNodeSorter](http://msdn2.microsoft.com/en-us/library/system.windows.forms.treeview.treeviewnodesorter.aspx) property back to original value.

You also don't need to call the [Sort](http://msdn2.microsoft.com/en-us/library/system.windows.forms.treeview.sort.aspx) method after you set the [TreeViewNodeSorter](http://msdn2.microsoft.com/en-us/library/system.windows.forms.treeview.treeviewnodesorter.aspx) property, since that is done for you when you set the property. This is actually true of most of the Sorter related properties on the Windows Forms controls. When you are adding a large amount of items to the control, set the sorter to null first, add the items, and then set the sorter back to the original value causing the appropriate Sort method to be called.
