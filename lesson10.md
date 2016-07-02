# SysInternals Pro: Wrapping Up and Using the Tools Together

## [Lesson 10: Wrapping Up and Using the Tools Together](http://www.howtogeek.com/school/sysinternals-pro/lesson10/)



![SysInternals 10](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



We’re at the end of our SysInternals series, and it’s time to wrap everything up by talking about all the little utilities that we didn’t cover through the first nine lessons. There are definitely a lot of tools in this kit.

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

We’ve learned how to use Process Explorer to troubleshoot unruly processes on the system, and Process Monitor to see what they are doing under the hood. We’ve learned about Autoruns, one of the most powerful tools to deal with malware infections, and PsTools to control other PCs from the command line.

Today we’re going to cover the remaining utilities in the kit, which can be used for all sorts of purposes, ranging from viewing network connections to seeing effective permissions on file system objects.

But first, we’ll walk through a hypothetical example scenario to see how you might use a number of the tools together to solve a problem and do some research on what is going on.

### Which Tool Should You Use?

There isn’t always just one tool for the job — it’s much better to use them all together. Here’s an example scenario to give you an idea of how you might tackle the investigation, although it’s worth noting that there are any number of ways to figure out what’s going on. This is just a quick example to help illustrate, and is by no means an exact list of steps to follow.

**Scenario: System is Running Slow, Suspected Malware**

The first thing you should do is open up Process Explorer and see what processes are using up resources on the system. Once you’ve identified the process, you should use the built-in tools in Process Explorer to verify what the process actually is, make sure it’s legitimate, and optionally scan that process for viruses using the built-in VirusTotal integration.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



This process is actually a SysInternals utility, but if it wasn’t, we’d be checking it.

_Note: _if you really think there might be malware, it’s often helpful to unplug or disable internet access on that machine while troubleshooting, although you might want to do VirusTotal lookups first. Otherwise that malware might download more malware, or transmit more of your information.

If the process is completely legitimate, kill or restart the offending process, and cross your fingers that it was a fluke. If you don’t want that process to start anymore, you can either uninstall it, or use Autoruns to stop the process from loading at startup.

If that doesn’t solve the problem, it might be time to pull out Process Monitor and analyze the processes that you’ve already identified and figure out what they are trying to access. This can give you clues into what is actually going on — maybe the process is trying to access a registry key or file that doesn’t exist or it doesn’t have access to, or maybe it is just trying to hijack all of your files and do lots of sketchy things like accessing information that it probably shouldn’t, or scanning your whole drive for no good reason.

In addition, if you suspect that the application is connecting to something that it shouldn’t, which is very common in the case of spyware, you’d pull out the TCPView utility to verify whether that is the case.

At this point you might have determined that the process is malware or at crapware. Either way you don’t want it. You can run through the uninstall process if they are listed in Control Panel’s Uninstall Programs list, but many times they aren’t listed, or don’t clean up properly. This is when you pull out Autoruns and find every place that the application has hooked into the startup, and nuke them from there, and then nuke all of the files.

> Running a full virus scan of your system is also helpful, but lets be honest… most crapware and spyware gets installed despite anti-virus applications being installed. In our experience, most anti-virus will happily report “all clear” while your PC can barely operate because of spyware and crapware.

### TCPView

This utility is a great way to see what applications on your computer are connecting to what services over the network. You can see most of this information on the command prompt using netstat, or buried in the Process Explorer / Monitor interface, but it’s much easier to just pop open TCPView and see what is connecting to what.

The colors in the list are pretty simple and similar to the other utilities — bright green means that the connection just showed up, red means the connection is closing, and yellow means the connection changed.

You can also look at the process properties, end the process, close the connection, or pull up a Whois report. It’s simple, functional, and very useful.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



_Note: _When you first load TCPView, you might see a ton of connections from [System Process] to all sorts of internet addresses, but this usually isn’t a problem. If all of the connections are in the TIME_WAIT state, that means that the connection is being closed, and there isn’t a process to assign the connection to, so they should up as assigned to PID 0 since there’s no PID to assign it to.

This usually happens when you load up TCPView after having connected to a bunch of things, but it should go away after all the connections close and you keep TCPView open.

### Coreinfo

Shows information on the system CPU and all of the features. Ever wondered if your CPU is 64-bit or if it supports hardware-based virtualization? You can see all that and much, much more with the coreinfo utility. This can be really useful if you want to see whether an older computer can run the 64-bit version of Windows or not.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)

 

### Handle

This utility does the same thing that Process Explorer does — you can quickly search to find out which process has an open handle that is blocking access to a resource, or from deleting a resource. The syntax is pretty simple:

> handle 

And if you want to close the handle, you can use the hexadecimal handle code (with -c) in the list combined with the process ID (the -p switch) to close it.

> handle -c  -p 



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



It’s probably a lot easier to use Process Explorer for this task.

### ListDlls

Just like Process Explorer, this utility lists out the DLLs that are loaded as part of a process. It’s a lot easier to use Process Explorer, of course.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



### RamMap

This utility analyzes your physical memory usage, with loads of different ways to visualize the memory, including by physical pages, where you can see the location in RAM that each executable is loaded into.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



### Strings Finds Human-Readable Text in Apps and DLLs

If you see a weird URL as a string in some software package, it is time to worry. How would you see that weird string? Using the strings utility from the command prompt (or using the function in Process Explorer instead).



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



[Next Page: Configuring Auto Logon and ShellRunAs](http://www.howtogeek.com/school/sysinternals-pro/lesson10/2/)

*   1

*   [2](http://www.howtogeek.com/school/sysinternals-pro/lesson10/2/)
*   [Next](http://www.howtogeek.com/school/sysinternals-pro/lesson10/2/)

[JOIN THE DISCUSSION (6 REPLIES)](#)

*   [April 4, 2014](#)
Iszi

About ShellRunAs: If you're in an enterprise environment which enforces smart card usage for authentication to the system, this may not work for you. Also, in Windows 7 (maybe Vista and 8 also) the functionality is built-in to the Shift+Right-Click menu.

*   [April 4, 2014](#)
Lowell Heddings

I knew I was forgetting something when I was writing it... ended up being a bit rushed while writing this one, and it definitely comes through in the text.

Updated the ShellRunAs section.

*   [April 4, 2014](#)
Iszi

Cool. I had to find this out myself the hard way one time when my organization rolled out smart card logon enforcement and suddenly the ShellRunAs wouldn't work for me. I called support and they couldn't figure out why it wasn't working either - until finally it came up that I wasn't using Shift+Right-Click. They were assuming that I was trying to use Windows' built-in RunAs functionality (which does support smart card logon) instead of a Sysinternals tool.

*   [April 5, 2014](#)
Te Kooti

Found a wonderful GUI that imports both Sysinternals and Nirsoft utilities and operates as a front end.

[http://www.kls-soft.com/wscc/](http://www.kls-soft.com/wscc/)

Saves a LOT of time and trouble.

Keep fixing....

Fred

*   [April 7, 2014](#)
rseiler

The link that you provide in the Autologon section is an easy way of doing the same thing, yes. However, that method will not work for domain-joined machines. Autologon will.

### [Got Feedback? Click Here to Join the Discussion](http://discuss.howtogeek.com/t/wrapping-up-and-using-the-tools-together/14763)



[Tweet](https://twitter.com/share)

[**Lowell Heddings**](http://www.howtogeek.com/author/thegeek/), better known online as the How-To Geek, spends all his free time bringing you fresh geekery on a daily basis. You can follow him on [Google+](https://plus.google.com/115673881208416151793/?rel=author) if you'd like.

*   Published 04/4/14

[](https://twitter.com/lowellheddings)



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)


http://www.howtogeek.com/school/sysinternals-pro/lesson10/