---
layout: post
title: Kendo Grid MVC Wrapper Automatic Column Configuration
date: 2015-11-05 19:17:02 -05:00
---

The Telerik Kendo Grid control is really powerful, especially when combined with the MVC wrappers. One of the things that make the MVC wrapper so useful is the ability to automatically (and easily) generate data-bound columns. It’s a single line of code:

.Columns(columns => columns.AutoGenerate(true))

The code behind `AutoGenerate(true)` understands some of the `[System.ComponentModel.DataAnnotations](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations(v=vs.110).aspx)` attributes. Specifically, it knows how to automatically configure the grid column for these attributes: 



<table width="1468" border="0" cellspacing="0" cellpadding="2"><tbody>
    <tr>
      <td width="200" valign="top">**Attribute**</td>

      <td width="1266" valign="top">**Description**</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[Compare](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.compareattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Compares two properties.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[CreditCard](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.creditcardattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Specifies that a data field value is a credit card number. </td>
    </tr>

    <tr>
      <td width="200" valign="top">`[CustomValidation](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.customvalidationattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Specifies a custom validation method that is used to validate a property.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[DataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.datatypeattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Specifies the name of an additional type to associate with a data field.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[Display](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Provides a general-purpose attribute that lets you specify localizable strings for types and members of entity partial classes.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[DisplayColumn](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displaycolumnattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Specifies the column that is displayed in the referred table as a foreign-key column.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[DisplayFormat](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.displayformatattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Specifies how data fields are displayed and formatted by ASP.NET Dynamic Data.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[Editable](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.editableattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Indicates whether a data field is editable. </td>
    </tr>

    <tr>
      <td width="200" valign="top">`[EmailAddress](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.emailaddressattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Validates an email address.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[EnumDataType](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.enumdatatypeattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Enables a .NET Framework enumeration to be mapped to a data column.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[FileExtensions](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.fileextensionsattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Validates file name extensions.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[FilterUIHint](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.filteruihintattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Represents an attribute that is used to specify the filtering behavior for a column.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[MaxLength](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.maxlengthattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Specifies the maximum length of array or string data allowed in a property.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[MinLength](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.minlengthattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Specifies the minimum length of array or string data allowed in a property.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[Phone](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.phoneattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Specifies that a data field value is a well-formed phone number using a regular expression for phone numbers.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[Range](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.rangeattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Specifies the numeric range constraints for the value of a data field.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[RegularExpression](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.regularexpressionattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Specifies that a data field value in ASP.NET Dynamic Data must match the specified regular expression.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[Required](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.requiredattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Specifies that a data field value is required.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[ScaffoldColumn](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.scaffoldcolumnattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Specifies whether a class or data column uses scaffolding.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[StringLength](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.stringlengthattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Specifies the minimum and maximum length of characters that are allowed in a data field.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[UIHint](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.uihintattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Specifies the template or user control that Dynamic Data uses to display a data field.</td>
    </tr>

    <tr>
      <td width="200" valign="top">`[Url](https://msdn.microsoft.com/en-us/library/system.componentmodel.dataannotations.urlattribute(v=vs.110).aspx)`</td>

      <td width="1266" valign="top">Provides URL validation.</td>
    </tr>
  </tbody></table>



What’s nice about this support is that you can use these attributes to adorn your model properties and declaratively describe some of the metadata about the column.

The problem, though, is that you can’t also set the Kendo Grid specific properties, such as column width, if the column is locked or not, and if it should be included in the column menu (to name just a few). 

Fortunately, we can hook into the `[AdditionalValues](https://msdn.microsoft.com/en-us/library/system.web.mvc.modelmetadata.additionalvalues(v=vs.118).aspx#P:System.Web.Mvc.ModelMetadata.AdditionalValues)` dictionary of the `Metadata` property on a data-bound column (which is of type `Kendo.Mvc.UI.GridBoundColumn<TModel, TValue>`). This property holds an instance of a `[System.Web.Mvc.ModelMetadata](https://msdn.microsoft.com/en-us/library/system.web.mvc.modelmetadata(v=vs.110).aspx)` (more specifically an instance of a `[CachedModelMetadata<TPrototypeCache>](https://msdn.microsoft.com/en-us/library/gg512055(v=vs.118).aspx)`) object, which has all of the metadata related attributes defined on the properties of the model and is the key to our solution of providing automatic column configuration based on data annotation attributes. To do this, we simply define our own attribute and implement the `[IMetadataAware](https://msdn.microsoft.com/en-us/library/system.web.mvc.imetadataaware(v=vs.118).aspx)` interface. The runtime will handle everything for us and our new attribute will be added to the `AdditionalValues` dictionary. 

I created a `GridColumnAttribute` to allow all of the additional Kendo specific properties to be set.

```csharp
using System;
using System.Web.Mvc;

namespace Cadru.Web.KendoExtensions
{
    public class GridColumnAttribute : Attribute, IMetadataAware
    {
        public const string Key = "GridColumnMetadata";

        public bool Hidden { get; set; }

        public bool IncludeInMenu { get; set; }

        public bool Lockable { get; set; }

        public bool Locked { get; set; }

        public int MinScreenWidth { get; set; }

        public string Width { get; set; }

        public void OnMetadataCreated(ModelMetadata metadata)
        {
            metadata.AdditionalValues[GridColumnAttribute.Key] = this;
        }
    }
}
```

Now, we can decorate our model with the new attribute:

```csharp
public class EmployeeModel
{
    [Editable(false)]
    [GridColumn(Width = "100px", Locked = true)]
    public string EmployeeID { get; set; }

    [GridColumn(Width = "200px", Locked = true)]
    public string EmployeeName { get; set; }

    [GridColumn(Width = "100px")]
    public string EmployeeFirstName { get; set; }

    [GridColumn(Width = "100px")]
    public string EmployeeLastName { get; set; }
}
```

However, that’s only part of the solution. We still need to tell the Kendo Grid that it needs to do something with this new attribute. To do this we can use the overload for the `AutoGenerate` method which takes an `Action`:

.Columns(columns => columns.AutoGenerate(c => GridColumnHelpers.ConfigureColumn(c)))

The ` method looks like` 

```csharp
using Kendo.Mvc.UI;
using System;
using System.Web.Mvc;

namespace Cadru.Web.KendoExtensions
{
    public static class GridColumnHelpers
    {
        public static void ConfigureColumn<T>(GridColumnBase<T> column) where T : class
        {
            CachedDataAnnotationsModelMetadata metadata = ((dynamic)column).Metadata;
            object attributeValue = null;
            if (metadata.AdditionalValues.TryGetValue(GridColumnAttribute.Key, out attributeValue))
            {
                var attribute = (GridColumnAttribute)attributeValue;
                column.Width = attribute.Width;
                column.Locked = attribute.Locked;
                column.Hidden = attribute.Hidden;
                column.IncludeInMenu = attribute.IncludeInMenu;
                column.Lockable = attribute.Lockable;
                column.MinScreenWidth = attribute.MinScreenWidth;
            }
        }
    }
}
```

This takes advantage of the fact that the method is being called in the context of automatically generating data-bound columns, so it’s able to take the column and cast it to a `dynamic` object in order to reference the `Metadata` property. We have to do this because the `IGridBoundColumn` doesn’t expose the `Metadata` property and we can’t cast it directly to a `GridBoundColumn<TModel, TValue>` because (among other reasons) we don’t know the type for `TValue`. That leaves us with casting it to `dynamic` and letting the dynamic dispatcher figure out how to give us back the requested property. From there, we look to see if the `AdditionalValues` dictionary contains our attribute, and if it does we then set the column properties to their respective values as specified by the attribute. We now have the ability to automatically configure the additional column properties using metadata specified in our model while still automatically generating the data-bound columns.
