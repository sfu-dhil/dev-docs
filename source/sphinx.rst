Installing and Running Sphinx
=============================

`Sphinx`_ is our documentation system.

Install
-------

1. Install homebrew python

.. code-block:: console

  $ brew install python

That may take some time.

2. Use python's package manager to install Sphinx

.. code-block:: console

  $ pip install Sphinx

.. _Sphinx: http://www.sphinx-doc.org/en/master/

Usage
-----

The documentation repositories are pre-configured for sphinx installed as above
and include a build setup. Generate the HTML documentation like so:

.. code-block:: console

  $ make html

The documentation will then be available in ``build/html/index.html``. Some
projects have been configured to output the documentation to the ``web/docs/``
directory.

.. seealso::

  For more information, check out the `First Steps with Sphinx`_ documentation.

.. note::
  If you are using the `Atom`_ editor with the `ReStructuredText Preview package`_,
  you may also need to install `pandoc`_. The extension uses it, instead of Sphinx,
  to create previews.

  .. code-block:: console

    $ brew install pandoc

.. _`Atom`: https://atom.io/
.. _`ReStructuredText Preview package`: https://atom.io/packages/rst-preview
.. _`pandoc`: https://pandoc.org/
.. _`First Steps with Sphinx`: http://www.sphinx-doc.org/en/stable/tutorial.html
