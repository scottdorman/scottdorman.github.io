---
layout: post
title: Porting an NAnt Task to MSBuild
date: 1/9/2008 9:37:05 AM
---

I have been working and talking a lot about MSBuild over the last few months. As part of that work, I have implemented several custom tasks for MSBuild. Most of those tasks were ones that I had written as part of an NAnt based build system while others were part of the NAntContrib project. There is a very good basic explanation of how to write a task on [MSDN](http://msdn2.microsoft.com/en-us/library/t9883dzc.aspx), so instead I will cover how to port a task from NAnt to MSBuild. To keep things simple, I'm going to focus on creating an MSBuild v3.5 task in C#.

The first step is to create a new C# .NET Framework 3.5 based Class Library. You then need to add the following references:

*   Microsoft.Build.Framework  
*   Microsoft.Build.Utilities.v3.5 

Once you do that, you can create a new class file for the new MSBuild task. After the class is created, you need to add the using statements for the MSBuild namespaces:
 <div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 179px; background-color: #f4f4f4">

<span style="color: #0000ff">using</span> System;
<span style="color: #0000ff">using</span> Microsoft.Build.Framework;
<span style="color: #0000ff">using</span> Microsoft.Build.Utilities;

<span style="color: #0000ff">namespace</span> MSBuildContrib.Tasks
{
    <span style="color: #0000ff">public</span> <span style="color: #0000ff">class</span> Attrib : Task
    {
    }
}

</div>


Make sure to derive your task from [Microsoft.Build.Utilities.Task](http://msdn2.microsoft.com/ms126274.aspx "Task Class"), which is very similar to the NAnt.Core.Task class. At this point, you will encounter the first difference between the two tasks. MSBuild tasks do not use attributes like NAnt tasks, so you don't need to decorate the class with the TaskName attribute.

The minimal task implementation is to override the public Execute method. This is has a different signature than the Execute method in an NAnt task. Instead of being a void function, it returns a boolean value. The class should now look like this:

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 228px; background-color: #f4f4f4">

<span style="color: #0000ff">using</span> System;
<span style="color: #0000ff">using</span> Microsoft.Build.Framework;
<span style="color: #0000ff">using</span> Microsoft.Build.Utilities;

<span style="color: #0000ff">namespace</span> MSBuildContrib.Tasks
{
    <span style="color: #0000ff">public</span> <span style="color: #0000ff">class</span> Attrib : Task
    {
        <span style="color: #0000ff">public</span> <span style="color: #0000ff">override</span> <span style="color: #0000ff">bool</span> Execute()
        {
        }
    }
}
</div>


The boolean value returned by the Execute task informs the MSBuild engine of the tasks success or failure. If the task succeeded, you should return true; otherwise you should return false. Ideally you would want to log any exceptions that are encountered in the Execute method and return false.

The next step is to create the properties that will be available in the build script. Unlike NAnt, which requires a TaskAttribute attribute, any public property is exposed to the build script. By default, all properties are optional so if you want a required property you will need to decorate it with the Required attribute.

While the lack of attributes makes things simpler it also means that the property return values are more restricted. MSBuild supports only the basic data types: [System.Boolean](http://msdn2.microsoft.com/a28wyd50.aspx "Boolean Structure"), [System.String](http://msdn2.microsoft.com/s1wwdcbf.aspx "String Class"), and any of the numeric types [System.Int32](http://msdn2.microsoft.com/td2s409d.aspx "Int32 Structure"), [System.Int64](http://msdn2.microsoft.com/6yy583ek.aspx "Int64 Structure"), or [System.Int16](http://msdn2.microsoft.com/e07e6fds.aspx "Int16 Structure"). It's at this point that you start to see the major difference between the two, since NAnt allowed you to use any of the .NET data types.

This restriction might seem like it is too limiting at first, but so far I haven't encountered any problems with it. In fact, it's the exact opposite. To expose a collection as a return type, NAnt requires you to use a FileSet or BuildElement datatype. On the other hand, MSBuild allows you to specify these as a String or [Microsoft.Build.Framework.ITaskItem](http://msdn2.microsoft.com/ms124355.aspx "ITaskItem Interface") array.

Let's look at an example to make this a bit clearer. The NAnt AttribTask declares the following property:

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 152px; background-color: #f4f4f4">

<span style="color: #0000ff">private</span> FileSet _fileset = <span style="color: #0000ff">new</span> FileSet();

[BuildElement(<span style="color: #006080">"fileset"</span>)]
<span style="color: #0000ff">public</span> FileSet AttribFileSet 
{
    get { <span style="color: #0000ff">return</span> _fileset; }
    set { _fileset = <span style="color: #0000ff">value</span>; }
}

</div>


The corresponding property for the MSBuild Attrib task declares the property like this:

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; background-color: #f4f4f4">

<span style="color: #0000ff">private</span> ITaskItem[] inputFiles;

[Required]
<span style="color: #0000ff">public</span> ITaskItem[] InputFiles
{
    get { <span style="color: #0000ff">return</span> inputFiles; }
    set { inputFiles = <span style="color: #0000ff">value</span>; }
}

</div>


Alternatively, it could have been declared like this:

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 149px; background-color: #f4f4f4">

<span style="color: #0000ff">private</span> <span style="color: #0000ff">string</span>[] inputFiles;

[Required]
<span style="color: #0000ff">public</span> <span style="color: #0000ff">string</span>[] InputFiles
{
    get { <span style="color: #0000ff">return</span> inputFiles; }
    set { inputFiles = <span style="color: #0000ff">value</span>; }
}

</div>


The only difference between these two declarations is that by using an ITaskItem array, you gain access to the additional [item metadata](http://msdn2.microsoft.com/en-us/library/ms164313.aspx) that MSBuild makes available. If you don't need that metadata, declaring this as a string array is just fine.

The benefit to using arrays is that MSBuild will implicitly convert a semi-colon delimited list to the array. This means that you can call the task like this:

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 42px; background-color: #f4f4f4">

<span style="color: #0000ff"><</span><span style="color: #800000">Attrib</span> <span style="color: #ff0000">InputFiles</span><span style="color: #0000ff">="File1.txt;File2.txt;File3.txt;File4.txt"</span> <span style="color: #0000ff">/></span>
</div>


And be able to iterate over the list of files using a foreach or a for loop:

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 88px; background-color: #f4f4f4">

<span style="color: #0000ff">for</span> (<span style="color: #0000ff">int</span> i = 0; i < <span style="color: #0000ff">this</span>.inputFiles.Length; i++)
{
    <span style="color: #008000">// Do something with each file.</span>
}
</div>


For NAnt properties that were returning a [System.IO.FileInfo](http://msdn2.microsoft.com/akth6b1k.aspx "FileInfo Class") or [System.IO.DirectoryInfo](http://msdn2.microsoft.com/8s2fzb02.aspx "DirectoryInfo Class") you can return a String or ITaskItem. Again, the only difference between declaring the property with an ITaskItem return type is that you gain access to the additional item metadata.

The other difference for properties is that MSBuild does not include equivalents for NAnt's validator attributes. If you need to validate the property input you must do so in the property setter or the Execute method.

At this point, the class should look like this:

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 411px; background-color: #f4f4f4">

<span style="color: #0000ff">using</span> System;
<span style="color: #0000ff">using</span> Microsoft.Build.Framework;
<span style="color: #0000ff">using</span> Microsoft.Build.Utilities;

<span style="color: #0000ff">namespace</span> MSBuildContrib.Tasks
{
    <span style="color: #0000ff">public</span> <span style="color: #0000ff">class</span> Attrib : Task
    {
        <span style="color: #0000ff">private</span> ITaskItem[] inputFiles;

        [Required]
        <span style="color: #0000ff">public</span> ITaskItem[] InputFiles
        {
            get { <span style="color: #0000ff">return</span> inputFiles; }
            set { inputFiles = <span style="color: #0000ff">value</span>; }
        }

        <span style="color: #0000ff">public</span> <span style="color: #0000ff">override</span> <span style="color: #0000ff">bool</span> Execute()
        {
            <span style="color: #0000ff">bool</span> flag = <span style="color: #0000ff">true</span>;
            <span style="color: #0000ff">return</span> flag;
        }
    }
}

</div>


We are now ready to actually implement the Execute method. As I mentioned earlier, you generally want to try and minimize the exceptions that are thrown during the task execution and instead just log them as errors. If we take this into consideration when implementing the Execute method, we end up with a method that looks like this:

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 221px; background-color: #f4f4f4">

<span style="color: #0000ff">public</span> <span style="color: #0000ff">override</span> <span style="color: #0000ff">bool</span> Execute()
{
    <span style="color: #0000ff">bool</span> flag = <span style="color: #0000ff">true</span>;
 
    <span style="color: #0000ff">for</span> (<span style="color: #0000ff">int</span> i = 0; i < <span style="color: #0000ff">this</span>.inputFiles.Length; i++)
    {
        flag &= <span style="color: #0000ff">this</span>.UpdateAttributes(<span style="color: #0000ff">this</span>.inputFiles[i].ItemSpec);
    }   

    <span style="color: #0000ff">return</span> flag;
}

</div>


This brings us to another difference between MSBuild and NAnt: logging task errors and messages. Unfortunately, this is an area that I think NAnt still does a considerably better job of doing. In NAnt, each task has a verbose property that controls the level of detail that is to be reported during task execution. Going beyond that, the logging levels are independent of the verbosity since the levels determine the type of message logged. MSBuild does not have a similar concept of verbosity at the task level, and the logging levels in MSBuild are actually verbosity levels and are tied to the /verbose command line switch. You also don't have a built-in exception that can be thrown, like the NAnt BuildException. Instead, you can either throw the exception or log it as a failure.

To see this in action, lets look at the UpdateAttributes method:

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 419px; background-color: #f4f4f4">

<span style="color: #0000ff">private</span> <span style="color: #0000ff">bool</span> UpdateAttributes(<span style="color: #0000ff">string</span> path)
{
    <span style="color: #0000ff">bool</span> flag = <span style="color: #0000ff">true</span>;

    <span style="color: #0000ff">try</span>
    {
        <span style="color: #008000">// Change the attributes</span>
        Log.LogMessage(MessageImportance.Normal, <span style="color: #006080">"Attributs changed for {0}."</span>, path);
    }
    <span style="color: #0000ff">catch</span> (IOException ex)
    {
        Log.LogError(<span style="color: #006080">"Failed to change attributes for {0}. {1}"</span>, path, ex.Message);
        flag = <span style="color: #0000ff">false</span>;
    }
    <span style="color: #0000ff">catch</span> (Exception ex)
    {
        <span style="color: #0000ff">if</span> (ExceptionHandling.NotExpectedException(ex))
        {
            <span style="color: #0000ff">throw</span>;
        }
        Log.LogError(<span style="color: #006080">"Failed to change attributes for {0}. {1}"</span>, path, ex.Message);
        flag = <span style="color: #0000ff">false</span>;
    }
    <span style="color: #0000ff">return</span> flag;
} 
</div>


One of the nice features that NAnt tasks provided was the ability to set properties from within the task. MSBuild tasks don't allow you to do this, but you can create output properties. These output properties are captured in an Output element declared in the build script. It accomplishes the same thing with just a little bit of extra work. It also has the added benefit of not creating global properties that aren't used...just because the task declares an output property does not require it to be captured in the build script. Declaring an output property is as simple as decorating it with the Output attribute. The attribute name is a little misleading, however, since these properties are actually bi-directional. That is, a property decorated with an Output attribute can also be used as input. If you do create output properties, they should be set to a valid value by the time the Execute method completes.

To put all of this together in a simple to follow list:

*   MSBuild tasks do not use attributes to declare the task or the properties that are available to the build script. 

*   Properties can only be the following data types: 


    *   [System.Boolean](http://msdn2.microsoft.com/a28wyd50.aspx "Boolean Structure") 

    *   [System.String](http://msdn2.microsoft.com/s1wwdcbf.aspx "String Class") or [System.String](http://msdn2.microsoft.com/s1wwdcbf.aspx "String Class")[] 

    *   Any of the numeric types [System.Int32](http://msdn2.microsoft.com/td2s409d.aspx "Int32 Structure"), [System.Int64](http://msdn2.microsoft.com/6yy583ek.aspx "Int64 Structure"), or [System.Int16](http://msdn2.microsoft.com/e07e6fds.aspx "Int16 Structure") 

    *   [Microsoft.Build.Framework.ITaskItem](http://msdn2.microsoft.com/ms124355.aspx "ITaskItem Interface") or [Microsoft.Build.Framework.ITaskItem](http://msdn2.microsoft.com/ms124355.aspx "ITaskItem Interface")[]

*   Required properties are marked with the single Required attribute. 

*   Tasks cannot set project properties directly, instead you must declare a property and decorate it with the Output attribute. 

*   Task logging is different (and not as flexible). 

*   There is not an equivalent to the BuildException exception, instead just throw a normal .NET exception. 

*   The Execute method returns a boolean indicating the task success or failure.


The complete source code for the MSBuild Attrib task can be found in the [MSBuildContrib](http://www.codeplex.com/MSBuildContrib) project on CodePlex.
