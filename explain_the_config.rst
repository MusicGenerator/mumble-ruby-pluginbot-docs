.. _configexplain-label:

Explain the config
==================

The following config shows all available configuration options as of version 0.10.x::

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
      password: ''
      channel: Bottest


Syntax within this help
-----------------------

If we refer to a configuration option in this help text we write for example "main:tempdir" if we mean::

    main:
        tempdir: "/home/botmaster/temp/"


Explanations
============

.. table:: Configuration options

   +-------------------------------------------------------+-------------+-------------------------------------------+-----------------------------+
   | Config Path                                           | Type        | Default value                             | Value range                 |
   +=======================================================+=============+===========================================+=============================+
   |                                                       |             |                                           |                             |
   +-------------------------------------------------------+-------------+-------------------------------------------+-----------------------------+
   |                                                       |             |                                           |                             |
   +-------------------------------------------------------+-------------+-------------------------------------------+-----------------------------+
   |                                                       |             |                                           |                             |
   +-------------------------------------------------------+-------------+-------------------------------------------+-----------------------------+
   |                                                       |             |                                           |                             |
   +-------------------------------------------------------+-------------+-------------------------------------------+-----------------------------+
   |                                                       |             |                                           |                             |
   +-------------------------------------------------------+-------------+-------------------------------------------+-----------------------------+
   |                                                       |             |                                           |                             |
   +-------------------------------------------------------+-------------+-------------------------------------------+-----------------------------+
   |                                                       |             |                                           |                             |
   +-------------------------------------------------------+-------------+-------------------------------------------+-----------------------------+
   |                                                       |             |                                           |                             |
   +-------------------------------------------------------+-------------+-------------------------------------------+-----------------------------+
   |                                                       |             |                                           |                             |
   +-------------------------------------------------------+-------------+-------------------------------------------+-----------------------------+

config:version
--------------

* Type: boolean
* Default: true
* Possible values: true, false

This is for internal reasons only and is not meant to be changed.

debug
-----

* Type: boolean
* Default value: true
* Possible values: true, false

Set this to false to disable debug output in the logfile.

language
--------

* Type: string
* Default: en
* Possible values: en, de, bar

Set this to the preferred language. "bar" is Bavarian.

main
----

main:tempdir
^^^^^^^^^^^^

* Type: string
* Default: "/home/botmaster/temp/"

This is where the bot downloads new music to.

main:logfile
^^^^^^^^^^^^

* Type: string
* Default: "/home/botmaster/logs/bot1.log"

The path to the bots log file.

main:ducking
^^^^^^^^^^^^

* Type: boolean
* Default: false

If true the bot automatically reduces its volume while users in the channel are talking.

main:automute_if_alone
^^^^^^^^^^^^^^^^^^^^^^

* Type: boolean
* Default: true

The bot automatically mutes itself if he is alone in a channel.

main:stop_on_unregistered
^^^^^^^^^^^^^^^^^^^^

* Type: boolean
* Default: true

The bot pauses the music or stops a radiostream if an unregistered user enters the channel.

main:channel_notify
^^^^^^^^^^^^^^^^^^^

* Type: int
* Default: 0

Calculating value for 'channel_notify':

Add all values for the desired channel notification

1    send message when volume change
2    send message when database update
4    send message when random mode changed
8    send message when single mode changed
16   send message when crossfading changed
32   send message when consume-mode changed
64   send message when repeat-mode changed
128  send message when state changes

sum = value

main:controllable
^^^^^^^^^^^^^^^^^

* Type: boolean
* Default: true

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

main:control:message:registered_only
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Type: boolean
* Default: true

main:control:historysize
^^^^^^^^^^^^^^^^^^^^^^^^

* Type: int
* Default: 20



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
password: ''
channel: Bottest






















  automute_if_alone: true
  stop_on_unregistered: true

















FIXME
