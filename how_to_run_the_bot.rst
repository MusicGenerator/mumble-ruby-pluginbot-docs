.. _howtorunthebot-label:

How to run the bot
==================

There are several methods to run the bot.

Installation options
--------------------

Option 1: Install it on your own – Installation Howto
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Using this installation howto is basically a copy and paste task, even if you are unexperienced with Linux.

See :ref:`installationonyourown-label`.

.. _virtualboxappliance-label:

Option 2: Use a VirtualBox Virtual Appliance – Download a Fully set up Mumble Ruby Pluginbot
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Instead of setting up the bot yourself you can download a fully set up Mumble-Ruby-Pluginbot as a virtual appliance for VirtualBox. All you need to do after importing it to VirtualBox is to change one configuration file and add your server address and bot name.

The howto can be here: :ref:`appliance-label`.

Option 3: Use Docker
^^^^^^^^^^^^^^^^^^^^

There is a `Dockerfile available`_ to automatically build a Docker container running MPD and the current stable branch of `Mumble-Ruby-Pluginbot`_.

.. _Dockerfile available: https://github.com/MusicGenerator/mumble-ruby-pluginbot-docker
.. _Mumble-Ruby-Pluginbot: /

Option 4: Preconfigured images for different systems
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

See :ref:`systemimages-label`.

Maintenance
-----------

Automatic update
^^^^^^^^^^^^^^^^

Login as botmaster and run::

  ~/src/mumble-ruby-pluginbot/scripts/updater.sh

Select the first entry and press enter when prompted :)

Then restart your bot(s). Thats it :)

Be aware that this only works if you installed the bot with the official installation howto, see :ref:`installationonyourown-label`.

Manual update (not recommended)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you did install the bot yourself and did not use the official installation howto then please check the updater.sh script in the scripts directory in order to know what you need to update by hand.
