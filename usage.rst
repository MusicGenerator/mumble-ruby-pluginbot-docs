.. _usage-label:

Usage
=====

The bot reacts to text commands, prefixed with a control string.


.. note::

  The default control string is a dot ``.``

A good start for learning to control the bot is::

    .help


.. seealso::

    See also :ref:`plugins-label`.

Example
-------

Lets say you want to listen to music from Mozart...

- First lets search on youtube::

    .yts mozart

- The bot responds with::

    0 Mozart for Baby (3 Hours) - ...
    1 The Best of Mozart | 3 HOURS Piano Sonatas ...
    2 Mozart for Studying and ...

- Now you can either let the bot download all search results::

    .yta all

- or just one specific song::

    .yta 2

- In both cases the bot will inform you about the current download status::

    [21:59:22] ♫ Music Bot 1: do 1 time(s)...
    [21:59:22] ♫ Music Bot 1: fetch and convert

- Followed by a database update::

    [21:59:48] ♫ Music Bot 1: Waiting for database update complete...

- Now lets show the current music queue::

    .queue

- The bot responds with::

    0 The Best of Mozart _ 3 HOURS Piano Sonatas ...

- Now lets playl the file with::

    .play 0
