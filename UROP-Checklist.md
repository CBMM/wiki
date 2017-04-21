## Getting started at CBMM

Welcome to CBMM! The purpose of this checklist is to prepare your system to run experiments at CBMM using [[OpenMind]] and [[Polestar]]. Once you have gotten each of the following technologies going on your machine you will be able to deploy code to those clusters, process some data, and get the results back. We've supplied instructions and resources on how to get set up for each requisite piece of technology.

## Basic Tools

### Slack

CBMM has a [Slack](https://slack.com) community. This is the fastest way to get help from our partners at [Obsidian Systems](https://obsidian.systems) and your advisors. On slack we have a #tech channel for answering any and all techincal questions. Ask away! The person who is on-boarding you should invite you to Slack.

### Command Line

If you know how to use a command line already, feel free to skip this section.

A command line shell allows you to interact with your computer through a text based interface. Most of the tools we use at CBMM are designed to be most efficiently used on the command line.

#### Where to get it

##### Linux

You already have a command line. How you access it depends on your distribution. For example on Ubuntu you can open it by pressing `Ctrl + Alt + T`.

##### Mac OS X

You already have a command line. You can access it by opening the `Terminal` application.

##### Windows

On Windows the situation is a little trickier. The command line on Windows by default isn't functional enough to perform the basic tasks you will be doing regularly. You have a few options:

  * [Install Bash on ubuntu on Windows](https://msdn.microsoft.com/en-us/commandline/wsl/about)

    This is the most thorough solution but requires you to have a modern Windows machine. If you install this, then you ought to do all of your CBMM work in the Linux subsystem and never on Windows itself. This solution allows you to follow along with all of our guides and resources as if you're on an Ubuntu machine.

  * [Use the Bash shell that comes with git for windows](https://git-for-windows.github.io/)

    This is a lightweight option if you don't want to get a UNIX shell. Note that this shell won't allow you to do more sophisticated things than interact with Git.

  * [Use PowerShell](https://msdn.microsoft.com/en-us/powershell/mt173057.aspx)

    This option is quite powerful and natively Windows, but we don't have many resources for how to use it, and no one at CBMM really uses it. If you're already comfortable using PowerShell, all the power to you! However, you'll still need to learn how to use a UNIX command line because that is what is available on OpenMind and Polestar.

#### How to use it


  * [Crash course in shell](https://learnpythonthehardway.org/book/appendixa.html)

    The prose is sometimes obnoxious but this is a good guide to performing basic shell tasks.

  * [Unix command cheat sheet](https://math.mit.edu/services/help/new/unix)

    A nice summary of useful basic commands in a Unix shell.

  * [The Bash Guide](http://guide.bash.academy/)

    This guide will teach you how to write _scripts_ for your shell. Scripting allows you to automate complicated shell tasks and invoke them as easily as a basic command.

### SSH

If you know how to use SSH already, feel free to skip this section.

SSH is a network protocol for secure remote access to a machine. We use SSH to connect to OpenMind and Polestar. You can SSH into a machine from the command line and interact with the remote machine as if you were typing directly to it.

#### Where to get it

##### Linux

SSH comes standard on most Linux distributions.

##### Mac OS X

SSH comes standard on Mac OS X.

##### Windows

The situation on Windows is a bit different.

  * If you're using Ubuntu on Windows, you have SSH in your Ubuntu subsystem.

  * If you're using git bash, it comes with ssh.

  * [Get putty otherwise](http://www.putty.org/)

#### How to use it

  * [SSH Essentials](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys)

  * [Github Explains SSH](https://help.github.com/articles/connecting-to-github-with-ssh/)

### Git

If you're already comfortable with `git`, feel free to skip this section.

`git` is a [Version control system](https://en.wikipedia.org/wiki/Version_control). It will keep track of your files and changes to those files. This helps keep your projects in a consistent state and easily recoverable from errors. It will also make it easier for you to share your code with others and collaborate on projects.

#### Where to get it

##### Linux

[Installation instructions here](https://git-scm.com/download/linux)

##### Mac OS X

[Go here and click on 'Mac OS X'](https://git-scm.com/downloads)

##### Windows

[Git for Windows](https://git-for-windows.github.io/)

#### How to use it

  * [The Git Book](https://git-scm.com/book/en/v2)

    In particular chapters `4. Git on the Server` and `6. GitHub` are valuable to read.

  * [Git Cheatsheet](https://services.github.com/on-demand/downloads/github-git-cheat-sheet.pdf)

    Always handy!

  * [Lynda Git training](https://www.lynda.com/Git-training-tutorials/1383-0.html)

    MIT students get free access to Lynda.

  * [Github Documentation](https://help.github.com/articles/set-up-git/)

    Good documentation that will also set you up with GitHub.

  * [Repository of .gitignore templates](https://github.com/github/gitignore)

    A `.gitignore` file tells `git` which files not to track. These templates will make it easier to use `git` while ignoring noise.

### GitHub

If you're on GitHub, great! If you're not, you will need to get an account there. Once you have an account, the person on-boarding you will invite you to the [CBMM GitHub organization](https://github.com/CBMM).

## Programming Languages

### Python

Python is a programming language that is quite popular in scientific research. There are some associated technologies that make using Python more robust and effective.

#### Which Python version?

There are two versions of Python which are subtly incompatible with each other, Python 2 and Python 3. Python 3 is the version of Python that is intended to be supported in the long run. It used to be very important which version you were on, but not these days. Most things you will want to do with Python can be done with either. If you have no preference, _use the version your advisor prefers_.

#### Where to get it

[The hitchhiker's guide to installing Python](http://python-guide-pt-br.readthedocs.io/en/latest/starting/installation/)

#### How to use it

  * [Python 3 documentation](https://docs.python.org/3/)

    Includes tutorials, HOWTOs, set up help, and references.

  * [Python 2 documentation](https://docs.python.org/2.7/)

    Same as above, but with Python 2

  * [The Hitchhiker's guide to Python](http://python-guide-pt-br.readthedocs.io/en/latest/)

    This guide will not quite teach the basics of Python, but it will teach you a lot about good practices and how to keep your code clean, well understood, and under control.

### virtualenv

Python comes with a tool for installing packages called `pip`. By default `pip` installs packages globally for your system. This can be bad if you have different projects that require conflicting versions of the same package. It also makes it difficult to reproduce your code elsewhere. `virtualenv` is a tool for both Python 2 and 3 that allows you to isolate the installed packages for different projects. It is highly recommended that you always install the dependencies for a project in a virtual environment.

#### Where to get it

[Install it with pip](https://virtualenv.pypa.io/en/stable/installation/)

#### How to use it

  * [Official user guide](https://virtualenv.pypa.io/en/stable/userguide/)

  * [Hitchhiker's guide to virtualenv](http://python-guide-pt-br.readthedocs.io/en/latest/dev/virtualenvs/#virtualenv)

  * [Quick tutorial](http://libzx.so/main/learning/2016/03/13/best-practice-for-virtualenv-and-git-repos.html)
