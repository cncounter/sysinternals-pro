# SysInternals Pro: Analyzing and Managing Your Files, Folders, and Drives

## [Lesson 9: Analyzing and Managing Your Files, Folders, and Drives](http://www.howtogeek.com/school/sysinternals-pro/lesson9/)



![SysInternals 9](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



We’re almost done with our Geek School series on SysInternals tools, and today we’re going to talk about all of the utilities that help you deal with files and folders — whether you are finding hidden data or securely deleting a file.

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

There are quite a few utilities in the toolkit that deal with all sorts of things that are related to files or folders or finding data that you didn’t know was there, and there are a few that are a little on the silly side. Either way, we’ll be covering them all.

The most important file-related tools in the kit to get to know are probably the Sigcheck and Streams utilities, but it would be wise to read through them all carefully.

### Streams Finds and Displays Hidden NTFS Streams

Most people don’t know about this feature, but Windows will let you [store data inside a hidden compartment in the file system](http://www.howtogeek.com/howto/windows-vista/stupid-geek-tricks-hide-data-in-a-secret-text-file-compartment/) called alternate data streams. This basically works by appending a colon and a unique key to the end of a filename when interacting with it.

RELATED ARTICLE

[![](data:image/jpeg;base64,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)](http://www.howtogeek.com/howto/windows-vista/stupid-geek-tricks-hide-data-in-a-secret-text-file-compartment/)

[Stupid Geek Tricks: Hide Data in a Secret Text File Compartment](http://www.howtogeek.com/howto/windows-vista/stupid-geek-tricks-hide-data-in-a-secret-text-file-compartment/)
In today's edition of Stupid Geek Tricks (where we show off little-known tricks to impress your non-geek friends), we'll learn how to hide data in a text file that can't be seen by anybody else unless they know the name of the secret compartment. [[Read Article]](http://www.howtogeek.com/howto/windows-vista/stupid-geek-tricks-hide-data-in-a-secret-text-file-compartment/)

For instance, if you wanted to hide some data in a file, you could do something like _echo Secret > filename.txt:hiddenstuff _and even if you opened up that text file in Notepad, you wouldn’t see the “Secret” text that you added, and there would be no other way to know that it was even there. In fact, you can do nearly anything you want using this technique. (Make sure to [read our article on the subject](http://www.howtogeek.com/howto/windows-vista/stupid-geek-tricks-hide-data-in-a-secret-text-file-compartment/) for the full explanation).

This is also the technique that allows Windows to [magically know that files have been downloaded from the internet](http://www.howtogeek.com/70012/what-causes-the-file-downloaded-from-the-internet-warning-and-how-can-i-easily-remove-it/), by hiding data inside the Zone.Identifier field. In fact, you can delete this alternate data stream using the Streams utility.

The syntax is simple — to see the streams, type the following at the prompt:

> streams 

You can also use “streams *.exe” or something like that to see all the files with hidden stream data, if there are any. The quickest way to see something is to head into your downloads directory and run it there.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



To delete one of the streams or many of them, you can use the -d option:

> streams -d 

You can also use the -s option to go into subdirectories recursively.

### SigCheck Analyzes Files That Aren’t Digitally Signed (Like Malware)

This very useful utility analyzes the digital signatures of files on your system and tells you whether they are valid or missing a certificate. You can also use it to check files against VirusTotal from the command line, which is convenient, because that’s the real point of this tool, is to find malware.

The normal and most useful syntax is to add the -u switch, which only reports problems, and the -e switch, which only checks executable files. So you could run something like this to check your system32 directory and make sure that all the files there are digitally signed. Anything else should be examined very closely.

> sigcheck -e -u C:\Windows\System32

You can also use the -v option for an additional check against VirusTotal, but you will need to use the -vt option the first time to accept their terms and conditions.

> sigcheck -v -vt 



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



### SDelete Securely Deletes Files

If you are the paranoid type, you’ll be glad to know that you can securely wipe files from the command line any time you want. Just use the sdelete utility to whack the file with DoD compliant deletion protocols. (Of course the NSA probably still has a copy of your file). The syntax is simple:

> sdelete 

You can alternatively clean the free space on a drive by using the _sdelete -c _option, which will take longer, but is a good option if you forgot to use sdelete to remove the file in the first place.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



### Contig Defragments One or Many Individual Files

If you want to defragment just one single file, or a list of files, you can use the Contig utility to do just that. Sure, you don’t really need to defragment files in modern versions of Windows that do it automatically. And yeah, if you are using a solid state drive you should never defragment nor do you need to. But if you absolutely, positively, must defragment a single file, this is the utility to do it.  The syntax is simple:

> contig 

If you want to analyze the fragmentation of a file without actually doing anything, you can use the -a switch as shown below:



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



It’s worth noting that even if a file is fragmented, if the file is very large and is only broken into a few large pieces, you will gain essentially nothing from defragmenting and will have wasted more time bothering with it than you would save.

### du Shows Disk Usage

You can always just right-click any file or folder in Windows Explorer and choose Properties, or use the ALT + ENTER keyboard shortcut to see the size of a file or folder. But what if you want to see that data from the command prompt? That’s where the du utility comes in, and it is also a bit more accurate because it doesn’t count symbolic linked files, and it does check alternate data streams as well.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



The -n option only checks a single folder, without recursing into subdirectories, while the -v option does recurse and also shows each directory as it goes through the list, and the -l (n) option checks just “n” levels deep. As in, -l 2 would check 2 levels deep.

### PendMoves Displays Files Moving on Next Reboot

Have you ever wondered [why application installs make you reboot your computer](http://www.howtogeek.com/howto/31204/why-do-application-installs-make-you-reboot-and-close-other-apps/)? The answer is usually that they want to move some files around that can’t be moved around while Windows is running, so they use a built-in Windows feature that handles moving or deleting files on reboot.

The only thing you need to do is run the command, and it will output the data. Why is a copy of Process Explorer scheduled to move into the Windows folder on the next reboot? Read on.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



### MoveFiles Moves System Files when You Reboot

This utility uses the built-in Windows feature to schedule a move, delete, or rename of a file or directory so that it will happen during the next reboot cycle, before Windows is fully loaded. The syntax is really simple:

> movefile  

If you want to delete a file, you can use an empty destination by using quotes, like _movefile  “”. _As you can see in the screenshot below, we used the Movefile command to schedule a copy of process explorer to be moved into the Windows directory to illustrate how it all works.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



### Junction Creates Symbolic Links

RELATED ARTICLE

[![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)](http://www.howtogeek.com/howto/16226/complete-guide-to-symbolic-links-symlinks-on-windows-or-linux/)

[Complete Guide to Symbolic Links (symlinks) on Windows or Linux](http://www.howtogeek.com/howto/16226/complete-guide-to-symbolic-links-symlinks-on-windows-or-linux/)
Want to easily access folders and files from different folders without maintaining duplicate copies? Here’s how you can use Symbolic Links to link anything in Windows 7, Vista, XP, and Ubuntu. [[Read Article]](http://www.howtogeek.com/howto/16226/complete-guide-to-symbolic-links-symlinks-on-windows-or-linux/)

Windows supports symbolic links for files and folders, so that you can have more than one path point to the same file to save space instead of having multiple copies of a file. The idea is similar to shortcuts, except this is on the file system level and built into NTFS.

The Junction utility allows you to create and delete these links easily. You can also delete them using _junction -d ._

> junction  

The reality, however, is that Windows since Vista has had [the ability to create symlinks with the mklink command](http://www.howtogeek.com/howto/16226/complete-guide-to-symbolic-links-symlinks-on-windows-or-linux/), and you may as well use that one instead.

### FindLinks Finds Hard Links to Files

This little utility finds all hard links pointing to a file. Hard links are different from symbolic links in that deleting one hard link does not actually delete the file if there are more hard links to that file, it just appears to delete it until you have deleted all the hard links. Once you delete the final hard link, the file will be deleted.

_Note_: this could actually be an interesting way to make sure that a particular file isn’t really deleted by somebody that has the habit of deleting files. Just create a hard link to all the files that you don’t want them to lose.

In any case, you can use this command easily enough:

> findlinks 

The only problem is that Windows 7 and 8 have a built-in command that does the same thing. Use this one instead:

> fsutil hardlink list 

_Note: _It’s always better to learn to use the built-in stuff when possible, because you never know when you’ll need to do something on somebody else’s computer when you don’t have your toolkit.

### DiskView Displays Disk Structure

This utility allows you to see the structure of your hard drive in great detail, and you can even zoom all the way in and pick a file to highlight in the list, so you can see where a particular file is on the drive, and also see whether it is fragmented or not. It’s not terribly useful for most people, but hopefully you’ve got a scenario where you might need to use it.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



### Disk2vhd Turns PCs into Virtual Hard Drives

This utility creates a clone of your computer’s hard drive while it is running, and bundles it all up into a Virtual Hard Drive file that can be used in a virtual machine. And it does this while the PC is running.

That’s right, you can create a virtual machine of your hard drive while your computer is running. This could also be really helpful for scenarios where you want to do some forensic analysis of a machine but on your own computer — you could just create a clone and then boot it as a virtual machine instead.

The option for Vhdx tells Disk2vhd to use the newer VHDX file format instead of the VHD file format, which had a number of limitations. By default Disk2vhd is going to create separate files for each physical drive, but put partitions into the same file. If you simply plan to attach this VHD file to another virtual machine, or even just mount it on a regular Windows computer, you can uncheck partitions that you don’t need in the list. If you plan to make a virtual machine out of it, you should probably leave everything checked.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



The VHD output file can actually be placed onto the same drive that you are making a copy of, but we’d recommend using a second drive if possible just to make it all go faster.

### PageDefrag is Obsolete

This utility allowed you to defragment system files during boot, but since it doesn’t work on recent versions of Windows, you should skip it.

### Sync Writes Cached Data to Your Disk

This utility simply syncs all cached data out to the disk to make sure all file changes are written to the drive and not stored in some buffer somewhere. Of course, you [should use the Safely Remove option](http://www.howtogeek.com/118546/htg-explains-do-you-really-need-to-safely-remove-usb-sticks/) every time if you want to be sure you won’t lose data when pulling a flash drive.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



### Disk Monitor Shows You Real-Time Hard Drive Activity

This utility shows actual hard drive activity happening in real time — sectors, reads, writes, the length of the data, it’s all there. The only problem is that it isn’t terribly useful for most people.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



What is a little more useful, maybe, is the disk monitoring “Tray Disk Light” that you can choose from the Options menu. Once you enable that mode, it will move into the system tray and blink red for writes, green for reads, or stay gray when nothing is happening.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



If only the icon matched Windows 8 a little better.

### VolumeID Changes the Drive’s Serial Number

Have you ever noticed how every drive has a serial number that looks like 064B-1E81 or something equally uninteresting? If you want to change that serial number to something more fun, you can do it by using the VolumeID utility with this syntax:

> volumeid XXXX-XXXX

Please note that the syntax requires using hexadecimal characters, so you can’t type in GEEK-1337 like we did, because it just won’t work.



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)



### Next Lesson

Tomorrow we’re going to wrap up the series with a look at some of the little utilities that we missed, as well as some guidance on using all of the tools together, and when you should pull out each tool.

[Next Page: Wrapping Up and Using the Tools Together](http://www.howtogeek.com/school/sysinternals-pro/lesson10/)

[JOIN THE DISCUSSION (7 REPLIES)](#)

*   [April 3, 2014](#)
Iszi

A lot of great tools in here I haven't gotten around to playing around with yet. Thanks again for doing this series! 

Couldn't SigCheck theoretically be used to scan a whole partition with VirusTotal - kind-of an ultimate antivirus scan for your PC?

sigcheck -s -vt -vs C:\

Seems like this would be a little abusive. Does it submit all files to VirusTotal, or just unsigned files? Limiting it to just unsigned files would definitely reduce the impact of a whole-system scan like this, but probably not by much when you start counting in the content of user profile folders. Is there anything stopping you from doing this? If not, has VirusTotal commented on the issue at all to say whether it's an approved usage?

*   [April 3, 2014](#)
Lowell Heddings

You can definitely use this to submit all your files, although I'm not sure if VirusTotal would rate-limit you or something. Since I'm guessing most files have been submitted to VirusTotal at some point, it will mostly be just sending the hash of the file to see whether it was already reported, and only new executables that VirusTotal hadn't seen would be uploaded.

Where it would be really useful is to create some type of script that runs against your Downloads folder, since that is where most of the problems are going to arrive from.

*   [April 3, 2014](#)
Iszi



geek said:

> only new executables that VirusTotal hadn't seen would be uploaded



I'm pretty sure that's not right. In small-scale testing (just against some files on my desktop and a few DLLs in System32) it appears that SigCheck looks at and submits everything unless you specify -e. That means that all files will be checked against VirusTotal regardless of their type, and any file not recognized (e.g.: probably 90% of My Documents) will be submitted.

*   [April 3, 2014](#)
Lowell Heddings

Right, I was assuming that you would only check it against executables. Only files that VirusTotal hadn't seen would be actually uploaded, the rest would be sent as a hash.

*   [April 3, 2014](#)
CLARK C CLINE

I have enjoyed reading all of these educational guides for sysinternals, G mail, Office, and others. I just have one question. Why, on some days, the entire article is shown on one web page, while on other days there is a "next" button at the bottom that continues the article on a second, or even third web page?

When I don't have time to read the entire article, I use the Chrome print feature to save it in PDF format. It's a lot more convenient to print or save it when it is not broken up into several sections - there is no need to rename each section.

Just sayin'

*   [April 4, 2014](#)
Lowell Heddings

On some of the days, the lessons are just extremely long, so we break it up into multiple pages. On the days when the lesson isn't quite as long, we let it go on a single page.

### [Got Feedback? Click Here to Join the Discussion](http://discuss.howtogeek.com/t/analyzing-and-managing-your-files-folders-and-drives/14737)



[Tweet](https://twitter.com/share)

[**Lowell Heddings**](http://www.howtogeek.com/author/thegeek/), better known online as the How-To Geek, spends all his free time bringing you fresh geekery on a daily basis. You can follow him on [Google+](https://plus.google.com/115673881208416151793/?rel=author) if you'd like.

*   Published 04/3/14

[](https://twitter.com/lowellheddings)



![](http://www.howtogeek.com/pagespeed_static/1.JiBnMqyl6S.gif)

http://www.howtogeek.com/school/sysinternals-pro/lesson9/