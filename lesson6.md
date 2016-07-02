
## [Lesson 6: Using Autoruns to Deal with Startup Processes and Malware](http://www.howtogeek.com/school/sysinternals-pro/lesson6/)



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Most geeks have their tool of choice to deal with processes that start up automatically, whether that is MS Config, CCleaner, or even Task Manager in Windows 8 — but none of them are as powerful as Autoruns, which is also our Geek School lesson for today.

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

In the olden days, software would start itself automatically by adding an entry to the Startup folder in the Start Menu, or adding a value into the Run key in the registry, but as people and software became more savvy at finding unwanted entries and deleting them, the makers of questionable software started finding ways to get more and more sneaky.

These shady crapware companies started figuring out how to automatically load their software through browser helper objects, services, drivers, scheduled tasks, and even through some extremely advanced techniques like image hijacks and AppInit_dlls.

Checking for each of these conditions manually would not only be time-consuming, but nearly impossible to do for the average person.

That’s where Autoruns comes in and saves the day. Sure, you can use Process Explorer to look through the process list and delve deep into threads and handles, and Process Monitor can figure out exactly which registry keys are being opened by which process and show you incredible amounts of information. But neither one stops crapware or malware from being loaded again the next time you boot your PC.

> Of course, a smart strategy would be to use all three together. Process Explorer sees what is currently running and using up your CPU and memory, Process Monitor sees what the application is doing under the hood, and then Autoruns comes in to clean things up so they don’t come back.

Autoruns allows you to see nearly every single thing that is loaded automatically on your computer, and disable it as easy as clicking a checkbox. It’s incredibly easy to use, and nearly self-explanatory, except for some of the really complicated things you need to know to understand what some of the tabs actually mean. That’s what this lesson is going to teach.

### Working With the Autoruns Interface

You can grab the Autoruns tool from the [SysInternals web site](http://technet.microsoft.com/en-us/sysinternals/bb842062) just like all of the rest and run it without installing. You’ll want to do that before proceeding.

_Note:_ Autoruns doesn’t require running as administrator, but realistically it makes the most sense to just do that, since there are a few features that won’t work as well otherwise, and there’s a good chance your malware is running as administrator as well.

When you first launch the interface you’ll see a ton of tabs and a list of things that are being started automatically on your computer. The default Everything tab shows everything from every tab, but it can be a little confusing and lengthy, so we’d advise to just go through each tab separately.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



It’s worth noting that by default, Autoruns hides everything that is built into Windows and set to automatically start. You can enable showing of those items in the options, but we wouldn’t recommend it.

#### **Disabling Items**

To disable any item in the list, you can just remove the check box. That’s all you have to do, just go through the list and remove everything you don’t need, reboot your computer, and then run it again to make sure everything is good.

_Note: _some malware will constantly monitor the locations where they trigger autostart from, and will immediately put the value back. You can use the F5 key to rescan and see if any of the entries came back after disabling them. If one of them showed up again, you should use Process Explorer to suspend or kill that malware before disabling it here.

#### **The Colors**

Like most SysInternals tools, the items in the list can be different colors, and here is what they mean:

*   **Pink** – this means that no publisher information was found, or if code verification is on, means that the digital signature either doesn’t exist or doesn’t match, or there is no publisher information.

*   **Green** – this color is used when comparing against a previous set of Autoruns data to indicate an item that wasn’t there last time.

*   **Yellow** – the startup entry is there, but the file or job it points to doesn’t exist anymore.

Also just like most of the SysInternals tools, you can right-click on any entry and perform a number of actions, including jumping to the entry or image (the actual file in Explorer). You can search online for the name of the process or the data in the column, see the detailed properties, or see if that entry is running by doing a quick search through Process Explorer — although many processes have a loader that then launches something else before exiting, so just because that feature shows no results doesn’t mean anything.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



If you clicked Jump to Entry, you’ll be taken straight over to the Registry Editor, where you can see that particular registry key and look around. If the entry was something else, you might be taken to a different utility, like the Task Scheduler. The reality is that most of the time, Autoruns displays all of the same information right in the interface, so you don’t usually need to bother unless you want to learn more.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



The User menu allows you to analyze a different user account, which can be really useful if you’ve loaded up Autoruns on a different account on the same computer. It’s worth noting that you would obviously need to be running as administrator to see other user accounts on the PC.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



### Verifying Code Signatures

The Filter Options menu item takes you to an options panel where you can select one very useful option: Verify Code Signatures. This will check to make sure that each digital signature is analyzed and verified, and display the results right in the window. You’ll notice that all the items in pink in the screenshot below are not verified or the publisher information does not exist.

And for extra credit, you might notice that this screenshot below is almost the same as the one near the beginning, except in that one some of the items in the list where not marked as pink. The difference is that by default without the Verify Code Signatures option turned on, Autoruns will only alert you with the pink row if no publisher information exists.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



### Analyze an Offline System (As in Hooking Up a Hard Drive to Another PC)

Imagine that your friend’s computer is completely messed up and either won’t boot or just boots so slowly that you can’t really use it. You’ve tried safe mode and recovery options like System Restore, but it doesn’t matter because it is unusable.

Rather than pull the “reinstall” card, which is often just the “I give up” card, you could yank out the hard drive and hook it up to your PC or laptop with [your handy USB hard drive dock](http://www.howtogeek.com/182452/how-to-get-data-off-an-old-hard-drive-without-putting-it-in-a-pc/). You do have one, right? Then you just load up Autoruns and go to File -> Analyze Offline System.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



Browse to find the Windows directory on the other hard drive, and the user profile of the user you are trying to diagnose, and click OK to start.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



You’ll need write access to the drive, of course, because you will want to save the settings to remove whatever nonsense you end up finding.

### Comparing Against Another PC (Or Previous Clean Install)

The File -> Compare option seems nondescript, but it can be one of the most powerful ways to analyze a PC and see what has been added since the last time you scanned, or to compare against a known clean PC.

To use this feature, just load up Autoruns on the PC you are trying to inspect, or using the Offline mode we described earlier, then head to File -> Compare. Everything that has been added since the compared file version will show up in bright green. It’s as simple as that. To save a new version, you’d use the File -> Save option.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



If you really want to be a pro, you could save a clean configuration from a new install of Windows and put that on a flash drive to take with you. Save a new version every time you touch a PC for the first time to make sure you can quickly identify all of the new crapware the owner has added.

### Looking at the Tabs

As you’ve seen so far, Autoruns is a very simple but powerful utility that could probably be used by almost anybody. I mean, all you have to do is uncheck a box, right? It is, however, useful to have some more information about what all of these tabs mean, so we’ll try and educate you here.

[Next Page: Logon, Scheduled Tasks, and Image Hijacking](http://www.howtogeek.com/school/sysinternals-pro/lesson6/2/)

*   1

*   [2](http://www.howtogeek.com/school/sysinternals-pro/lesson6/2/)
*   [Next](http://www.howtogeek.com/school/sysinternals-pro/lesson6/2/)

[JOIN THE DISCUSSION (6 REPLIES)](#)

*   [March 31, 2014](#)
Iszi

> there’s a good chance your malware is running as administrator as well.



[![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)](http://static.fjcdn.com/pictures/Nuke_d3c65a_638430.jpg)



> If you really want to be a pro, you could save a clean configuration from a new install of Windows and put that on a flash drive to take with you. Save a new version every time you touch a PC for the first time to make sure you can quickly identify all of the new crapware the owner has added.

There's a great feature I didn't know about! Unfortunately, I'll probably only get around to doing this when I finally do a re-build where I actually stop to make a clean backup, too - i.e.: probably never. #thingsweswearwelldonexttimebutneverreallydo

*   [March 31, 2014](#)
Iszi

[@geek](http://www.howtogeek.com/users/geek) What does it mean to have un-checked items in the list? Should they be deleted? I notice that there seems to be a lot already, before I even tried unchecking things.

*   [April 1, 2014](#)
Peter 

> Rather than pull the “reinstall” card, which is often just the “I give up” card

I wouldn't necessarily say it's giving up. If the machine is really messed up, unbootable, or you know it is virus infected, reinstalling may be the best option. Reinstalling is the only way to know with 100% certainty that all traces of the infection/malware are removed. With any other type of removal you can never be absolutely sure you have removed every part of it. Reinstalling may also be faster than trying to clean up a severely infected machine.

*   [April 1, 2014](#)
Peter 

One of the first things I do after a rebuild or fresh install is install all the needed updates and then run a backup. That way if something gets messed up with reinstalling all the applications or user data I can easily restore from the backup and not have to reinstall all the updates. The updates usually are more time consuming then the fresh Windows install.

*   [April 1, 2014](#)
Iszi

I wholeheartedly agree with you in principle. In practice, I'm usually too eager to (finally) use my computer after the whole process of rebuilding and updating that I just can't bother myself to stop and do backups or other configuration management type stuff until months later.

### [Got Feedback? Click Here to Join the Discussion](http://discuss.howtogeek.com/t/using-autoruns-to-deal-with-startup-processes-and-malware/14661)



[Tweet](https://twitter.com/share)

[**Lowell Heddings**](http://www.howtogeek.com/author/thegeek/), better known online as the How-To Geek, spends all his free time bringing you fresh geekery on a daily basis. You can follow him on [Google+](https://plus.google.com/115673881208416151793/?rel=author) if you'd like.

*   Published 03/31/14

[](https://twitter.com/lowellheddings)



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)

http://www.howtogeek.com/school/sysinternals-pro/lesson6/