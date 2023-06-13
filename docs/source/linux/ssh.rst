*****
SSH
*****

SSH is a secure way of connecting to a remote machine. SSH relies on
public-private key cryptography to secure the connection. The private
key is a secret that only you should know. The public key should be
given to other people. Generally, RSA is used as the algorithm for
generating keys.

The following guide will demonstrate how to setup SSH for connecting to
an SSH server.

Creating the keys
==================

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

Ensuring permissions
=====================

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

How does chmod work?
---------------------

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

Key registration
==================

Your key will then have to be registered with the SSH server. This is
typically done using the ssh-copy-id.

.. code:: bash

   ssh-copy-id -f -i ~/.ssh/id_rsa [USERNAME]@[IP]

If the machine has a custom port number, the command’s syntax is as
follows:

.. code:: bash

   ssh-copy-id -f -i ~/.ssh/id_rsa -p [PORT] [USERNAME]@[IP]

Connecting to a machine
========================

To connect to a machine, use the “ssh” command. The command roughly has
the following syntax:

.. code:: bash

ssh -p [PORT] -i [PRIVATE_KEY] [USERNAME]@[IP]

Generally, if everything is default (SSH key, port number), the command
would look like:

.. code:: bash

ssh [USERNAME]@[IP]