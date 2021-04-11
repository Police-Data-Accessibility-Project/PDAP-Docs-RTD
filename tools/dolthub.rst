==================
Dolthub - Database
==================
..

    *This is how we keep our data stream safe and accurate.*

Getting Started with Dolthub
============================
The instructions `here
<https://docs.dolthub.com/dolthub/getting-started>`_ are excellent. Here’s our `dolt org <https://www.dolthub.com/organizations/pdap>`_.

Generally, Dolt is used to make changes to PDAP. Anyone can create a Pull Request to be merged into the database via the SQL UI at DoltHub, command line, `SQL editor integration <https://github.com/dolthub/docs/blob/gitbook-dev/content/integrations/sql-editors.md>`_, or Python.

Supported statements
--------------------

https://docs.dolthub.com/interfaces/sql/sql-support/supported-statements
These are limited, so dolt is not great for managing a bunch of schemas.

Useful statements
-----------------

Spreadsheets
^^^^^^^^^^^^

Dolt has a `guide here <https://docs.dolthub.com/integrations/spreadsheets>`_ for spreadsheets generally, including ODBC setup.
Using the CLI, first ensure you’ve initialized the repo you’d like to pull from. Export a table like this:

:: 

    dolt table export source_types > source_types.csv
    dolt table export <table_name> > <file_name>

Add new files

:: 

    dolt table import -c --pk <primary_key> <table_name> <file_name>
    dolt table import -c --pk name format_types format_types.csv

Use `dolt add .` to start tracking all new files in the directory.

Submit a new dataset
====================

DoltHub CLI
-----------

1. `Install Dolt <https://docs.dolthub.com/getting-started/installation>`_.

2. Run these commands to init the project locally

::

    dolt init
    dolt clone pdap/datasets && cd datasets
    dolt table export datasets > datasets.csv

3. Open the datasets.csv file, make changes, and save.
    URL must be unique. Some fields are required.

4. Run the following commands

::

    dolt branch <branch name e.g. add-georgia-counties>
    dolt checkout <your branch>
    dolt table import -u datasets datasets.csv


*There are often errors at this stage, typically related to non-unique URLs or missing fields which must be present.*

5. Run this command

::

    dolt add .

*The “.” is important.*

6. Push the commit

::

    dolt commit -m “<message e.g. added 5 counties>”
    dolt push --set-upstream origin <your branch>

7. Head to https://www.dolthub.com/repositories/pdap/datasets/
8. Create a `Pull Request <https://docs.dolthub.com/dolthub/getting-started#pull-requests>`_ to merge your dataset into master.
