# A Beginner's Guide to the Command Line

Most of the command-line commands in this guide work in much the same way across different operating systems. The examples here use Linux, because that is the environment you will be working with most.

If you use Windows, you can install Windows Subsystem for Linux (WSL). WSL gives you a Linux environment inside Windows, so you can use the same commands and tools without needing a separate Linux computer. It is also worth getting familiar with WSL, since Linux and command-line tools are commonly used in programming, development and server environments.

## Where am I? (`pwd`)

`pwd` stands for **print working directory**. It shows the directory you are currently in.

```bash
pwd
```

Example output:

```text
/home/student/Documents
```

This is useful when you are not sure where you are in the file system.

---

## What's in this directory? (`ls`)

`ls` lists the files and directorys in your current directory.

```bash
ls
```

You can also give commands extra options, called **arguments** or **flags**.

For example:

```bash
ls -al
```

Here, `-a` shows hidden files and `-l` gives a more detailed listing.

Options can often be combined, so:

```bash
ls -a -l
```

and:

```bash
ls -al
```

do the same thing.

---

## Change directory (`cd`)

`cd` lets you move between directories.

```bash
cd Documents
```

Move back one directory:

```bash
cd ..
```

Go to your home directory:

```bash
cd ~
```

You can also use a complete path:

```bash
cd /home/student/Documents
```

A useful trick is to type part of a filename or directory name and press **Tab**. The terminal can often complete the name for you.

---

## Make a directory (`mkdir`)

`mkdir` creates a new directory.

```bash
mkdir project
```

You can then enter it with:

```bash
cd project
```

---

## Copy files (`cp`)

`cp` copies a file.

```bash
cp notes.txt notes-backup.txt
```

You can also copy a file into another directory:

```bash
cp notes.txt backup/
```

### Copying directories recursively

A directory can contain other directories and files. To copy all of them, use `-r`, which means **recursive**.

```bash
cp -r project project-backup
```

This copies the directory and everything inside it.

---

## Move or rename files (`mv`)

`mv` moves files and directories.

```bash
mv notes.txt Documents/
```

It is also used to rename things:

```bash
mv old-name.txt new-name.txt
```

The same works for directories:

```bash
mv old-project new-project
```

---

## Remove files (`rm`)

`rm` deletes a file.

```bash
rm notes.txt
```

Be careful with `rm`. Files deleted from the command line usually do not go into your recycle bin.

### Wildcards

The `*` character is a **wildcard**. It can represent any number of characters.

For example:

```bash
rm *.txt
```

removes every file in the current directory whose name ends in `.txt`.

Another example:

```bash
rm test*
```

matches names such as:

```text
test.txt
testing.js
test-data.csv
```

Be especially careful when combining wildcards with `rm`.

### Removing directories recursively

To remove a directory and everything inside it:

```bash
rm -r old-project
```

Again, use this carefully. A recursive removal can delete many files at once.

---

## Directory traversal

You do not always need to move into a directory with `cd` before working with files inside it. Commands can refer to files and directories using **paths**.

A path describes where something is located in the file system.

Suppose you have this structure:

```text
/home/student/
├── Documents/
│   ├── essay.txt
│   └── notes.txt
└── projects/
    └── website/
        └── index.html
```

If you are currently in:

```text
/home/student
```

you can display `essay.txt` without first entering `Documents`:

```bash
cat Documents/essay.txt
```

You can also copy it somewhere else:

```bash
cp Documents/essay.txt projects/
```

### Relative paths

A **relative path** describes a location relative to your current directory.

For example:

```bash
Documents/essay.txt
```

means:

```text
start in the current directory
go into Documents
find essay.txt
```

The special name:

```text
..
```

means the parent directory, or one level higher in the directory tree.

If you are in:

```text
/home/student/Documents
```

then:

```bash
cat ../projects/website/index.html
```

means:

```text
go up from Documents to /home/student
go into projects
go into website
open index.html
```

You can go up more than one level:

```bash
cd ../..
```

or refer to a file several levels higher:

```bash
cat ../../notes.txt
```

The special name:

```text
.
```

means the current directory.

For example:

```bash
./script.sh
```

means "the file called `script.sh` in the current directory".

### Absolute paths

An **absolute path** gives the complete location starting from the root of the file system.

Absolute paths begin with `/`.

For example:

```bash
cat /home/student/Documents/essay.txt
```

This refers to the same file regardless of which directory you are currently in.

You can use paths with most commands:

```bash
cp ../notes.txt .
```

copies `notes.txt` from the parent directory into the current directory.

```bash
mv project/file.txt ../backup/
```

moves a file from the `project` directory into a neighbouring `backup` directory.

```bash
wc -w ~/Documents/essay.txt
```

counts the words in a file inside your home directory.

Thinking in terms of paths is important. You do not need to constantly use `cd` to move around before doing something.

---

## Create an empty file (`touch`)

`touch` can create an empty file.

```bash
touch notes.txt
```

If the file already exists, `touch` updates its modification time rather than deleting its contents.

It is useful when you quickly need to create a new file:

```bash
touch main.js
```

---

## Variables

The shell can store values in **variables**.

For example:

```bash
name="Alex"
```

To use the value, put `$` before the variable name:

```bash
echo $name
```

Output:

```text
Alex
```

Do not put spaces around `=` when assigning a shell variable.

This works:

```bash
course="Computer Science"
```

This does not:

```bash
course = "Computer Science"
```

---

## Print something (`echo`)

`echo` prints text to the terminal.

```bash
echo "Hello world"
```

Output:

```text
Hello world
```

It can also display variables:

```bash
name="Sam"
echo "Hello $name"
```

Output:

```text
Hello Sam
```

---

## Display a file (`cat`)

`cat` can display the contents of a text file.

```bash
cat notes.txt
```

For short files, this is a quick way to see what is inside them.

You can also combine files:

```bash
cat part1.txt part2.txt
```

For very long files, `less` is usually more convenient.

---

## Read long files (`less`)

`less` lets you view a file one screen at a time.

```bash
less large-file.txt
```

Useful controls include:

```text
Space      Move forward
b          Move backward
/word      Search for "word"
q          Quit
```

Unlike `cat`, it does not print the entire file onto the screen at once.

---

## Get help with a command (`--help`)

Many commands explain themselves if you add:

```bash
--help
```

For example:

```bash
ls --help
```

or:

```bash
cp --help
```

This normally shows the command's available options and how to use them.

---

## Read the manual (`man`)

Linux and Unix systems have manual pages for many commands.

For example:

```bash
man ls
```

This opens the manual page for `ls`.

You can scroll through it and press:

```text
q
```

to quit.

Other examples:

```bash
man cp
man chmod
man cat
```

When you are unsure how a command works, `--help` and `man` are good places to start.

---

## The `PATH` and finding programs

When you type a command such as:

```bash
ls
```

the shell needs to find the program that implements `ls`.

Executable programs are often called **binaries** or **executables**.

Many of them are stored in directories such as:

```text
/usr/bin
/bin
/usr/local/bin
```

For example, on many Linux systems you can find `ls` at:

```text
/usr/bin/ls
```

You could run it using its complete path:

```bash
/usr/bin/ls
```

but normally you simply type:

```bash
ls
```

This works because the shell uses a special environment variable called `PATH`.

You can display it with:

```bash
echo $PATH
```

You may see something like:

```text
/usr/local/bin:/usr/bin:/bin
```

The directories are separated by `:`.

When you type:

```bash
ls
```

the shell searches these directories in order until it finds an executable called `ls`.

Conceptually, it tries something like:

```text
/usr/local/bin/ls
/usr/bin/ls
/bin/ls
```

and runs the first matching program it finds.

### Finding where a command is located

The `which` command can show the path of many commands:

```bash
which ls
```

Example output:

```text
/usr/bin/ls
```

Another example:

```bash
which node
```

might produce:

```text
/usr/bin/node
```

The shell also has a useful command called `command -v`:

```bash
command -v ls
```

This can also tell you what will run when you enter a command.

---

## Who am I logged in as? (`whoami`)

`whoami` displays your current username.

```bash
whoami
```

Example:

```text
student
```

This can be useful on university servers where you may be logged into a computer remotely.

---

## Permissions and `chmod`

Linux and Unix systems have permissions that decide who can read, modify or execute a file.

If you run:

```bash
ls -l
```

you might see something like:

```text
-rw-r--r-- 1 student students 1200 Oct 5 12:00 notes.txt
```

The characters at the beginning describe the file's permissions.

The three main permissions are:

```text
r    read
w    write
x    execute
```

`chmod` means **change mode** and is used to change these permissions.

For example, to make a script executable:

```bash
chmod +x script.sh
```

You can then run it with:

```bash
./script.sh
```

You may also see numerical permissions:

```bash
chmod 755 script.sh
```

These are common, but you do not need to memorise the numbers immediately. When starting out, understanding `r`, `w` and `x` is more important.

---

## Piping with `|`

One of the most useful features of the command line is that you can connect commands together.

The pipe symbol:

```text
|
```

takes the output of one command and gives it to another command.

For example:

```bash
cat notes.txt | wc -w
```

`cat` produces the contents of `notes.txt`, and `wc -w` counts the words.

Another example:

```bash
ls | wc -l
```

This counts how many entries `ls` produces.

You will often see commands combined this way.

---

## Redirecting output

Normally, a command prints its output to the terminal. You can instead send that output to a file using `>`.

For example:

```bash
echo "Hello" > message.txt
```

The file `message.txt` will now contain:

```text
Hello
```

Be careful: `>` replaces the existing contents of the file.

To add something to the end of a file instead, use `>>`:

```bash
echo "Another line" >> message.txt
```

You can redirect other commands too:

```bash
ls > files.txt
```

This stores the output from `ls` inside `files.txt`.

---

## Putting commands together

The real usefulness of the command line becomes clearer when commands are combined.

For example:

```bash
ls -al
```

shows detailed information about your files.

```bash
cat essay.txt | wc -w
```

counts the words in an essay.

```bash
ls *.txt > text-files.txt
```

finds names ending in `.txt` and saves the list to a file.

```bash
mkdir backup
cp -r project backup/
```

creates a backup directory and copies a project into it.

---

## Scripting

You can put several command-line commands together in a file and run them as a **script**.

A shell script is simply a text file containing commands that the shell executes in order.

For example, create a file:

```bash
touch backup.sh
```

You could put the following commands inside it:

```bash
mkdir backup
cp *.txt backup/
ls -l backup/
```

When the script runs, the shell executes the commands from top to bottom.

This is useful when you regularly perform the same sequence of commands.

### Running a script with `bash`

You can run a shell script by giving it to `bash`:

```bash
bash backup.sh
```

You do not need to make the file executable when running it this way.

For example, a script called `report.sh` might contain:

```bash
pwd
echo "Files in this directory:"
ls
echo "Number of text files:"
ls *.txt | wc -l
```

Run it with:

```bash
bash report.sh
```

The commands are executed just as if you had typed them into the terminal yourself.

### Making a script executable

Shell scripts often begin with a line called a **shebang**:

```bash
#!/usr/bin/env bash
```

A complete script might look like:

```bash
#!/usr/bin/env bash

echo "Creating backup directory"
mkdir backup

echo "Copying text files"
cp *.txt backup/

echo "Backup contains:"
ls -l backup/
```

The shebang tells the operating system which program should run the script.

You can then make the file executable:

```bash
chmod +x backup.sh
```

and run it:

```bash
./backup.sh
```

### Variables in scripts

The same variables you use interactively can also be used in scripts.

For example:

```bash
#!/usr/bin/env bash

name="Alex"

echo "Hello $name"
echo "Your current directory is:"
pwd
```

You can also use variables to avoid repeating paths:

```bash
#!/usr/bin/env bash

backup="backup"

mkdir $backup
cp *.txt $backup/
ls -l $backup/
```

When a variable contains a filename or directory name that might include spaces, putting it inside quotes is safer:

```bash
directory="My Documents"

ls "$directory"
```

### Combining commands in scripts

Scripts become useful because you can combine the ideas from earlier sections.

For example:

```bash
#!/usr/bin/env bash

echo "Creating report"

pwd > report.txt
echo "Files:" >> report.txt
ls -al >> report.txt
echo "Word count:" >> report.txt
wc -w essay.txt >> report.txt

echo "Report created"
```

This script creates a file called `report.txt` containing information produced by several commands.

Another example:

```bash
#!/usr/bin/env bash

mkdir backup
cp Documents/*.txt backup/
ls backup/ > backup-files.txt
wc -l backup-files.txt
```

This:

```text
creates a backup directory
copies text files into it
stores a list of the copied files
counts how many entries are in that list
```
