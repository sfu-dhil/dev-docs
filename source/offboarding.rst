.. _section-offboarding:

Offboarding
===========

This page contains instructions on how to remove the Digital Humanities Innovation Lab's 
developing environment from your computer. The current instructions are only for Mac computers.
Tools are presented in the order they appear in the developing environment set-up guide.

Xcode Command Line Tools
------------------------

If you installed the XCode command line tools following the instructions in this guide, you can
uninstall it by removing the ``/Library/Developer/CommandLineTools`` directory. The command looks like

.. code-block:: console

  $ sudo rm -rf /Library/Developer/CommandLineTools

You will need to run this command using sudo, which will prompt you for your administrator password.

Homebrew
--------

You can uninstall Homebrew using the uninstall command that is printed on the `Homebrew FAQs`_ page. 
It looks like

.. code-block:: console

  $ ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"

That command will attempt to uninstall and remove all homebrew pacakages. If it does not completely 
remove all packages, you may need to run the command using sudo, which will prompt you for your 
administrator password.

.. _Homebrew FAQs: https://docs.brew.sh/FAQ

Sphinx and Python
-----------------

As python and Sphinx are installed using Homebrew, if you remove all Homebrew packages and uninstall 
Homebrew, python and Sphinx will also be uninstalled. However, if you wish to keep Homebrew and only 
remove python and Sphinx, you can do so using the following command

.. code-block:: console

  $ brew uninstall python --force

``--force`` is required to ensure all Homebrew versions of python are uninstalled. Otherwise, 
Homebrew will continue to install the latest version of python (or any package) that it knows 
about when you update all packages using ``brew upgrade``.

As Sphinx is a python package, if you wish you keep Homebrew and the Homebrew installation of 
Python but remove Sphinx, you can do so using python's package manager. The command to do so is

.. code-block:: console

  $ pip3 uninstall Sphinx

This will remove Sphinx but will not affect Homebrew or your Homebrew installation of python.

MySQL
-----

.. todo::

  Add instructions on how to uninstall MySQL.
  I do not know how to do this propperly and have had trouble with it in the past, so I don't want
  to write out incorrect instructions. --Erik

PHP
---

The set-up guide for PHP includes the PHP installation as well as the installation of a number of 
PHP extensions. PHP and the extensions (pkg_config, imagemagick, and composer) can be uninstalled 
using Hombrew. To remove all four packages, run

.. code-block:: console

  $ brew uninstall php@5.6 pkg_config imagemagick composer --force

This will also remove all configuration files edited when installing :ref:`section-php`.

.. todo::

  Does PHP need to be unlinked in Homebrew before uninstalling? If so, include as a step. Also, 
  will running ``brew uninstall php --force`` remove all versions of PHP installed? If so, is 
  that preferable to run? --Erik

.. todo::

  Add information about pecl and imagick as I don't think I was able to get them to work on my 
  computer. --Erik

Node and Node Tools
-------------------

.. todo::

  Include node and npm uninstall instructions once installation instructions are complete.

Apache
------

Apache was installed using Homebrew so you can use Homebrew to remove it. The command is 

.. code-block:: console

  $ brew uninstall httpd --force

This will also remove all configuration files edited when installing :ref:`section-apache`.

Git
---

Git was installed using Homebrew so you can use Homebrew to remove it. The command is 

.. code-block:: console

  $ brew uninstall git --force

DHIL Symfony Apps
-----------------

If you have been following this guide, all Symfony apps will be held within the 
``~/Sites`` directory. To uninstall the app from your computer you will need to:

  - Delete the app from the ``~/Sites`` directory
  - Remove the database and user from MySQL.

To remove the app from the command line, enter the following command where ``app_name``
is the name of the app directory.

.. code-block:: console

  $ rm -rf ~/Sites/app_name

If you are completely removing MySQL, you will not need delete individual databases as 
they will be removed when MySQL is deleted. If you would like to remove the databse for 
a single app, complete the following steps.

.. todo::

  Add instructions to remove individual database and user.
