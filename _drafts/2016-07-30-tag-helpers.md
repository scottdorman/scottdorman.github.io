---
layout: post
title: Tag Helpers
date: 2016-07-30 -05:00
---

For those of you who aren't familiar with Tag Helpers in ASP.NET Core 1.0, you can think of them as the next logical evolution of Html Helpers. The differences between them are much more significant though. While Html Helpers were a good improvement that simplified things, they didn't provide an HTML-friendly development experience. Tag Helpers, however, look like standard HTML markup. For example, if you wanted to include a link in your Razor view to your "About" page, you'd need to write the following using HTML Helpers:

```
@Html.ActionLink("About Us", "About", "Home")
```

This would translate into a standard HTML `a` tag, but it doesn't look like standard HTML markup. Using the new tag helpers, this same link is written as

```
<a asp-action="About" asp-controller="Home">About Us</a>
```

Now, our link looks like standard HTML markup, but with a few new attributes. These attributes are provided by a Tag Helper, which knows how to turn them in to a properly formatted `a` tag.

Where Tag Helpers really show off is in forms, and Microsoft has provided a lot of Tag Helpers for forms. For example, the tag helpers for the `<input>` element contains the `asp-for` attribute, which extracts the name of the specified model property into the rendered HTML. Given the following simple view model

```c#
public class LoginViewModel
{
    [Required]
    [EmailAddress]
    [Display(Name = "Email address")]
    public string Email { get; set; }

    [Required]
    [DataType(DataType.Password)]
    public string Password { get; set; }
}
```

The following Razor markup:

```
<input asp-for="Email"></input>
```

Generates the following HTML:

```
<input name="Email" id-"Email" type="Email" value="" data-val-required="The Email field is required." data-val-email="The Email field is not a valid e-mail address." data-val="true">Email</input>
```

This is really nice and all comes for free with the out of the box `InputTagHelper` class. What's missing, however, is support for the `placeholder` attribute. What would be really nice is if we could simply write this in Razor:

```
<input asp-for="Email" asp-placeholder-for="Email"></input>
```

and have it generate the following HTML:

```
<input name="Email" id-"Email" placeholder="Email address" type="Email" value="" data-val-required="The Email field is required." data-val-email="The Email field is not a valid e-mail address." data-val="true">Email</input>
```

Thankfully, tag helpers are pretty easy to write, and the ASP.NET Core docs have a pretty good [tutorial](https://docs.asp.net/en/latest/mvc/views/tag-helpers/authoring.html). What's particularly interesting (and very useful) is that you can extend other tag helpers. Let's do that, and extend `InputTagHelper` to add support for an `asp-placeholder-for` attribute.

The code for doing that is:

```c#
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

This class inherits from `InputTagHelper`, which it lets do most of the work. The `HtmlTargetElement` attribute indicates that this tag helper targets the `input` tag and that it adds an `asp-placeholder-for` attribute. We then associate the `Placeholder` property with the new HTML property using the `HtmlAttributeName` attribute. Finally, the `Process` method is where all of the magic happens. This method first lets the base `InputTagHelper` do its work to generate the appropriate `input` tag for the model proprty. Then it looks at the model metadata and retrieves the Placeholder property value, or if the placeholder is empty the display name. If the `placeholder` attribute has alredy been provided, then it's value is used; otherwise, the attribute is added to the output attributes. 

We now have a tag helper for the `input` tag that allows us to easily set the `placeholder` attribute value based on the `Name` or `Prompt` properties of the `Display` attribute. 