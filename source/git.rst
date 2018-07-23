Git
===

All of the DHIL projects use Git for version control.

Installation
------------

Mac OS X provides a ``git`` command as part of the XCode suite. It is usually
out of date, so it's best to install Git from Homebrew.

.. code-block:: shell

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
questions. Press enter to accept the defaults.

.. code-block:: ssh

  $ ssh-keygen
  Generating public/private rsa key pair.
  Enter file in which to save the key (/Users/mjoyce/.ssh/id_rsa):
  Created directory '/Users/mjoyce/.ssh'.
  Enter passphrase (empty for no passphrase):
  Enter same passphrase again:
  Your identification has been saved in /Users/mjoyce/.ssh/id_rsa.
  Your public key has been saved in /Users/mjoyce/.ssh/id_rsa.pub.
  The key fingerprint is:
  SHA256:tOqBch6x5Ls46/KBmGJFMipSl0z5Th7DR723IQbI7Ec mjoyce@d207-023-216-204.wireless.sfu.ca
  The key's randomart image is:
  +---[RSA 2048]----+
  |    .+ . .       |
  |   o..+ E .      |
  | o..++ o.. .     |
  |..+.  B.o.+ o    |
  |+  .o+ =S. o o   |
  |+o.o +o.    .    |
  |=.o * o          |
  |+ .* + .         |
  | +=o+..          |
  +----[SHA256]-----+
  $ ls ~/.ssh/
  id_rsa          id_rsa.pub

Success.

`SourceTree`_ is a fine alternative to using the command line.

.. todo::

  Actually write this.

.. _`SourceTree`: https://www.sourcetreeapp.com/
