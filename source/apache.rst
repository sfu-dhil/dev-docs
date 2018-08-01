.. _section-apache:

Apache
======

You should have working installs of MySQL and PHP at this point. The server
software to install is called Apache, but the name of the service is httpd.

Installation
------------

Install the basic Apache web server.

.. code-block:: console
  :linenos:

  $ brew install httpd
  $ sudo brew services start httpd

Line 1 will install the server and configure the defaults for Apache to listen
on port 8080. This is the same port that eXist-db will listen on and may
cause conflicts later. We will fix this by changing the Apache port later.

Line 2 will start the server. ``sudo`` will run the command as root, to ensure
that all permissions are set up correctly.

At this point you should be able to visit http://localhost:8080 in a web browser
and see that it works.

Configuration
-------------

The apache config file is /usr/local/etc/httpd/httpd.conf. Open it in a text
editor and make the following changes.

1. ``Listen 8080``
    Change this to ``Listen 80``.
2. ``User _www``
    Change ``_www`` to your user name. [#f1]_
3. ``Group _www``
    Change ``_www`` to ``staff``.

Uncomment these lines by removing the '#' character.

1. ``#ServerName www.example.com:8080``
    Also change **www.example.com:8080** to ``localhost``
2. ``#LoadModule rewrite_module lib/httpd/modules/mod_rewrite.so``
    Remove the leading ``#``. No other changes are necessary for this line.

Change where Apache will find documents to serve. Find the DocumentRoot
section of the configuration file. It will look like this:

.. code-block:: apacheconf

  DocumentRoot "/usr/local/var/www"
  <Directory "/usr/local/var/www">
      #
      # Possible values for the Options directive are "None", "All",
      # or any combination of:
      #   Indexes Includes FollowSymLinks SymLinksifOwnerMatch ExecCGI MultiViews
      #
      # Note that "MultiViews" must be named *explicitly* --- "Options All"
      # doesn't give it to you.
      #
      # The Options directive is both complicated and important.  Please see
      # http://httpd.apache.org/docs/2.4/mod/core.html#options
      # for more information.
      #
      Options Indexes FollowSymLinks

      #
      # AllowOverride controls what directives may be placed in .htaccess files.
      # It can be "All", "None", or any combination of the keywords:
      #   AllowOverride FileInfo AuthConfig Limit
      #
      AllowOverride None

      #
      # Controls who can get stuff from this server.
      #
      Require all granted
  </Directory>

Change it to the following. Changed lines are highlighted. Use your login in
place of ``username`` on lines 1 and 2.

.. code-block:: apacheconf
  :emphasize-lines: 1,2,15,16,23

  DocumentRoot "/Users/username/Sites"
  <Directory "/Users/username/Sites">
      #
      # Possible values for the Options directive are "None", "All",
      # or any combination of:
      #   Indexes Includes FollowSymLinks SymLinksifOwnerMatch ExecCGI MultiViews
      #
      # Note that "MultiViews" must be named *explicitly* --- "Options All"
      # doesn't give it to you.
      #
      # The Options directive is both complicated and important.  Please see
      # http://httpd.apache.org/docs/2.4/mod/core.html#options
      # for more information.
      #
      Options All FollowSymLinks Multiviews
      MultiviewsMatch Any

      #
      # AllowOverride controls what directives may be placed in .htaccess files.
      # It can be "All", "None", or any combination of the keywords:
      #   AllowOverride FileInfo AuthConfig Limit
      #
      AllowOverride All

      #
      # Controls who can get stuff from this server.
      #
      Require all granted
  </Directory>

These changes will configure Apache to listen on port 80, which is the usual
port for a web server. It will serve files from the ``Sites`` directory in your
home directory. Anything you place in that directory will be available to the
public.

Finally, create the Sites folder if it doesn't already exist and add some
content to it.

.. code-block:: console

  $ mkdir -p ~/Sites
  $ echo "<h1>Howdy do!</h1>" > ~/Sites/index.html

.. note::

  The tilde (``~``) character has special meaning: It represents your home
  directory. So ~/Sites is the Sites directory inside your home directory.

Once these changes are complete, you must restart Apache for them to take effect.

.. code-block:: console

  sudo apachectl restart

Now if you visit http://localhost you should see "Howdy do!" in the page.

Add PHP to Apache
-----------------

At this point Apache can serve static files like images or text to a browser.
It cannot generate a web page or run a program. To do that we must add the PHP
module to Apache.

Add this text, as it is, to the httpd.conf file.

.. code-block:: apacheconf
  :linenos:

  LoadModule php5_module /usr/local/opt/php@5.6/lib/httpd/modules/libphp5.so
  <FilesMatch .php$>
    SetHandler application/x-httpd-php
  </FilesMatch>

Line 1 loads the PHP 5.6 module, and lines 2-4 tell Apache to use it for all
files that have a ``.php`` suffix.

.. note::

  You can only have one PHP module active at a time. To use a different version
  of PHP you must change the ``LoadModule`` line and restart Apache.

Finally, test that Apache and PHP work together.

.. code-block:: console
  :linenos:

  $ sudo apachectl restart
  $ echo "<?php phpinfo();" > ~/Sites/info.php

Now you should be able to visit http://localhost/info.php to see some very
useful information about your PHP installation.

Troubleshooting
---------------

Check if Apache is running at all.

.. code-block:: console

  $ ps ax  | grep httpd
  34512   ??  Ss     0:00.08 /usr/local/opt/httpd/bin/httpd -D FOREGROUND
  34515   ??  S      0:00.00 /usr/local/opt/httpd/bin/httpd -D FOREGROUND

Read the apache error log. The most recent error output is at the end of the
log.

.. code-block:: console

  $ open -a Console.app /usr/local/var/log/httpd/error_log

Check the Apache configuration.

.. code-block:: console

  $ sudo apachectl -S
  VirtualHost configuration:
  ServerRoot: "/usr/local/opt/httpd"
  (and many more lines)

Start, stop, or restart the web server.

.. code-block:: console

  $ sudo apachectl start
  $ sudo apachectl stop
  $ sudo apachectl restart

.. rubric:: Footnotes

.. [#f1] Use the ``whoami`` command to find your username if you aren't sure.
