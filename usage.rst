.. _usage-label:

Usage
=====

Basic overview
--------------

The bot reacts to text commands, prefixed with a control string. The default control string is a dot ``.``

A good start for learning to control the bot is::

    .help

.. note::

  If you are really excited and want to know all the commands available then try the commands::

      .help all

  and::

      .internals

But first you need the bot to come into your channel, that is done with::

    .ch

which is a command of the :ref:`Control plugin <label_plugins_control>`, see::

    .help control

The basic music related commands you need for volume control, skip forward/backward, select the title to play, etc. are located in the :ref:`MPD plugin <label_plugins_mpd>`. If you don't want to download new music this is basically all that you need. To get the help of this plugin write to the bot::

    .help mpd

If there is no music in the bot yet you need to download some, see for example :ref:`label-usage_example_4`. But there are other plugins, too, which are able to download new music, see :ref:`Plugins of Mumble-Ruby-Pluginbot <plugins-label>`.

Usage examples
--------------

Example 1 – Volume control
::::::::::::::::::::::::::

The music is playing but you want to lower the volume, lets say the current volume is 65% and you want to lower it to 50%, you may do::

    .v---

    .v 50

Every ``-`` after the ``.v`` command (note that there is no space character) means 5% less.

Write ``.help mpd`` to the bot for details.

Example 2 – Change state
::::::::::::::::::::::::

The bot takes its music from a queue. To show the current queue use the command ``.queue``.

Each song in the queue is prefixed with an index number. This number can be used to play a specific song in the queue.

Use the command ``.play 5`` to play the 5th song in the list. Note that the first song has the index number 0.

Write ``.help mpd`` to the bot for details.

Example 3 – Listen to a radio station
:::::::::::::::::::::::::::::::::::::

First you must tell the bot to download/update the list of known radion stations with ``.radioupdate``.

Now you can get a list of available categories with ``.radiocategories``.

Choose one of them, for example **Electro** and lets display all the streams within this category with the command ``.radiocategory Electro``.

Now choose one of the available streams with ``.radioselect Electro 0``, in this example the first stream in the category Electro.

Now it may happen that the stream offers more than one stream because of several quality ranges. The bot may write you to "choose" one of them.

In order to do so use the command ``.choose`` and the bot will show a list of them. Then use ``.choose 1`` to choose the second stream in this case.

Yeay, it is not very user friendly currently but you have the ability to choose between thousands of radio streams and thats fantastic :)

.. _label-usage_example_4:

Example 4 – Download music from Youtube
:::::::::::::::::::::::::::::::::::::::

Lets say you want to listen to music from Mozart...

- First lets search on youtube::

    .yts mozart

- The bot responds with::

    0 Mozart for Baby (3 Hours) - ...
    1 The Best of Mozart | 3 HOURS Piano Sonatas ...
    2 Mozart for Studying and ...

- Now you can either let the bot download all search results::

    .yta all

- or just one or more specific song(s)::

    .yta 0 2

- In both cases the bot will inform you about the current download status::

    [21:59:22] ♫ Music Bot 1: do 2 time(s)...
    [21:59:22] ♫ Music Bot 1: fetch and convert
    [21:59:23] ♫ Music Bot 1: fetch and convert

- Followed by a database update::

    [21:59:48] ♫ Music Bot 1: Waiting for database update complete...

- Now lets show the current music queue::

    .queue

- The bot responds with::

    0 Mozart for Baby (3 Hours) - ...
    1 Mozart for Studying and ...

- Now lets play the first song in the queue with::

    .play first
