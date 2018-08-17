.. _exist-label:

eXistDb & oXygen
================

They really do like their silly capitalization don't they?

`eXistDb`_ is a XML database. It's useful for storing documents and
searching or processing them, especially if they don't really fit in a
traditional SQL database. The Wilde Trials and any TEI project will use
eXist as the storage layer. It is open-source and freely available.

`oXygen`_ is an XML editor with built-in schemas for TEI, XHTML, and other document
formats. It also supports XSLT and XQuery transformations via different engines
and validation via RelaxNG, Schematron, and loads of other schemas. It isn't
open-source, nor is it free. But the library has a site license so shouldn't
cost the DHIL anything to use.

Installing eXistDb
------------------

The eXistDb developers distribute their software via `BinTray`_. The page lists
a number of release versions. Navigate to the most recent stable release [#f1]_
and download the ``-setup-VERSION.jar``. This will give you an application that
is easy to configure and run.

Once the .jar file is finished downloading, double click on it and follow the
installation instructions. The application will be installed in
``/Applications/eXist-db`` because developers aren't ever consistent with
naming things.

To run the Wilde Trails application, you must make one change to an eXistDb
configuration file. Open ``/Applications/eXist-db/conf.xml`` in a text editor
and look for this element.

  .. code-block:: xml
    :linenos:
    :lineno-start: 773
    :caption: This line may be in a different position for other versions of eXistDb.

    <xquery enable-java-binding="no" disable-deprecated-functions="no"
            enable-query-rewriting="yes" backwardCompatible="no"
            enforce-index-use="always"
            raise-error-on-failed-retrieval="no">

Change ``enable-java-binding="no"`` to ``enable-java-binding="yes"``, save the
file, and restart eXistDb if you need to.

.. note::

  eXistDb listens on port 8080 by default. If you have installed
  :ref:`Apache <section-apache>` following the directions there it may also
  be listening on port 8080. Only one program can listen on a port at a time, so
  either stop Apache (``brew services stop apache``) or change Apache or eXistDb
  to listen on another port.

  To change eXistDb's port, open ``/Applications/eXist-db/tools/jetty/etc/jetty-http.xml``
  and change the port number on line 38. In the examples below, line breaks and
  indentation have beeb added to improve readability.

  .. code-block:: xml
    :emphasize-lines: 4

    <Set name="port">
      <Property name="jetty.http.port" deprecated="jetty.port">
        <Default>
          <SystemProperty name="jetty.port" default="8080"/>
        </Default>
      </Property>
    </Set>

Using eXistDb
-------------

Most access to the eXistDb service is through a web interface. If you visit

* accessing the database
* monitor
* exide
* installing an app - eg. wilde data
* symlinking an app - eg. wilde app

Installing & Using oXygen
-------------------------

#. download
#. license
#. install
#. connect to exist
#. create a project

.. rubric:: Footnotes

.. [#f1]

  The preview releases are usually named with a -RC suffix, like 5.0.0-RC1. They
  *should* work fine, but may cause compatibility problems. Stick to the most
  recent, non-preview version.

.. _eXistDb: http://exist-db.org/exist/apps/homepage/index.html
.. _oXygen: https://www.oxygenxml.com/
.. _BinTray: https://bintray.com/existdb/releases/exist
