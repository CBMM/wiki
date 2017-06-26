## Getting started at CBMM

Welcome to CBMM! The purpose of this checklist is to prepare your system to run experiments at CBMM using [[OpenMind]] and [[Polestar]]. Once you have gotten each of the following technologies going on your machine you will be able to deploy code to those clusters, process some data, and get the results back. We've supplied instructions and resources on how to get set up for each requisite piece of technology.

#### Table of Contents

1. [Introduction](#getting-started-at-cbmm)
2. [Windows Users](#windows-users)
3. [Basic Tools](#basic-tools)
    * [Slack](#slack)
    * [Command Line](#command-line)
    * [SSH](#ssh)
    * [Git](#git)
    * [GitHub](#github)
4. [Programming Languages](#programming-languages)
    * [Python](#python)
    * [Matlab](#matlab)
5. [Environments](#environments)
    * [OpenMind](#openmind)
    * [Toolkit](#toolkit)


## Connecting to computational resources

Almost all scientific computing should be done one of two linux systems which are: 1) polestar or 2) openmind. You can connect to these systems in a number of ways that depend on the operating system your computer is using which we describe below.

### Windows Users

If you use a Windows system, one method to connect to polestar/OpenMind recommend using [VirtualBox](https://www.virtualbox.org/) which will let you run a virtual Linux machine from within Windows. Once you have VirtualBox, you can install a virtual Ubuntu machine for your work at CBMM. A guide to this process is [located here](https://linus.nci.nih.gov/bdge/installUbuntu.html).

Another method is to use [x2go](http://wiki.x2go.org/doku.php), which you can download from  [http://wiki.x2go.org/doku.php](http://wiki.x2go.org/doku.php). Once you have installed x2go on our system you can connect to OpenMind and polestar as described below. 

#### Connecting to OpenMind

Open x2goclient and configure a new session
* hostname: openmind7.mit.edu
* login: your-username
* SSH post: 22
* Use RSA/DSA [...] : leave empty unless you know what it means
* Try auto-login [...]: check
* Use Proxy server [...]: uncheck
* Session type: choose XFCE
 *Command: leave empty

Once you get the interface, you can open up terminals and then connect to the nodes.  To run an interactive job (e.g., if you want to use the MATLAB GUI) you can run the following commands: 

* srun --x11 --pty bash    
* module add mit/matlab/2016b
* matlab


***Important: Never run Matlab or any intensive job on the head node but instead always use srun into one of the gpu nodes before doing any work***


#### Connecting to polestar

Connecting to polestar using x2go is similar to connecting to OpenMind, and you should use the same configuration options - i.e., use XFCE, etc.

Once you get the interface on polestar, you should also open up a terminal and but connecting to polestar nodes involves running a different set of commands which is:

* ssh -Y gpu-15   (or gpu-13, gpu-14 etc) to see wh
* matlab &     (to start a new Maltab interactive session)

***Important: Never run Matlab or any intensive job on the head node but instead always ssh into one of the gpu nodes before doing any work***


### Mac Users

You can also use x2go for Macs. Additionally you can use X11. 


### Linux Users


You can also use x2go for Linux. Additionally you can...




## Basic Tools

### Slack

CBMM has a [Slack](https://slack.com) community. This is the fastest way to get help from our partners at [Obsidian Systems](https://obsidian.systems) and your advisors. On slack we have a #tech channel for answering any and all techincal questions. Ask away!

#### Sign Up

[Click here to sign up.](https://eitgroup.slack.com/x-167842209222-173638783185/signup) You will have to use your mit email address.

---

### Command Line

If you know how to use a command line already, feel free to skip this section.

A command line shell allows you to interact with your computer through a text based interface. Most of the tools we use at CBMM are designed to be most efficiently used on the command line.

#### Where to get it

##### Linux

You already have a command line. How you access it depends on your distribution. For example on Ubuntu you can open it by pressing `Ctrl + Alt + T`.

##### Mac OS X

You already have a command line. You can access it by opening the `Terminal` application.

#### How to use it


  * [Crash course in shell](https://learnpythonthehardway.org/book/appendixa.html)

    The prose is sometimes obnoxious but this is a good guide to performing basic shell tasks.

  * [Unix command cheat sheet](https://math.mit.edu/services/help/new/unix)

    A nice summary of useful basic commands in a Unix shell.

  * [The Bash Guide](http://guide.bash.academy/)

    This guide will teach you how to write _scripts_ for your shell. Scripting allows you to automate complicated shell tasks and invoke them as easily as a basic command.

---

### SSH

If you know how to use SSH already, feel free to skip this section.

SSH is a network protocol for secure remote access to a machine. We use SSH to connect to OpenMind and Polestar. You can SSH into a machine from the command line and interact with the remote machine as if you were typing directly to it.

#### Where to get it

##### Linux

SSH comes standard on most Linux distributions.

##### Mac OS X

SSH comes standard on Mac OS X.

#### How to use it

  * [SSH Essentials](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys)

  * [Github Explains SSH](https://help.github.com/articles/connecting-to-github-with-ssh/)

---

### Git

If you're already comfortable with `git`, feel free to skip this section.

`git` is a [Version control system](https://en.wikipedia.org/wiki/Version_control). It will keep track of your files and changes to those files. This helps keep your projects in a consistent state and easily recoverable from errors. It will also make it easier for you to share your code with others and collaborate on projects.

#### Where to get it

##### Linux

[Installation instructions here](https://git-scm.com/download/linux)

##### Mac OS X

[Go here and click on 'Mac OS X'](https://git-scm.com/downloads)

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

---

### GitHub

If you're on GitHub, great! If you're not, you will need to get an account there. Once you have an account, the person on-boarding you will invite you to the [CBMM GitHub organization](https://github.com/CBMM).

---

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

---

### virtualenv

Python comes with a tool for installing packages called `pip`. By default `pip` installs packages globally for your system. This can be bad if you have different projects that require conflicting versions of the same package. It also makes it difficult to reproduce your code elsewhere. `virtualenv` is a tool for both Python 2 and 3 that allows you to isolate the installed packages for different projects. It is highly recommended that you always install the dependencies for a project in a virtual environment.

#### Where to get it

[Install it with pip](https://virtualenv.pypa.io/en/stable/installation/)

#### How to use it

  * [Official user guide](https://virtualenv.pypa.io/en/stable/userguide/)

  * [Hitchhiker's guide to virtualenv](http://python-guide-pt-br.readthedocs.io/en/latest/dev/virtualenvs/#virtualenv)

  * [Quick tutorial](http://libzx.so/main/learning/2016/03/13/best-practice-for-virtualenv-and-git-repos.html)

---

### Matlab

Matlab is for data crunching.

#### Where to get it

  [Get Matlab from MIT](https://ist.mit.edu/matlab/all)

#### How to use it

  * [Matlab documentation](https://www.mathworks.com/help/matlab/)

  * [Lynda course](https://www.lynda.com/MATLAB-training-tutorials/1646-0.html)

---

## Environments

### OpenMind

OpenMind is a computing cluster shared by all neuroscience at MIT. You will need to get acquainted with it in order to run serious experiments. OpenMind is primarily accessed through `ssh` and managed with [[SLURM]].

#### Where to get it

[Getting started with OpenMind](https://github.mit.edu/MGHPCC/OpenMind/wiki/Cookbook:-Getting-started)

  You'll have to log in with your MIT credentials in order to access the MIT github. It can take a few days to be granted access to OpenMind.

#### How to use it

  * [Video tutorial](https://www.youtube.com/watch?v=NGHlPNiYJcA)

  * [OpenMind wiki](https://github.mit.edu/MGHPCC/OpenMind/wiki)

    You will need to log in with your MIT credentials in order to access the wiki.

  * [[OpenMind]] on this wiki

    Will be a little anemic until we've developed more tools for working with OpenMind.

---

### Toolkit

This is the wiki of the [CBMM Toolkit](https://github.com/CBMM/toolkit)! It contains useful scripts and tools to make it easier to manage projects. A lot of the resources here assume that you are using it.

#### Where to get it

Once you've set up [GitHub](#github) you can clone the toolkit anywhere:

`git clone git@github.com:CBMM/toolkit.git`
