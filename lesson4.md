
## [Lesson 4: Understanding Process Monitor](lesson4.md)



![SysInternals 4](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Today in this edition of Geek School we’re going to teach you about how the Process Monitor utility allows you to peek under the hood and see what your favorite applications are really doing behind the scenes — what files they are accessing, the registry keys they use, and more.

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

Unlike the Process Explorer utility that we’ve spent a few days covering, Process Monitor is meant to be a passive look at everything that happens on your computer, not an active tool for killing processes or closing handles. This is like taking a peek at a global logfile for every single event that happens on your Windows PC.

Want to understand which registry keys your favorite application is actually storing their settings in?  Want to figure out what files a service is touching and how often? Want to see when an application is connecting to the network or opening a new process? It’s Process Monitor to the rescue.

We don’t do a lot of registry hack articles anymore, but back when we first started we would use Process Monitor to figure out what registry keys were being accessed, and then go tweak those registry keys to see what would happen. If you’ve ever wondered how some geek figured out a registry hack that nobody has ever seen, it was probably through Process Monitor.

The Process Monitor utility was created by combining two different old-school utilities together, Filemon and Regmon, which were used to monitor files and registry activity as their names imply. While those utilities are still available out there, and while they might suit your particular needs, you’d be much better off with Process Monitor, because it can handle a large volume of events better due to the fact that it was designed to do so.

It’s also worth noting that Process Monitor always requires administrator mode because it loads a kernel driver under the hood to capture all of those events. On Windows Vista and later, you’ll be prompted with a UAC dialog, but for XP or 2003, you’ll need to make sure the account you use has Administrator privileges.

### The Events that Process Monitor Captures

Process Monitor captures a ton of data, but it doesn’t capture every single thing that happens on your PC. For instance, Process Monitor doesn’t care if you move your mouse around, and it doesn’t know whether your drivers are working optimally. It’s not going to track which processes are open and wasting CPU on your computer — that’s the job of Process Explorer, after all.

What it does do is capture specific types of I/O (Input / Output) operations, whether they happen through the file system, registry, or even the network. It will additionally track a few other events in a limited fashion. This list covers the events that it does capture:

*   **Registry** – this could be creating keys, reading them, deleting them, or querying them. You’ll be surprised just how often this happens.

*   **File System** – this could be file creation, writing, deleting, etc, and it can be for both local hard drives and network drives.

*   **Network** – this will show the source and destination of TCP/UDP traffic, but sadly it doesn’t show the data, making it a bit less useful.

*   **Process** – These are events for processes and threads where a process is started, a thread starts or exits, etc. This can be useful information in certain instances, but is often something you’d want to look at in Process Explorer instead.

*   **Profiling** – These events are captured by Process Monitor to check the amount of processor time used by each process, and the memory use. Again, you would probably want to use Process Explorer for tracking these things most of the time, but it’s useful here if you need it.

So Process Monitor can capture any type of I/O operation, whether that happens through the registry, file system, or even the network — although the actual data being written isn’t captured. We’re just looking at the fact that a process is writing to one of these streams, so we can later figure out more about what is happening.

### The Process Monitor Interface



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



When you first load up the Process Monitor interface, you’ll be presented with an enormous number of rows of data, with more data flying in quickly, and it can be overwhelming. The key is to have some idea, at least, about what you are looking at, as well as what you are looking for. This isn’t the type of tool that you spend a relaxing day browsing through, because within a very short time period, you’ll be looking at millions of rows.

The first thing you’ll want to do is filter those millions of rows down to the much smaller subset of data you want to see, and we’re going to teach you how to create filters and zero in on exactly what you want to find. But first, you should understand the interface and what data is actually available.

### Looking at the Default Columns

The default columns show a ton of useful information, but you’ll definitely need some context to understand what data each one actually contains, because some of them might look like something bad happened when they are really innocent events that happen all the time under the hood. Here’s what each of the default columns is used for:

*   **Time** – this column is fairly self-explanatory, it shows the exact time that an event occurred.

*   **Process Name** – the name of the process that generated the event. This doesn’t show the full path to the file by default, but if you hover over the field you can see exactly which process it was.

*   **PID** – the process ID of the process that generated the event. This is very useful if you are trying to understand which svchost.exe process generated the event. It’s also a great way to isolate a single process for monitoring, assuming that process doesn’t re-launch itself.

*   **Operation** – this is the name of the operation that is being logged, and there is an icon that matches up with one of the event types (registry, file, network, process). These can be a little confusing, like RegQueryKey or WriteFile, but we’ll try and help you through the confusion.

*   **Path** – this is not the path of the process, it is the path to whatever was being worked on by this event. For instance, if there was a WriteFile event, this field will show the name of the file or folder being touched. If this was a registry event, it would show the full key being accessed.

*   **Result** – This shows the result of the operation, which codes like SUCCESS or ACCESS DENIED. While you might be tempted to automatically assume that an BUFFER TOO SMALL means something really bad happened, that isn’t actually the case most of the time.

*   **Detail** – additional information that often doesn’t translate into the regular geek troubleshooting world.

You can also add some additional columns to the default display by going to Options -> Select Columns. This wouldn’t be our recommendation for your first stop when you start testing, but since we’re explaining columns, it’s worth mentioning already.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



One of the reasons for adding additional columns to the display is so you can very quickly filter by those events without being overwhelmed with data. Here are a few of the extra columns that we use, but you might find use for some others in the list depending on the situation.

*   **Command Line** – while you can double-click on any event to see the command line arguments for the process that generated each event, it can be useful to see at a quick glance all of the options.

*   **Company Name** – the main reason that this column is useful is so you can simply exclude all Microsoft events quickly and narrow down your monitoring to everything else that isn’t part of Windows. (You’ll want to make sure that you don’t have any weird rundll32.exe processes running using Process Explorer though, since those could be hiding malware).

*   **Parent PID** – this can be very useful when you are troubleshooting a process that contains many child processes, like a web browser or an application that keeps launching sketchy things as another process. You can then filter by the Parent PID to make sure that you capture everything.

It’s worth noting that you can filter by column data even if the column isn’t showing, but it’s much easier to right-click and filter than manually do it. And yes, we mentioned filters again even though we haven’t explained them yet.

### Examining a Single Event

Viewing things in a list is a great way to quickly see a lot of different data points at once, but it definitely isn’t the easiest way to examine a single piece of data, and there is only so much information you can see in the list. Thankfully you can double-click on any event to access a treasure trove of extra information.

The default Event tab gives you information that is largely similar to what you saw in the list, but will add a bit more information to the party. If you are looking at a file system event, you’ll be able to see certain information like the attributes, file create time, the access that was attempted during a write operation, the number of bytes that were written, and the duration.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Switching over to the Process tab gives you lots of great information about the process that generated the event. While you’ll generally want to use Process Explorer to deal with processes, it can be very useful to have a lot of information about the specific process that generated a specific event, especially if it is something that happened very quickly and then disappeared from the process list. This way the data is captured.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



The Stack tab is something that will sometimes be extremely useful, but often times will not be useful at all. The reason why you would want to look at the stack is so you can troubleshoot by examining the Module column for anything that doesn’t look quite right.

As an example, imagine that a process was constantly trying to query or access a file that doesn’t exists, but you weren’t sure why. You could look through the Stack tab and see if there were any modules that didn’t look right, and then research them. You might find an out of date component, or even malware, is causing the problem.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Or, you might find that there isn’t anything useful here for you, and that’s just fine too. There is a lot of other data to look at.

### Notes on Buffer Overflows

Before we even proceed further, we’re going to want to note a result code that you’re going to start seeing a lot in the list, and based on all your geek knowledge so far, you might freak out a little bit about. So if you start seeing BUFFER OVERFLOW in the list, please don’t assume that somebody is trying to hack your computer.

[Next Page: Filtering the Data that Process Monitor Captures](lesson4.md2/)

*   1

*   [2](lesson4.md2/)
*   [Next](lesson4.md2/)

[JOIN THE DISCUSSION (2 REPLIES)](#)

*   [March 28, 2014](#)
Peter

Your series on the SysInternals suite is superb! Not only do I study each lesson, but I've saved links both on my computer, but also on a flash drive along with the SI files. I'm recommending the lessons to all who have asked me for computer info... you are really performing a great service to would-be geekdom! Thanks,Peter

### [Got Feedback? Click Here to Join the Discussion](http://discuss.howtogeek.com/t/understanding-process-monitor/14569)



[Tweet](https://twitter.com/share)

[**Lowell Heddings**](http://www.howtogeek.com/author/thegeek/), better known online as the How-To Geek, spends all his free time bringing you fresh geekery on a daily basis. You can follow him on [Google+](https://plus.google.com/115673881208416151793/?rel=author) if you'd like.

*   Published 03/27/14

[](https://twitter.com/lowellheddings)



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)

http://www.howtogeek.com/school/sysinternals-pro/lesson4/
