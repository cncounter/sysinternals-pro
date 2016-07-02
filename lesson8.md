
## [Lesson 8: Using PsTools to Control Other PCs from the Command Line](lesson8.md)



![SysInternals 8](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



In today’s lesson in our Geek School series covering SysInternals, we’re going to show you how to use the PsTools set of utilities to perform all sorts of administration tasks both locally, and on remote computers as well.

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

If you’ve ever wanted to connect to another computer and run a command, quickly get information about processes running and optionally kill them, or even stop a service on another PC, you can use the PsTools utilities to do all of these things and even more.

Obviously you can use Remote Desktop or a similar service to connect to any Windows computer and actually see the desktop and do anything that you would do locally, but the PsTools utilities allow you to do many tasks from the command line — or better yet, from a script that you can re-use later.

These are the type of utilities that work best in a corporate environment, and mastering these tools will definitely make you much better at your system administration job, save you time, and let you do things in a much smarter way. Doing things smarter and faster is a critical skill for being a great sysadmin.

There are twelve tools in the PsTools set, and while some of them are extremely useful, others have been superseded with tools built into more recent versions of Windows, and there are a few others which aren’t useful for most people. We’ll go through all of them so you understand how they work and why you might want to use each one.

*   PsExec – executes processes on a remote computer

*   PsFile – shows files that are opened on the remote computer through the network

*   PsGetSid – displays the security identifier for a computer or user

*   PsInfo – lists information about a system

*   PsKill – kills processes by name or ID

*   PsList – list information about processes on the command line

*   PsLoggedOn – list accounts that are logged on either on the machine or connecting remotely

*   PsLogList – pull the event log on the command line

*   PsPasswd – change the password for users

*   PsPing – a fairly simple ping utility with some additional features

*   PsService – list and make changes to Windows services

*   PsShutdown – shut down, log off, or suspend a computer

*   PsSuspend – suspend and resume processes (rather than killing them)

> It’s worth noting that you can use a tool like PsExec to execute all sorts of command-line utilities on remote computers… including really useful ones like the Autoruns command line tool and many more. The possibilities are endless once you’ve embraced the power of PsTools.

All of these tools can be used on local computers, but they are mostly useful for connecting to remote computers and performing commands on them.

### Connecting to Remote Computers ( Syntax for All Utilities)

All of the utilites can be run on either the local or remote computer, so they all have the same first argument for computer name if needed. Note that you could use the IP address if you wanted instead. If you omit this argument, the command will operate on your local computer.

> psinfo \\computername

You can also list multiple computers like psinfo \\computer1, computer2, computer3, or you could put all of the names into a file and reference that like psinfo @computerlist.txt. The final syntax is psinfo \\* which operates on all computers in the domain, which probably isn’t something you’ll use every day.

If you need to connect with alternate credentials because your local computer’s account has a different username and password than the other computer, you can use the -u and -p options, though we’d note that you might not want to use -p on the command line with a password in the command for security reasons. _Update: [as of the latest release of PsExec](https://twitter.com/markrussinovich/status/451704267246542848), no tool passes passwords as clear text anymore, so the only worry is if somebody can read your script files and see the password there._

> psinfo \\computername -u “user” -p “Password”

The “user” part of the command would change to “DOMAIN\user” if you are in a domain environment and need to change from the currently running user.

_Note: _you will generally need to connect to the remote computers with an administrator account.

### Configuring Remote Administration Access

If you are in a domain environment, which most people that need to use PsTools will be, you can ignore this section entirely as everything should work just fine. For anybody running Windows 7, 8, or Vista in a home environment or using a couple of computers in an office without a domain, you will need to tweak User Account Control on the remote computer to allow PsTools to properly run.

The problem is [described well by Microsoft](http://support.microsoft.com/kb/951016):

> When a user who is a member of the local administrators group on the target remote computer establishes a remote administrative connection by using the net use * \\remotecomputer\Share$ command, for example, they will not connect as a full administrator. The user has no elevation potential on the remote computer, and the user cannot perform administrative tasks.

To explain it in a different way, when you try to connect to another computer and run something that requires administrator access, there is no way to trigger the UAC prompt and accept it from your computer, so it won’t connect as administrator.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



And this isn’t a bad thing. You shouldn’t change this setting without fully understanding that you will be allowing an opening for malware to spread from one computer to another — assuming that malware has your local username and password, and that password is the same as the other computer, and the malware is that tricky, which most isn’t. But it still isn’t something to be taken lightly.

And again, if you are in a domain environment, this problem doesn’t exist and doesn’t need to be changed. And if you are just testing with a bunch of virtual machines, you don’t have much to worry about.

To tweak UAC to enable PsTools to run you’ll want to open up the Registry Editor and navigate to the following key:

> HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\
> 
> Windows\CurrentVersion\Policies\System

Once you are there, create a new 32-bit DWORD on the right-hand side, give it the name LocalAccountTokenFilterPolicy and the value of 1\. You don’t have to restart the computer to make the setting take effect.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



> _Note: _just to clarify, this setting needs to happen on the remote computer that you are connecting to.

### PsExec

PsExec is probably the most powerful tool in the kit, as you can execute any command in your local command prompt just like executing it on the remote computer. That includes anything that can be run on the command line — you can change registry values, run scripts and utilities, or connect from that PC to another one. The output of the commands will be shown on your local PC, rather than on the remote one.

The syntax is simple:

> psexec \\computername  apptorun.exe 

Realistically, though, you would want to also include the username and password on the command line. For example, to connect to another PC and check the network connections list, you would use something like this:

> psexec \\computername -u User -p Password ipconfig

That command would produce output similar to the following:



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



[Next Page: Using PsExec to Run Remote Commands](lesson8.md2/)

*   1

*   [2](lesson8.md2/)

*   [3](lesson8.md3/)
*   [Next](lesson8.md2/)

[JOIN THE DISCUSSION (6 REPLIES)](#)

*   [April 2, 2014](#)
Iszi

A note about using PsLoggedOn against another computer across the network: Be aware that you will see yourself as "logged on via resource share". This is to be expected even if you currently have no other connections to the remote computer, because PsLoggedOn relies on a Remote Registry connection to do its job. It likely does not mean someone's hijacked your account.

*   [April 2, 2014](#)
Iszi

About PsShutDown: Most of the functionality is available via the built-in shutdown command, which will even give you a nice GUI if you run it with the -i parameter. As mentioned in the article though, alternate shutdown states like Sleep or Hibernate are not available with the built-in utility.

*   [April 3, 2014](#)
Iszi

[@geek](http://www.howtogeek.com/users/geek) In case you miss this, since you weren't mentioned...

 [twitter.com](https://twitter.com/markrussinovich/status/451704267246542848) 


![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)


[markrussinovich](https://twitter.com/markrussinovich/status/451704267246542848) 
Correction on the Pstools How-To-Geek Lesson: as of the latest release of PsExec, no tool passes password in the clear

[Thu Apr 03 12:54:24 +0000 2014](https://twitter.com/markrussinovich/status/451704267246542848)



*   [April 3, 2014](#)
Lowell Heddings

I saw that and updated the article. What's funny is that I went back and added that line after reading something about the tool passing data in the clear. I should have done a little more research.

*   [April 7, 2014](#)
Stickman803

Did that report your virtual machine as having 2 MB of Physical Memory?

### [Got Feedback? Click Here to Join the Discussion](http://discuss.howtogeek.com/t/using-pstools-to-control-other-pcs-from-the-command-line/14718)



[Tweet](https://twitter.com/share)

[**Lowell Heddings**](http://www.howtogeek.com/author/thegeek/), better known online as the How-To Geek, spends all his free time bringing you fresh geekery on a daily basis. You can follow him on [Google+](https://plus.google.com/115673881208416151793/?rel=author) if you'd like.

*   Published 04/2/14

[](https://twitter.com/lowellheddings)



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)


http://www.howtogeek.com/school/sysinternals-pro/lesson8/