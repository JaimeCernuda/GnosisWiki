*********************
Introduction to Linux
*********************

All top500 supercomputers and the majority of cloud systems run Linux.
This tutorial will cover the basic aspects of using Linux.

1.1. Choosing an OS
===================

1.1.1. Which distro?
--------------------

There are many Linux distributions out there, and they all have
different quirks. The following is a list of distros which are currently
being used, or we expect may eventually be used 1.
`Ubuntu <https://ubuntu.com/download/desktop>`__: we use Ubuntu
currently in our cluster. It’s not widely used in HPC, but it’s a
mature, well-maintained distro. There are many ubuntu-like systems
(e.g., Linux Mint), feel free to use any of them. **We recommend using
an ubuntu-like system for the purposes of our research**. 2.
`Centos7/8 <https://www.centos.org/download/>`__: CentOS 7 and 8 are
used pretty commonly in HPC. However, they have been discontinued. We
don’t recommend using them for your main OS, but you should be aware you
may have to deal with them for software portability 3.
`Rocky <https://rockylinux.org/>`__: a replacement to CentOS, and is a
potential candidate for HPC systems. 4.
`Alma <https://almalinux.org/>`__: another CentOS-like system, which is
also a potential candidate for HPC systems

1.1.2. What if I have Windows?
------------------------------

Microsoft Windows has the Windows Subsystem for Linux (WSL). It’s
competent for the majority of Linux development. If you don’t want to
kill your current windows installation, WSL should be sufficient for
most cases of our research. WSL provides an **Ubuntu** installation.
Follow `Microsoft’s
instructions <https://learn.microsoft.com/en-us/windows/wsl/install>`__
on how to enable WSL (it likely is not by default).

1.1.3. What if I have a Mac?
----------------------------

Mac’s are a bit tricky. Mac and Linux are NOT the same thing. Generally
speaking, we highly recommend developing on a Linux distribution which
is similar to what is used in HPC. Unfortunately, Macs don’t have
something like WSL. We recommend using either a container (e.g.,
Docker/Singularity) or a virtual machine (VirtualBox/Qemu) for
development. Generally, containers are much faster than VMs. We
recommend using a container for **Ubuntu**.

1.2. Basics of using a Terminal
===============================

In this section, we will use Ubuntu 22.04 as our Linux distro. First, we
will discuss the basic aspects of using a Linux terminal.

A terminal provides a way of interacting with the OS using a command
prompt. Users enter commands into the terminal based on memory instead
of using a graphical user interface (GUI). This can be faster since it
avoids clicking and memorizing menus. However, it is also necessary
since many HPC machines are remote and do not support fancy GUIs. There
are many commands Linux users should be familiar with in general.

1.2.1. Interacting with the Filesystem
--------------------------------------

Examples of the basic filesystem operations are as follows:

.. code:: bash

# Create a directory
mkdir hello

# Create directories + subdirectories
mkdir -p hello/hi/hi2

# Change into the "hello" directory
# cd: "change directory"
cd hello

# Create 4 empty files
touch hi.txt
touch hi2.txt
touch hi3.txt hi4.txt

# List the hello directory (view its contents)
ls hello

# Change into the "hi2" directory
# NOTE: ./ is optional
# cd hi/hi2 would do the same thing
cd ./hi/hi2

# Go to the parent directory (hi)
cd ..
# Go to hello's parent
cd ../../

# Remove 3 of the files
rm hello/hi.txt
rm hello/hi2.txt hello/hi3.txt

# Remove directories and subdirectories
# "r" means to "recursively" delete all data in the directory
# "f" means "force" delete the directory without asking for confirmation
rm -rf hello

1.2.2. What are environment variables?
--------------------------------------

Environment variables are used to store some sort of information without
having to hard-code it each time. Many programs rely on environment
variables as a way of passing information to the program.

The most basic example

1.2.3. Simple text editing
--------------------------

There are three main terminal text editors: nano, vim, and emacs. vim
and emacs rely heavily on memorizing key bindings. For new users, this
is typically challenging. In general, we do not code using terminal text
editors, we only use them to do minor changes. We recommend that large
changes to files be made in an IDE, office tool, or graphical text
editor.

For this reason, we will discuss only the basics of vim and nano. We
will not touch emacs, as vim and nano are almost always the default text
editors. Generally, we recommend nano since it’s simple. Some cases, vim
may be the default, so it will be discussed too.

1.2.3.1. Nano
~~~~~~~~~~~~~

To open or create a file using nano, do the following:

.. code:: bash

   nano ~/hello.txt

The file can be edited immediately (if you have edit rights to the
file).

The main keybindings to be aware of are as follows: 1. “Ctrl s” will
save a file 2. “Ctrl x” will close the file

1.2.3.2. Vim
~~~~~~~~~~~~

To open a file using vim, do the following:

.. code:: bash

   vi ~/hello.txt

When the file is opened, the main keybindings to consider are is
follows: 1. Initially, the file is opened in “normal mode”. **You must
press “i” in order to switch to “edit mode”.** 2. When you have finished
editing, press ESCAPE on your keyboard. This will bring you back to
normal mode 3. Press “:” to bring you into “command mode” 4. Then type
“wq” to “write” and then “quit”. Press enter, and the editor will close

NOTE: if you accidentally press “Ctrl s”, you will not be able to type
anything (not even commands). To get out of this, type “Ctrl q”

1.3. SSH
--------

SSH is a secure way of connecting to a remote machine. SSH relies on
public-private key cryptography to secure the connection. The private
key is a secret that only you should know. The public key should be
given to other people. Generally, RSA is used as the algorithm for
generating keys.

The following guide will demonstrate how to setup SSH for connecting to
an SSH server.

1.3.1. Creating the keys
~~~~~~~~~~~~~~~~~~~~~~~~

**SSH keys can be given passwords, but we recommend against**. We
consider the SSH key itself to be secret enough that a password is
completely unnecessary. This is referred to as “passwordless-ssh”.
**Passwordless-ssh is required for many HPC programs**.

To create a public/private key pair, run the following command:

.. code:: bash

ssh-keygen

The default names for the keys are as follows: 1. The private key is
“~/.ssh/id_rsa” 2. The public key is “~/.ssh/id_rsa.pub”

You can use other names (it doesn’t have to be id_rsa), **but we
recommend against this in general**. Many SSH-based tools become
cumbersome with keys which are non-default.

1.3.2. Ensuring permissions
~~~~~~~~~~~~~~~~~~~~~~~~~~~

SSH is very particular about the permissions of the ~/.ssh directory and
the files in that directory. Below describes the permissions that need
to be set to make SSH behave.

For convenience, feel free to copy-paste this. A detailed description of
what these do is under “How does chmod work?”

.. code:: bash

   sudo chmod 700 ${HOME}/.ssh
   sudo chmod 644 ${HOME}/.ssh/id_rsa.pub
   sudo chmod 600 ${HOME}/.ssh/id_rsa
   sudo chmod 600 ${HOME}/.ssh/authorized_keys
   sudo chmod 600 ${HOME}/.ssh/config

1.3.2.1. How does chmod work?
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

chmod stands for “change mode”. It has the following syntax

.. code:: bash

   sudo chmod [mode] [path]

-  “mode” is a 3-digit code.
-  Each digit is between 0 and 7
-  The digits have the following meaning: [owner] [group] [user]
-  owner: typically you
-  group: files can be apart of a group. Only one group per file or
   directory.
-  user: typically anyone other than you

A single digit can have the following values:

0. No permissions
1. Execute only
2. Write only
3. Write and execute (2 + 1 = 3)
4. Read only
5. Read and execute (4 + 1 = 5)
6. Read and write (4 + 2 = 6)
7. Read, write, and execute (4 + 2 + 1 = 7)

.. code:: bash

   # The SSH directory
   # Owner has read, write, execute permissions. 
   # No one else can touch this directory.
   sudo chmod 700 ${HOME}/.ssh

   # The public key
   # Owner has read + write permissions.
   # Other users can read this file
   sudo chmod 644 ${HOME}/.ssh/id_rsa.pub

   # The private key
   # Owner has read + write permissions
   # Nobody else has permissions
   sudo chmod 600 ${HOME}/.ssh/id_rsa

   # Authorized keys
   # Owner has read + write permissions
   # Nobody else has permissions
   sudo chmod 600 ${HOME}/.ssh/authorized_keys

   # User Config
   # Owner has read + write permissions
   # Nobody else has permissions
   sudo chmod 600 ${HOME}/.ssh/config

1.3.3. Key registration
~~~~~~~~~~~~~~~~~~~~~~~

Your key will then have to be registered with the SSH server. This is
typically done using the ssh-copy-id.

.. code:: bash

   ssh-copy-id -f -i ~/.ssh/id_rsa [USERNAME]@[IP]

If the machine has a custom port number, the command’s syntax is as
follows:

.. code:: bash

   ssh-copy-id -f -i ~/.ssh/id_rsa -p [PORT] [USERNAME]@[IP]

1.3.4. Connecting to a machine
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To connect to a machine, use the “ssh” command. The command roughly has
the following syntax:

.. code:: bash

ssh -p [PORT] -i [PRIVATE_KEY] [USERNAME]@[IP]

-
-
-
-

Generally, if everything is default (SSH key, port number), the command
would look like:

.. code:: bash

ssh [USERNAME]@[IP]
