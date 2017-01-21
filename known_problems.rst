.. _knownproblems-label:

Known problems
==============

.. seealso::

  Please check also the `issues on the project page`__.

__ https://github.com/MusicGenerator/mumble-ruby-pluginbot/issues

General information
-------------------
Watch log files
^^^^^^^^^^^^^^^

.. note::

  By default the bot does a very detailed :ref:`logging <settings_main_logfile>` into ~/logs/*.log. You may use any tool to view those logs.

  If debug logging is disabled you can enable it via the debug setting, see :ref:`here <settings_debug>`.


You can also watch the log files with manage.sh::

  ~/src/mumble-ruby-pluginbot/scripts/manage.sh log

Press ``Ctrl + c`` to stop the log output.

Running the bot without the manage.sh script
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
**Only for experts**: If you want to start the bot without the manage.sh script you must manually run the following commands after every login in order to use the correct bot environment::

  source ~/.rvm/scripts/rvm

  rvm use @bots

Now you can try to start the bot from the shell.

MPD versions that cause problems
--------------------------------

The following MPD versions cause problems and should be avoided:

- 0.19.1 in Debian 8 crashes on AAC format radio streams.
- 0.20.1 causes loud noise/slow playback after songchange, see `here`__.

__ https://www.musicpd.org/news/2017/01/mpd-0-20-2-released/

Bot starts and crashes and cannot connect to MPD
------------------------------------------------

If the log contains the line::

  [...]
  pluginbot is starting...
  start
  /home/botmaster/.rvm/gems/ruby-2.2.1@bots/gems/ruby-mpd-0.3.3/lib/ruby-mpd.rb:106:in `connect': Unable to connect (possibly too many connections open) (MPD::ConnectionError)
        from /home/botmaster/src/mumble-ruby-pluginbot/plugins/mpd.rb:84:in `init'
        from /home/botmaster/src/mumble-ruby-pluginbot/pluginbot.rb:233:in `block in mumble_start'
        from /home/botmaster/src/mumble-ruby-pluginbot/pluginbot.rb:232:in `each'
        from /home/botmaster/src/mumble-ruby-pluginbot/pluginbot.rb:232:in `mumble_start'
        from /home/botmaster/src/mumble-ruby-pluginbot/pluginbot.rb:565:in `block in <main>'
        from /home/botmaster/src/mumble-ruby-pluginbot/pluginbot.rb:560:in `loop'
        from /home/botmaster/src/mumble-ruby-pluginbot/pluginbot.rb:560:in `<main>'
  [...]

You can also check whether connecting via mpc works with::

  mpc -p 7701 status

If it says::

  error: Connection closed by the server

Or if you find the mentioned lines in your log file then add the following line to the file ``/etc/hosts.allow``::

  mpd: LOCAL

And restart the bot.

Unregistered users recognition
------------------------------

Be aware that there is a bug in the recognition whether an unregistered user is in the channel. This is the reason why we disabled this feature (``main:stop_on_unregistered``) earlier in this tutorial, because the bot recognizes itself as unregistered and doesn't start the music. If you didn't change the variable to false you should register your bot as an admin before starting music with the ``.play`` command.

The bot does not start
----------------------

- Make sure that the desired bot name is not already registered on your server.
- Make sure you that you changed the mumbleserver_host in the bot's configuration file.

Downloading videos with special characters does not work
--------------------------------------------------------

When you get something like this in your debug console::

  UnicodeEncodeError: 'ascii' codec can't encode character u'\u2605' in position 49: ordinal not in range(128)
  (END)

Make sure that your system has an appropriate locale available and add the following line to the second line of your manage.sh::

  export LANG="en_US.UTF-8"

Replace this by your locale or use the above one. Make sure it is activated in ``/etc/locale.gen``.


Bot does not start completely and shows plugins named false
-----------------------------------------------------------

If the ``.plugin`` command shows one or more plugins named ``false`` then you must change the configuration setting ``plugin:mpd:testpipe`` to ``false``.
