---
layout: post
title: On This Day
date: '2006-07-13 08:38:00 -05:00'
---

~~Check out my [article](http://geekswithblogs.net/sdorman/articles/85062.aspx) on adding an "On this day" section to your blog.~~

I've always thought it was cool to be able to find out what happened in history on a particular day. This used to be limited to encyclopedias and birthday cards, but in the "information age" this type of information is available from a lot of places fairly easily. The more I have been blogging, the more I wanted to incorporate this kind of information in my personal blog.

Since my personal blog is a blogger.com hosted blog, I started searching the blogger.com help and ran across some information on how to do this, but the link was dead. Fortunately, I was able to find a site that had it implemented (which I believe is the original) and was able to view the javascript code.

After looking at the code for a few minutes, I decided that it would get the job done but that it could be better. I rewrote it, added some stylesheet definitions, and implemented it on my blog. I posted an entry on how to use it, but thought I would write a more in-depth article.

The idea behind this function is very simple. You pass a properly formatted date string as the only argument to the function, which returns a fully formatted HTML string that can be embedded in your blog. I had the following goals in mind when I wrote this function:

* Simplicity
* Extensibility
* Performance

In order to use this function, you must have the ability to customize the look of your blog. For those of you who are hosting your own blogs this isn't a problem. Those blogs that are on public blog hosting sites need the ability to customize the template you are using. Blogger.com allows you to do this, but GeeksWithBlogs does not.

The first step is to add the Javascript function to your template. The best place to do this is in the `<HEAD>` section.

```javascript
<SCRIPT language="javascript" type="text/javascript">
function OnThisDay(thisDay)
{
   // This is the fully formatted string that is returned.
   //
   var returnString = "<span class=\"on-this-day\">On this day: #Wikipedia# á #HistoryChannel# á #NYTimes# á #BBC# á #IMDB# á #Reference# á #Britannica# á #DailyBleed# á #OnThisDay#</span>";
   
   // These variables represent the template URL for each site to be displayed. 
   // The template will be filled in after the date is calculated.
   //
   // The template parameters are:
   //
   //    #month#
   //    #day#
   //    #year#
   //
   // To add a new site, create a new variable to hold the templated URL.
   //
   var Wikipedia      = "<a target=\"_blank\" href=\"http://en.wikipedia.org/wiki/#month#_#day#\">Wikipedia</a>";
   var HistoryChannel = "<a target=\"_blank\" href=\"http://www.historychannel.com/tdih/tdih.jsp?month=#month#&day=#day#&cat=10272946\">The History Channel</a>";
   var NYTimes        = "<a target=\"_blank\" href=\"http://www.nytimes.com/learning/general/onthisday/#year##month##day#.html\">The New York Times</a>";
   var BBC            = "<a target=\"_blank\" href=\"http://news.bbc.co.uk/onthisday/hi/dates/stories/#month#/#day#/default.stm\">BBC News</a>";
   var IMDB           = "<a target=\"_blank\" href=\"http://www.imdb.com/OnThisDay?day=#day#&month=#month#\">IMDb</a>";
   var Reference      = "<a target=\"_blank\" href=\"http://reference.com/thisday/index.html?m=#month#&d=#day#\">Reference.com</a>";
   var Britannica     = "<a target=\"_blank\" href=\"http://www.britannica.com/eb/dailycontent?month=#month#&day=#day#\"><font style=\"font-variant:small-caps;\">Encyclop∆dia BRITANNICA</font></a>";
   var DailyBleed     = "<a target=\"_blank\" href=\"http://www.eskimo.com/~recall/bleed/#month#_#day#.htm\">Daily Bleed</a>";
   var OnThisDay      = "<a target=\"_blank\" href=\"http://www.on-this-day.com/onthisday/thedays/alldays/#month##day#.htm\">On-This-Day</a>";
 
   // Now we are ready to do the actual work to calculate the date. 
   // We setup some standard variables that are used in fixing up the template URLs.
   //
   var monthNames = new Array(
      "January",
      "February",
      "March",
      "April",
      "May",
      "June",
      "July",
      "August",
      "September",
      "October",
      "November",
      "December"
   );
 
   var date = new Date(thisDay);
   var day = date.getDate();
   var month = date.getMonth() + 1; // fixup the month number since getMonth() returns a zero based number;
   var year = date.getFullYear();
   var monthName = monthNames[month - 1];
 
   // Fixup the template URLs. The way each URL template is modified depends on the particular site, but 
   // most of them are simple replacements.
   //
   var wikipedia = Wikipedia.replace(/#month#/, monthName).replace(/#day#/, day);
   var historyChannel = HistoryChannel.replace(/#month#/, 10272953 + (month - 1)).replace(/#day#/, 10272965 + day);
   var nyTimes = NYTimes.replace(/#year#/, year).replace(/#month#/, (month < 10 ? "0" + month : month)).replace(/#day#/, (day < 10 ? "0" + day : day));
   var bbc = BBC.replace(/#month#/, monthName.toLowerCase()).replace(/#day#/, day);
   var imdb = IMDB.replace(/#month#/, monthName).replace(/#day#/, day);
   var reference = Reference.replace(/#month#/, month).replace(/#day#/, day);
   var britannica = Britannica.replace(/#month#/, month).replace(/#day#/, day);
   var brainyHistory = BrainyHistory.replace(/#month#/, monthName.toLowerCase()).replace(/#day#/, day);
   var onThisDay = OnThisDay.replace(/#month#/, monthName.toLowerCase().substr(0, 3)).replace(/#day#/, (day < 10 ? "0" + day : day));
 
   // Now that we have fixed up all of the template URLs, we need to fixup the returnString value.
   //
   return returnString.replace(/#Wikipedia#/, wikipedia)
      .replace(/#HistoryChannel#/, historyChannel)
      .replace(/#NYTimes#/, nyTimes)
      .replace(/#BBC#/, bbc)
      .replace(/#IMDB#/, imdb)
      .replace(/#Reference#/, reference)
      .replace(/#Britannica#/, britannica)
      .replace(/#BrainyHistory#/, brainyHistory)
      .replace(/#OnThisDay#/, onThisDay)
      ;
}
</SCRIPT>
```

Now that you have added the Javascript, you need to include the relevant CSS definitions. This can be done by adding them to an included stylesheet or by including them in an in-line stylesheet. You are free to change them to fit the look of your own blog, but I don't recommend changing the class name. The definitions that I used are:

```css
.on-this-day-header {
  border-bottom:2px dotted #999;
}
 
.on-this-day {
  margin:1.5em 0 .5em;
  font:78%/1.4em "Trebuchet MS",Trebuchet,Arial,Verdana,Sans-serif;
  text-transform:uppercase;
  letter-spacing:.2em;
  color:#999;
}
```

Now you are ready to incorporate the function call. This really can be done anywhere in your blog, but it makes the most sense to include it with the date header. This will be different for every blog, but for a Blogger.com hosted blog, you are looking for the section enclosed by the `<BLOGDATEHEADER>` element. It usually looks like this:

```html
 <BLOGDATEHEADER>
      <H2 class="date-header"><$BlogDateHeaderDate$></H2>
   </BLOGDATEHEADER>
```

You need to change the `<BLOGDATEHEADER>` content so it looks like this:

```html
<BLOGDATEHEADER>
      <DIV class="on-this-day-header">
         <H2 class="date-header"><$BlogDateHeaderDate$></H2>
         <SCRIPT type="text/javascript">document.write(OnThisDay("<$BlogDateHeaderDate$>"));</SCRIPT>
      </DIV>
</BLOGDATEHEADER>
```

If you want to add a new site to the function, there are 4 simple steps to follow. For example, to add the BrainyHistory site to the function:

1. Modify the returnString variable to include the placeholder text for your new site. Remember, the order of the entries listed here will be the same order they are displayed, so make sure you put it in the correct spot.
```javascript
var returnString = "<SPAN class='\"on-this-day\"'>On this day: #Wikipedia# &#8225; #HistoryChannel# &#8225; #NYTimes# &#8225; #BBC# &#8225; #IMDB# &#8225; #Reference# &#8225; #Britannica# &#8225; #BrainyHistory# &#8225; #DailyBleed# &#8225; #OnThisDay#</SPAN>";
```
2. Add the following template variable:
```javascript
var BrainyHistory  = "<a target=\"_blank\" href=\"http://www.brainyhistory.com/days/#month#_#day#.html\">Brainy</a>";
```
3. Add the following fixup code:
```javascript
var dailyBleed = DailyBleed.replace(/#month#/, (month < 10 ? "0" + month : month)).replace(/#day#/, (day < 10 ? "0" + day : day));
```

In this case, the URL requires some additional logic to fixup the template parameters. This logic should be encapsulated in the template fixup code only.

4. Modify the return statement to add the new URL
```javascript
   return returnString.replace(/#Wikipedia#/, wikipedia)
           .replace(/#HistoryChannel#/, historyChannel)
           .replace(/#NYTimes#/, nyTimes)
           .replace(/#BBC#/, bbc)
           .replace(/#IMDB#/, imdb)
           .replace(/#Reference#/, reference)
           .replace(/#Britannica#/, britannica)
           .replace(/#BrainyHistory#/, brainyHistory)
           .replace(/#DailyBleed#/, dailyBleed)
           .replace(/#OnThisDay#/, onThisDay)
           ;
```