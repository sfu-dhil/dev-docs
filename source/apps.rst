.. _section-apps:

Installing a DHIL Symfony App
=============================

Each project should have its own documentation, including instructions for
`getting the source code`_ from GitHub. We also publish that documentation on
the `project website`_. Those instructions are summarized here for convenience.

The following instructions use the Database of Canada's Early Women Writers
(ceww) project as an example. You may need to change ``ceww`` to something
else for a different project. [#fc]_

#. Log in to Github's website and create a fork of the project. There's a "Fork"
   button in the project's repository page for this.

#. Clone your fork to your computer. The code below will fetch the submodules
   and set them up correctly.

    .. code-block:: console

      $ git clone --recursive git@github.com:USERNAME/ceww.git

#. Create a database and database user in mysql. These are sample commands.

    .. code-block:: console

      $ mysql
      mysql> create user ceww@localhost;
      mysql> create database ceww;
      mysql> grant all on ceww.* to ceww@localhost;
      mysql> set password for ceww@localhost = password('hotpockets');

   Composer will ask for the database name, database user name, and database
   password in the next step.

#. Install the composer dependencies. These are PHP packages and libraries that
   provide functionality like database connectivity and logging and many other
   good things.

    .. code-block:: console

      $ composer install

   Sometimes Composer runs out of memory. If that happens, try this alternate.

    .. code-block:: console

      $ php -d memory_limit=-1 `which composer` install

#. Update file permissions if needed. If you followed the directions in the
   :ref:`section-apache` section this should not be necessary.

   The user running the web server must be able to write to `var/cache/*` and
   `var/logs/*` and `var/sessions/*`. The symfony docs provide `recommended commands`_
   depending on your OS.

   And if you're working on an application that takes file uploads, you may
   need to give additional permissions to the file upload directory. Check the
   documentation.

#. Install the assets.

    .. code-block:: console

      $ ./bin/console ckeditor:install
      $ ./bin/console assets:install --symlink

#. Install the bower dependencies. These are javascript and CSS packages like
   Bootstrap. [#fn1]_

    .. code-block:: console

     $ bower install

#. Load the schema into the database. This is done with the Symfony console.

    .. code-block:: console

      $ ./bin/console doctrine:schema:update --force

#. At this point, the web interface should be up and running, and you should be
   able to load some pages. The URL for the app should be something like
   http://localhost/ceww/web/app_dev.php

   .. note::

     If you're a pleb without access to port 80: http://localhost:8080/ceww/web/app_dev.php

#. Create an application user with full admin privileges. This is also done
   with the Symfony console.

    .. code-block:: console

      $ ./bin/console fos:user:create admin@example.com
      $ ./bin/console fos:user:promote admin@example.com ROLE_ADMIN

   You should now be able to login to the app by following the Login link
   in the top right corner of any application page.

#. Build the documentation.

    .. code-block:: console

      $ cd docs
      $ make html

#. Hack and slash your way through the code. The source code for symfony apps is
   very organized. Application configuration is in ``app/config``. Actual
   runnable source code is in ``src/AppBundle``. Tests for the code lives in
   ``src/AppBundle/Tests``. There are also some reusable bundles in
   ``src/Nines`` which should have come from a git submodule.

#. Run some tests. The composer dependencies include PHPUnit for testing. The
   source code includes all the tests, and should always be runnable.

    .. code-block:: console

      $ ./vendor/bin/phpunit
      PHPUnit 5.7.27 by Sebastian Bergmann and contributors.

      ...............................................................  63 / 434 ( 14%)
      ............................................................... 126 / 434 ( 29%)
      ............................................................... 189 / 434 ( 43%)
      ............................................................... 252 / 434 ( 58%)
      ............................................................... 315 / 434 ( 72%)
      ............................................................... 378 / 434 ( 87%)
      ........................................................        434 / 434 (100%)

      Time: 1.7 minutes, Memory: 354.75MB

      OK (434 tests, 775 assertions)

   The git repositories contain a default config file called
   ``phpunit.xml.dist``. If you want to customize the configuration, copy the file
   to ``phpunit.xml`` and configure as needed. Git will ignore the ``phpunit.xml``
   file.

.. rubric:: Footnotes

.. [#fc]

  The repository name for the DoCEWW project is ceww for historical reasons. It
  should be doceww to be consistent with the proper name of the project. The
  name is consistent in the canonical URL: https://dhil.lib.sfu.ca/doceww

.. [#fn1]

  `Bower`_ is an old and deprecated system, that will probably eventually be
  unsupported. We should begin converting the apps to use `Yarn`_ instead of
  Bower as soon as possible.

.. _`getting the source code`: https://github.com/sfu-dhil/ceww-docs/blob/master/source/install.rst
.. _`project website`: https://dhil.lib.sfu.ca/doceww/docs/html/install.html
.. _`recommended commands`: http://symfony.com/doc/current/setup/file_permissions.html
.. _`Bower`: https://bower.io/
.. _`Yarn`: https://yarnpkg.com/en/
