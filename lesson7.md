
## [Lesson 7: Using BgInfo to Display System Information on the Desktop](lesson7.md)



![SysInternals 7](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



If you have ever done system administration, you probably have the problem where you connect to so many servers that you have no idea which computer you are connected to half the time. BGInfo is a great utility that lets you display useful system information right on the desktop. And it works for regular Windows users as well.

SCHOOL NAVIGATION

1.  [What Are the SysInternals Tools and How Do You Use Them?](lesson1.md)
2.  [Understanding Process Explorer](lesson2.md)
3.  [Using Process Explorer to Troubleshoot and Diagnose](lesson3.md)
4.  [Understanding Process Monitor](lesson4.md)
5.  [Using Process Monitor to Troubleshoot and Find Registry Hacks](lesson5.md)
6.  [Using Autoruns to Deal with Startup Processes and Malware](lesson6.md)
7.  [Using BgInfo to Display System Information on the Desktop](lesson7.md)
8.  [Using PsTools to Control Other PCs from the Command Line](lesson8.md)
9.  [Analyzing and Managing Your Files, Folders, and Drives](lesson9.md)
10.  [Wrapping Up and Using the Tools Together](lesson10.md)

If you’ve been following along with our series, you might be surprised at the huge departure from hunting malware and deleting crapware to displaying stuff on the desktop, but the SysInternals tools aren’t just about finding things to kill. There are also many utilities in the toolkit used for displaying information, and we’re going to look at some of them.

The BGInfo utility displays information on the desktop, and it works in a server environment as well — in fact, that’s probably where it is the most useful, but it also works on anybody’s computer, so you can test things out on your local machine before running the configuration on the server.

You can also save information from BGInfo to a text file or even a database without even displaying on the desktop, so if you are looking for a quick way to [capture information on all the computers in your network](http://www.howtogeek.com/51544/use-bginfo-to-build-a-database-of-system-information-of-your-network-computers/), you can use BGInfo and some batch scripts to solve your problem.

> It’s worth noting that BGInfo displays information by writing text over top of your wallpaper, if you have wallpaper set. It will create a new wallpaper file and then assign that as your new default wallpaper.

If this isn’t your cup of tea, make sure to read through the rest of the series and wait for tomorrow’s lesson, when we’ll be discussing the very powerful set of PsTools provided by SysInternals.

### Using the BGInfo Interface

Using BGInfo is very simple: open it and click the Apply button, and your desktop will have a ton of system information plastered all over it right away. If you want that information to update regularly, we’ll need to add a shortcut to the startup folder, or create a scheduled task to do it.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Looking at the interface up close, you can see that there is an editor, a list of fields, and a bunch of formatting options. You can tweak and change it in any way that you’d like, and even insert data from text files and other places like the registry.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Once you’ve tweaked and created your configuration (more on that below), you can just save it out to a configuration file to load again any time you need it. Next you’ll need to make sure that BGInfo updates the information on a somewhat regular basis.

### Running BGInfo at Startup

The simplest thing to do is create a shortcut to BGInfo and place it into your startup folder, and modify that shortcut to include the path to the configuration that you’ve created and saved using the editor. You’ll also need to add a couple of command-line switches to make it happen.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



The important switches for our purposes are the /TIMER:0 switch, which sets the timeout before it applies to zero, the /SILENT switch which keeps everything quiet, and the /NOLICPROMPT switch, which skips the EULA dialog.

_Note: _the /POPUP switch and the /TASKBAR switch will stick BGInfo into your system tray and pop up a dialog with system information whenever you click on it, which is definitely a very useful option.

For example, if we save BGInfo.exe into the C:\Users\Lowell\bin\ folder and put the configuration as config.bgi into the same folder, we’d use this as the command line:

> bginfo.exe c:\users\lowell\bin\config.bgi /timer:0 /nolicprompt /silent

To make it run every time we startup the computer, open up Windows Explorer and type _shell:startup _into the location bar to open up the Startup folder.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Then type out the full path to BGInfo followed by the path to the configuration file, followed by the three switches we mentioned earlier.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



At this point you should have a shortcut in your Startup folder that should immediately display the configuration on the desktop.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



You could also open up Task Scheduler and create a new task that runs every x minutes if you want the information updated more often, but that’s a little beyond the scope of this lesson.

### Tweaking the Displayed Information

Changing the data that is displayed on the screen is easy enough, as the editor panel is just like any other rich text editor. You can add fields from the pane on the right, tweak the display of the data, etc. For instance, I wanted to just have a line across the top right-hand side of my monitor with some useful system information, and then show the name of the system below it in larger text, so I simply edited, used the align right button, and changed the font size for the element I wanted to change.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



After clicking Apply, this is what displayed in the top right-hand corner of my monitor — handy stuff for a system administrator.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



The Background dialog lets you change the wallpaper behind the image if necessary. For best results, you’d want to use the “Copy user’s wallpaper settings” the first time, and then change to the “Use these settings” to specifically select one if necessary.

_Note:_ One little problem is that if you create a new configuration, BGInfo gets a little confused and resets your wallpaper to black, so you have to set the wallpaper again, and then apply the configuration.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



You can use the Position button to change where on the screen the data will show up, and tweak a few other variables if necessary.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Clicking the Custom button underneath the Fields box will let you create user-defined fields that display special data that isn’t normally available, including pulling data from the registry, environment variables, WMI, files, or even VB Script. By extending BGInfo this way, you can make it display absolutely anything that you’d like to see on the desktop.

For example, if you want to grab the build number of Windows to use as a data point on the desktop, you would click the Registry value and then paste in the full path to a registry key in the Path field. (If you are running 64-bit Windows you would want to check the 64-bit registry view box or your lookup will be redirected to the 32-bit compatibility section of the registry.)

The Identifier would then show up in the Fields list, and you can select it to insert into the rich text editor.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



For WMI you can actually browse through all of the zillions of pieces of data and pick one to display. This would work the same way as the registry value — you’d give it a name, and then add that name to the rich text editor from the fields list.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



For the text file and VB Script user defined fields, you can pull in either the contents of a text file, which can come from anywhere, or you can create a VB script that runs on the command line and outputs data that illustrates anything you’d like.

For instance, to show your public IP address on the desktop, you could create a new script in Notepad, paste the following, and then save it as publicip.vbs.

> 

```
> Dim o
> Set o = CreateObject("MSXML2.XMLHTTP")
> o.open "GET", "http://ifconfig.me/ip", False
> o.send
> echo o.responseText
> 

```

Once you added this to the list, you would then have access to display the public IP address by adding “publicip” out of the Fields list. As you can imagine, there is a lot more that you can do with this, to the point of being nearly unlimited.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



RELATED ARTICLE

[![](data:image/jpeg;base64,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)](http://www.howtogeek.com/51544/use-bginfo-to-build-a-database-of-system-information-of-your-network-computers/)

[Use BGInfo to Build a Database of System Information of Your Network Computers](http://www.howtogeek.com/51544/use-bginfo-to-build-a-database-of-system-information-of-your-network-computers/)
The SysInternals suite has a number of great tools, but one you might not have used before is BGInfo, which you can use to customize the server wallpaper so you can see at a glance what server specs there are. [[Read Article]](http://www.howtogeek.com/51544/use-bginfo-to-build-a-database-of-system-information-of-your-network-computers/)

For the truly advanced users, you can also create a database on your network and [set BGInfo to run automatically on the client computers to populate the database](http://www.howtogeek.com/51544/use-bginfo-to-build-a-database-of-system-information-of-your-network-computers/). This way you could immediately know anything about them without having to pay for expensive management software.  Be sure to read the linked article for the entire guide.

### Next Lesson

Tomorrow we’re going to delve back into the super geeky world of SysInternals with a thorough examination of some of the command line tools, so be sure to check back for the rest of the series.

[Next Page: Using PsTools to Control Other PCs from the Command Line](lesson8.md)

[JOIN THE DISCUSSION (1 REPLY)](#)

### [Got Feedback? Click Here to Join the Discussion](http://discuss.howtogeek.com/t/using-bginfo-to-display-system-information-on-the-desktop/14689)



[Tweet](https://twitter.com/share)

[**Lowell Heddings**](http://www.howtogeek.com/author/thegeek/), better known online as the How-To Geek, spends all his free time bringing you fresh geekery on a daily basis. You can follow him on [Google+](https://plus.google.com/115673881208416151793/?rel=author) if you'd like.

*   Published 04/1/14

[](https://twitter.com/lowellheddings)



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)





http://www.howtogeek.com/school/sysinternals-pro/lesson7/


