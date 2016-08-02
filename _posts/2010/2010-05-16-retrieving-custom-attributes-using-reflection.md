---
layout: post
title: Retrieving Custom Attributes Using Reflection
date: 2010-05-16 12:56:23 -05:00
---

The .NET Framework allows you to easily add metadata to your classes by using attributes. These attributes can be ones that the .NET Framework already provides, of which there are over 300, or you can create your own.

Using reflection, the ways to retrieve the custom attributes of a type are:

* [`System.Reflection.MemberInfo`](http://msdn2.microsoft.com/en-us/8fek28hz)       
    * `public abstract object[] GetCustomAttributes(bool inherit);`
    * `public abstract object[] GetCustomAttributes(Type attributeType, bool inherit);` 
    * `public abstract bool IsDefined(Type attributeType, bool inherit);`   
* [`System.Attribute`](http://msdn2.microsoft.com/en-us/e8kc3626)       
    * `public static Attribute[] GetCustomAttributes(MemberInfo member, bool inherit);`
    * `public static bool IsDefined(MemberInfo element, Type attributeType, bool inherit);`      

If you take the following simple class hierarchy:
 
```csharp
public abstract class BaseClass
{
   private bool result;

   [DefaultValue(false)]
   public virtual bool SimpleProperty
   {
      get { return this.result; }
      set { this.result = value; }
   }
}

public class DerivedClass : BaseClass
{
   public override bool SimpleProperty
   {
      get { return true; }
      set { base.SimpleProperty = value; }
   }
}
```
Given a `PropertyInfo` object (which is derived from `MemberInfo`, and represents a propery in reflection), you might expect that these methods would return the same result. Unfortunately, that isn't the case. 

The `MemberInfo` methods strictly reflect the metadata definitions, ignoring the inherit parameter and not searching the inheritance chain when used with a `PropertyInfo`, `EventInfo`, or `ParameterInfo` object. It also returns all custom attribute instances, including those that don't inherit from `System.Attribute`. 

The `Attribute` methods are closer to the implied behavior of the language (and probably closer to what you would naturally expect). They do respect the inherit parameter for `PropertyInfo`, `EventInfo`, and `ParameterInfo` objects and search the implied inheritance chain defined by the associated methods (in this case, the property accessors). These methods also only return custom attributes that inherit from `System.Attribute`.

This is a fairly subtle difference that can produce very unexpected results if you aren't careful.

For example, to retrieve the custom  attributes defined on `SimpleProperty`, you could use code similar to this:

```csharp
PropertyInfo info = typeof(DerivedClass).GetProperty("SimpleProperty");
var attributeList1 = info.GetCustomAttributes(typeof(DefaultValueAttribute), true));
var attributeList2 = Attribute.GetCustomAttributes(info, typeof(DefaultValueAttribute), true));
```

The `attributeList1` array will be empty while the `attributeList2` array will contain the attribute instance, as expected.
