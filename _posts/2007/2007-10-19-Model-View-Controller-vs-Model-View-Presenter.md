---
layout: post
title: Model View Controller vs Model View Presenter
date: 10/19/2007 9:24:39 PM
---

You've probably heard all of the buzz around Microsoft's new [ASP.NET MVC Framework](http://weblogs.asp.net/scottgu/archive/2007/10/14/asp-net-mvc-framework.aspx). This is a framework methodology that divides an application's implementation into three component roles: models, views, and controllers. You've probably also heard about a slightly different approach called Model View Presenter (MVP). If you ever wanted to know the difference between the  MVC and MVP patterns and why you should use one over the other, Todd Snyder from Infragistics has an excellent [explanation](http://blogs.infragistics.com/blogs/tsnyder/archive/2007/10/17/mvc-or-mvp-pattern-whats-the-difference.aspx).

He sums it up by describing the key differences between the two patterns:

**MVP Pattern** 

*   View is more loosely coupled to the model. The presenter is responsible for binding the model to the view. 
*   Easier to unit test because interaction with the view is through an interface 
*   Usually view to presenter map one to one. Complex views may have multi presenters.


**MVC Pattern** 

*   Controller are based on behaviors and can be shared across views 
*   Can be responsible for determining which view to display ([Front Controller Pattern](http://msdn2.microsoft.com/en-us/library/ms978723.aspx))
