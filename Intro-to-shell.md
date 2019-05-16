# Intro to UNIX Shell

# Getting started

* Open `Terminal` or `git bash` and type `which nano` (then hit the Enter or Return key to submit the command) into the Terminal window to make sure you have the `nano` editor installed. You should see something like '/bin/nano' or '/usr/bin/nano' on the screen.

## What is the shell?

The shell is a program that interfaces with the Operating System to allow you to access and manipulate files and hardware devices. We are going to learn the most common commands and how we can combine them to automate repetitive tasks. The shell is also called a command-line interface because you type commands on a line like this:

> ```$ ls -l```

There are several different shells. We will be using bash (Born Again Shell), which is very common on UNIX and Linux operating systems. One thing you'll notice is that many commands are abbreviations or shorthands for words or phrases. ****Commands and file names are case sensitive, and when you pass additional information to a command, you must always type a space after the command name.****

## The three systems and shells used in this workshop

### Windows

If you are on Windows, you'll be using the bash emulator that you installed with Git. This emulator allows bash commands to work on Windows.

### MacOS

MacOS is built on UNIX so it has a built-in command-line with all of the UNIX commands we need for this workshop.

### Linux

Most versions of Linux come with bash by default.

# Today's Topics

| Shell Introduction |
| ------------- |
| Understanding the UNIX File System|
| Exploring Files |
| Manipulating Data with Command Pipelines|
| Other Useful Commands and Shortcuts |

# UNIX File System structure

The UNIX file system is organized in an inverted tree structure, with the "root" at the top. In UNIX, folders are referred to as "directories." We'll start by looking at some examples and running some simple shell commands.

# Navigating Files and Folders (Directories)

Open File Explorer and go to the `home` directory. Snap this window next to the terminal or git-bash window so you can see them side-by-side.

(Windows people can use Window-key + arrow to snap windows)

```
C:\Users\<your user name here>
```

Let's start with listing files and folders.

```
$ ls
```

What did you see? Does it look similar to what you saw in File Explorer?

`ls` is short for "list" and it displays a list of files and folders.

## Where am I?

Knowing where you are in the filesystem is less obvious using the command line, but there is a command to help.

```
pwd
```

`pwd` stands for `present working directory` and it will tell you the `path` to where you are in the filesystem, beginning with the filesystem root.

In UNIX the root is `/` and in Windows it will likely be something like `C:\`.

What did you see? Does it look like the path you see in File Explorer?

## `ls` (list files and folders)

Let's get back to `ls`.

`ls` has lots of options that you can use to sort and format the listing, just like you can do in File Explorer.

Let's see what they are. On Windows you can run the command:

```
ls --help
```

and on Mac you can use:

```
man ls
```

(Notice that we _always_ type a space after the command name.) What did you see? A description and lots of options? Great.

Let's try one of the options. These are typically one letter or digit codes that alter the default behavior of the command.

```
ls -l
```

What did you see? It looks a little different than the output from

```
ls
```

Try them both. See the difference?

`ls -l` shows us more details about the files:

* d or - to indicate whether the file is a directory or not
* permissions
* last date modified (or created)
* file size in bytes

This is called the `long` format, hence `-l`.

Sometimes there are hidden files and folders. These start with a `.`. `ls` won't show hidden things unless you give the -a option. Do be careful with hidden files and folders - if they are altered without retaining proper formats, this could prevent other software from working correctly. The files are "hidden" to reduce the likelihood that they are accidentally modified.

```
ls -a
```

Now you will see all files or folders. You can also combine options like this:

```
ls -la
```

This shows all files and outputs the long format.

> REMEMBER: You can combine options for any of the shell commands that have options.

## Moving around the File System

In a File Explorer you can double-click on a folder to move into it and see its contents. In the shell, we use the `cd` command, short for `change directory`.

On Windows:
```
cd --help
```
and on Mac:
```
man cd
```

Here are two ways to `change directory`:

`cd` followed by a `path` to where you want to go. Remember to type a space after the `cd`:
```
cd /lets/go/here
```
`cd` followed by `..` to go up one level in the filesystem (go into the parent folder)
```
cd ..
```

### Going home
We should currently be in the `home directory`. This is a location in the filesystem where your your personal files are stored by default, and where you are when you first open a terminal. The `home directory or folder` is a common operating system convention.

On Windows this will be:
```
C:\Users\<your user name here>
```

There is a shortcut for returning to the `home` directory.

```
cd ~
```

If you get lost and need to get back home, use the above command. Try it now and then list the files.

```
cd ~
ls -l
```

Do you see the same files you did before?

## Absolute paths and relative paths

Let's talk about file and directory paths some more. We can get to files and directories with a `relative` path or an `absolute` path.

### Absolute paths

Absolute paths always start from the `root` of the filesystem.

```
/Users/hank/folderA/folderB/folderC
```

### Relative paths

Relative paths are relative to the current location

```
folderB/folderC
```

You can also go up levels `relative` to the current location.

```
cd ../../..
```

# Getting files for the Workshop

We'll use the `git clone` command to pull some files down from the Internet. If you want to learn about version control using `git`, go to the workshop on Wednesday afternoon! For now, move to your home directory and then type this git command:

```
cd ~
git clone https://github.com/sjmillerAZ/ResBaz_UNIXIntro
```

What do you see when you list your files now?
```
ls -l
```

We can run `ls` on any directory by specifying that directory after any command options we want to use. For example:

```
ls -l ResBaz_UNIXIntro
```

# Working with Files and Directories

We will create some new directories and files. Beneath the ResBaz_UNIXIntro directory we have a Data directory that contains a .csv file and a subdirectory named 'gapminder_by_country'. Let's setup the rest of the directory structure that we will use for the workshop. It should look like this:

```
~/ResBaz_UNIXIntro
    |
    Data
        |
        TopSpotify2017.csv
        gapminder_by_country
    |
    GapminderAnalysis
    SpotifyAnalysis
```

 We need to create the GapminderAnalysis and SpotifyAnalysis directories. First we need to move into the ResBaz_UNIXIntro directory, and we can use a shortcut called `Tab completion`. After typing `cd` (space), type 'Res' and then hit the Tab key. What happens?

```
cd ResBaz_UNIXIntro/
```

Remember to use Tab to complete file and directory names. All you need is a unique prefix to start, and the shell will do the rest!

Now let's create the `GapminderAnalysis` and `SpotifyAnalysis` folders with the `mkdir` (make directory) command.

```
mkdir GapminderAnalysis
mkdir SpotifyAnalysis
```

Use `ls` to verify that your new directories have been created.

Use `cd` to move into the Data folder. Check where you are with `pwd`.
What files and directories do you see in the Data folder? Do these match up with the structure of files listed above?

## ASSESSMENT

How do I get back to my home directory?

1) cd /
2) cd ..
3) cd ~
4) cd /home
5) cd /Users/

Now how do I get back into the ResBaz_UNIXIntro directory?

```
cd ~/ResBaz_UNIXIntro
```

## Creating and Editing Files

Let's create a file called `README` using the `nano` text editor.

```
nano README
```

This will open `nano`.

> All of the nano commands are shown at the bottom of the window

Type this sentence in the nano window:
Spotify and gapminder data for learning UNIX.

To save the file, hold the Control (Ctrl) key and type the letter `o`, then answer the questions as prompted.

```
Ctrl + o
```

To exit, use:

```
Ctrl + x
```

Check to see if the file is there.

```
ls -l
```

# Moving files around

In File Explorer you can click and drag to move files around. We can move files using the shell too.

To move files we use the `mv` command. `mv` stands for `move`.

Let's move the README file into the Data directory.

To do this you use the `mv` command and tell it the `path to` and the `name of` the file you want to move and the path to the new location. You can use the relative or absolute path. Let's use the relative path.

```
mv README Data/
```

What happened? Let's list the files.

```
ls -l
```

You don't see README where you created it, but you should see it where you moved it.

```
cd Data
ls -l
```

> You can also use mv to rename files

Let's rename README to README.txt

```
mv README README.txt
```

```
ls -l
```

You should see the new file name. Remember that `mv` can be used to rename a file, as well as to move a file into a different directory.

## Copying files

Let's make a copy of the TopSpotify2017.csv file. To do this you use the `cp` command.  Just like `mv`, you tell it the `path to` and the `name of` the file you want to move and the `path to` the new location. You can use a relative or absolute path.

```
cp TopSpotify2017.csv TopSpotify2017.csv.bak
```

```
ls -l
```

Do you see your two files?

## ASSESSMENT

I want to move a file from one location to another. What command do I use?

1) move
2) Copy
3) mv
4) cp


What if we want to make a copy of an entire directory?

To copy a directory we need to use the `-R` option with the `cp` command. This tells the copy command that it needs to be `recursive`, meaning that it needs to dig through all of the subdirectories and files in the directory. Try it:

```
cp  -R  gapminder_by_country  gapminder_by_country.bak
```

What was copied? List the contents of the original gapminder_by_country directory and the backup copy you created.

```
ls gapminder_by_country
ls gapminder_by_country.bak
```

That's a lot of files. Let's start working with them.

First change directories so you are in the `gapminder_by_country` folder.

```
cd gapminder_by_country
```

```
pwd
```

## Gapminder

The gapminder study collected data on GDP and life expectancy over time for many countries. In the gapminder_by_country directory you see all of the files for countries with GDP data. Let's look at one of them.

# Output

We don't need to use nano to see what is inside a file. We can send (output) the contents of a file to the screen. There are two commands we can use to do that. We will start with `cat` (short for concatenate).

## cat

`cat` will output the entire contents of a file to the screen all at once. Let's see that in action.

```
cat Japan.cc.txt
```

What did you see? To see a description of the data, use `cat` to show the contents of the file country.cc.txt along with the data from Japan.cc.txt:


```
cat country.cc.txt Japan.cc.txt
```

Now do you understand why cat is short for concatenate?

## Wildcard characters

Suppose we wanted to see data for all the countries whose names begin with 'J'. If we knew ahead of time that these countries are Jamaica, Japan, and Jordan, we could use the command:
```
cat country.cc.txt Jamaica.cc.txt Japan.cc.txt Jordan.cc.txt
```

A better solution is to use "*" as a wildcard:

```
ls J*.cc.txt
```

```
cat country.cc.txt J*.cc.txt
```

The "*" wildcard matches zero or more characters, and can be used without preceding or following characters:

```
ls *.cc.txt
ls J*
```

Now let's save the outputs from the J countries into a new file, in the GapminderAnalysis folder we created. We'll use the ">" (greater than symbol) for _output redirection_:

```
cat country.cc.txt J* > ../../GapminderAnalysis/all_J.txt
```

You see that the ">" symbol causes output to be sent to a file rather than displayed on the screen. Why did we use "../.." in the output path?

_Be careful when using ">" for output redirection - if the file you are redirecting to already exists, its content will be overwritten! You can append data to the end of an existing file by using the ">>" output redirection._

# History

A really helpful shell command is "history". What do you think it does? Try it! How can we save our command history to a file in our home directory?

```
history > ~/FirstDayUnix_history.txt
```

Now if you need to go back to see commands you used, you have them conveniently saved! What commands can you use to see what is in the file you just created?

# Review

Let's review what we've learned so far (10 commands and 7 shortcuts):

| Command | What it Does |
| ------------- | ------------ |
| ls -l \[_dir_\]| list files and directories in _dir_ (or current dir)(-l for long listing )|
| man _cmd_ | Show manual page for _cmd_ |
| pwd | show present working directory |
| cd _dest_ | change directory to _destination_ |
| mkdir _dirname_ | Make directory named _dirname_ |
| nano _file_ | Open nano editor on _file_ |
| mv _src_ _dest_ | Move _source_ file to _destination_ |
| cp _src_ _dest_ | Copy _source_ file to _destination_ |
| cat _file1_ _file2_ ... | Concatenate _files_ in list and display contents on screen|
| history | Output history of commands typed |

| Shortcut or Shell Feature | What it Does |
| ------------- | ------------ |
| ~ | Home directory |
| .. | Parent directory (one level up)|
| Tab | Tab key for filename completion |
| Up-Arrow | Retrieve previous command(s) |
| * | Wildcard to match any number of characters |
| > _file_ | Output redirect to create/overwrite _file_ |
| >> _file_ | Output redirect to append to _file_ |

# Exploring Data

## word and line count

You may be familiar with text or document editors that will show you a count of the number of lines, words, and characters in a file. Now we'll see how to get that information from the command line.

`wc` will count the number of words, lines, and characters in a file.

> From man/help: Print newline, word, and byte counts

Let's try this on some gapminder_by_country txt files (and remember to use Tab to complete parts of the file path):

```
cd ~/ResBaz_UNIXIntro/Data/gapminder_by_country
wc Japan.cc.txt
```
We can also use a wildcard with wc (or any command that can operate on a list of files):

```
wc J*.cc.text
```

How many lines are in each country file?

Often we care more about number of lines than number of words or characters. Conveniently, `wc` has an option to show ONLY the line count:

```
wc -l J*.cc.txt
```

How can we see if ALL of the gapminder_by_country files have the same number of lines?

```
wc -l *.cc.txt
```

Are all of the line counts the same? What does this suggest about the country.cc.txt file? How can we display the contents of country.cc.txt?

```
cat country.cc.txt
```

We'll see more uses for `wc` later. Now let's learn more commands for examining the contents of files.

## tail and head

We can output only parts of a file. This is particularly useful for files containing many lines.

### tail

`tail` will output the last 10 lines in a file, or any number of lines you request with an option. Let's see it in action:

```
tail Japan.cc.txt

tail -2 Japan.cc.txt
```

How could we view only the last line in the file?

```
tail -1 Japan.cc.txt
```

Similar to `tail` for looking at lines at the end of a file, there is a command for looking at lines at the beginning of a file.

### head

`head` will output the first 10 lines (or a number of lines specified with an option) of a file

```
head Japan.cc.txt

head -5 Japan.cc.txt
```

Let's answer a question.

> What was the GDP for Japan in 2002?

## Getting data for year 2002

We could use `tail -2 Japan.cc.txt` but that also shows data for 2007.

If we only want to look at the data for 2002 we need to filter our data. There is a command for that called `grep` (short for 'get regular expression and print', in case you were wondering!).

`grep` works on a list of files and takes a pattern to search for. The pattern is specified first, followed by a list of files:

```
grep 2002 J*.cc.txt
```

Some remarks about `grep`: it only reports lines that contain one or more instances of the pattern given to it. Run this command and see if you can explain the output:

```
grep 2007 P*.cc.text
```

Why do we see a line of data for 2002?
We can create a more specific pattern for grep by including "word boundaries". We use the backslash character with the letter b, as follows:

```
grep "\b2007\b" P*.cc.txt
```

Do you see what the "word boundary" does?

Let's save this output into a file up in the GapminderAnalysis directory. What do we need to add to the command?

```
grep "\b2007\b" P*.cc.txt > ../GapminderAnalysis/allP_2007.txt
```

## Command Pipelines

Let's look at another way to compare the output of the `grep` commands with and without word boundaries in the pattern. To do this we can send the output of the `grep` command into the input of the `wc` command. This is called a _command pipeline_, and it allows us to chain commands together to create more powerful tools. To do this chaining or pipelining we use the `|` character. (It's often just above the Return or Enter key.) Let's count lines in the grep outputs:

```
grep 2007 P*.cc.txt | wc -l
```

```
grep "\b2007\b" P*.cc.txt | wc -l
```

Notice that the counts are different.

## sort

We can sort data too. Let's sort the grep output:


```
grep "\b2007\b" P*.cc.txt | sort
```

To sort in reverse alphabetical order:

```
grep "\b2007\b" P*.cc.txt | sort -r
```

Do you see that the country names are in reverse alpha order?

### More chaining

We can chain together as many commands as we want with pipelines. What command could we add to the above pipeline to see only the data for the first 3 countries in reverse alphabetical order?

```
grep "\b2007\b" P*.cc.txt | sort -r | head -3
```

What if we only want to see the country names?

## cut (show only the columns you tell it to show)

```
grep "\b2007\b" P*.cc.txt | sort -r | head -3 | cut -f 1
```

This will show only the first column in the data, which is the country name. The -f option is short for 'fields'.

What will we see if we run this command?

```
grep "\b2007\b" P*.cc.txt | sort -r | head -3 | cut -f 1,4
```

If you need to sort numerically, use the -n option with sort (and this can be used in combination with -r.) Hopefully you are starting to see how to combine commands to do very useful things!

### More counting with `wc`

Using `ls` and `wc`, how can we tell how many countries we have gapminder data for?

```
ls | wc -l
```

## Working with large files

Now we will explore the data in the TopSpotify2017.csv file. First we need to move up to the Data directory. What command will do that?

```
cd ..
```

How many lines are in the TopSpotify2017.csv file? What happens if we use the `cat` command to look at the file contents?

```
cat TopSpotify2017.csv
```

When looking at longer files, the `less` command will show one screenful at a time, and allow you to jump around to different parts of a file or even search for patterns. (Why is it called `less`? Because it's based on an older command named `more` (short for one _more_ screenful). That's really funny, right?)

```
less TopSpotify2017.csv
```

Hit the Space bar to see the next screen of data. Press Return or Enter to move down by a single line. Type the character 'b' (lower case) to go back up one screen.

Let's look for an artist's name in the file. Type '/Sheer' and what happens?

If you want to exit out of `less` you can type a 'q' or Ctrl-C. Exit out of less and run the command again.

Now from the first screen of data, search with '/Sheer' and then type the character 'n'. What happens?


## Deleting files and directories

To delete a file we use the `rm` command. `rm` is short for `remove`.

> `rm` is forever. Files do not go in a recycle bin.

You can remove a directory by using the -rf (recursive and force options):
```
rm -rf gapminder_by_country.bak
```
_Be especially cautious when using wildcards with the `rm` command (or don't use wildcards with rm)! You could potentially remove ALL of your files unintentionally, with no way to retrieve them unless they are backed up elsewhere._

## Remote login to other systems

The `ssh` (secure shell) command allows you to login to another system on which you have an account. For example, to login to the UA High Performance Computing systems:

```
ssh _myNetID_@hpc.arizona.edu
```
You'll be prompted for your password and 2-factor authentication. Once you've successfully logged in you can use the commands you've learned today. For more information about the UA High Performance Computing systems, attend the ResBaz workshop on Wednesday afternoon, or check the Events calendar at http://datascience.arizona.edu

## Getting Un-stuck

It's not hard to end up in a situation where you are "stuck" if you forget to pass enough information to a command or pipeline. In such cases, Ctrl-C can usually get you out of trouble. Unlike in Windows, where Ctrl-C is a copy to the clipboard, in UNIX Ctrl-C will interrupt a running program or command. If you find that you are seeing an unusual prompt, or no prompt at all, you can try typing Ctrl-C to get back to the normal prompt. In the worst case you may need to end your Terminal session and start a fresh one, hoping that you have saved your work!

## More practice

Let's write a command to save the first 50 lines of TopSpotify2017.csv to a file in the SpotifyAnalysis directory:

```
head -50 TopSpotify2017.csv > ../SpotifyAnalysis/Top50Spotify2017.csv
```

How would we count the number of lines in this new file to check whether we got what we intended?

```
wc -l ../SpotifyAnalysis/Top50Spotify2017.csv
```

We saw earlier that `ls` has many options. We can use this pipeline to see the most recently modified files:

```
ls -ltr | tail
```

This is a good way to remind yourself where you left off!

Some nice uses of `history`:

```
history | grep git
```

What about this?

```
history | grep grep
```

At this point you may want to run the history command and save it to the ~/FirstDayUnix_history.txt file. Would it make sense to use ">" or ">>" to save our history now?

## Review

Let's review what we've learned in the 2nd half of the workshop (9 more commands and the pipeline and Ctrl-C features):

| Command | What it Does |
| ------------- | ------------ |
| wc -l | count number of lines |
| head _-n file_ | Show _n_ lines at the top of a file |
| tail _-n file_ | Show _n_ lines at the end of a file |
| grep _pattern file_ | output lines containing _pattern_ in _file_ |
| sort _-nr file_ | sort lines (numerically and/or reverse order) in _file_ |
| cut -f _n,m_ _file_ | Show columns _n_ and _m_ from _file_ |
| less _file_ | Show 1 screenful at a time from _file_ |
| rm _file_ | Remove _file_ (DELETES PREMANENTLY!)|
| rm -rf _dir_ | Remove _dir_ and all of its contents (DELETES PREMANENTLY!)|
| ssh _destination_ | Remotely login to _destination_ system using secure shell |

| Shortcut or Shell Feature | What it Does |
| ------------- | ------------ |
| \| | Send output of one command to input of the next command |
| Ctrl-C | Interrupt a running program, command, or pipeline |


## Homework!

The `cut` command has another option, _-d_, to specify a column _delimiter_. How can you use `cut -d ','` with other `cut` options to extract the 'danceability' column from the TopSpotify2017.csv file? (Hint: which column number is 'danceability'?)

Once you've been able to output the 'danceability' column, write a pipeline to do a numeric sort of that output.

For a more advanced exercise, read the man page or help for the `sort` command to understand what this pipeline does:
```
cut -f 2-4 -d ',' TopSpotify2017.csv | sort -n -k 3 -t ','
```

## Going Further

Today we've just scratched the surface of what's possible with UNIX commands. Be sure to practice and check out the resources below to improve your skills and productivity!

## Other Resources

[Software Carpentry Intro to Shell](https://swcarpentry.github.io/shell-novice/01-intro/index.html)
[Software Carpentry Navigating Files and Folders](https://swcarpentry.github.io/shell-novice/02-filedir/index.html)
[Software Carpentry Working with Files and Directories](https://swcarpentry.github.io/shell-novice/03-create/index.html)
[Software Carpentry Pipes and Filters](http://swcarpentry.github.io/shell-novice/04-pipefilter/index.html)

### ssh
http://blog.robertelder.org/what-is-ssh/


### 10,20,50 most frequently used Unix commands
http://www.informit.com/blogs/blog.aspx?b=2e1a39cd-e73b-4f8d-82f2-5f9b769132e1
http://www-users.york.ac.uk/~hcb1/unix20.html
https://www.thegeekstuff.com/2010/11/50-linux-commands/?utm_source=feedburner

### Useful tools
https://explainshell.com/
https://itsfoss.com/tldr-linux-man-pages-simplified/

### Great command pipelines
https://onceupon.github.io/Bash-Oneliner/
