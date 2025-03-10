.. image:: https://github.com/rcgsheffield/sheffield_hpc/actions/workflows/static.yml/badge.svg
    :target: https://github.com/rcgsheffield/sheffield_hpc/actions/workflows/static.yml

Sheffield High Performance Computing Documentation
==================================================

This is the source for the documentation of Stanage and Bessemer, The University of Sheffield's High Performance Computing clusters.

It is written in the reStructuredText_ (*rst*) format and the Sphinx_ tool is used to convert this to a set of HTML pages.

For a guide on the rst file format see `this <http://thomas-cokelaer.info/tutorials/sphinx/rest_syntax.html>`_ document.

Rendered Documentation
----------------------
`This website <https://docs.hpc.shef.ac.uk/en/latest/>`_  is currently automatically built from this repository:
each push to the ``master`` branch causes a `GitHub Actions <https://github.com/rcgsheffield/sheffield_hpc/actions/>`__ workflow to build and serve the documentation via GitHub Pages.

How to Contribute
-----------------
To contribute to this documentation, first you have to fork it on GitHub and clone it to your machine,
see `Fork a Repo <https://help.github.com/articles/fork-a-repo/>`_ for the GitHub documentation on this process.

Once you have the git repository locally on your computer,
you will need to ensure you have Python and the Tox_ build tool installed.

Once you have made your changes and updated your Fork on GitHub you will need to `Open a Pull Request <https://help.github.com/articles/using-pull-requests/>`_.
All changes to the repository should be made through Pull Requests, including those made by the people with direct push access.

Building the documentation on a local Windows machine
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Install **Python 3** on your machine by downloading and running the Miniconda_ installer:

   * Install for *just you*;
   * Install to the default location (e.g. ``C:\Users\myusername\Miniconda3``);
   * Do **not** *add Anaconda to your PATH environment variable*;
   * Do **not** *register Anaconda as your default Python 3*.

#. Click *Start* -> *Anaconda3 (64-bit)* -> *Anaconda Prompt* to open a terminal window.

#. Create a new *conda environment* for building the documentation by running the following from this window: ::

    conda create --name sheffield_hpc python=3.10
    conda activate sheffield_hpc	# . activate sheffield_hpc on older versions of conda
    pip install tox

#. To build the HTML documentation run: ::

    tox -e py310

The output should be written to ``./_build/html``.

Building the documentation on a local Linux machine
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Ensure one of Python 3.10 or 3.11 are installed.
#. Ensure the Tox_ build tool is installed and can be used/seen by your chosen Python interpreter.

#. Run Tox to create an isolated Python virtual environment then build documentation: ::

     tox -e py310
     tox -e py311

The output should be written to ``./_build/html``.

Building the documentation on a local Mac machine
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. Ensure Python 3 is installed.  If you do not already have a python distribution installed, we recommend you install Miniconda_.
#. Install the Python packages needed to build the HTML documentation.  If you are using (mini)conda create a new *conda environment* for building the documentation by running: ::

    export PATH=${HOME}/miniconda3/bin:$PATH
    conda create -n sheffield_hpc python=3.10
    conda activate sheffield_hpc	# . activate sheffield_hpc on older versions of conda
    pip install tox

#. To build the HTML documentation run::

    tox -e py310

The output should be written to ``./_build/html``.

Check external links
^^^^^^^^^^^^^^^^^^^^

Do this with: ::

   tox -e py310-linkcheck

Continuous build and serve
^^^^^^^^^^^^^^^^^^^^^^^^^^

Build and serve the site and automatically rebuild when source files change: ::

   tox -e py310-livehtml

Testing the building of the documentation
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The validity of the reStructuredText in this repo and the ability to convert that to HTML with Sphinx can be tested in three ways:

* Locally by contributors when they run e.g. ``tox -e py310-livehtml``
* By a `GitHub Actions <https://github.com/rcgsheffield/sheffield_hpc/actions/>`__ Workflow each time a contributor creates or updates a Pull Request.
* By a `GitHub Actions <https://github.com/rcgsheffield/sheffield_hpc/actions>`__) Workflow on each push to the ``master`` branch.

Important files / folders
^^^^^^^^^^^^^^^^^^^^^^^^^

* ``conf.py`` - Sphinx configuration file.
* ``requirements.txt`` - Main requirements file.
* ``setuptoolsrequirements.txt`` - Initial requirements file set in order to first pin setuptools to version 57.5.0 to `retain support for the current theme <https://github.com/ryan-roemer/sphinx-bootstrap-theme/issues/216>`__.
* ``tox.ini`` - Tox configuration file.
* ``Makefile`` 
* ``global.rst`` - A globally included file (goes into all pages) which is excluded from direct building using exclude_patterns in ``conf.py``.
* ``referenceinfo/imports`` - sub-folder tree of files to be included by not directly built. This is excluded from direct building using exclude_patterns in ``conf.py``.
* ``_static/css/custom.css`` - custom CSS overrides for the theme.
* ``.github/workflows`` - GitHub Actions workflows for pull requests, pushes to ``master`` and link checking.

Making or using imported files from the ``referenceinfo/imports`` area
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

This area is intended to be used to contain .rst files which we wish to use in more than one location which can be imported. The general method for making use of imported files is as follows:

* Make a new file to be imported within a sensible subdirectory within this area e.g. ``/referenceinfo/imports/software/mysoftware/import.rst``
* Import your new file into your main page with: ``.. include:: /referenceinfo/imports/software/mysoftware/import.rst``
* Build the documentation and ensure that hierarchical elements are correct e.g. titles within toctrees must be correct to fit in the parent document properly.
* Add a comment within the import / parent document to explain why the import is necessary if it is not immediately obvious.

(Re)-generating PNG images from Mermaid.js diagram definitions
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Some diagrams, such as ``images/hpcgateway-sequence-diag.png`` 
have been generated with `mermaid-cli <https://github.com/mermaid-js/mermaid-cli>`__ 
and Mermaid.js diagram definitions such as ``images/hpcgateway-sequence-diag.mmd``.
How to install mermaid-cli and regenerate one of these diagrams: ::

  yarn add @mermaid-js/mermaid-cli 
  ./node_modules/.bin/mmdc -i images/hpcgateway-sequence-diag.mmd -o images/hpcgateway-sequence-diag.png

.. _Sphinx: https://www.sphinx-doc.org/en/master/
.. _reStructuredText: https://docutils.sourceforge.io/rst.html
.. _Miniconda: https://conda.io/miniconda.html
.. _Tox: https://tox.readthedocs.io/en/latest/
