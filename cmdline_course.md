---
layout: default
---


## Command-Line Tools for Linguists

This course is aimed at students in the Bachelor's program in Linguists,
especially those with an interest in language technology. 
A command-line interface refers to the Shell or Terminal where users
of a computer are able to interact with computer programs by inputting lines of
text on the command-lines. In this course, we were introduced to essential skills
and tools for working in such environments. I have a Windows 11 operating system
so I worked in a Ubuntu via WSL, which provides a Unix-like system, 
but students with Mac computers were able to work directly in the Apple environment.  

During the weekly lessons of this course, we went over numerous ways of navigating
around the computer using command-line tools. For example, we learned how to 
work with directories, install and run programs, and create scripts for processing
linguistic corpus data. By the end of the course we as students are 
equipped with the skills and knowledge to create a GitHub-hosted webpage
that includes a home page, a link to a CV created in the Overleaf environment,
and this page that you are currently reading.

## What we learned each week

### Week 1 | Getting started in the command-line environment

The first step into working in a command-line interface is setting it up. We
followed detailed instructions provided by our teachers. During the week also got
familiar with working in the Terminal and with files. Here are some basic–but 
very important–commands we learned:

`whoami` - check your username  
`pwd` - print the name of current directory you are working in  
`ls` - list the contents of the directory  
`wget link` - fetch files from the web  
`mkdir` - create a directory  
`mv filename target` - move file, can also be used to rename files  
`cd` - change directory  
`rm` - remove a file  
`cat filename` - view text file by printing its contents into the terminal  
`less filename` - view text file in less  
`nano filename` - view and edit text file in nano

### Week 2

In the second week of the course we dove even deeper into navigating the UNIX system
and how to edit text in text editor programs, such as nano.

We learned how to further handle directories. For example, on week 1 we leaarned the command
`mkdir` that creates a directory. However, we can only remove files with the command
`rm` which cannot be used to remove directories. To do that we learned the command
`rmdir` or `rm -R`.

Another important thing, among many others, we learned is operating remote terminals.
We did this as exercise:
1. Use `ssh` command to connect to **puhti.csc.fi**
2. In the remote terminal, create a directory called **remote_dir**
3. Still in the remote server, change into the **remote_dir** directory
4. Within the **remote_dir** directory, open a text file called **remote_log.txt**
5. In the **remote_log.txt** note the current time and date
6. Save the file and exit
7. Close the connection to the remote server
8. Use the command `scp`, copy the entire **remote_dir** folder from **puhti.csc.fi** to your local computer

Using remote servers allows the user to access greater computing power or storage,
or a specialized environtment that might not be accessable on the local computer.
I personally used the puhti server later in the course to test out some commands
I was not able to use due to having used a computer provided by the 
Faculty of Science earlier in the first six weeks of the course.

