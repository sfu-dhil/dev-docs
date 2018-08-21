.. _section-php:

PHP
===

Mac OS X includes a version of PHP which is often out of date. Luckily Homebrew
makes installing another PHP very easy.

Installation
------------

The DHIL production server runs PHP 5.6, so we will install that. installing
other versions of PHP is possible and quite easy. See below for more information.

.. code-block:: console
  :linenos:

  $ brew install php@5.6
  $ brew link php@5.6 --force
  $ brew install pkg-config imagemagick
  $ pecl install imagick
  $ brew install composer

Line 1 installs PHP, and specifies version 5.6. The install command will print
a lot of information to the terminal which you can mostly ignore.

Line 2 puts symlinks in place to make PHP work from the command line.

We will need a few PHP extensions to get all the projects working. Line 3
installs a package configuration manager (pkg-config) and an image manipulation
library (imagemagick).

Line 4 installs the PHP extension that uses imagemagick. It uses PHP's package
manager to download and configure it. The command will ask for a path to the
imagemagick library. Press enter to accept the default (autodetect) which
should find the library.

.. todo::

  Is pecl something that needs to be installed separately or is it included when
  PHP is installed? I wasn't able to tell. --Erik

Line 5 installs Composer, a different kind of PHP package manager.

Configuring
-----------

The pecl install step (line 4 above) will automatically configure PHP to find
the imagick extension. Other configuration options are available in
``/usr/local/etc/php/5.6/php.ini``

You must set the timezone in the ``php.ini`` file. Open the file in your text
editor, and find the ``[Date]`` section.

.. code-block:: ini
  :linenos:

  [Date]
  ; Defines the default timezone used by the date functions
  ; http://php.net/date.timezone
  ;date.timezone =

Uncomment line 4 by removing the semicolon at the start of the line, then add
"America/Vancouver" to the end. The result should be

.. code-block:: ini
  :linenos:

  [Date]
  ; Defines the default timezone used by the date functions
  ; http://php.net/date.timezone
  date.timezone = America/Vancouver

Other recommended settings are:

 * ``memory_limit = 128M`` Change this to 256M or higher.

 * ``html_errors = On`` Change this to Off.

 * ``post_max_size = 8M`` Change this to 64M or higher.

 * ``upload_max_filesize = 2M`` Change this to 60M or higher. It should be less than
   the value of ``post_max_size``.

Test PHP
--------

PHP includes a few command line tools. These sample commands should all work and
print useful things. If you try these commands and get an error message, something
has gone wrong in the installation.

.. code-block:: console

  $ php --version
  PHP 5.6.36 (cli) (built: Jun 22 2018 00:08:38)
  Copyright (c) 1997-2016 The PHP Group
  Zend Engine v2.6.0, Copyright (c) 1998-2016 Zend Technologies
      with Zend OPcache v7.0.6-dev, Copyright (c) 1999-2016, by Zend Technologies

  [14:02:03][michael@sophie devenv]$ php -m
  [PHP Modules]
  bcmath
  bz2
  calendar
  Core
  (and many many more)

Other PHP Versions
------------------

As mentioned above, it's possible and even easy to install and manage multiple
versions of PHP via Homebrew.

.. code-block:: console
  :linenos:

  $ brew unlink php@5.6
  $ brew install php@7.2
  $ brew link php@7.2 --force

Line 1 makes PHP 5.6 inactive. Line 2 installs a new version of PHP, and line 3
makes the new version active again. Each new version of PHP will require you
to install the ``pecl`` extensions. You should not need to reinstall
imagemagick or composer.

.. code-block:: console

  $ pecl install imagick

After installing the extensions, you will also need to configure the new version
of PHP exactly as you did above. Replace ``5.6`` with the version of PHP you
installed (``7.2`` in these examples).

To switch from one version of PHP to another you must unlink the current version
and then link the new one. For example

.. code-block:: console

  $ brew unlink php@7.2
  $ brew link php@5.6
