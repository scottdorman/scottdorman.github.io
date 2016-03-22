---
layout: post
title: Visual Studio user settings per project/solution - update
date: 2007-04-25 20:12:13 -04:00
---

The other day, I [posted]({% post_url /2007/2007-04-23-111900 %}) about a [feature request](https://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=272773) submitted to Microsoft Connect. Well, it ended up getting 21 votes before Microsoft closed it as "Closed (Won't Fix)". The comment they left was

> Thanks for reporting this suggestion. Unfortunately we will not be able to address this in time for the upcoming release of Visual Studio (codename Orcas) but we will track this suggestion in our future release feature request database.

Now, I don't mind the fact that they said they won't be able to address it in time for the Orcas release. I know all too well the pressures of trying to release a product and the trade-offs that have to be made in order to meet the deadlines. However, it would be nice if I had a way to track this request once it does make its way on the feature list for a "future release".

It turns out that a [similar request](https://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=253597) was posted earlier this year, which was also closed. However, a workaround was provided that makes use of macros in Visual Studio. The details are here:

> Start by opening your solution. Make a note of the path where your .sln file is (you can click on the Solution node in the Solution Explorer tool window and view its Path in the Properties toolwindow)
> 
> To create the .vssettings file:
> 1. Set up the editor options the way you want them.
> 2. Export these settings using the "Tools/Import and Export Settings..." wizard like so:
> 2a. Select "Export selected environment settings" and click Next
> 2b. In the tree view, uncheck "All Settings" and expand the Options/Text Editor node
> 2c. Check only the nodes for which you want to save settings. The description pane on the right can help you decide which categories you need.
> 2d. Click Next
> 2e. Name the file "VSEditorFormatting.vssettings"
> 2f. For the directory, click the "Browse..." button and use the file dialog to navigate to the folder containing your solution (.sln) file. Click OK
> 2g. Click "Finish"
> 
> Now you have created the .vssettings file, add it to the associated solution like this:
> 1. Show the Solution Explorer if it isn't already (Ctrl+Alt+L)
> 2. Right click on the Solution node (at the top)
> 3. Select "Add Existing Item..."
> 4. Browse to the .vssettings file you saved earlier and click "Add"
> 
> At this point, if your project is under source code control you might want to add this new .vssettings file to your source code control.
> 
> Now, here comes the macro magic!
> 1. Launch the Macros IDE (Alt+F11)
> 2. In the "Project Explorer" toolwindow, double-click on "MyMacros" to expand it
> 3. Double-click on "EnvironmentEvents" to show the source code
> 4. Add this code just above the "End Module" statement at the end of the file:
> 
> '''''''''''''
>     Private Sub SolutionEvents_Opened() Handles SolutionEvents.Opened
>         Dim item As ProjectItem = DTE.Solution.FindProjectItem("VsEditorFormatting.vssettings")
>         If Not item Is Nothing Then
>             Dim name = item.FileNames(1)
>             DTE.ExecuteCommand("Tools.ImportandExportSettings", "/import:""" & name & """")
>         End If
>     End Sub
> '''''''''''''
> 
> What this does is hook up a handler for the "Solution.Opened" event. When it fires, the code looks for your "VsEditorFormatting.vssettings" file in the solution and, if it's found, it imports that file.
> 
> 5. Close the Macros IDE
> 6. Close Visual Studio (you will get prompted to save "MyMacros")
> 
> Now, every time you open a solution containing a "VsEditorFormatting.vssettings" file, it will be automatically imported for you. You will can need to share this macro with your co-workers so that they can take advantage of it.

Another solution, sent to the [Subtext](http://subtextproject.com/) mailing list by [Andrew Connell](http://andrewconnell.com/blog/ "Andrew Connell"), uses multiple shortcuts that launch Visual Studio 2005 and automatically load a settings file. The command line is:

> devenv.exe /resetsettings settingsfile.vssettings

To see the full details on how to do this, check out Andrews blog [post](http://andrewconnell.com/blog/archive/2006/08/25/3995.aspx).
