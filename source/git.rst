Git
===

All of the DHIL projects use Git for version control.

Installation
------------

Mac OS X provides a ``git`` command as part of the XCode suite. It is usually
out of date, so it's best to install Git from Homebrew.

.. code-block:: console

  $ brew install git
  $ git --version
  git version 2.18.0

Encryption Keys
---------------

Command line git is easiest to use when you've set up ssh keys. They enable
secure password-less communication between computers.

.. sidebar:: Existing Keys

  You might already have a public/private key pair. Check for them like so::

  $ ls ~/.ssh/

  If the output includes a file called ``id_rsa.pub`` you can skip this step.

Start by generating a public/private key pair. The command below will ask some
questions. Press enter to accept the defaults. There will be a lot of output, so
only the important lines are shown below.

.. code-block:: console

  $ ssh-keygen
  Generating public/private rsa key pair.
  Enter file in which to save the key (/Users/USERNAME/.ssh/id_rsa):
  Enter passphrase (empty for no passphrase):
  Enter same passphrase again:
  Your identification has been saved in /Users/USERNAME/.ssh/id_rsa.
  Your public key has been saved in /Users/USERNAME/.ssh/id_rsa.pub.

  (lots of output cut)

  $ ls ~/.ssh/
  id_rsa          id_rsa.pub

Success. From this point forward, git will attempt to use the ssh keys generated
above to interact with servers.

Create a Github Account
-----------------------

We use `GitHub`_ to manage most of our souce code. Visit the website, sign up,
and we will add you as a contributor to the `SFU DHIL account`_.

.. sidebar:: Hidden Files and Directories

  File and directory names that start with a dot(.) are hidden. The OS X Finder
  won't show you these directories by default. One example is the ``.ssh``
  directory inside your home directory. You can open that directory in the
  finder: ``open ~/.ssh`` to see the contents.

Once you've signed up for an account you should add your SSH public key. It
lives in ``/Users/USERNAME/.ssh/id_rsa.pub``. That's inside a hidden directory.
To open it, return to the command line.

.. note::

  In the next example, the public key file is named ``id_rsa.pub``. It is
  perfectly safe to distribute this key to the world. There's also a file in
  the directory called ``id_rsa`` (note the missing ``.pub`` suffix). This file
  must be kept private and confidential.

.. code-block:: console

  $ cat ~/.ssh/id_rsa.pub
  ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDf/SMEHG3tLUDDVwbBAlZNJTrS24enBBwV
  dfkuTXDRBtSaeCt0ImuQfi6hNE9Kl0W6E0rnbu3itM7uqnNF3AcexHKHwUawjFPCRmEO8Dx+
  tOmQX0cbMUeCuMcV7wRMmCSjRY9p781X1wqGw6pYA4DeuFqtTzctmOsXMqsZig28USNYvXIc
  VkevWoJzZn4ftfMbnkkrGR6B7H4D8z3Pw98MisM4M2jN8/8GbTHFSKawNmY2Guy+hT9ndinX
  Rs0I5thvpDqLsVS1z1+9NGmJgM5x/LTyOjgO0DwNx5q/uU2BmImu8MQEA9qe5sZ0bddtpiL6
  xh5LyRJpv1RB+Yyc6x3b USERNAME@COMPUTERNAME

Open your `Github Profile`_ page, navigate to the SSH & GPG keys section. Copy
and paste the contents of the key (from ``ssh-rsa`` to ``USERNAME@COMPUTERNAME``)
into the box, and give the key a name.

You can have multiple public keys registered in GitHub, but this is really only
useful if you have multiple computers.

Using Git and Github
--------------------

.. todo::

  Actually finish this section.

Alternatives to the Command Line
--------------------------------

`SourceTree`_ is a fine alternative to using the command line. It will show
commit history, create commits and branches, push them to different repositories
and does all sorts of other nice things.

`GitHub Desktop`_ is also a good client, but one that is very specific to
GitHub. It offers many of the same features as SourceTree but isn't quite as
polished.

.. _`SourceTree`: https://www.sourcetreeapp.com/
.. _`GitHub`: https://github.com
.. _`SFU DHIL account`: https://github.com/sfu-dhil
.. _`Github Profile`: https://github.com/settings/profile
