---
layout: post
title: Input Tag Helper With Placeholder Support
date: '2016-08-01 09:46:00 -05:00'
---

Earlier, I [wrote about]({% post_url /2016/2016-08-01-tag-helpers %}) Tag Helpers and showed how useful they are when creating HTML forms. In that post, we saw how simple it is to use Tag Helpers to generate an `input` element:

```html
<input asp-for="Email"></input>
```

The .NET Framework code responsible for this is the [`InputTagHelper`](https://github.com/aspnet/Mvc/blob/dev/src/Microsoft.AspNetCore.Mvc.TagHelpers/InputTagHelper.cs) class. What's missing, however, is support for the `placeholder` attribute. What would be really nice is if we could simply write this as:

```html
<input asp-for="Email" asp-placeholder-for="Email"></input>
```

and have it automatically use the value of either the `Name` or `Prompt` properties of the `Display` attribute for the `placeholder` attribute. That allows us to keep the content in the model as localizable metadata. 

Thankfully, Tag Helpers are pretty easy to write, and the ASP.NET Core docs have a pretty good [tutorial](https://docs.asp.net/en/latest/mvc/views/tag-helpers/authoring.html). What's particularly nice is that you can extend other tag helpers. 

Let's do that, and extend `InputTagHelper` to add support for an `asp-placeholder-for` attribute.

The code for doing that is:

```csharp
using System;
using Microsoft.AspNetCore.Mvc.TagHelpers;
using Microsoft.AspNetCore.Mvc.ViewFeatures;
using Microsoft.AspNetCore.Razor.TagHelpers;

namespace Cadru.TagHelpers
{
    [HtmlTargetElement("input", Attributes = PlaceholderAttributeName, TagStructure = TagStructure.WithoutEndTag)]
    public class InputPlaceholderTagHelper : InputTagHelper
    {
        private const string PlaceholderAttributeName = "asp-placeholder-for";

        public InputPlaceholderTagHelper(IHtmlGenerator generator) : base(generator)
        {
        }

        /// <summary>
        /// An expression to be evaluated against the current model.
        /// </summary>
        [HtmlAttributeName(PlaceholderAttributeName)]
        public ModelExpression Placeholder { get; set; }


        public override void Process(TagHelperContext context, TagHelperOutput output)
        {
            base.Process(context, output);

            var placeholder = GetPlaceholder(Placeholder.ModelExplorer);
            TagHelperAttribute placeholderAttribute;

            if (!output.Attributes.TryGetAttribute("placeholder", out placeholderAttribute))
            {
                output.Attributes.Add(new TagHelperAttribute("placeholder", placeholder));
            }
        }

        private string GetPlaceholder(ModelExplorer modelExplorer)
        {
            string placeholder;
            placeholder = modelExplorer.Metadata.Placeholder;

            if (String.IsNullOrWhiteSpace(placeholder))
            {
                placeholder = modelExplorer.Metadata.GetDisplayName();
            }

            return placeholder;
        }
    }
}
```

This class inherits from `InputTagHelper`, which it lets do most of the work. The `HtmlTargetElement` attribute indicates that this Tag Helper targets the `input` tag and that it adds an `asp-placeholder-for` attribute. We then associate the `Placeholder` property with the new HTML property using the `HtmlAttributeName` attribute. Finally, the `Process` method is where all of the magic happens. This method first lets the base `InputTagHelper` do its work to generate the appropriate `input` tag for the model proprty. Then it looks at the model metadata and retrieves the `Placeholder` property value, or if the placeholder is empty the display name. If the `placeholder` attribute has alredy been provided, then it's value is used; otherwise, the attribute is added to the output attributes.

Now we can simply add the `asp-placeholder-for` attribute to our `input` tag and it automatically use the value of either the `Name` or `Prompt` properties of the `Display` attribute for the value of the `placeholder` attribute. If the model doesn't include a `Display` attribute, the metadata will automatically return the property name, in much the same way as the `LabelTagHelper`.
