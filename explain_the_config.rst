.. _configexplain-label:

Explain the configs
===================

Configuration files
-------------------

There is a main configuration file named ``config/config.yml``.

Also every plugin does have its own configuration file, see ``plugins/*.yml``.

Default configuration and override configuration
------------------------------------------------

The bot always reads the default configuration files from ``config/config.yml`` and all plugin configuration files from ``plugins/*yml``.

If you want to use an own configuration file you don't need to write one with all configuration settings but only with those you want to change. A small sample override configuration file is available in ``templates/override_config.yml``. All settings that you set there will overwrite those from the default configuration file ``config/config.yml`` and also those from every single plugin configuration file ``plugins/*.yml``.

Syntax within this help
-----------------------

If we refer to a configuration option in this help text we write for example ``main:tempdir`` if we mean::

    main:
        tempdir: "/home/botmaster/temp/"

Notes for editing the configuration
-----------------------------------

The documentation uses the YAML syntax, that means that it is based on indentation by space characters.

When you write a **string** you can enclose it in double quotes::

    "--external-downloader aria2c"

Enclose the string into single quotes if you want to use double quotest within a string::

    '--external-downloader aria2c --external-downloader-args "-j 6 -k 1M -x 10"'

Default config/config.yml
-------------------------

The following config shows all available configuration options of the ``config/config.yml`` as of version 0.10.x::

    ---
    config:
      version: 2.1

    debug: true
    language: en

    main:
      tempdir: "/home/botmaster/temp/"
      logfile: "/home/botmaster/logs/bot1.log"
      ducking: false
      automute_if_alone: true
      stop_on_unregistered: true
      channel_notify: 0
      controllable: true
      control:
        string: "."
        message:
          private_only: false
          registered_only: true
        historysize: 20
      display:
        comment:
          set: true
      user:
        superuser:
          72x60721xx216x4xx017f3x1x476d4358x48x648: dafoxia
          1234567890ABCDEFGHIJKLMNOPQRSTUVWXYZ1234: anotheruser
        banned:
          123452342348234782937ckjfvo32ckj20938473: user3
          df92lkjvdkfj2okdfh20398vhj209eu2hjd092hn: anotherusername4
        bound: # "1234567890ABCDEFGHIJKLMN"
      certfolder: "/home/botmaster/certs/"
      fifo: "/home/botmaster/mpd1/mpd.fifo"
      logo: "../config/logo/logo.html"
      timer:
        ticks:  3600
      blacklisted_commands: ""

    mumble:
      use_vbr: true
      bitrate: 72000
      host: m.natenom.com
      port: 64738
      name: "MumbleRubyPluginbot"
      password: ""
      channel: Bottest

Main settings
-------------

config:version
^^^^^^^^^^^^^^

* Type: float
* Default: 2.1

This is for internal reasons only and is not meant to be changed.

.. _settings_debug:

debug
^^^^^

* Type: boolean
* Default: true
* Possible values: true, false

Set this to false to disable debug output in the logfile.

.. _settings_language:

language
^^^^^^^^

* Type: string
* Default: en
* Possible values: en, de, bar

Set this to the preferred language. "bar" is Bavarian.

.. _settings_main_tempdir:

main:tempdir
^^^^^^^^^^^^

* Type: string
* Default: "/home/botmaster/temp/"

This is the base path where the bot downloads new music to, but every plugin that downloads music adds an own subdirectory to this path.

After the download the bots copies the downloaded files into the final directory definied in ``plugin:mpd:musicfolder``, also into a plugin specific folder.

For example these are the resulting directories for the Youtube plugin:

- temp: ``/home/botmaster/temp/youtubeplugin/``
- final: ``/home/botmaster/music/downloadedfromyt/``

.. _settings_main_logfile:

main:logfile
^^^^^^^^^^^^

* Type: string
* Default: "/home/botmaster/logs/bot1.log"

The path to the bots log file.

main:ducking
^^^^^^^^^^^^

* Type: boolean
* Default: false
* Possible values: true, false

If true the bot automatically reduces its volume while users in the channel are talking.

main:automute_if_alone
^^^^^^^^^^^^^^^^^^^^^^

* Type: boolean
* Default: true
* Possible values: true, false

The bot automatically mutes itself if he is alone in a channel.

main:stop_on_unregistered
^^^^^^^^^^^^^^^^^^^^

* Type: boolean
* Default: true
* Possible values: true, false

The bot pauses the music or stops a radiostream if an unregistered user enters the channel.

main:channel_notify
^^^^^^^^^^^^^^^^^^^

* Type: int
* Default: 0

Calculating value for 'channel_notify':

Add all values for the desired channel notification

* 1    send message when volume change
* 2    send message when database update
* 4    send message when random mode changed
* 8    send message when single mode changed
* 16   send message when crossfading changed
* 32   send message when consume-mode changed
* 64   send message when repeat-mode changed
* 128  send message when state changes

Sum up all you need and use it as the configuration value.

main:controllable
^^^^^^^^^^^^^^^^^

* Type: boolean
* Default: true
* Possible values: true, false

Bot is only controllable if this is set to true. If false it will ignore all text commands.

main:control:string
^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "."

This is the character/string a user must prepend to text commands. The bot ignores commands not starting with that character/string.

main:control:message:private_only
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: boolean
* Default: false
* Possible values: true, false

If true the bot reacts only to private messages and not to channel messages. If false, the bot reacts to channel and private messages.

main:control:message:registered_only
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: boolean
* Default: true
* Possible values: true, false

If true the bot reacts only to registered users. If false also unregistered users can control the bot.

main:control:historysize
^^^^^^^^^^^^^^^^^^^^^^^^

* Type: int
* Default: 20

Store this many entries in the command history of the bot.

main:display:comment:set
^^^^^^^^^^^^^^^^^^^^^^^^

* Type: boolean
* Default: true
* Possible values: true, false

If true the bot sets its comment to display the current music that is being played.

main:user:superuser
^^^^^^^^^^^^^^^^^^^
You can define several superusers here. To get a users hash use the command ``.showhash``, see ``.internals``.

The commands ``.reset``, ``.set`` and ``.settings`` can only be used by the defined superusers.

Safety Information: All predefined entries for superuser are only there to show you how it works, they will never work.

Example::

    72x60721xx216x4xx017f3x1x476d4358x48x648: dafoxia


main:user:banned
^^^^^^^^^^^^^^^^
You can define several banned users here. To get a users hash use the command ``.showhash``, see ``.internals``.

The bot will ignore the defined users completely.

Safety Information: All predefined entries for banned users are only there to show you how it works, they will never work.

Example::

    123452342348234782937ckjfvo32ckj20938473: user3

main:user:bound
^^^^^^^^^^^^^^^
Only ONE user hash as a string. If definied nobody will be able to use the bind command anymore but the defined user. The blacklist command can only be used after being bound.

main:certfolder
^^^^^^^^^^^^^^^

* Type: string
* Default: "/home/botmaster/certs/"

In this folder the bot automatically creates an openssl certificate per :ref:`Mumble username <settings_mumble_name>` you set up.

main:fifo
^^^^^^^^^

* Type: string
* Default: "/home/botmaster/mpd1/mpd.fifo"

This fifo must also be used by the MPD the bot connects to.

main:logo
^^^^^^^^^

* Type: string
* Default: "../config/logo/logo.html"

A relative path to the logo the bot uses.

main:timer:ticks
^^^^^^^^^^^^^^^^

* Type: int
* Default: 3600

FIXME

main:blacklisted_commands
^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: ""

Here you can disable specific commands. Be aware that currently the bot checks this very stupid. That means that it checks only the beginning of a word. For example if you blacklist set then settings is also blacklisted.

mumble:use_vbr
^^^^^^^^^^^^^^

* Type: boolean
* Default: true
* Possible values: true, false

If true the bot encodes with a variable bitrate. If false it encodes with a constant bitrate.

mumble:bitrate
^^^^^^^^^^^^^^

* Type: int
* Default: 72000

The overall bandwidth the bot is allowed to use. Please note that the bot is able to ask the server for its maximum bandwidth and so can reduce its bitrate if you set it higher than possible.

mumble:host
^^^^^^^^^^^

* Type: string
* Default: m.natenom.com

The hostname or IP address of the Mumble server your bot connects to.

mumble:port
^^^^^^^^^^^

* Type: int
* Default: 64738

The port of the Mumble server your bot connects to.

.. _settings_mumble_name:

mumble:name
^^^^^^^^^^^

* Type: string
* Default: "MumbleRubyPluginbot"

The name of your bot. Be aware that on most Mumble servers you are not allowed to use white spaces or other special characters.

mumble:password
^^^^^^^^^^^^^^^

* Type: string
* Default: ""

If your user is registered via a password, set it here or if the server uses a password, use this, too.

mumble:channel
^^^^^^^^^^^^^^

* Type: string
* Default: "Bottest"

The channel the bot connects to. This is also the channel the bot tries to enter if you command it to ``.gotobed``.

Bandcamp plugin settings
------------------------

plugin:bandcamp:folder:download
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "downloadedfrombc/"

The subdirectory the bot copies downloaded audio files into. The full path is built from ``plugin:mpd:musicfolder+plugin:bandcamp:folder:download``.

plugin:bandcamp:folder:temp
^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "bandcampplugin/"

The subdirectory the bot downloads new audio files into. The full path is built from ``main:tempdir+plugin:bandcamp:folder:temp``.

plugin:bandcamp:youtube_dl:path
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "/home/botmaster/src/youtube-dl"

plugin:bandcamp:youtube_dl:options
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: ""

plugin:bandcamp:youtube_dl:prefixes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: ""

plugin:bandcamp:to_mp3
^^^^^^^^^^^^^^^^^^^^^^

* Type: undefined
* Default: nil

By default the bot tries to download OPUS encoded audio files or whatever is available.

Set this to true but nil in order to convert audio files into MP3.

Ektoplazm plugin settings
-------------------------

plugin:ektoplazm:prefixes
^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: ""

plugin:ektoplazm:folder:download
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "ektoplazm/"

The subdirectory the bot copies downloaded audio files into. The full path is built from ``plugin:mpd:musicfolder+plugin:ektoplazm:folder:download``.

plugin:ektoplazm:folder:temp
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "ektoplazmplugin/"

The subdirectory the bot downloads new audio files into. The full path is built from ``main:tempdir+plugin:ektoplazm:folder:temp``.

Idle plugin settings
--------------------

plugin:idle:maxidletime
^^^^^^^^^^^^^^^^^^^^^^^

* Type: int
* Default: 600

Time in seconds the bot can idle before doing an action, see ``plugin:idle:action``.

plugin:idle:action
^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "channel"
* Possible values: "channel", "deafen"

If "channel" the bot enters its home channel when being idle longer than ``plugin:idle:maxidletime``.

Mixcloud plugin settings
------------------------

plugin:mixcloud:folder:download
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "downloadedfrommc/"

The subdirectory the bot copies downloaded audio files into. The full path is built from ``plugin:mpd:musicfolder+plugin:mixcloud:folder:download``.

plugin:mixcloud:folder:temp
^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "mixcloudplugin/"

The subdirectory the bot downloads new audio files into. The full path is built from ``main:tempdir+plugin:mixcloud:folder:temp``.

plugin:mixcloud:youtube_dl:path
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "/home/botmaster/src/youtube-dl"

plugin:mixcloud:youtube_dl:options
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: '--external-downloader aria2c --external-downloader-args "-j 6 -k 1M -x 10"'

plugin:mixcloud:youtube_dl:prefixes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: ""

plugin:mixcloud:to_mp3
^^^^^^^^^^^^^^^^^^^^^^

* Type: undefined
* Default: nil

By default the bot tries to download OPUS encoded audio files or whatever is available.

Set this to true but nil in order to convert audio files into MP3.

MPD plugin settings
-------------------

plugin:mpd:testpipe
^^^^^^^^^^^^^^^^^^^

* Type: boolean
* Default: true
* Possible values: true, false

When this is set to true the bot will test whether MPD is running before it continues to start fully.

.. note::

  On some systems this may fail and cause the bot to show several plugins named "false" when you use the command ``.plugins``; set this value to ``false`` in such a case.

plugin:mpd:volume
^^^^^^^^^^^^^^^^^

* Type: int
* Default: 65
* Value range: 0 to 100

The default volume in % when the bot starts.

plugin:mpd:host
^^^^^^^^^^^^^^^

* Type: string
* Default: localhost

The host where your MPD server is running on.

plugin:mpd:port
^^^^^^^^^^^^^^^

* Type: int
* Default: 65

The port your MPD server is reachable at.

plugin:mpd:musicfolder
^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "/home/botmaster/music/"

plugin:mpd:template:comment:disabled
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "<b>Artist: </b>DISABLED<br /><b>Title: </b>DISABLED<br/><b>Album: </b>DISABLED<br /><br /><b>Write %shelp to me, to get a list of my commands!"

plugin:mpd:template:comment:enabled
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "<b>Artist: </b>%s<br /><b>Title: </b>%s<br /><b>Album: </b>%s<br /><br /><b>Write %shelp to me, to get a list of my commands!</b>"

Soundcloud plugin settings
--------------------------

plugin:soundcloud:folder:download
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "downloadedfromsc/"

The subdirectory the bot copies downloaded audio files into. The full path is built from ``plugin:mpd:musicfolder+plugin:soundcloud:folder:download``.

plugin:soundcloud:folder:temp
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "soundcloudplugin/"

The subdirectory the bot downloads new audio files into. The full path is built from ``main:tempdir+plugin:soundcloud:folder:temp``.

plugin:soundcloud:youtube_dl:path
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "/home/botmaster/src/youtube-dl"

plugin:soundcloud:youtube_dl:options
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: ""

plugin:soundcloud:youtube_dl:prefixes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: ""

plugin:soundcloud:to_mp3
^^^^^^^^^^^^^^^^^^^^^^^^

* Type: undefined
* Default: nil

By default the bot tries to download OPUS encoded audio files or whatever is available.

Set this to true but nil in order to convert audio files into MP3.

Youtube plugin settings
-----------------------

plugin:youtube:folder:download
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "downloadedfromyt/"

The subdirectory the bot copies downloaded audio files into. The full path is built from ``plugin:mpd:musicfolder+plugin:youtube:folder:download``.

plugin:youtube:folder:temp
^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "youtubeplugin/"

The subdirectory the bot downloads new audio files into. The full path is built from ``main:tempdir+plugin:youtube:folder:temp``.

plugin:youtube:youtube_dl:path
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: "/home/botmaster/src/youtube-dl"

plugin:youtube:youtube_dl:options
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: ""

plugin:youtube:youtube_dl:prefixes
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: string
* Default: ""

plugin:youtube:youtube_dl:maxresults
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: int
* Default: 200

plugin:youtube:to_mp3
^^^^^^^^^^^^^^^^^^^^^

* Type: undefined
* Default: nil

By default the bot tries to download OPUS encoded audio files or whatever is available.

Set this to true but nil in order to convert audio files into MP3.
