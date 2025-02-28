---
layout: post
title: Creating a tag helper to conditionally render content
date: '2025-02-27 23:50:00 -05:00'
tags: .net .net-core asp.net-core c# tag-helpers
---

Tag Helpers are probably one of the best features that have been added to ASP.NET, starting all the way back to ASP.NET Core 1.0. I've [talked about them before]({% post_url /2016/2016-07-30-tag-helpers %}), but tag helpers are a fairly powerful construct with a pretty simple syntax. They look like standard HTML attributes that are added to to an element and they can also be entirely new tags.

One disadvantage is that there are some C# structures that don't have a Tag Helper equivalent. One of the most common of these structures is conditional rendering. I think conditionally rendering some HTML is something we've all done. It's not difficult, but can lead to some messy looking HTML. A simple example might look like this:

```cshtml 
@if (Model == null)
{
  <p>We're having trouble retrieving the information you asked for.<p>
}
else
{
  <p><b>Name</b> @Model.Name<p>
  <p><b>Email</b> @Model.Email<p>
}
```
This code renders a friendly error message if the `Model` is `null` and if it's not, then it shows the `Name` and `Email` properties. While this code is easy to read, it can be a bit jarring trying to read code that switches between markup and C#, especially if there is a lot of it. How much nicer would it be to write this as
```cshtml 
<p asp-include-when="@Model == null">We're having trouble retrieving the information you asked for.<p>
<p asp-include-when="@Model != null"><b>Name</b> @Model.Name<p>
<p asp-include-when="@Model != null"><b>Email</b> @Model.Email<p>
```
In this example, the markup element is only included if the `asp-include-when` attribute evaluates to `true`.

While this is much simpler, we could simplify it even more by being able to write
```cshtml 
<p asp-include-when="@Model == null">We're having trouble retrieving the information you asked for.<p>
<if asp-include-when="@Model != null">
   <p><b>Name</b> @Model.Name<p>
   <p asp-include-when="@Model != null"><b>Email</b> @Model.Email<p>
</if>
```
Here, we introduce a new `if` markup element which also includes an `asp-include-when` attribute. In this case, if inner markup is included only when the attribute evaluates to `true`.

This can be accomplished through a pretty simple custom tag helper implementation. The frist two `HtmlTargetElement` attributes add an `asp-include-when` and an `asp-exclude-when` attribute to any valid HTML markup. By providing an include and an exclude attribute, we gain some flexibility to either include or exclude markup based on a condition. The last `HtmlTargetElement` attribute allows us to include or exclude markup using a new `if` markup element. We then override the `Process` method. If we're dealing with an `<if>` element, we don't want the tag rendered in the final output, so we set `output.TagName = null`. If we shsouldn't suppress the output, we just return from the method, allowing the content to render normally. If we aren't going to render the content, we suppress the output by calling `output.SuppressOutput()`.
```cs
using Microsoft.AspNetCore.Razor.TagHelpers;

namespace Cadru.AspNetCore.Razor.TagHelpers;

[HtmlTargetElement(Attributes = IncludeConditionAttributeName)]
[HtmlTargetElement(Attributes = ExcludeConditionAttributeName)]
[HtmlTargetElement("if")]
public class ConditionTagHelper : TagHelper
{
    private const string IncludeConditionAttributeName = "asp-include-when";
    private const string ExcludeConditionAttributeName = "asp-exclude-when";

    [HtmlAttributeName(IncludeConditionAttributeName)]
    public bool Include { get; set; } = true;

    [HtmlAttributeName(ExcludeConditionAttributeName)]
    public bool Exclude { get; set; } = false;

    public override void Process(TagHelperContext context, TagHelperOutput output)
    {
        if (context.TagName == "if")
        {
            // Strip the outer tag name as we never want <if> to render
            output.TagName = null;
        }

        if (Include && !Exclude)
        {
            return;
        }

        output.SuppressOutput();
    }
}
```
