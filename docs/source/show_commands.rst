===============
 Show Commands
===============

One of the most common patterns with command line programs is the need
to print properties of objects. cliff provides a base class for
commands of this type so that they only need to prepare the data, and
the user can choose from one of several output formatter plugins to
see the data in their preferred format.

ShowOne
=======

The :class:`cliff.show.ShowOne` base class API extends
:class:`Command` to add a :func:`get_data` method. Subclasses should
provide a :func:`get_data` implementation that returns a two member
tuple containing a tuple with the names of the columns in the dataset
and an iterable that contains the data values associated with those
names. See the description of :ref:`the file command in the demoapp
<demoapp-show>` for details.

Show Output Formatters
======================

cliff is delivered with output formatters for show
commands. :class:`ShowOne` adds a command line switch to let the user
specify the formatter they want, so you don't have to do any extra
work in your application.

PrettyTable
-----------

The ``PrettyTable`` formatter uses PrettyTable_ to produce output
formatted for human consumption.

.. _PrettyTable: http://code.google.com/p/prettytable/

::

    (.venv)$ cliffdemo file setup.py
    +---------------+--------------+
    |     Field     |    Value     |
    +---------------+--------------+
    | Name          | setup.py     |
    | Size          | 5825         |
    | UID           | 502          |
    | GID           | 20           |
    | Modified Time | 1335569964.0 |
    +---------------+--------------+

Creating Your Own Formatter
---------------------------

If the standard formatters do not meet your needs, you can bundle
another formatter with your program by subclassing from
:class:`cliff.formatters.base.ShowFormatter` and registering the
plugin in the ``cliff.formatter.show`` namespace.
