# The Command Line

This short course is designed to introduce you to the basics of using the command line.

It does not assume any previous knowledge of using the command line, so if you've used it before feel free to skim through it until you get to things that are new to you (if any!).

Take it at your own pace. You're not expected to absorb everything, especially not at first glance! It's enough to have an overall idea of what you need to do, and to know where to find the details.

Becoming familiar with the command line is a matter of practice; learning by doing. An important part of this is looking at examples and tweaking them until you get them to do what you need them to do. Unfortunately, the start of this learning curve can be steep and changing examples without a clear idea of *what* needs changing and *why* can be an exercise in frustration. This course aims to take you over that first hill so you can get to grips with the command line well enough to develop your skills at your own pace, when you need to use the command line in future.

## What is the command line?

The command line is an interface to run programs and interact with files. You type the commands as text rather than using a mouse. Information is presented back to you also as text.

There are many different flavours of command line. Programming languages often have their own command line (or 'console'), to allow you to execute code line by line. Historically, each operating system also had its own command line, with its own unique quirks.

Modern computers all offer access to a version of the **UNIX shell**, (shell = command line). Although there are different versions of this shell, they all conform to the same standard and behave the same (apart from when they don't). This shell is a programming language in its own right, but one designed primarily for manipulating files and managing how and when programs run. The most common UNIX shell is called **bash**, which stands for "Bourne Again SHell". It was written as a replacement for the Bourne Shell, and the name is an example of programmer humour.

A **terminal** window is how you can access the command line. You can have multiple terminal windows open at once.

## Why use the command line?

- Some tasks are **quicker** to perform using the command line than with a graphical user interface.
- You can keep a **record** of your commands in a text file, which allows you to **reproduce** the steps exactly,or **copy** them to make alterations for a similar task.
- The command line is used for a lot of **automation**, setting programs to run automatically one after the other, and for computing clusters and cloud computing.
- Many **bioinformatics tools** run primarily from the command line.

## Where is the command line?

**Linux** computers have the terminal built in. If you're using Linux you almost certainly know how to find this already.

**Mac OS X** computers also already have a terminal built-in (the operating system is a UNIX-like one behind the scenes). You can find it in Applications/Utilities/Terminal. Drag into your dock to make it easily available. Some minor details differ between this shell and the default Linux one, but they shouldn't 

For **Windows** computers, you can install something called the **Linux Subsystem for Windows** (WSL). This installs a complete Linux system you can access from within Windows. Windows's own command line tools, 'cmd.exe' and 'powershell.exe', work differently to the examples here and if you accidentally find yourself in one of them, close the window and back away slowly.

For **all** computers, there are tools that embed terminal windows in an app or browser window. Jupyter notebook is one example. These allow you to put your notes, and your code from different programming languages, alongside each other in a single document. This lets you keep all the information for a particular project in one place, rather than spread out across multiple files.

When using a **high performance computing** cluster or a **cloud computing** product, it's common to need to log in to the terminal of that system, and use the command line to interact with it..

### Installing the Windows Subsystem for Linux

The UNIX terminal for Windows requires Windows 10 or above. The full installation instructions are available on-line, but here's a brief guide.

You will need administrator permissions to install WSL. If you don't have those permissions, contact your IT team to install it for you.
1. Start a Windows command prompt as an administrator. To do this, type 'command' into the start menu search box. Don't left-click on the '**Command Prompt**' app!
2. Instead, right-click and select 'run as administrator'.
3. You will be asked to allow the app to make changes to your device – click yes.
4. In the command prompt window, type: `wsl --install -d Ubuntu` and press Enter.
5. The first part of the installation will take a minute or two. During this time you'll see various messages about Windows downloading and installing various components.
6. When this process has finished, reboot your computer.
7. Once you log back in, the installation will continue - a window will open saying 'Installing: Ubuntu'. Don't panic! It's not removing Windows, just adding a version of Ubuntu embedded inside Windows.
8. Once installation is complete, you should have a new Ubuntu app in your start menu. The first time you click it, it will ask you to choose a new username and password. I suggest using the same username as you have on your computer, but in any case don't forget these!
9. If it doesn't seem to work, you might need to restart your PC one final time and try again.


##### Section break and reminder questions


## I have a Unix-like terminal, now what?
These examples assume you are using bash for the command line, but should steer clear of situations where the small difference between UNIX-like shells matter.

### The Command Prompt

When you log in, you will usually see the 'message of the day'. This was more of a thing back when these messages were changed regularly with news about the computing facilities. The meaningful part is the command prompt:
`$`
This is what the command line shows when it is ready to receive input.

Once you type a command and press Enter, the command line will execute it, display any output, and when it is finished it will show you the prompt again. If the processing takes a long time, it can be a while before you get back to the prompt.

It's common in tutorials like this to include this prompt in the examples of commands, **but you do not need to type it**. It's there as a reminder that the example is for the command line.

Try the command:
`$ echo "Look at me"`
(Remember you don't have to type the $)

The `echo` command simply echoes input text back as output.

The command line is **case sensitive**, that is, capitalisation matters. It's usual for everything to be in lower case, both commands and file names, to help avoid errors. If you accidentally type:
`$ Echo "Look at me"`
You will see an error similar to:
```
Command 'Echo' not found, did you mean:
  command 'echo' from deb coreutils (8.32-4.1ubuntu1)
Try: sudo apt install <deb name>
```
This is telling you that the system does not know any command called `Echo`. It then helpfully looks to see if any similarly-named commands exist, that you don't have installed. This is useful when you know you need a command but don't know which package to install to get it. It is less useful when it's just a typing error and the command you wanted is already installed.

All commands are a special type of file (most of them are hidden deep in the guts of the operating system). When you download a new tool you need, it will exist as a file as well (possibly with a few directories containing examples, help documents, supporting files and so on).

### Useful tricks

The command line has a number of tricks to make it easier and quicker to use. These are useful not just to do things faster when you're comfortable with the command line, but to do things faster while you're learning, so it's good to start using them right away.

- Pressing *Control+C* will force the command line to **cancel** the command it is currently executing. Use this if you realise you've executed the wrong command, or if the command line becomes unresponsive.
- Because of the above, copying and pasting works a little differently.
- *Control+Shift+C* will copy, and *Control+Shift+V* will paste.
  - Middle-click will also paste. 
  - On platforms other than WSL, highlighting any text with the mouse will copy it to the clipboard.
  - There are other ways to copy and paste, some of which are inconsistent between OSes, which is a mess.
- The command line keeps a (long) list of the most recent commands you have entered. You can use the up and down arrow keys to skip backwards and forwards through this **history**, to execute the same command again, or alter it slightly to fix a mistake.
- When you press the tab key, the command line will attempt to complete what you are typing, based on the commands it knows and the files available. If you've typed enough for the **tab completion** to be unique, the rest of it will be filled in. If there are multiple possibilities, it will fill in as much as it can.
  - Pressing tab a second time will make the command line show you a list of the possible further completions. You can use this to view the possibilities, and to work out what letters you can type next to get the full tab completion you want

### Directories

Files on computers are stored in a nested series of **directories** (or folders). When working on the command line, you are 'in' a specific folder, and commands are run in that context.

On some platforms, this **working directory** appears before the prompt symbol, so you don't forget where you are.

Try the command:
`$ pwd`
This stands for 'print working directory'. Very short abbreviations for commands is common in bash.

You'll see what is called an **absolute path** to your working directory. If you compare this with what appears before the prompt, you'll see that only the last part of the absolute path is shown, for brevity.

When you first log in, your working directory is probably your **home directory**. This is a directory on the system that's exclusively for your use, similar to 'My Documents' on windows..

Try the command:
`$ cd ..`
This stands for 'change directory'. Don't worry about what the '..' means yet. This command is used to navigate the directory structure, changing your working directory as you go. The command you just ran has changed to one directory 'up'.

Repeat the command:
`$ pwd`
You can see that the last directory in the chain is no longer there.

### Special symbols

The '/' symbol is used to separate the directory names as you work through the tree. **Absolute paths** all start with a '/', to say that they begin at the very top of the tree.

There is also something called a **relative path**, which starts from your current working directory. Relative paths do not start with a '/'.

The special character '.' represents the current directory. `./somefolder` is equivalent to `somefolder`, is also equivalent to `./././somefolder`.

The special character '..' represents the parent directory. You used this with the `cd` command, earlier. This is very useful, as you can use it to move up the directory structure without having to use an absolute path.

Another important special character is `~` (tilde). This is a shorthand for the absolute path to your home directory.
`$ cd ~`
will take you back to your home directory. You can also use it as part of a longer absolute path, for example: `~/some_folder/some_file.txt`

The last important special character is `#`. This is used to create comments. The `#` symbol, and everything after it on the same line, is ignored. This lets you type free text in amongst your commands. This is most useful in scripts (which are discussed in a later section).


## Other simple commands

Here are some other simple commands you can try:

| Command | What it does | Example |
|---|---|---|
| `ls` | List files in a directory, or a file or files you specify. Defaults to the working directory. | `ls /etc/` |
| `cat` | Show the contents of a text file. | `cat ~/.bashrc` |
| `cp` | Make a copy of a file in a new location. If you end the destination in a directory, the new file is in that directory with the same name. | `cp ~/.bash_history bash_history2` |
| `mv` | Move a file to a new location. Works like cp, except the original file is removed. | `mv bash_history2 bash_history_copy` |
| `rm` | Removes a file. **You will not be asked if you are sure you want to delete the file.** Important operating system files are generally protected from accidental removal. | `rm bash_history_copy`
| `mkdir` | Create a new directory. | `mkdir new_directory` |
| `rmdir` | Removes an entire directory. Fails if the directory is not empty. | `rmdir new_directory` |
| `wc` | Counts the lines, words and letters in a file. | `wc the_dictionary.txt` |
| `grep` | Searches for a snippet of text in a file, showing all the lines that contain that text. | `grep alias .bashrc` |

You can see that with these simple tools, you can manage files and inspect them. However, you might have noticed that we've not mentioned any way to create a file yet! We'll cover that after these recap exercises.

##### Recap Questions
1. If the command line appears to be hanging, what keyboard shortcut would you use to try and get back to the command prompt?
2. What symbol can you use as shorthand for your home directory?
3. How many levels up from your current directory does the path `../../../` refer to?
4. You tried to copy a line of text from the terminal, but instead the command line seemed to execute an empty command. Can you work out what has happened?
5. What two commands could you use, one after the other, to replicate the use of the `mv` command?
