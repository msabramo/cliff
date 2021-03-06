===============
 List Commands
===============

One of the most common patterns with command line programs is the need
to print lists of data. cliff provides a base class for commands of
this type so that they only need to prepare the data, and the user can
choose from one of several output formatter plugins to see the list of
data in their preferred format.

Lister
======

The :class:`cliff.lister.Lister` base class API extends
:class:`Command` to add a :func:`get_data` method. Subclasses should
provide a :func:`get_data` implementation that returns a two member
tuple containing a tuple with the names of the columns in the dataset
and an iterable that will yield the data to be output. See the
description of :ref:`the files command in the demoapp <demoapp-list>`
for details.

List Output Formatters
======================

cliff is delivered with two output formatters for list
commands. :class:`Lister` adds a command line switch to let the user
specify the formatter they want, so you don't have to do any extra
work in your application.

csv
---

The ``csv`` formatter produces a comma-separated-values document as
output. CSV data can be imported into a database or spreadsheet for
further manipulation.

::
    
    (.venv)$ cliffdemo files -f csv
    "Name","Size"
    "build",136
    "cliffdemo.log",2690
    "Makefile",5569
    "source",408

html
----

The ``html`` formatter uses tablib_ to produce HTML output as a table.

::

  (.venv)$ cliffdemo files -f html
  <table>
  <thead>
  <tr><th>Name</th>
  <th>Size</th></tr>
  </thead>
  <tr><td>build</td>
  <td>136</td></tr>
  <tr><td>cliffdemo.log</td>
  <td>3252</td></tr>
  <tr><td>Makefile</td>
  <td>5569</td></tr>
  <tr><td>requirements.txt</td>
  <td>33</td></tr>
  <tr><td>source</td>
  <td>782</td></tr>
  </table>

json
----

The ``json`` formatter uses tablib_ to produce JSON output.

::
    
  (.venv)$ cliffdemo files -f json
  [{"Name": "build", "Size": 136}, {"Name": "cliffdemo.log", "Size":
  3461}, {"Name": "Makefile", "Size": 5569}, {"Name":
  "requirements.txt", "Size": 33}, {"Name": "source", "Size": 782}]

table
-----

The ``table`` formatter uses PrettyTable_ to produce output formatted
for human consumption.

.. _PrettyTable: http://code.google.com/p/prettytable/

::
    
    (.venv)$ cliffdemo files
    +---------------+------+
    |      Name     | Size |
    +---------------+------+
    | build         |  136 |
    | cliffdemo.log | 2546 |
    | Makefile      | 5569 |
    | source        |  408 |
    +---------------+------+

yaml
----

The ``yaml`` formatter uses tablib_ to produce YAML output as a
sequence of mappings.

::

  (.venv)$ cliffdemo files -f yaml
  - {Name: build, Size: 136}
  - {Name: cliffdemo.log, Size: 3043}
  - {Name: Makefile, Size: 5569}
  - {Name: requirements.txt, Size: 33}
  - {Name: source, Size: 816}


Creating Your Own Formatter
---------------------------

If the standard formatters do not meet your needs, you can bundle
another formatter with your program by subclassing from
:class:`cliff.formatters.base.ListFormatter` and registering the
plugin in the ``cliff.formatter.list`` namespace.


.. _tablib: https://github.com/kennethreitz/tablib
