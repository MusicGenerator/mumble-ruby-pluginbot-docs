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

config:version
--------------

.. table::

   +--------------------------------------+
   | Type                      | float    |
   +---------------------------+----------+
   | Default value             | 2.1      |
   +---------------------------+----------+
   | Available values          |          |
   +---------------------------+----------+


.. table::

   +--------------------------------------+
   | config:version                       |
   +===========================+==========+
   | Type                      |    |
   +---------------------------+----------+
   | Default value             |    |
   +---------------------------+----------+
   | Available values          |    |
   +---------------------------+----------+

* Type: boolean
* Default value: true
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
* Default value: en
* Possible values: en, de, bar

Set this to the preferred language. "bar" is bavarian.


main
----

* Default value:
* Possible values:


main:tempdir
^^^^^^^^^^^^

* Type: string
* Default value: "/home/botmaster/temp/"



  tempdir:

  logfile: "/home/botmaster/logs/bot1.log"
  ducking: false
  automute_if_alone: true
  stop_on_unregistered: true






FIXME
