---
layout: post
title: Data Binding an Enum with Descriptions
date: 2007-08-02 00:21:25 -05:00
---

Every once in a while I need to bind an enumerated type to a Windows Forms control, usually a ComboBox. 

The simplest is to use the <font face="Consolas" size="2">Enum.GetValues()</font> method, setting its result to the <font face="Consolas" size="2">DataSource</font> property of the ComboBox. If you have the following enum:
 <div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 147px; background-color: #f4f4f4"> <div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">

<span style="color: #606060">   1:</span> <span style="color: #0000ff">public</span> <span style="color: #0000ff">enum</span> SimpleEnum

<span style="color: #606060">   2:</span> {

<span style="color: #606060">   3:</span>    Today,

<span style="color: #606060">   4:</span>    Last7

<span style="color: #606060">   5:</span>    Last14,

<span style="color: #606060">   6:</span>    Last30,

<span style="color: #606060">   7:</span>    All

<span style="color: #606060">   8:</span> }
</div></div>


You can bind it to a ComboBox like this:

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 50px; background-color: #f4f4f4">
<div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">

<span style="color: #606060">   1:</span> ComboBox combo = <span style="color: #0000ff">new</span> ComboBox();

<span style="color: #606060">   2:</span> combo.DataSource = Enum.GetValues(<span style="color: #0000ff">typeof</span>(SimpleEnum));
</div></div>


While this does work, there are a couple of problems with this:

1.  There is no support for localization. 

2.  There is no support for more readable descriptions.


If you want to support one or both of these requirements, it can start to get complicated. The complication comes in the form of numerous different ways to accomplish the same thing. These range from custom type descriptors, to generic (and non-generic) "details" classes, to hard-coded string resource lookups, and many others.

The majority of the articles and techniques I have seen all attempt to solve the simple problem of data binding an enum to a ComboBox while displaying a human readable string as the ComboBox display string. Overall, there isn't anything wrong with these approaches and they all have pros and cons. However, they are generally more complicated than necessary and, in some cases, require a lot of work on either the developer implementing the enum, the developer using it, or both.

The easiest way to accomplish this is actually using a little bit of Reflection and decorating the enum values with an attribute. You don't need generics, custom classes, or custom type descriptors...just two static methods that are both less than 10 lines of code.

The first step is to add a description attribute to your enum. For simplicity, you can use the <font face="Consolas" size="2">System.ComponentModel.DescriptionAttribute</font> class, but I would recommend deriving your own <font face="Consolas" size="2">EnumDescriptionAttribute</font>.

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 600px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 518px; background-color: #f4f4f4">
<div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">

<span style="color: #606060">   1:</span> <span style="color: #008000">/// <summary></span>

<span style="color: #606060">   2:</span> <span style="color: #008000">/// Provides a description for an enumerated type.</span>

<span style="color: #606060">   3:</span> <span style="color: #008000">/// </summary></span>

<span style="color: #606060">   4:</span> [AttributeUsage(AttributeTargets.Enum | AttributeTargets.Field, AllowMultiple = <span style="color: #0000ff">false</span>)]

<span style="color: #606060">   5:</span> <span style="color: #0000ff">public</span> <span style="color: #0000ff">sealed</span> <span style="color: #0000ff">class</span> EnumDescriptionAttribute :  Attribute

<span style="color: #606060">   6:</span> {

<span style="color: #606060">   7:</span>     <span style="color: #0000ff">private</span> <span style="color: #0000ff">string</span> description;

<span style="color: #606060">   8:</span>  

<span style="color: #606060">   9:</span>     <span style="color: #008000">/// <summary></span>

<span style="color: #606060">  10:</span>     <span style="color: #008000">/// Gets the description stored in this attribute.</span>

<span style="color: #606060">  11:</span>     <span style="color: #008000">/// </summary></span>

<span style="color: #606060">  12:</span>     <span style="color: #008000">/// <value>The description stored in the attribute.</value></span>

<span style="color: #606060">  13:</span>     <span style="color: #0000ff">public</span> <span style="color: #0000ff">string</span> Description

<span style="color: #606060">  14:</span>     {

<span style="color: #606060">  15:</span>         get

<span style="color: #606060">  16:</span>         {

<span style="color: #606060">  17:</span>             <span style="color: #0000ff">return</span> <span style="color: #0000ff">this</span>.description;

<span style="color: #606060">  18:</span>         }

<span style="color: #606060">  19:</span>     }

<span style="color: #606060">  20:</span>  

<span style="color: #606060">  21:</span>     <span style="color: #008000">/// <summary></span>

<span style="color: #606060">  22:</span>     <span style="color: #008000">/// Initializes a new instance of the </span>

<span style="color: #606060">  23:</span>     <span style="color: #008000">/// <see cref="EnumDescriptionAttribute"/> class.</span>

<span style="color: #606060">  24:</span>     <span style="color: #008000">/// </summary></span>

<span style="color: #606060">  25:</span>     <span style="color: #008000">/// <param name="description">The description to store in this attribute.</param></span>

<span style="color: #606060">  26:</span>     <span style="color: #0000ff">public</span> EnumDescriptionAttribute(<span style="color: #0000ff">string</span> description)

<span style="color: #606060">  27:</span>         : <span style="color: #0000ff">base</span>()

<span style="color: #606060">  28:</span>     {

<span style="color: #606060">  29:</span>         <span style="color: #0000ff">this</span>.description = description;

<span style="color: #606060">  30:</span>     }

<span style="color: #606060">  31:</span> }
</div></div>


Now that we have our description attribute, we need to decorate the enum with it:

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 400px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 292px; background-color: #f4f4f4">
<div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">

<span style="color: #606060">   1:</span> <span style="color: #0000ff">public</span> <span style="color: #0000ff">enum</span> SimpleEnum

<span style="color: #606060">   2:</span> {

<span style="color: #606060">   3:</span>    [EnumDescription(<span style="color: #006080">"Today"</span>)]

<span style="color: #606060">   4:</span>    Today,

<span style="color: #606060">   5:</span>  

<span style="color: #606060">   6:</span>    [EnumDescription(<span style="color: #006080">"Last 7 days"</span>)]

<span style="color: #606060">   7:</span>    Last7,

<span style="color: #606060">   8:</span>  

<span style="color: #606060">   9:</span>    [EnumDescription(<span style="color: #006080">"Last 14 days"</span>)]

<span style="color: #606060">  10:</span>    Last14,

<span style="color: #606060">  11:</span>  

<span style="color: #606060">  12:</span>    [EnumDescription(<span style="color: #006080">"Last 30 days"</span>)]

<span style="color: #606060">  13:</span>    Last30,

<span style="color: #606060">  14:</span>  

<span style="color: #606060">  15:</span>    [EnumDescription(<span style="color: #006080">"All"</span>)]

<span style="color: #606060">  16:</span>    All

<span style="color: #606060">  17:</span> }
</div></div>


Using a custom attribute allows you to keep the human readable description in the code where the enum is defined. It also allows you to retrieve localized versions of the description. In order to do that, you simply need to change the way the attribute works to lookup the appropriate string in the string resources.

The next part is what actually does all of the work. As I mentioned, both of these functions are less than 10 lines of code. The easiest way to work with these functions is to create a static (or sealed, if you aren't using .NET 2.0 or later) class that holds these two static functions.

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 1000px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 838px; background-color: #f4f4f4">
<div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">

<span style="color: #606060">   1:</span> <span style="color: #008000">/// <summary></span>

<span style="color: #606060">   2:</span> <span style="color: #008000">/// Provides a static utility object of methods and properties to interact with enumerated types. </span>

<span style="color: #606060">   3:</span> <span style="color: #008000">/// </summary></span>

<span style="color: #606060">   4:</span> <span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">class</span> EnumHelper

<span style="color: #606060">   5:</span> {

<span style="color: #606060">   6:</span>    <span style="color: #008000">/// <summary></span>

<span style="color: #606060">   7:</span>    <span style="color: #008000">/// Gets the <see cref="DescriptionAttribute"/> of an <see cref="Enum"/> type value.</span>

<span style="color: #606060">   8:</span>    <span style="color: #008000">/// </summary></span>

<span style="color: #606060">   9:</span>    <span style="color: #008000">/// <param name="value">The <see cref="Enum"/> type value.</param></span>

<span style="color: #606060">  10:</span>    <span style="color: #008000">/// <returns>A string containing the text of the <see cref="DescriptionAttribute"/>.</returns></span>

<span style="color: #606060">  11:</span>    <span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> <span style="color: #0000ff">string</span> GetDescription(Enum <span style="color: #0000ff">value</span>)

<span style="color: #606060">  12:</span>    {

<span style="color: #606060">  13:</span>       <span style="color: #0000ff">if</span> (<span style="color: #0000ff">value</span> == <span style="color: #0000ff">null</span>)

<span style="color: #606060">  14:</span>       {

<span style="color: #606060">  15:</span>          <span style="color: #0000ff">throw</span> <span style="color: #0000ff">new</span> ArgumentNullException(<span style="color: #006080">"value"</span>);

<span style="color: #606060">  16:</span>       }

<span style="color: #606060">  17:</span>  

<span style="color: #606060">  18:</span>       <span style="color: #0000ff">string</span> description = <span style="color: #0000ff">value</span>.ToString();

<span style="color: #606060">  19:</span>       FieldInfo fieldInfo = <span style="color: #0000ff">value</span>.GetType().GetField(description);

<span style="color: #606060">  20:</span>       EnumDescriptionAttribute[] attributes = (EnumDescriptionAttribute[])fieldInfo.GetCustomAttributes(<span style="color: #0000ff">typeof</span>(EnumDescriptionAttribute), <span style="color: #0000ff">false</span>);

<span style="color: #606060">  21:</span>  

<span style="color: #606060">  22:</span>       <span style="color: #0000ff">if</span> (attributes != <span style="color: #0000ff">null</span> && attributes.Length > 0)

<span style="color: #606060">  23:</span>       {

<span style="color: #606060">  24:</span>          description = attributes[0].Description;

<span style="color: #606060">  25:</span>       }

<span style="color: #606060">  26:</span>       <span style="color: #0000ff">return</span> description;

<span style="color: #606060">  27:</span>    }

<span style="color: #606060">  28:</span>  

<span style="color: #606060">  29:</span>    <span style="color: #008000">/// <summary></span>

<span style="color: #606060">  30:</span>    <span style="color: #008000">/// Converts the <see cref="Enum"/> type to an <see cref="IList"/> compatible object.</span>

<span style="color: #606060">  31:</span>    <span style="color: #008000">/// </summary></span>

<span style="color: #606060">  32:</span>    <span style="color: #008000">/// <param name="type">The <see cref="Enum"/> type.</param></span>

<span style="color: #606060">  33:</span>    <span style="color: #008000">/// <returns>An <see cref="IList"/> containing the enumerated type value and description.</returns></span>

<span style="color: #606060">  34:</span>    <span style="color: #0000ff">public</span> <span style="color: #0000ff">static</span> IList ToList(Type type)

<span style="color: #606060">  35:</span>    {

<span style="color: #606060">  36:</span>       <span style="color: #0000ff">if</span> (type == <span style="color: #0000ff">null</span>)

<span style="color: #606060">  37:</span>       {

<span style="color: #606060">  38:</span>          <span style="color: #0000ff">throw</span> <span style="color: #0000ff">new</span> ArgumentNullException(<span style="color: #006080">"type"</span>);

<span style="color: #606060">  39:</span>       }

<span style="color: #606060">  40:</span>  

<span style="color: #606060">  41:</span>       ArrayList list = <span style="color: #0000ff">new</span> ArrayList();

<span style="color: #606060">  42:</span>       Array enumValues = Enum.GetValues(type);

<span style="color: #606060">  43:</span>  

<span style="color: #606060">  44:</span>       <span style="color: #0000ff">foreach</span> (Enum <span style="color: #0000ff">value</span> <span style="color: #0000ff">in</span> enumValues)

<span style="color: #606060">  45:</span>       {

<span style="color: #606060">  46:</span>          list.Add(<span style="color: #0000ff">new</span> KeyValuePair<Enum, <span style="color: #0000ff">string</span>>(<span style="color: #0000ff">value</span>, GetDescription(<span style="color: #0000ff">value</span>)));

<span style="color: #606060">  47:</span>       }

<span style="color: #606060">  48:</span>  

<span style="color: #606060">  49:</span>       <span style="color: #0000ff">return</span> list;

<span style="color: #606060">  50:</span>    } 

<span style="color: #606060">  51:</span> }
</div></div>


As you can see, the <font face="Consolas" size="2">GetDescription</font> method uses a little bit of Reflection to retrieve the <font face="Consolas" size="2">EnumDescription</font> attribute on the specified enum value. If it doesn't find the attribute, it simply uses the value name. The <font face="Consolas" size="2">ToList</font> method returns an <font face="Consolas" size="2">IList</font> of <font face="Consolas" size="2">KeyValuePair<Enum, string></font> instances that hold the enum value (the key) and the description (the value). If you aren't using .NET 2.0 or later, you will need to use <font face="Consolas" size="2">DictionaryEntry</font> instead of <font face="Consolas" size="2">KeyValuePair<TKey, TValue></font>.

In order to bind the ComboBox, you now need to do the following:

<div style="border-right: gray 1px solid; padding-right: 4px; border-top: gray 1px solid; padding-left: 4px; font-size: 8pt; padding-bottom: 4px; margin: 20px 0px 10px; overflow: auto; border-left: gray 1px solid; width: 97.5%; cursor: text; max-height: 200px; line-height: 12pt; padding-top: 4px; border-bottom: gray 1px solid; font-family: consolas, 'Courier New', courier, monospace; height: 81px; background-color: #f4f4f4">
<div style="padding-right: 0px; padding-left: 0px; font-size: 8pt; padding-bottom: 0px; overflow: visible; width: 100%; color: black; border-top-style: none; line-height: 12pt; padding-top: 0px; font-family: consolas, 'Courier New', courier, monospace; border-right-style: none; border-left-style: none; background-color: #f4f4f4; border-bottom-style: none">

<span style="color: #606060">   1:</span> ComboBox combo = <span style="color: #0000ff">new</span> ComboBox();

<span style="color: #606060">   2:</span> combo.DataSource = EnumHelper.ToList(<span style="color: #0000ff">typeof</span>(SimpleEnum));

<span style="color: #606060">   3:</span> combo.DisplayMember = <span style="color: #006080">"Value"</span>;

<span style="color: #606060">   4:</span> combo.ValueMember = <span style="color: #006080">"Key"</span>;
</div></div>


You now have a ComboBox whose values are your enum type values and whose display are the string specified in the EnumDescription attribute. This works with any control that supports data binding, including the ToolStripComboBox, although you will need to cast the <font face="Consolas" size="2">ToolStripComboBox.Control</font> property to a ComboBox to get to the <font face="Consolas" size="2">DataSource</font> property. (In that case, you will also want to perform the same cast when  you are referencing the selected value to work with it as your enum type.)
