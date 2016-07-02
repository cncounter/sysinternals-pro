## [Lesson 1: What Are the SysInternals Tools and How Do You Use Them?](lesson1.md)



![SysInternals 1](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



This How-To Geek School series will teach you how to use SysInternals tools like a pro, so your geek cred will never be in question. Not that we are questioning your geek skills. You do use SysInternals tools, right?

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

There are many other admin tools built into Windows, available for free on the web, or even through commercial sources, but none of them are quite as indispensible as the SysInternals suite of tools. That’s right, there’s a full set of free tools to do almost any administrator task, from monitoring or starting processes to peeking under the hood to see what files and registry keys your applications are really accessing.

These tools are used by every single reputable computer guy — if you want to separate the wheat from the chaff, just ask your local PC repair guy what Process Explorer is used for. If he doesn’t have a clue, he’s probably not quite as good as he says. (Don’t worry, if you don’t have a clue about procexp.exe either, we’ll cover that in-depth starting in lesson 2 of this series tomorrow).

Remember that time Sony tried to embed rootkits into their music CDs? Yeah, it was a SysInternals utility that first detected the problem, and it was the SysInternals guys that made the announcement. In 2006, Microsoft finally bought the company behind SysInternals, and they continue to provide the utilities for free on their web site.

This series will walk you through each of the important tools in the kit, get you familiar with them and their many features, and then help you understand how to use them in a real-world scenario. It’s a lot of very geeky material, but it’ll be a fun ride, so be sure to stay tuned.

### What Are the SysInternals Tools Exactly?

The SysInternals suite of tools is simply a set of Windows applications that can be downloaded for free [from their section of the Microsoft Technet web site](http://technet.microsoft.com/en-us/sysinternals/default). They are all portable, which means that not only do you not have to install them, you can stick them on a flash drive and use them from any PC. In fact, you can actually run them without installing through SysInternals Live (which we’ll illustrate in a bit).

The tools include utilities such as Process Explorer, which is a lot like Task Manager with a plethora of extra features, or Process Monitor, which monitors your PC for filesystem, registry, or even network activity from almost any process on your system.

Autoruns helps you deal with startup processes, TCPView shows you what is connecting to resources on the internet, and there is an entire set of tools that run from the command line to help you deal with processes, services, and more.



![Windows_8_1__Installed_with_Tools_-_1___Running_](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Process Explorer is probably the most useful tool in the kit.

Most of these tools are going to require administrator access on your computer, so you’d be wise to test them out in a virtual machine or a test computer if you aren’t sure what you are doing — these are some heavy duty tools.

For example, say you have a really slow PC to troubleshoot, and you want to inspect all of the threads for a particular application, and then you want to see the entire stack for one of those threads to see exactly what DLLs and functions are being called. Process Explorer makes this trivial — you can simply double-click on the process, flip over to the Threads tab, and then click the Stack button.



![Windows_8_1__More_crapware__conduit__etc___Running_](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



This stack has not yet overflowed.

What does all this mean? Wait until lessons 2 and 3, where we will do our best to explain the concepts to you, and more importantly, explain why you’d want to bother digging this deep.

### How Do You Get the Tools?

Getting your hands on any of the SysInternals tools is as easy as [heading to the web site](http://technet.microsoft.com/en-us/sysinternals/bb842062), downloading the zip file with all of the utilities, or just grabbing the zip file for the individual application that you want to use.

Either way, unzip, and double-click on the particular utility you’d like to open. That’s it. There’s no installer.

### Running the Tools from SysInternals Live

If you don’t want to be troubled to download and unzip and then run the application, and you don’t want to keep a USB drive updated with the latest versions, or you just don’t have access to your drive while working on somebody else’s computer, you can always resort to SysInternals Live.

Basically what happened is that a number of years ago, the SysInternals guys were curious whether they could find a new way to distribute their software… so they created a Windows file share off their server and gave everybody on the internet access to it.

So you can simply type [\\live.sysinternals.com\](%5C%5Clive.sysinternals.com%5C) into the Windows Run box after pulling that up with the WIN + R shortcut key, and you’ll be able to browse their file share and look around.

_Note: _the \\server\share format is called a UNC (Universal Naming Convention) path, and it works just about anywhere in Windows. You can utilize it in the explorer address bar, file open and save dialog boxes, or anywhere that you’d normally use a file path.



![Screenshot_3_23_14__11_01_PM](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



The useful folder is probably the Tools one, that has all of the different utilities listed, and easily accessible with nothing more than a mouse click.



![Windows_8_1__More_crapware__conduit__etc___Running__2](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Browsing for the utilities on a remotely accessible file share really isn’t the fastest way to do things, though, so thankfully there is a much quicker way to launch any SysInternals utility from any internet-connected Windows PC.

Just follow this format to directly launch one of the utilities through the Run box:

> \\live.sysinternals.com\tools\

For instance, to launch Process Explorer, the executable name is procexp.exe, so you can use \\live.sysinternals.com\tools\procexp.exe to launch Process Explorer, or change procexp.exe to procmon.exe to launch Process Monitor instead.



![Windows_8_1__More_crapware__conduit__etc___Running__1](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



When you do launch one of the utilities, you’ll be prompted with a security warning dialog before you actually run any of them. This is a good thing, of course, because you wouldn’t want Windows to let anybody run anything from a file share. That would be a disaster!



![Windows_8_1__More_crapware__conduit__etc___Running_](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



We’d highly recommend just downloading and putting a copy of the tools on every PC that you touch, rather than running from the Live site every time. But in a pinch, it’s great to know that you can do it.

### Next Lesson: Understanding Process Explorer

Tomorrow’s lesson will familiarize you with the Process Explorer application, a task manager replacement with many more features. The interface is packed full of data and options, so we’ll go through and explain everything that you need to know — like what all those colors in the process list actually mean.

After that, we’ll cover how to use it in the real world to deal with problem processes, malware, and more. Then we’ll head into Process Monitor territory, and explain how to use one of the most powerful troubleshooting applications to figure out what is really going on under the hood of your PC.

And next week we’ll take a trip through some of the other utilities, like Autoruns, Bginfo, and many of the command line utilities included in the toolkit.

There’s a lot of material to cover, so go grab yourself a copy of the utilities so you can follow along starting tomorrow.

[Next Page: Understanding Process Explorer](lesson2.md)

[JOIN THE DISCUSSION (10 REPLIES)](#)

*   [March 24, 2014](#)
Shirl

I wouldn't leave these tools on most machines, Autoruns in the wrong hands can cripple a machine for instance. Simply keep them all on a thumb drive. 

*   [March 24, 2014](#)
StevenTorrey

This is a handy-dandy set of tools... But as always, interpeting the info can be something of a challange; no one wants to kill the computer by deleting the wrong thing... Looking forward to the rest of the series. I have been told when a person has two iexplores and one gobbles up lots of memory and is located in folders 32--that iexplore is a trojan and should be deleted. I wonder if this is true. I had a search redirect trojan/virus which I got rid of. But now I wonder about this iexplore--I have three... I might add Youtube offers lots of movies about these--but I an't about to tinker under the hood if it ain't broke and if the computer still works... So what, if someone from the Ukraine is reading all my emails and tracking my computer surfing... If Jimmy Carter can be paranoid--then paranoia must be the up and coming trend...

*   [March 24, 2014](#)
Iszi

SysInternals tools have been awesome since day 1\. I always like to keep them handy, but you definitely don't want them lying about where "regular" end-users can reach too easily.

These days, I keep them installed and up to date on my own systems via [Windows System Control Center](http://www.kls-soft.com/wscc/). It's a free utility that bundles SysInternals tools and [NirSoft](http://nirsoft.net/) utilities, and makes it easy to check for updates and new utilities. It also includes shortcuts to many built-in Windows tools, some of which can otherwise be hard to reach.

Come to think of it, I'd love to see some of the NirSoft utilities get the same "How-To Geek School" treatment sometime. There's a lot of great stuff in there.

One additional word of caution with WSCC and the NirSoft tools: Many of the utilities in that bundle are password recovery tools or other things that one might call "hacking tools". As such, some malware scanners may alert and quarantine those files.

*   [March 24, 2014](#)
Bruce Benson

Flabbergasted. I was sure you guys messed up with that \live.sysinternals.com\ link. I've used process explorer for years in tuning up PCs. This is a great way to get at the current version of all the tools. Thanks.

*   [March 24, 2014](#)
Lowell Heddings

I'm glad to hear that even geeks are finding use in our series 

*   [March 24, 2014](#)
Ronny N

SysinternalsUpdater, available here:http://www.wieldraaijer.nl/, is the best tool to download the most recent versions to your hard drive, if you prefer to have them offline, like me 

*   [March 26, 2014](#)
Roger McKeon

Re SysInternals Live. (See lower down)

Just a word to point out that what you should type into the Windows Run box is not \live.sysinternals.com\ but http://live.sysinternals.com/

Thanks for great article.

So you can simply type \live.sysinternals.com\ into the Windows Run box after pulling that up with the WIN + R shortcut key, and you’ll be able to browse their file share and look around.

*   [April 1, 2014](#)
Lou Iannone

I love the Geek newsletter guys ....keep up the great work!

*   [April 2, 2014](#)
DomadorSoftware

Though you may not want to leave these tools on regular users' machines, you can use the third-party Sysinternals Suite Installer ([http://www.domador.net/extras/programs/sysinternals-suite-installer/](http://www.domador.net/extras/programs/sysinternals-suite-installer/)) to create a Start Menu program group and entries for them on your own PC. 

### [Got Feedback? Click Here to Join the Discussion](http://discuss.howtogeek.com/t/what-are-the-sysinternals-tools-and-how-do-you-use-them/14470)



[Tweet](https://twitter.com/share)

[**Lowell Heddings**](http://www.howtogeek.com/author/thegeek/), better known online as the How-To Geek, spends all his free time bringing you fresh geekery on a daily basis. You can follow him on [Google+](https://plus.google.com/115673881208416151793/?rel=author) if you'd like.

*   Published 03/24/14

[](https://twitter.com/lowellheddings)



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



http://www.howtogeek.com/school/sysinternals-pro/lesson1/