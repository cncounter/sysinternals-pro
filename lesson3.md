
## [Lesson 3: Using Process Explorer to Troubleshoot and Diagnose](lesson3.md)



![SysInternals 3](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Understanding how Process Explorer’s dialogs and options work is all fine and good, but what about using it for some actual troubleshooting or to diagnose a problem? Today’s Geek School lesson will try and help you learn how to do just that.

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

Not that long ago, we started investigating all sorts of malware and crapware that gets installed automatically any time you don’t pay attention while installing software. Nearly every piece of freeware on the market, including the “reputable” ones, are bundling toolbars, search hijacking awfulness, or adware, and some of it is hard to troubleshoot.

We’ve seen many computers from people that we know that have so much spyware and adware installed that the PC barely even loads anymore. Trying to load the web browser, especially, is nearly impossible, as all of the adware and tracking software competes for resources to steal your private information and sell it to the highest bidder.

So naturally, we wanted to do a bit of investigation into how some of these work, and there’s no better place to start than the Conduit Search malware that has claimed hundreds of millions of computers worldwide. This nefarious awfulness hijacks your search engine in your browser, changes your home page, and most annoyingly, it takes over your New Tab page no matter what your browser is set to.

We’ll start with looking at that, and then we’ll show you how to use Process Explorer to troubleshoot errors that talk about locked files and folders that are in use.

And then we’ll round it out with another look at how some adware these days are hiding themselves behind Microsoft processes so they appear legit in Process Explorer or Task Manager, even though they really aren’t.

### Investigating the Conduit Search Malware

As we mentioned, the Conduit search hijacker is one of the most persistent, awful, and terrible things that nearly every one of your relatives probably has on their computer. They bundle their software in shady ways with any freeware they can, and in many instances, even if you select to opt-out, the hijacker will still be installed.

Conduit installs what they call “Search Protect”, which they claim prevents malware from making changes to your browser. What they don’t mention is that it also prevents you from making any changes to their browser unless you use their Search Protect panel to make those changes, which most people won’t know about since it’s buried in the system tray.

Not only will Conduit redirect all of your searches to their own custom Bing page, it will set that as  your home page. One would have to assume that Microsoft is paying them for all this traffic to Bing, since they are also passing some _?pc=conduit_ type of arguments in the query string.

_Fun fact: the company behind this piece of garbage is worth 1.5 Billion dollars and JP Morgan invested $100 million into them. Being evil is profitable._

### Conduit Hijacks the New Tab Page… But How?

Hijacking your search and home page is trivial for any malware — this is where Conduit steps up the evil and somehow rewrites the New Tab page to force it to show Conduit, even if you change every single setting.

You can uninstall all of your browsers, or even install a browser you didn’t have installed before, like Firefox or Chrome, and Conduit will still manage to hijack the New Tab page.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Somebody should be in jail, but they are probably on a yacht.

It doesn’t take much in terms of geek skills to eventually deduce that the problem is the Search Protect application running in the system tray. Kill that process, and suddenly your new tabs open just the way the browser maker intended.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



But how, exactly, does it do this? There are no add-ons or extensions installed into any of the browsers. There aren’t any plugins. The registry is clean. How do they do it?

This is where we turn to Process Explorer to do some investigation. First, we’ll find the Search Protect process in the list, which is easy enough because it is properly named, but if you weren’t sure, you can always open up the window and use the little bulls-eye icon next to the binoculars to figure out which process belongs to a window.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Now you can simply select the appropriate process, which in this case was one of the three that run automatically by the Windows Service that Conduit installs. How did I know that it was a Windows Service that restarts it? Because the color of that row is pink, of course. Armed with that knowledge, I could always go stop or delete the service (though in this particular case, you can simply uninstall from Uninstall Programs in Control Panel).

Now that you’ve selected the process, you can use the CTRL + H or CTRL + D shortcut keys to open the Handles view or the DLLs view, or you can use the View -> Lower Pane View menu to do it.

> _Note: _in the world of Windows, a “handle” is an integer value that is used to uniquely identify a resource in memory like a window, an open file, a process, or many other things. Each open application window on your computer has a unique “window handle”, for example, that can be used to reference it.
> 
> DLLs, or dynamic link libraries, are shared pieces of compiled code that are stored in a separate file to be shared among multiple applications. For instance, instead of having every application write their own File Open / Save dialogs, all applications can simply use the common dialog code provided by Windows in the comdlg32.dll file.

Looking through the list of handles for a few minutes brought us a little bit closer to what was going on, because we found handles to Internet Explorer and Chrome, both of which are currently open on the test system. We’ve definitely confirmed that Search Protect is doing something to our open browser windows, but we’ll need to do a little more research to figure out exactly what.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



The next thing to do is double-click the process in the list to open up the details view, and then flip over to the Image tab, which will give you information about the full path to the executable, the command line, and even the working folder. We’ll click the Explore button to take a look at the installation folder and see what else is hiding there.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Interesting! We’ve found a number of DLL files here, but for some weird reason none of these DLL files were listed in the DLL view for the Search Protect process when we were looking at it earlier. This could be a problem.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



[Next Page: Dealing with Locked Files and Folders](lesson3.md2/)

*   1

*   [2](lesson3.md2/)
*   [Next](lesson3.md2/)

[JOIN THE DISCUSSION (8 REPLIES)](#)

*   [March 26, 2014](#)
Shirl

I'm really enjoying this series.

One thing worth noting is that the Help utilities with most SysInternals programs are worth looking at. Some utilities have been around for years though and the Help is in an old format Winhlp32, and you may need to install KB917607 to read them.

*   [March 26, 2014](#)
corvynem

Excellent series, I'm learning quite a bit about how to go beyond the limited information in the task manager. Microsoft deserve much credit (never thought I'd say that!) for buying the company and providing the sysinternals suite for free.

*   [March 26, 2014](#)
Lowell Heddings

While helpful, I've found that the help files with the SysInternals tools are pretty limited in scope, though. I had to do a lot more digging to come up with some of the answers I was looking for.

*   [March 26, 2014](#)
Tracy Scanlon

When I click on the bulls-eye thing it says"drag over window" What window? I don't see what this does? When I click on it, it just goes to the back of everything? Dragging it around doesn't do anything either?

*   [March 27, 2014](#)
Marc Laflamme

Tracy,

The bullseye helps you find processes from their windows. If you open 3 programs and have them on screen at the same time and drag the bullseye over one of them and let go, Process Explorer will be moved back to focus and the process running the application you placed the bullseye over will be selected. Does that help?

### [Got Feedback? Click Here to Join the Discussion](http://discuss.howtogeek.com/t/using-process-explorer-to-troubleshoot-and-diagnose/14532)



[Tweet](https://twitter.com/share)

[**Lowell Heddings**](http://www.howtogeek.com/author/thegeek/), better known online as the How-To Geek, spends all his free time bringing you fresh geekery on a daily basis. You can follow him on [Google+](https://plus.google.com/115673881208416151793/?rel=author) if you'd like.

*   Published 03/26/14

[](https://twitter.com/lowellheddings)



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)




http://www.howtogeek.com/school/sysinternals-pro/lesson3/
