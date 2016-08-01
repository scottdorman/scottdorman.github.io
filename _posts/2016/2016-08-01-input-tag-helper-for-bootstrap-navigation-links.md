---
layout: post
title: Input Tag Helper For Bootstrap Navigation Links
date: 2016-08-01 -05:00
---

I've already [written about]{% post_url 2016-08-01-tag-helpers %} Tag Helpers and [showed]({% post_url 2016-08-01-input-tag-helper-with-placeholder-support %}) how easy it is to extend an existing Tag Helper. Now let's look at how to create a new Tag Helper for generating Bootstrap 3 navigation links.

One of the nice things with Bootstrap's `navbar` classes is the ability to indicate the active link by adding the `active` class to the `li` element. Unfortunately, this has always meant a lot of work for an ASP.NET MVC site to figure out when the class should be added. There have been a lot of solutions to this problem over the years, but those were all before Tag Helpers.

As a refresher, here is a simple navigation list that might be part of a larger navbar.

```
<ul class="nav navbar-nav">
    <li><a href="#">Action</a></li>
    <li><a href="#">Another action</a></li>
    <li><a href="#">Something else here</a></li>
</ul>
```

There are two parts to this list: the `li` element and the `a` element. What we want is a way to combine both using a single Tag Helper. That allows us to use markup like

```
<ul class="nav navbar-nav">
    <bootstrap-nav-link asp-controller="Home" asp-action="Index">Action</a></bootstrap-nav-link>
    <bootstrap-nav-link asp-controller="Home" asp-action="About">Another action</bootstrap-nav-link>
    <bootstrap-nav-link asp-controller="Home" asp-action="Contact">Something else here</bootstrap-nav-link>
</ul>
```

To do this, we're going to extend the `AnchorTagHelper`. In this case, we're not actually adding any new attributes. Instead, we're modifying the output of the Tag Helper so that the generated `a` element is wrapped inside an `li` which has the `active` class.

The code for doing that is:

```csharp
using System;
using System.Linq;
using Microsoft.AspNetCore.Mvc.Rendering;
using Microsoft.AspNetCore.Mvc.TagHelpers;
using Microsoft.AspNetCore.Mvc.ViewFeatures;
using Microsoft.AspNetCore.Razor.TagHelpers;

namespace Cadru.TagHelpers
{
    [OutputElementHint("li")]
    public class BootstrapNavLinkTagHelper : AnchorTagHelper
    {
        public BootstrapNavLinkTagHelper(IHtmlGenerator generator) : base(generator)
        {
        }

        private bool ShouldBeActive()
        {
            var routeData = ViewContext.RouteData.Values;
            var currentController = routeData["controller"] as string;
            var currentAction = routeData["action"] as string;
            var result = false;

            if (!String.IsNullOrWhiteSpace(Controller) && !String.IsNullOrWhiteSpace(Action))
            {
                result = String.Equals(Action, currentAction, StringComparison.OrdinalIgnoreCase) &&
                    String.Equals(Controller, currentController, StringComparison.OrdinalIgnoreCase);
            }
            else if (!String.IsNullOrWhiteSpace(Action))
            {
                result = String.Equals(Action, currentAction, StringComparison.OrdinalIgnoreCase);
            }
            else if (!String.IsNullOrWhiteSpace(Controller))
            {
                result = String.Equals(Controller, currentController, StringComparison.OrdinalIgnoreCase);
            }

            return result;
        }

        private void MakeActive(TagHelperOutput output)
        {
            TagHelperAttribute classAttribute;
            if (output.Attributes.TryGetAttribute("class", out classAttribute))
            {
                output.Attributes.SetAttribute("class", classAttribute.Value + " active");
            }
            else
            {
                output.Attributes.Add(new TagHelperAttribute("class", "active"));
            }
        }

        public async override void Process(TagHelperContext context, TagHelperOutput output)
        {
            base.Process(context, output);

            var childContent = await output.GetChildContentAsync();
            var content = childContent.GetContent();
            output.TagName = "li";

            var href = output.Attributes.FirstOrDefault(a => a.Name == "href");
            if (href != null)
            {
                var tagBuilder = new TagBuilder("a");
                tagBuilder.Attributes.Add("href", href.Value.ToString());
                tagBuilder.InnerHtml.AppendHtml(content);

                output.Content.SetHtmlContent(tagBuilder);
                output.Attributes.Remove(href);
            }
            else
            {
                output.Content.SetHtmlContent(content);
            }

            if (ShouldBeActive())
            {
                MakeActive(output);
            }
        }
    }
}
```

The bulk of the work happens in the `ShouldBeActive` method, which is responsible for looking at the controller and action values of the current request and comparing them to the `Controller` and `Action` properties of the Tag Helper. If they match, that means the `li` should have the `active` class added to it's class list. That happens in the `MakeActive` method.

This is a fairly simple but completely functional example. If you want to do "fancier" things, like add an icon before the text you can do that 


```
<ul class="nav navbar-nav">
    <bootstrap-nav-link asp-controller="Home" asp-action="Index"><div class="fa fa-home"></div>Action</a></bootstrap-nav-link>
    <bootstrap-nav-link asp-controller="Home" asp-action="About">Another action</bootstrap-nav-link>
    <bootstrap-nav-link asp-controller="Home" asp-action="Contact">Something else here</bootstrap-nav-link>
</ul>
```

<div class="alert alert-info">Even though this includes the `OutputElementHint` attribute to let Visual Studio know that it should be treated as an `li` tag, the markup shown above for adding an icon will generate a markup validation warning saying "Element 'div' cannot be nested inside element 'ul'." I'm currently investigating why this happens.</div>