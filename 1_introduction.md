# The Command Line - Introduction

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

