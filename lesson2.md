## [Lesson 2: Understanding Process Explorer](http://www.howtogeek.com/school/sysinternals-pro/lesson2/)



![SysInternals 2](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



This lesson in our Geek School series covers Process Explorer, perhaps the most used and useful application in the SysInternals toolkit. But how well do you really know this utility?

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

Process Explorer, a task manager and system monitor application, has been around since 2001, and while it used to even work on Windows 9x, the modern versions only support XP and above, and they’ve been continually updated with features for modern versions of Windows. It’s the defacto standard for dealing with troubleshooting processes.

### So What Can Process Explorer Do?

Some of the better features include the following, although this is by no means an exhaustive list. This application has many features, and many of those are buried deep within the interface. Amazingly it’s also a very small file.

*   The default tree view shows the hierarchical parent relationship between processes, and displays using colors to easily understand processes at a glance.

*   Very accurate CPU usage tracking for processes.

*   Can be used to replace Task Manager, which is especially useful on XP, Vista, and Windows 7.

*   Can add multiple tray icons to monitor CPU, Disk, GPU, Network, and more.

*   Figure out which process has loaded a DLL file.

*   Figure out which process is running an open window.

*   Figure out which process has a file or folder open and locked.

*   View complete data about any process, including threads, memory usage, handles, objects, and pretty much anything else there is to know.

*   Can Kill an entire process tree, including any processes started by the one you choose to kill.

*   Can Suspend a process, freezing all its threads so they do nothing.

*   Can see which thread in a process is actually maxing out the CPU.

*   The latest version (v16) integrates VirusTotal into the interface so you can check a process for viruses without leaving Process Explorer.

Any time you have a problem with an application, or something keeps freezing on your computer, or maybe you are trying to figure out what a particular DLL file is used for, Process Explorer is the tool for the job.

### Understanding The Tree View



![Windows_8_1__Installed_with_Tools_-_1___Running_](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



When you first launch Process Explorer, you are presented with a lot of visual data right away – there is a hierarchical tree view of the processes running on your computer, including CPU and RAM usage using numerical values for each process. There are some little mini activity graphs running at the top in the toolbar, showing you the CPU usage, which can be clicked on to display in a separate window.

There’s definitely a lot going on, and it would be easy to be overwhelmed by everything on the screen.

The initial display gives you a set of columns that include:

*   **Process** – the file name of the executable along with the icon if one exists.

*   **CPU** – the percentage of CPU time in the last second (or whatever the update speed is set to)

*   **Private Bytes** – the amount of memory allocated to this program alone.

*   **Working Set** – the amount of actual RAM allocated to this program by Windows.

*   **PID**  – the process identifier.

*   **Description** – the description, if the application has one.

*   **Company Name** – this one is more useful than you think. If something isn’t quite right, start by looking for processes that aren’t by Microsoft.

You can customize these columns and add many other options, or you can just click on any of the columns to sort by that field. If you’ve ever used Task Manager before, you’ve probably sorted by Memory or CPU, and you can do that here as well.

Clicking on Process will flip between sorting by the process name, or going back to the default tree view, which is very useful once you get used to it.

The view is updated once per second, but you can go to View -> Update Speed and customize how often it updates, the lowest being 0.5 seconds and the top level being 10 seconds. If you are using it for troubleshooting the default value is probably fine, but if you want to use it as a CPU monitor sitting in the system tray, 5 or 10 seconds might use less CPU while it runs in the background.

You can also pause the view under the same sub-menu, or by simply hitting the Space bar. This will freeze the view as a snapshot in time, which can be useful if you are trying to identify a process that starts and quickly dies, or if you have decided to sort by CPU usage and all the rows keep jumping around.

In the case of a quickly closing process, however, you would want to add extra columns to the default view for anything you might need to know, because clicking on a defunct process in the list won’t show much in the details view if the process isn’t running, even if you paused everything.

### Understanding All Those Colors

There are definitely a lot of colors in a typical Process Explorer list, which can be a little confusing for the beginner geek. It’s really important to learn what all these colors mean, because they aren’t there just for show — they each mean something important.

Whenever you can’t remember what one of the colors means, you can go to Options -> Configure Colors on the menu to pull up the Color Selection dialog. This is basically a quick cheat sheet to what everything means. Keep reading, since we’re going to explain it here as well.



![Windows 8](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Based on the colors in the picture above, here is what each of the selected items mean (the others aren’t really important).

*   **New Objects (Bright Green)** – When a new process shows up in Process Explorer, it starts out as bright green.

*   **Deleted Objects (Red)** – When a process is killed or closes it will usually flash red right before deleting.

*   **Own Processes (Light Blueish)** – Processes running as the same user account as Process Explorer.

*   **Services (Light Pink)** – Windows Service processes, although it’s worth noting that they might have child processes that are launched as a different user, and those might be a different color.

*   **Suspended Processes (Dark Gray)** – When a process is suspended it can’t do anything. You can easily use Process Explorer to suspend an application. Sometimes crashed apps will briefly show up in gray while Windows is handling the crash.

*   **Immersive Process (Bright Blue) –** This is just a fancy way of saying that the process is a Windows 8 application using the new APIs. In the screenshot earlier you might have noticed WSHost.exe, which is a “Windows Store Host” process that runs Metro apps. For some reason Explorer.exe and Task Manager will also show up as immersive.

*   **Packed Images (Purple)** – these processes might contain compressed code hidden inside of them, or at least Process Explorer thinks that they do by using heuristics. If you see a purple process, make sure to scan for malware!

Since there is obviously some overlap between these different scenarios, the colors will be applied in an order of precedence. If a process is a service and is suspended, it will display in dark gray because that color is more important.

From what we’ve learned while researching, the order is Suspended > Packed > Immersive > Services -> Own Processes.

### Verifying Application Identity

One really useful option that we’re surprised isn’t enabled by default is found at Options -> Verify Image Signatures.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



This option will check the digital signature for each executable file in the list, which is an invaluable troubleshooting tool when you are looking at some suspicious application that is running in the list.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



The vast majority of reputable software should be digitally signed at this point. If something isn’t, you should look very carefully at whether you should be using it.

### Taking Action on a Process

You can quickly take action on any process by right-clicking on it and choosing from one of the options, or by using the shortcut keys if you prefer. Those options include:

*   **Window** – has options including Bring to Front, which can be useful to help identify the window associated with a process. If there are no windows for that process, it will be grayed out.

*   **Set Priority** – you can use this to configure the priority of a process. This is mostly useful for taming a runaway process that you don’t want to kill.

*   **Kill Process** – just like you’d imagine, this quickly kills that process.

*   **Kill Process Tree** – This kills not just the item in the list, but also the children of that parent process.

*   **Restart** – spectacularly useful while testing, this just kills the process and then restarts it. It’s worth noting that killing processes might result in lost data.

*   **Suspend** – this handy option is great for troubleshooting when a process is out of control. You can simply suspend the process rather than kill it, and check to see if anything is out of whack.

*   **Check VirusTotal** – this is a new option that we’ll explain further along. It’s quite handy really, as it checks the process for viruses.

*   **Search Online** – this will just search the web for the name of the process.

And obviously if you open up Properties that will take you to even more useful information about the process, much of which we’ll get into in the next lesson.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



_Note:_ we tested out the Temp option but did not have any idea what it does.

### Running as Administrator

While you don’t absolutely have to run Process Explorer as Administrator, without doing so many of the useful features won’t work, and you won’t be able to see as much information about each process.

If you are running on Windows XP or 2003, you will need to be running as an account that has full Administrator rights to use most of the features. This is probably not a problem for most people, because XP gave the default account full privileges anyway, but if you are trying to use this at work without administrator access, it won’t work quite as well.

Since most of our readers are using Windows 7, 8.x, or even Vista, you’ll probably be familiar with running an application as Administrator. It’s really easy… just right-click and choose the option from the menu.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



_Fun fact:_ Process Explorer actually uses the Debug Programs privilege, which goes a long way to explain why it is so powerful.

### Forcing Process Explorer to Always Open as Administrator

If you want to make sure that Process Explorer always opens as Administrator without having to remember to right-click on it, you can force it by either making a special shortcut that requires Administrator mode, or by opening up the Properties for procexp.exe, going to Compatibility, and then choosing the option for “Run this program as an administrator”.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Either way will work just fine, or you could also just disable UAC if you prefer, which makes everything run as administrator all the time. We’re not recommending that, but you can do it.

### Using Process Explorer to Replace Task Manager

Process Explorer has long been used as a powerful replacement for the previously anemic Task Manager application in every version of Windows prior to Windows 8, and assuming you want some real power in your hands, it works really well as a replacement in that version too.

_Note:_ Windows 8’s Task Manager is greatly improved from previous versions. It’s still not as powerful as Process Explorer, but it’s probably easier for regular people to use. So don’t change mom’s computer to default to Process Explorer.

To make Process Explorer replace Task Manager, all you have to do is choose the Options -> Replace Task Manager option from the menu. That’s it.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Once you’ve done that, using CTRL + SHIFT + ESC or right-clicking on the Taskbar will both launch Process Explorer rather than Task Manager. Easy, right?

_Warning_: if you do replace Task Manager, make absolutely certain that you’ve put Process Explorer in a place that you won’t be accidentally moving or deleting the file. Otherwise you’ll be stuck with a system that can’t launch any Task Manager.

### Using Process Explorer as an Awesome Tray Icon Monitor



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



One of the best features of Process Explorer is the ability to minimize it into the system tray, but instead of just a single icon, it can minimize into a full set of icons that can monitor CPU, I/O, Disk, Network, GPU, and RAM, or any combination of them. You can configure them to display separately, or not at all, if you prefer.

To set this up, open up the Options menu, go to the Tray Icons section, and then click to enable each of the tray icons that you would like to see.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



You could just run Process Explorer every time you start running your computer, and then minimize it to the system tray so it will always be there for you. And, of course, if you used the option to replace Task Manager, you can quickly access it any time with a shortcut key – though you might want to use the “Allow Only One Instance” option to make sure you don’t open a bunch of separate windows.

### Using Process Explorer to Quickly Search VirusTotal

If you are working on a problem PC and want to figure out if a process is a virus, you can save yourself some time by using Process Explorer version 16 or above, because they’ve added VirusTotal integration directly into the application. Just right-click on anything in the list to see the option.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



The first time you run it, you’ll be asked to accept the VirusTotal terms of use, but after you do so, you will see the VirusTotal results show up right there in the list.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



You can click on the result to go to VirusTotal and see the details.  It’s a great new addition to one of the best utilities ever.

### Next Lesson: Using Process Explorer to Troubleshoot and Diagnose

In the next lesson in our series we’re going to go into a lot more depth about how to use Process Explorer in some real-world scenarios to troubleshoot common problems like malware and crapware. Make sure to stay tuned for the rest of the series.

[Next Page: Using Process Explorer to Troubleshoot and Diagnose](http://www.howtogeek.com/school/sysinternals-pro/lesson3/)

[JOIN THE DISCUSSION (9 REPLIES)](#)

*   [March 25, 2014](#)
Shirl

Excellent tutorial, I hadn't found the Virus Total thingy, thanks for that.

There is one good reason NOT to use Process Explorer to replace Task Manager and that's if you need to restart Windows Explorer. It works 100% of the time with Task Manager but occasionally it simply doesn't with PE.

*   [March 25, 2014](#)
Iszi

I didn't know about the VirusTotal option either - that's a pretty cool feature! I especially like how you can go into the Options menu and have it turned on for all processes, and then submit any files Virus Total doesn't recognize as a batch.

I found it rather interesting to see some of the items that got flagged by some of the VirusTotal scanners. (Well, just one scanner really.)

[iPodService.exe](https://www.virustotal.com/en/file/9cdd0b99f2c5dad573a9ea8d5ab2dbfd7a941454cbba5bfe34e49f2d4ee96a90/analysis/) (The 64-bit iPod Service Module)
[atiesrxx.exe](https://www.virustotal.com/en/file/f185eab171b8298abcae61b8265f57580ae8a2f424d5bd51e56c6ab482d26fce/analysis/) (AMD External Events Service Module)

The Verified Signer column is also a cool feature I hadn't come across yet. For as long as I've been using Process Explorer, I'm a little surprised at some of the things I never realized it could do.

*   [March 25, 2014](#)
Tracy Scanlon

This is a great article, but PE has more colors i would like to find out about. On the sysinternals, and Microsoft site is very complicated for a beginner.I have yellow, and brown too.

*   [March 26, 2014](#)
Iszi

To get the full coloring legend, go to Options->Configure Colors. According to that dialog, the default yellow may either be "Relocated DLLs" or ".Net Processes" and brown would be "Jobs" - however, none of these are enabled by default. (Neither, for that matter, is the "Immersive Process" option mentioned in the HTG article.)

*   [March 26, 2014](#)
Lowell Heddings

Immersive Process is enabled by default if you run Process Explorer on Windows 8.1 from what I can tell.

The .NET, Relocated, and Jobs are just mostly for developers and aren't actually used much or useful for regular troubleshooting.

*   [March 26, 2014](#)
Iszi

A couple more interesting VirusTotal findings. It looks like this "Anity-AVL" scanner has a fairly broad definition of "Trojan".

[SDWSCSvc.exe](https://www.virustotal.com/en/file/a9e86fe6efd3cfd4ea1a26121c706335a6791cc6f81ee98ae2be7ea566ecfebb/analysis/) (Spybot S&D Windows Security Center integration service)
[TrueCrypt.exe](https://www.virustotal.com/en/file/7f4e7ac770928e9d313b7e91db4b904a98f3d8bbac3e0b88fbca9ef15dd6ed71/analysis/) (Main executable for TrueCrypt)

*   [March 26, 2014](#)
Iszi



geek said:

> Immersive Process is enabled by default if you run Process Explorer on Windows 8.1 from what I can tell.



That explains it. I'm still sticking with Windows 7.

*   [March 26, 2014](#)
Tracy Scanlon

Thank you for the answer, I figured it out by playing around with the program (should have done that first...) Greenie.

### [Got Feedback? Click Here to Join the Discussion](http://discuss.howtogeek.com/t/understanding-process-explorer/14508)



[Tweet](https://twitter.com/share)

[**Lowell Heddings**](http://www.howtogeek.com/author/thegeek/), better known online as the How-To Geek, spends all his free time bringing you fresh geekery on a daily basis. You can follow him on [Google+](https://plus.google.com/115673881208416151793/?rel=author) if you'd like.

*   Published 03/25/14

[](https://twitter.com/lowellheddings)



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)




http://www.howtogeek.com/school/sysinternals-pro/lesson2/

