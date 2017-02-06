---
layout: post
title: Data Binding an Enum with Descriptions
date: '2007-08-02 00:21:25 -05:00'
---

Every once in a while I need to bind an enumerated type to a Windows Forms control, usually a ComboBox. 

The simplest is to use the `Enum.GetValues()` method, setting its result to the `DataSource` property of the ComboBox. If you have the following enum:

```csharp
public enum SimpleEnum
{
    Today,
    Last7
    Last14,
    Last30,
    All
}
```

You can bind it to a ComboBox like this:

```csharp
ComboBox combo = new ComboBox();
combo.DataSource = Enum.GetValues(typeof(SimpleEnum));
```

While this does work, there are a couple of problems with this:

1.  There is no support for localization. 
2.  There is no support for more readable descriptions.

If you want to support one or both of these requirements, it can start to get complicated. The complication comes in the form of numerous different ways to accomplish the same thing. These range from custom type descriptors, to generic (and non-generic) "details" classes, to hard-coded string resource lookups, and many others.

The majority of the articles and techniques I have seen all attempt to solve the simple problem of data binding an enum to a ComboBox while displaying a human readable string as the ComboBox display string. Overall, there isn't anything wrong with these approaches and they all have pros and cons. However, they are generally more complicated than necessary and, in some cases, require a lot of work on either the developer implementing the enum, the developer using it, or both.

The easiest way to accomplish this is actually using a little bit of Reflection and decorating the enum values with an attribute. You don't need generics, custom classes, or custom type descriptors...just two static methods that are both less than 10 lines of code.

The first step is to add a description attribute to your enum. For simplicity, you can use the `System.ComponentModel.DescriptionAttribute` class, but I would recommend deriving your own `EnumDescriptionAttribute`.

```csharp
/// <summary>
/// Provides a description for an enumerated type.
/// </summary>
[AttributeUsage(AttributeTargets.Enum | AttributeTargets.Field, AllowMultiple = false)]
public sealed class EnumDescriptionAttribute :  Attribute
{
    private string description;

    /// <summary>
    /// Gets the description stored in this attribute.
    /// </summary>
    /// <value>The description stored in the attribute.</value>
    public string Description
    {
        get
        {
            return this.description;
        }
    }

    /// <summary>
    /// Initializes a new instance of the 
    /// <see cref="EnumDescriptionAttribute"/> class.
    /// </summary>
    /// <param name="description">The description to store in this attribute.</param>
    public EnumDescriptionAttribute(string description)
        : base()
    {
        this.description = description;
    }
}
```

Now that we have our description attribute, we need to decorate the enum with it:

```csharp
public enum SimpleEnum
{
   [EnumDescription("Today")]
   Today,

   [EnumDescription("Last 7 days")]
   Last7,

   [EnumDescription("Last 14 days")]
   Last14,

   [EnumDescription("Last 30 days")]
   Last30,

   [EnumDescription("All")]
   All
}
```

Using a custom attribute allows you to keep the human readable description in the code where the enum is defined. It also allows you to retrieve localized versions of the description. In order to do that, you simply need to change the way the attribute works to lookup the appropriate string in the string resources.

The next part is what actually does all of the work. As I mentioned, both of these functions are less than 10 lines of code. The easiest way to work with these functions is to create a static (or sealed, if you aren't using .NET 2.0 or later) class that holds these two static functions.

```csharp
 /// <summary>
 /// Provides a static utility object of methods and properties to interact with enumerated types. 
 /// </summary>
 public static class EnumHelper
 {
    /// <summary>
    /// Gets the <see cref="DescriptionAttribute"/> of an <see cref="Enum"/> type value.
    /// </summary>
    /// <param name="value">The <see cref="Enum"/> type value.</param>
    /// <returns>A string containing the text of the <see cref="DescriptionAttribute"/>.</returns>
    public static string GetDescription(Enum value)
    {
       if (value == null)
       {
          throw new ArgumentNullException("value");
       }

       string description = value.ToString();
       FieldInfo fieldInfo = value.GetType().GetField(description);
       EnumDescriptionAttribute[] attributes = (EnumDescriptionAttribute[])fieldInfo
          .GetCustomAttributes(typeof(EnumDescriptionAttribute), false);

        if (attributes != null && attributes.Length > 0)
        {
           description = attributes[0].Description;
        }
        return description;
     }

     /// <summary>
     /// Converts the <see cref="Enum"/> type to an <see cref="IList"/> compatible object.
     /// </summary>
     /// <param name="type">The <see cref="Enum"/> type.</param>
     /// <returns>An <see cref="IList"/> containing the enumerated type value and description.</returns>
     public static IList ToList(Type type)
     {
        if (type == null)
        {
           throw new ArgumentNullException("type");
        }

        ArrayList list = new ArrayList();
        Array enumValues = Enum.GetValues(type);

        foreach (Enum value in enumValues)
        {
           list.Add(new KeyValuePair<Enum, string>(value, GetDescription(value)));
        }

        return list;
     }
  }
```
As you can see, the `GetDescription` method uses a little bit of Reflection to retrieve the `EnumDescription` attribute on the specified enum value. If it doesn't find the attribute, it simply uses the value name. The `ToList` method returns an `IList` of `KeyValuePair<Enum, string>` instances that hold the enum value (the key) and the description (the value). If you aren't using .NET 2.0 or later, you will need to use `DictionaryEntry` instead of `KeyValuePair<TKey, TValue>`.

In order to bind the ComboBox, you now need to do the following:

```csharp
ComboBox combo = new ComboBox();
combo.DataSource = EnumHelper.ToList(typeof(SimpleEnum));
combo.DisplayMember = "Value";
combo.ValueMember = "Key";
```

You now have a ComboBox whose values are your enum type values and whose display are the string specified in the `EnumDescription` attribute. This works with any control that supports data binding, including the ToolStripComboBox, although you will need to cast the `ToolStripComboBox.Control` property to a ComboBox to get to the `DataSource` property. (In that case, you will also want to perform the same cast when  you are referencing the selected value to work with it as your enum type.)
