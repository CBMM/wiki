## Getting started at CBMM

Welcome to CBMM! The purpose of this checklist is to prepare your system to run experiments at CBMM using [[OpenMind]] and [[Polestar]]. Once you have gotten each of the following technologies going on your machine you will be able to deploy code to those clusters, process some data, and get the results back. We've supplied instructions and resources on how to get set up for each requisite piece of technology.

### Slack

CBMM has a [Slack](https://slack.com) community. This is the fastest way to get help from our partners at [Obsidian Systems](https://obsidian.systems) and your advisors. On slack we have a #tech channel for answering any and all techincal questions. Ask away! To get invited to the CBMM Slack [submit an issue here](TODO-FILLME).

### Command Line

If you know how to use a command line already, feel free to skip this section.

Depending on your technical background you may already be comfortable interacting with a computer through a command line interface (CLI) instead of a graphical user interface (GUI). It is very important to get used to a command line for doing research. You don't have to become a wizard in order to get stuff done, but you shouldn't feel lost.

#### Where to get it

##### Ubuntu

You already have a command line. You can open it by pressing `Ctrl + Alt + T`.

##### Mac

You already have a command line. You can access it by opening the `Terminal` application.

##### Windows

On Windows the situation is a little trickier. The command line on Windows by default isn't functional enough to perform the basic tasks you will be doing regularly. You have a few options:

  * [Install Bash on ubuntu on Windows](https://msdn.microsoft.com/en-us/commandline/wsl/about)

    This is the most thorough solution but requires you to have a modern Windows machine. If you install this, then you ought to do all of your CBMM work in the Linux subsystem and never on Windows itself. This solution allows you to follow along with all of our guides and resources as if you're on an Ubuntu machine.

  * [Use the Bash shell that comes with git for windows](https://git-for-windows.github.io/)

    This is a lightweight option if you don't want to try to emulate a UNIX shell. Note that this shell won't allow you to do more sophisticated things than interact with Git.

  * [Use PowerShell](https://msdn.microsoft.com/en-us/powershell/mt173057.aspx)

    This option is quite powerful and natively Windows, but we don't have many resources for how to use it, and no one at CBMM really uses it. If you're already comfortable using PowerShell, all the power to you! However, you'll still need to learn how to use a UNIX command line because that is what is available on OpenMind and Polestar.

#### How to use it


  * [Crash course in shell](https://learnpythonthehardway.org/book/appendixa.html)

    The prose is sometimes obnoxious but this is a good guide to performing basic shell tasks.

  * [Unix command cheat sheet](https://math.mit.edu/services/help/new/unix)

    A nice summary of useful basic commands in a Unix shell.

  * [The Bash Guide](http://guide.bash.academy/)

    This guide will teach you how to write _scripts_ for your shell. Scripting allows you to automate complicated shell tasks and invoke them as easily as a basic command.
