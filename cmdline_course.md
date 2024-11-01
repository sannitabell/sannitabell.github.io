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
familiar with working in the Terminal and with files. Here are some basic—but 
very important—commands we learned:

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

### Week 2 | Becoming familiar with the UNIX system and remote servers

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

### Week 3 | Processing corpus data

At this point we had become proficient and comfortable enough with the Terminal so that we could start processing linguistic data. We started with learning about
different encoding systems and regex.

Let me explain the differences between the encoding systems we learned about.
- **ASCII** (American Standard Code for Information Interchange) is a 7-bit encoding
system and represents 128 characters: basic letters used when writing text in 
English, numbers, and control characters. This is a very limited system since it 
does not support, for example, accents or symbols used in languages other than the
English language, such as _ä_ or _ö_ in Finnish.
- **Latin-1** (ISO-8859-1) is an 8-bit system largely built on ASCII and has double the amount of represented
characters, such as accented letters (_ä_, _ã_) and symbols (_€_, _£_). It, however,
lacks a significant amount of characters used in non-Latin-based writing systems,
like Chinese (_你好_), Russian (_привет_) or Greek (_χαιρε_).
- **UFT-8** (Unicode Transformation Format - 8-bit) covers all Unicode characters
making it compatible with virtually any written language and the most versatile 
and widely-used encoding system. It is a variable-length encoding and uses between 1 and 4 
bytes per character. All ASCII text is valid in UTF-8 because it uses only 1 byte 
per ASCII character.

This is how to convert a text file encoding from _ASCII_ to _UTF-8_:  
`iconv -f ISO-8859-1 -t UTF-8 unputfile.txt -o outputfile.txt`

As mentioned, we also learned regex, which is an important tool in language 
technology. Regex allows us to search, exctract, and manipulate text by identifying
patterns, filtering specific language features, and parsing large datasets efficiently.

From a piece of text like this  
> this is mad man mango magroove  

we can find this pattern "man"  
> this is mad **man** **man**go **man**groove  

or a more specific pattern, like "$man^"  
> this is mad **man** mango mangroove  

### Week 4 | Applying text processing tools to corpus data analysis

After learning regex, we can now use it to manipulate text files. A good utility
for doing so it `sed` (stream editor). Here's what we can do with it:

1. Substituting a string of text (like "abc") with another ("xyz") in a text file:  
`sed 's/abc/xyz/g' filename.txt`

2. Deleting specific lines of text, like line 5:  
`sed '5d' filename.txt`

3. Printing specific lines, like lines 2 to 7:  
`sed -n '2,7p' filename.txt`

4. Inserting or appending text, like adding "Bye" after every line containing "Hello":  
`sed '/Hello/a Bye' filename.txt`

5. Transforming text, like converting all lowercase letters to uppercase:  
`sed 's/[a-z]/\U&/g' filename.txt`

Another important and useful feature we learned is using "|" to pipe commands.
Here is an example of chaining multiple commands together withs pipes:  
`cat filename.txt | grep "error" | sort | uniq -c | sort -nr`  
- Display contents of `filename.txt` with `cat`
- Find lines containing "error" with `grep`
- Sort those lines with `sort`
- Remove duplicates with `uniq -c`
- Sort the results in numerical order with `sort -nr`

Piping in useful for increasing efficiency and flexibility while working in Terminal.

### Week 5 | Scripts

To make processing data even more convenient, instead of writing and re-writing
lines of commands in the terminal, we can put it into a script file and run that
whenever needed. During week 5, we learned how to create simple **.sh** files 
(Bash files) to process text files.

First we created a bash script that takes one argument, an English adjective and prints its comparative form. In this case, we are only dealing with adjectives ending in consonants, such as dark - darker or new - newer.

```python
#! /bin/bash

#script: comparative_step1.sh
#author: Sanni-Lotta Tabell (October 2024)
#
#Gets adjective ending in a consonant from input and attaches suffix "-er" to it.
#Print output to standard output.


#Abort the script if argument is missing:
if [ $# -ne 1 ]
then
    echo "ERROR: Command line argument required: adjective!"
    echo "$0 adjective"
    exit 1
fi

adjective=$1

#Abort the script if adjective does not end in a consonant:
if [[ $adjective =~ [aeiouy]$ ]]
then
    echo "ERROR: The adjective must end in a consonant!"
    exit 1
fi

result="${adjective}er"
echo "$result"
```

Then we created a bash script that includes a while loop and that given a text file as an argument, reads every line and prints it in the terminal.

```python
! /bin/bash

#script: comparative_step2.sh
#author: Sanni-Lotta Tabell (October 2024)
#
#Reads every line of given text file and prints it in the terminal.


#Abort the script if argument is missing:
if [ $# -ne 1 ]
then
    echo "ERROR: Command line argument required: text file!"
    echo "$0 file.txt"
    exit 1
fi

#Abort the script if argument is not a file:
if [ ! -f "$1" ]
then
    echo "ERROR: File not found!"
    exit 1
fi

while read -r line
do
    echo "$line"
done < "$1"
```

Next we combined the two previous scripts in a brand new script **comparative_step3.sh** and made it so that the script takes the attached adjectives.txt file as an argument and prints its comparative form.

```python
#! /bin/bash

#script: comparative_step3.sh
#author: Sanni-Lotta Tabell (October 2024)
#
#Reads every line of given text file, takes its comparative form and prints it in the terminal.


#Abort the script if argument is missing:
if [ $# -ne 1 ]
then
    echo "ERROR: Command line argument required: text file!"
    echo "$0 file.txt"
    exit 1
fi

#Abort the script if argument is not a file:
if [ ! -f "$1" ]
then
    echo "ERROR: File not found!"
    exit 1
fi

while read -r adjective
do
    result="${adjective}er"
    echo "$result"
done < "$1"
```

Finally we created a script that also takes into consideration irregular comparative forms.

```python
! /bin/bash

#script: comparative_step4.sh
#author: Sanni-Lotta Tabell (October 2024)
#
#Reads every line of given text file, takes its comparative for and prints it in the terminal.


#Abort the script if argument is missing:
if [ $# -ne 1 ]
then
    echo "ERROR: Command line argument required: text file!"
    echo "$0 file.txt"
    exit 1
fi

#Abort the script if argument is not a file:
if [ ! -f "$1" ]
then
    echo "ERROR: File not found!"
    exit 1
fi

while read -r adjective
do
    if [[ $adjective =~ [aeiouy]$ ]]
    then
       if [[ $adjective =~ y$ ]]
       then
          result=$(echo "$adjective" | awk '{sub(/y$/, "ier"); print}')
       else
           result="${adjective}r"
       fi
    else
        if [[ $adjective =~ [^aeiou][aeiou][kptgbd]$ ]]
        then
            dup="${adjective: -1}"
            result="${adjective}${dup}er"
        else
            result="${adjective}er"
        fi
    fi
    echo "$result"
done < "$1"
```

### Week 6 | Installing software and automating tasks

Our focus on week 6 was largely how to install programs. We learned such commands
as `apt-get install`, `pip install` (for Python pachages), and `brew install` 
(for Mac users).

Oftentimes, when you want to install something with `apt-get`, you must be a root
user. To become a root user temporarily,  we can use `sudo`. Before doing so,
you must set a root user password for yourself. This is done by executing `sudo password`.
Now, you can install packages as a root user like this: `sudo apt-get install`.

To install Python packages, like nltk (Natural Language Tool Kit),
we can use `pip install`. This package in particular constains a multitude of
useful applications for us linguists.

During week 6, we also learned how to use `make` for building other programs, 
libraries, and other projects, like corpus collections. For example, we created
this Python file that deletes all metadata from given books.

```python
from sys import argv, stderr

START = "*** START OF THIS PROJECT GUTENBERG EBOOK"
STOP  = "*** END OF THIS PROJECT GUTENBERG EBOOK"

if __name__=="__main__":
    if len(argv) != 3:
        print("USAGE: %s input_file output_file" % argv[0], file=stderr)
        exit(1)

    ifile = open(argv[1])
    ofile = open(argv[2],"w")
    printing = 0
    for line in ifile:
        if STOP in line:
            break
        if printing: 
            print(line,end="",file=ofile)
        if START in line:
            printing = 1
````
