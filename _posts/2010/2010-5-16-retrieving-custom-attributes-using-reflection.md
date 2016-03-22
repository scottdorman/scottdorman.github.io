---
layout: post
title: Retrieving Custom Attributes Using Reflection
date: 5/16/2010 12:56:23 PM
---

The .NET Framework allows you to easily add metadata to your classes by using attributes. These attributes can be ones that the .NET Framework already provides, of which there are over 300, or you can create your own.

Using reflection, the ways to retrieve the custom attributes of a type are:

*   [System.Reflection.MemberInfo](http://msdn2.microsoft.com/en-us/8fek28hz)       

    *   public abstract object[] GetCustomAttributes(bool inherit); 
    *   public abstract object[] GetCustomAttributes(Type attributeType, bool inherit); 
    *   public abstract bool IsDefined(Type attributeType, bool inherit);    
*   [System.Attribute](http://msdn2.microsoft.com/en-us/e8kc3626)       

    *   public static Attribute[] GetCustomAttributes(MemberInfo member, bool inherit); 
    *   public static bool IsDefined(MemberInfo element, Type attributeType, bool inherit);      

If you take the following simple class hierarchy:
  <div style="border-bottom: silver 1px solid; text-align: left; border-left: silver 1px solid; padding-bottom: 4px; line-height: 12pt; background-color: #f4f4f4; margin: 20px 0px 10px; padding-left: 4px; width: 97.5%; padding-right: 4px; font-family: 'Courier New', courier, monospace; direction: ltr; height: 312px; max-height: 200px; font-size: 8pt; overflow: auto; border-top: silver 1px solid; cursor: text; border-right: silver 1px solid; padding-top: 4px" id="codeSnippetWrapper">   <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; padding-left: 0px; width: 100%; padding-right: 0px; font-family: 'Courier New', courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px" id="codeSnippet">     

<span style="color: #0000ff">public</span> <span style="color: #0000ff">abstract</span> <span style="color: #0000ff">class</span> BaseClass

{

   <span style="color: #0000ff">private</span> <span style="color: #0000ff">bool</span> result;

   [DefaultValue(<span style="color: #0000ff">false</span>)]

   <span style="color: #0000ff">public</span> <span style="color: #0000ff">virtual</span> <span style="color: #0000ff">bool</span> SimpleProperty

   {

      get { <span style="color: #0000ff">return</span> <span style="color: #0000ff">this</span>.result; }

      set { <span style="color: #0000ff">this</span>.result = <span style="color: #0000ff">value</span>; }

   }

}

<span style="color: #0000ff">public</span> <span style="color: #0000ff">class</span> DerivedClass : BaseClass

{

   <span style="color: #0000ff">public</span> <span style="color: #0000ff">override</span> <span style="color: #0000ff">bool</span> SimpleProperty

   {

      get { <span style="color: #0000ff">return</span> <span style="color: #0000ff">true</span>; }

      set { <span style="color: #0000ff">base</span>.SimpleProperty = <span style="color: #0000ff">value</span>; }

   }

}

</div>
</div>



Given a PropertyInfo object (which is derived from MemberInfo, and represents a propery in reflection), you might expect that these methods would return the same result. Unfortunately, that isn’t the case. 

The MemberInfo methods strictly reflect the metadata definitions, ignoring the inherit parameter and not searching the inheritance chain when used with a PropertyInfo, EventInfo, or ParameterInfo object. It also returns all custom attribute instances, including those that don’t inherit from System.Attribute. 

The Attribute methods are closer to the implied behavior of the language (and probably closer to what you would naturally expect). They do respect the inherit parameter for PropertyInfo, EventInfo, and ParameterInfo objects and search the implied inheritance chain defined by the associated methods (in this case, the property accessors). These methods also only return custom attributes that inherit from System.Attribute.

This is a fairly subtle difference that can produce very unexpected results if you aren’t careful.

For example, to retrieve the custom  attributes defined on SimpleProperty, you could use code similar to this:


<div style="border-bottom: silver 1px solid; text-align: left; border-left: silver 1px solid; padding-bottom: 4px; line-height: 12pt; background-color: #f4f4f4; margin: 20px 0px 10px; padding-left: 4px; width: 97.5%; padding-right: 4px; font-family: 'Courier New', courier, monospace; direction: ltr; max-height: 200px; font-size: 8pt; overflow: auto; border-top: silver 1px solid; cursor: text; border-right: silver 1px solid; padding-top: 4px" id="codeSnippetWrapper">
  <div style="border-bottom-style: none; text-align: left; padding-bottom: 0px; line-height: 12pt; border-right-style: none; background-color: #f4f4f4; padding-left: 0px; width: 100%; padding-right: 0px; font-family: 'Courier New', courier, monospace; direction: ltr; border-top-style: none; color: black; font-size: 8pt; border-left-style: none; overflow: visible; padding-top: 0px" id="codeSnippet">
    

PropertyInfo info = <span style="color: #0000ff">typeof</span>(DerivedClass).GetProperty(<span style="color: #006080">"SimpleProperty"</span>);

var attributeList1 = info.GetCustomAttributes(<span style="color: #0000ff">typeof</span>(DefaultValueAttribute), <span style="color: #0000ff">true</span>));

var attributeList2 = Attribute.GetCustomAttributes(info, <span style="color: #0000ff">typeof</span>(DefaultValueAttribute), <span style="color: #0000ff">true</span>));


</div>
</div>



The attributeList1 array will be empty while the attributeList2 array will contain the attribute instance, as expected.


<div style="padding-bottom: 0px; margin: 0px; padding-left: 0px; padding-right: 0px; display: inline; float: none; padding-top: 0px" id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:ca27cbc8-e92a-464f-807f-3c3e3f4191b6" class="wlWriterSmartContent">Technorati Tags: [Reflection](http://technorati.com/tags/Reflection),[Custom Attributes](http://technorati.com/tags/Custom+Attributes),[PropertyInfo](http://technorati.com/tags/PropertyInfo)</div>

<div style="text-align: right; padding-bottom: 4px; margin: 0px; padding-left: 0px; padding-right: 0px; padding-top: 4px" id="postToolbar"> </div><div class="wlWriterHeaderFooter" style="text-align:right; margin:0px; padding:4px 0px 4px 0px;">[![Digg This](http://digg.com/img/badges/100x20-digg-button.png "Digg This")](http://digg.com/submit?url=http%3a%2f%2fgeekswithblogs.net%2fsdorman%2farchive%2f2010%2f05%2f16%2fretrieving-custom-attributes-using-reflection.aspx&title=Retrieving+Custom+Attributes+Using+Reflection)</div>
