---
layout: post
title: Tag Helpers
date: '2016-07-30 09:46:00 -05:00'
---

For those of you who aren't familiar with Tag Helpers in ASP.NET Core 1.0, you can think of them as the next logical evolution of Html Helpers. The differences between them are much more significant though. While Html Helpers were a good improvement that simplified things, they are invoked as methods mixed in with HTML in your Razor views. This isn't exactly an HTML-friendly development experience and causes you to bounce between HTML syntax and code syntax in your views. Tag Helpers, however, look like standard HTML markup, which creates a much friendlier (and simpler) development experience. Not only that, Tag Helpers have IntelliSense support, something that was severely lacking with Html Helpers.

Let's take a look at a simple scenario to see how Tag Helpers are used (and how they're different from Html Helpers). For example, if you were creating a form and wanted to use the standard Bootstrap `form-horizontal` styling, you need to add a `control-label` class to each of your HTML `label` elements. To do this using Html Helpers, you would need to write 

```html
@Html.Label("Email", "Email address", new { @class = "control-label" })
```

This isn't exactly HTML friendly markup, because all of the parameters are strings, IntelliSense can't help, and we have to use an anonymous class to represent the attributes (remembering to use the @ prefix on class so C# interprets it as a property name and not the class keyword).

Using a Tag Helper, the same markup is

```html
<label class="control-label" asp-for="Email"></label>
```

This looks like standard HTML markup, with a new attribute. This attribute is provided by a Tag Helper, in this case the `LabelTagHelper`, which knows how to turn it in to a properly formatted `label` tag.

Where Tag Helpers really show off is in forms, and Microsoft has provided a lot of Tag Helpers for forms. For example, consider the standard Register.cshtml Razor view generated with the legacy ASP.NET 4.5.x MVC template:

```html
@using (Html.BeginForm("Register", "Account", FormMethod.Post, new { @class = "form-horizontal", role = "form" }))
{
    @Html.AntiForgeryToken()
    <h4>Create a new account.</h4>
    <hr/>
    @Html.ValidationSummary("", new { @class = "text-danger" })
    <div class="form-group">
        @Html.LabelFor(m => m.Email, new { @class = "col-md-2 control-label" })
        <div class="col-md-10">
            @Html.TextBoxFor(m => m.Email, new { @class = "form-control" })
            @Html.ValidationMessageFor(m => m.Email, "", new { @class = "text-danger" })
        </div>
    </div>
    <div class="form-group">
        @Html.LabelFor(m => m.Password, new { @class = "col-md-2 control-label" })
        <div class="col-md-10">
            <div class="form-group">
                @Html.PasswordFor(m => m.Password, new { @class = "form-control" })
                @Html.ValidationMessageFor(m => m.Password, "", new { @class = "text-danger" })
            </div>
        </div>
    </div>
    <div class="form-group">
        @Html.LabelFor(m => m.ConfirmPassword, new { @class = "col-md-2 control-label" })
        <div class="col-md-10">
            <div class="form-group">
                @Html.PasswordFor(m => m.ConfirmPassword, new { @class = "form-control" })
                @Html.ValidationMessageFor(m => m.ConfirmPassword, "", new { @class = "text-danger" })
            </div>
        </div>
    </div>
    <div class="form-group">
        <div class="col-md-offset-2 col-md-10">
            <button type="submit" class="btn btn-default" value="Register" />
        </div>
    </div>
}
```

Looking at that code, the majority of it isn't HTML markup at all. It's Html Helpers. Compare that to the same form written using Tag Helpers

```html
<form asp-action="Register" asp-controller="Account" method="post" class="form-horizontal" role="form">
    <h4>Create a new account.</h4>
    <hr/>
    <div asp-validation-summary="ValidationSummary.All" class="text-danger"></div>
    <div class="form-group">
        <label asp-for="Email" class="col-md-2 control-label"></label>
        <div class="col-md-10">
            <input asp-for="Email" class="form-control" />
            <span asp-validation-for="Email" class="text-danger"></span>
        </div>
    </div>
    <div class="form-group">
        <label asp-for="Password" class="col-md-2 control-label"></label>
        <div class="col-md-10">
            <input asp-for="Password" class="form-control" />
            <span asp-validation-for="Password" class="text-danger"></span>
        </div>
    </div>
    <div class="form-group">
        <label asp-for="ConfirmPassword" class="col-md-2 control-label"></label>
        <div class="col-md-10">
            <input asp-for="ConfirmPassword" class="form-control" />
            <span asp-validation-for="ConfirmPassword" class="text-danger"></span>
        </div>
    </div>
    <div class="form-group">
        <div class="col-md-offset-2 col-md-10">
            <button type="submit" class="btn btn-default" value="Register" />
        </div>
    </div>
}
```

This markup actually looks like HTML markup and is easier to read and maintain than the Html Helpers approach.

You can [read more about Tag Helpers](https://docs.asp.net/en/latest/mvc/views/tag-helpers/intro.html) in the ASP.NET Core docs, including a tutorial on how to [write your own Tag Helper](https://docs.asp.net/en/latest/mvc/views/tag-helpers/authoring.html).
