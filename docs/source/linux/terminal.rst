****************************
Basics of using a Terminal
****************************

In this section, we will use Ubuntu 22.04 as our Linux distro. First, we
will discuss the basic aspects of using a Linux terminal.

A terminal provides a way of interacting with the OS using a command
prompt. Users enter commands into the terminal based on memory instead
of using a graphical user interface (GUI). This can be faster since it
avoids clicking and memorizing menus. However, it is also necessary
since many HPC machines are remote and do not support fancy GUIs. There
are many commands Linux users should be familiar with in general.

Interacting with the Filesystem
================================

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

What are environment variables?
================================

Environment variables are used to store some sort of information without
having to hard-code it each time. Many programs rely on environment
variables as a way of passing information to the program.

The most basic example

Simple text editing
====================

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

Nano
----

To open or create a file using nano, do the following:

.. code:: bash

   nano ~/hello.txt

The file can be edited immediately (if you have edit rights to the
file).

The main keybindings to be aware of are as follows: 1. “Ctrl s” will
save a file 2. “Ctrl x” will close the file

Vim
-----

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