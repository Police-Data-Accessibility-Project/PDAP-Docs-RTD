=============================
Read the Docs - Documentation
=============================

-----------------------------------------------------------
A guide to mastering RST and helping us with documentation!
-----------------------------------------------------------

:subheader:`Let's Begin!`

Introduction
============

Our documentation is stored in `Github here <https://github.com/Police-Data-Accessibility-Project/PDAP-Docs>`_ and parsed automatically by `ReadtheDocs <https://readthedocs.org>`_.

The main frameworks behind this technology are Sphinx and ReStructed Tex (RST). RST is very similar to markdown, but with a slightly different syntax and much more versatile, including the ability to define your own custom roles for text!

The PDAP is always looking for volunteers to help us, and if your expertise is in documentation, then this guide is for you! Here we will walk you through how to fork the repo to make changes, provide a cheatsheet of the commonly used syntax at your disposal, and show you how to send a pull request so we can take a look and accept your edits!

Pre-Requisites
==============
You will need to have Git (or GitHub Desktop), Python 3.7+, pip already installed. The repo also provides a ``requirements.txt`` to install packages unique to the repo, such as Sphinx, and our docs theme.


Forking & Working Locally
=========================

1. use your preferred version of Git to clone and fork the repo to your machine.
2. Next, open your preferred terminal and ``cd`` into the cloned repo directory
3. Run ``pip install -r requirements.txt`` to download our packages and dependencies for this project
4. Run ``.\make html`` to build a local version of the docs in the `_build` dir. You can open the ``/_build/html/index.html`` file in your browser to visualize any changes!
5. Anytime you do make changes, be sure to re-run the ``.\make html`` command and then refresh the page! Take note of any warnings or errors during the build process.


Syntax Cheatsheet
=================

Titles
-------
**Note**: due to the way RST parses things, I cannot put a title here or it will throw a warning. An example of a title, subtitle and subheader are shown at the top of this page.

**Note 2**: The - / = signs MUST match the length of the word or phrase encapsulated by the symbols. If the phrase is 10 characters long, you must have 10 - or = above and below it exactly or RST will throw an error.

**Note 3**: The ``:subheader:`` role is a custom role made for our docs to get a slightly smaller variant of the subtitle

::

    =====
    Title
    =====

    --------
    Subtitle
    --------

    :subheader:`SubHeader`


Section Headers
---------------

Section headers are similar to titles except you only have a line under the text. For the most part, you will never use Parts or Chapters, just use Sections and Subsections.

#####
Parts
#####

********
Chapters
********

Sections
========

Subsections
-----------


::

    #####
    Parts
    #####

    ********
    Chapters
    ********

    Sections
    ========

    Subsections
    -----------

Formatting
----------
RST has quite a few built in formatters that are quite similar to markdown:

**bold**

*italic*

``literal``


- List 1
- List 2
    - Nested List 3



1. Numbered Item 1
2. Numbered Item 2
#. AutoNumbered Item 3
#. AutoNumbered Item 4 (useful if you add another step, you don't need to renumber the whole list)

:: 

    **bold**

    *italic*

    ``literal``

    - List 1
    - List 2
        - Nested List 3

    1. Numbered Item 1
    2. Numbered Item 2
    #. AutoNumbered Item 3
    #. AutoNumbered Item 4 (useful if you add another step, you don't need to renumber the whole list)

**NOTE**: You may notice the ``::`` followed by an empty line. That is how you do a literal block, or a code block. It allows you to paste RST without the parser actually transforming the text. It is important that you put the ``::`` and an empty line directly after it, or you will get an error. Also, be sure to indent everything in the block.

Links and files
---------------
You may want to link to an another page in our docs, or to another website entirely. Maybe you want to display an image or parse a csv:

`Link to website <https://pdap.io>`_

:doc:`Link to doc </tools/readthedocs/>`

.. csv-table:: Example Table
   :file: example.csv
   :widths: 33, 33, 33
   :header-rows: 1

.. image:: ../_static/images/smiley.png
   :width: 200

::

    `Link to website <https://pdap.io>`_

    :doc:`Link to doc </tools/readthedocs/>`

    .. csv-table:: Example Table
        :file: example
        :widths: 33, 33, 33
        :header-rows: 1

    .. image:: ../_static/images/smiley.png
        :width: 200




PDAP Custom Formatting
----------------------
The nice thing about RST and Sphinx is the extensibility. You can add custom css to ``_static\css\s5defs-roles.css``. Then, navigate to the ``conf.py`` in the root of the project. At the bottom you will see something like this:


.. code-block:: python

    rst_prolog = """
    .. role:: highlight-red
    .. role:: highlight-orange
    .. role:: highlight-yellow
    .. role:: highlight-green
    .. role:: subheader
    .. role:: shell(code)
    :language: shell
    :class: highlight
    """

Here is where we can setup custom roles / classes. Make sure the name of the role in the :shell:`conf.py` matches the name of the class in :shell:`_static\css\s5defs-roles.css`.

We've already seen one example, the subheader, above. Here is another few examples of calling the custom roles:

:highlight-red:`This text is red.`
:highlight-orange:`This text is orange.`
:highlight-yellow:`This text is yellow.`
:highlight-green:`This text is green.`
:subheader:`This is a subheader`
:shell:`This is inline-code`

::

    :highlight-red:`This text is red.`
    :highlight-orange:`This text is orange.`
    :highlight-yellow:`This text is yellow.`
    :highlight-green:`This text is green.`
    :subheader:`This is a subheader`
    :shell:`This is inline-code`


Indexing
--------
This is an important piece if you create new files or subfolders.
Sphinx uses the ``.. toctree`` directive to populate the sidebar for the entire website. It is manually created, so if you add anything at the root level, you will need to modify the toctree directive in ``index.rst`` to tell it where the new folder is. It is also good practice to create an ``index.rst`` in each sub-directory, and you can use globbing to then auto discover files in the sub-directories, like so:

::

    .. toctree::
        :glob:
        :caption: SubDirectory Name (this is what shows on the sidebar)
        :maxdepth: 1
        
        *

Feel free to browse the directories and files and copy the ``..toctree`` directives from there when you make new files. You also may have to completely delete everything in ``_build`` when you make a change to the toctree so when you run the ``make`` command, it builds fresh.

More Information
----------------

Still looking for more? This isn't a full list, but should help you with most of the markup on our documentation. Here are some additional resources on the rst markup:

- https://github.com/ralsina/rst-cheatsheet/blob/master/rst-cheatsheet.rst
- https://sublime-and-sphinx-guide.readthedocs.io/en/latest/index.html
- https://documentation.help/Sphinx/toctree.html


Pull Request
============
Hopefully this is a good enough beginner guide to helping you make changes on the PDAP docs! Once you finalize your changes, make a pull request and someone will look over the changes and possibly pull it into our live site!