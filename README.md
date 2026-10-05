# A Beginner's Guide to the Command Line

Most of the command-line commands in this guide work in much the same way across different operating systems. The examples here use Linux, because that is the environment you will be working with most.

If you use Windows, you can install Windows Subsystem for Linux (WSL). WSL gives you a Linux environment inside Windows, so you can use the same commands and tools without needing a separate Linux computer. It is also worth getting familiar with WSL, since Linux and command-line tools are commonly used in programming, development and server environments.

## Where am I? (`pwd`)

`pwd` stands for **print working directory**. It shows the folder you are currently in.

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

`ls` lists the files and folders in your current directory.

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

## Count words, lines and characters (`wc`)

`wc` stands for **word count**.

```bash
wc notes.txt
```

It normally shows the number of lines, words and bytes in the file.

You can ask for something specific:

```bash
wc -l notes.txt
```

counts lines.

```bash
wc -w notes.txt
```

counts words.

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
