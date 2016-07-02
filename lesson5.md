
## [Lesson 5: Using Process Monitor to Troubleshoot and Find Registry Hacks](http://www.howtogeek.com/school/sysinternals-pro/lesson5/)



![SysInternals 5](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



In today’s edition of Geek School we’re going to teach you how to use Process Monitor to actually accomplish troubleshooting and figuring out registry hacks that you would not know about otherwise.

SCHOOL NAVIGATION

1.  [What Are the SysInternals Tools and How Do You Use Them?](http://www.howtogeek.com/school/sysinternals-pro/lesson1/)
2.  [Understanding Process Explorer](http://www.howtogeek.com/school/sysinternals-pro/lesson2/)
3.  [Using Process Explorer to Troubleshoot and Diagnose](http://www.howtogeek.com/school/sysinternals-pro/lesson3/)
4.  [Understanding Process Monitor](http://www.howtogeek.com/school/sysinternals-pro/lesson4/)
5.  [Using Process Monitor to Troubleshoot and Find Registry Hacks](http://www.howtogeek.com/school/sysinternals-pro/lesson5/)
6.  [Using Autoruns to Deal with Startup Processes and Malware](http://www.howtogeek.com/school/sysinternals-pro/lesson6/)
7.  [Using BgInfo to Display System Information on the Desktop](http://www.howtogeek.com/school/sysinternals-pro/lesson7/)
8.  [Using PsTools to Control Other PCs from the Command Line](http://www.howtogeek.com/school/sysinternals-pro/lesson8/)
9.  [Analyzing and Managing Your Files, Folders, and Drives](http://www.howtogeek.com/school/sysinternals-pro/lesson9/)
10.  [Wrapping Up and Using the Tools Together](http://www.howtogeek.com/school/sysinternals-pro/lesson10/)

Process Monitor is one of the most impressive tools that you can have in your toolkit, as there is almost no other way to see what an application is actually doing under the hood. It is the only way to know what files are being written to by which process, and where things are stored in the registry, and which files are accessing them.

We’ll start off with today’s lesson by looking at how to find registry keys using Windows setting dialogs and Process Monitor, and then we’ll go through an actual troubleshooting scenario that we encountered on one of our computers in the lab, and easily solved using Process Monitor.

### Using Process Explorer to Find Registry Keys for Common Settings

Everybody has clicked a checkbox or changed the value of a drop-down box at some point, but have you ever wondered where those values are actually stored? Many applications, and virtually everything in Windows, is stored in the Registry… somewhere.

For today’s example we’re going to use the first option on the first pane of Taskbar and Navigation Properties, which is a dialog that should exist in all versions of Windows. So now our mission is to figure out where that setting is actually stored in the registry. You can follow along with this particular setting, or you can try one of the other settings on the same dialog — or anywhere else you’d like to find the hidden setting location for.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



The first thing you’ll want to do whenever trying to capture a set of data is to launch Process Monitor, and then change the setting. At that point you can stop Process Monitor from continuing to capture events, so the list doesn’t get out of control. (Hint: the File menu has the option, or it’s the third icon from the left).

Now that we’ve got a ton of data in the list, it’s time to filter the list to reduce the number of rows that we’re going to have to look through. Since we’re looking at a registry value that is being changed, we’ll need to filter by “RegSetValue”, which is what Windows uses to actually set a registry key to a new setting. Use the “Include” option to show _only_ those events.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Your list should now be limited to just registry keys that were changed, so it’s time to take a look at the events and try to figure out which registry key it might be. Since we’re checking the “Lock the Taskbar” setting, and one of the registry keys being set includes the word “Taskbar” in the name, that’s a good place to start. Right-click on the path and choose to Jump To the location.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Process Monitor will open up the Registry Editor and highlight the key in the list. Now we need to make sure that this is actually the right key, which is pretty easy to figure out. Take a look at the setting, and then take a look at the key. Right now the setting is on, and the key is set to 0.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



So change the setting, hit Apply on the dialog, and then use the F5 key to refresh the Registry Editor window. In our case we definitely picked the right setting, so now you can see that the TaskbarSizeMove value is set to 1.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



If you didn’t pick the right value, you won’t see a change when you do the setting test again. So go and find the next logical one, and start over.

### Troubleshooting Problems with Process Monitor

It’s not really possible to illustrate in a single article how to troubleshoot any problem with Process Monitor, or any other tool for that matter. There are just way too many combinations of issues that could possibly go wrong.

What we can do, however, is show how we actually used Process Monitor to troubleshoot a real problem that actually happened to one of our test computers. We had been installing some crapware, and then decided to try and clean the computer up. The problem was an entry in the Uninstall Programs panel that just wouldn’t go away.

[Next Page: Troubleshooting Problems with Process Monitor](http://www.howtogeek.com/school/sysinternals-pro/lesson5/2/)

*   1

*   [2](http://www.howtogeek.com/school/sysinternals-pro/lesson5/2/)
*   [Next](http://www.howtogeek.com/school/sysinternals-pro/lesson5/2/)

[JOIN THE DISCUSSION (6 REPLIES)](#)

*   [March 28, 2014](#)
Tracy Scanlon

Here's a couple of screen shots, I'm lost. I guess not.It won't let me. I guess I will fiddle around with PM some more.What filters are you using? Because i put in operation is regsetvalue, and then i drug the bulls-eye over the taskbar window and i get expoler.exe HKCU ,user assist, but nothing with taskbar in the path. Then i tried path contains taskbar and nothing comes up.

*   [March 28, 2014](#)
Iszi

Glad to know the Sysinternals series is getting more than a week. There's so much more than just Process Explorer and Process Monitor, even though those on their own are pretty epic tools.

[@geek](http://www.howtogeek.com/users/geek) - Do you mind giving us an idea of which command-line tools you plan on featuring?

*   [March 28, 2014](#)
Lowell Heddings

Still deciding, I haven't actually finished the second half of the series yet. Any preferences? There are definitely a ton of tools, and I don't know if another 5 parts will be enough time to cover them all.

*   [March 31, 2014](#)
Iszi

It looks like you've got a lot of the big ones already covered, or on tap. In "using PsTools" I might suggest covering PSLoggedOn. It's probably more use to enterprise admins than at-home geeks, but also probably the command-line SysInternals tool I personally use the most.

Another one of interest might be Desktops - the virtual desktop manager. Haven't tried it myself (the idea of multiple desktops never really caught on with me) but I'm sure there's others who would be interested.

ShellRunAs is cool, but deprecated with Shift+Right-Click in Win7 (and maybe Vista).

I'm not sure what the purpose of PsShutdown is, since Windows already has a built-in shutdown utility usable via CLI or GUI - and it works across the network as well. Maybe it is from a time before that was part of the standard build.

*   [March 31, 2014](#)
Iszi

TCPView! How did I forget TCPView?!

[TCPView](http://technet.microsoft.com/en-us/sysinternals/bb897437.aspx) is pretty awesome.

### [Got Feedback? Click Here to Join the Discussion](http://discuss.howtogeek.com/t/using-process-monitor-to-troubleshoot-and-find-registry-hacks/14602)



[Tweet](https://twitter.com/share)

[**Lowell Heddings**](http://www.howtogeek.com/author/thegeek/), better known online as the How-To Geek, spends all his free time bringing you fresh geekery on a daily basis. You can follow him on [Google+](https://plus.google.com/115673881208416151793/?rel=author) if you'd like.

*   Published 03/28/14

[](https://twitter.com/lowellheddings)



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)

http://www.howtogeek.com/school/sysinternals-pro/lesson5/