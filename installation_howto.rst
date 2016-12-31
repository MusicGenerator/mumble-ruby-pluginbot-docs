.. _installationonyourown-label:

Installation HowTo
==================

In this tutorial/howto we install the :ref:`start-label` into a users home directory. No system services are used.

.. seealso::

  - :ref:`compatibility-label`
  - :ref:`howtorunthebot-label`

How much time will you need?
--------------------------

This tutorial works well using copy and paste if you want one bot only. If you want more bots, read the note boxes and warning boxes :)

After ~20 minutes it should be finished, depending on your servers internet connection.

How will it look like?
----------------------

This will be the directory structure when this howto is completed::

  /home/botmaster/
  ├── mpd1
  │   ├── playlists
  │   ├── mpd1.log
  │   ├── mpd.conf
  │   ├── mpd.fifo
  │   ├── pid
  │   ├── state
  │   ├── sticker.sql
  │   └── tag_cache
  ├── (optional) more mpd directories ... mpd2, mpd3, etc.
  ├── logs
  ├── music
  │   └── downloadedfromyt
  │   └── downloadedfromsc
  │   └── [...]
  ├── src
  │   └── certs
  │       └── nameofyourbot_cert
  │       └── [...]
  │   └── mumble-ruby
  │   └── mumble-ruby-pluginbot
  │   │   └── scripts
  │   │       └── mumblerubypluginbot.service
  │   │       └── overwrite_conf.rb
  │   │       └── manage.sh
  │   │       └── updater.sh
  │   │   └── [...]
  │   └── bot1_conf.yml
  │   └── (optional) more bot<number>_conf.yml
  │   └── [...]
  ├── temp
  │   └── youtubeplugin
  │   └── bandcampplugin
  │   └── [...]
  [...]

On Arch Linux only: Install and set up system package dependencies
------------------------------------------------------------------

Install the following dependencies as root or via sudo::

  pacman -S libyaml opus zlib openssl git mpd mpc tmux automake \
  autoconf libogg psmisc util-linux libtool curl base-devel wget aria2

On Debian/Ubuntu based Distributions only: Install and set up system package dependencies
-----------------------------------------------------------------------------------------

Install the following dependencies as root or via sudo (please not that this is one command, copy and paste all four lines)::

  apt-get install curl libyaml-dev git libopus-dev \
  build-essential zlib1g zlib1g-dev libssl-dev mpd mpc tmux \
  automake autoconf libtool libogg-dev psmisc util-linux libgmp3-dev \
  dialog unzip ca-certificates aria2

The message about ``no database /var/lib/mpd/tag_cache`` can be ignored. The database will be created as soon as you start the MPD server.

As we do not need the system wide MPD it can be disabled. To do this open the file ``/etc/default/mpd`` as root or via sudo and change ``START_MPD`` to ``false``. At the next system start it will not be started any more.

.. note::

  On newer distributions instead of editing the file you need to disable the MPD service by running the following command as root or with sudo::

    systemctl disable mpd

    systemctl stop mpd

Create a user which should contain all the relevant bot structures
------------------------------------------------------------------

.. note::

  It is crucial that you use the same username as in this tutorial. Otherwise you need to manually adapt most scripts and configuration files to another username.

As root or via sudo::

  adduser botmaster

All relevant scripts will run within this user context.

Now it is the time to log in as your new user with::

  su - botmaster

All the following steps are done as the user botmaster.

Create all needed directories and subdirectories for MPD and the bot(s)
-----------------------------------------------------------------------

Create a directory for the source code and scripts::

  mkdir ~/src

Create a direcotry for log files::

  mkdir ~/logs

Create a directory for the certificates::

  mkdir ~/src/certs

Create a directory for the music::

  mkdir ~/music

Create a directory for the temp files::

  mkdir ~/temp

Create the directories for bot 1::

  mkdir -p ~/mpd1/playlists

.. note::

  Note that you can use more than one bots with this tutorial. Just create a new directory structure for every additional bot, for example with::

    mkdir -p ~/mpd2/playlists

  and so on.

Install and set up ruby and all needed libraries
------------------------------------------------

We are using RVM (`Ruby Version Manager`_) to install a local version of Ruby instead of using a system wide installed Ruby which may be too old.

.. _Ruby Version Manager: http://rvm.io

First get and add the GPG key of RVM::

  gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3

We need at least Ruby 1.9.x, here we use the latest stable version::

  curl -L https://get.rvm.io | bash -s stable

Now we need to tell our current shell to use rvm::

  source ~/.rvm/scripts/rvm

Because of 'I don't remember' we disable autolibs :P::

  rvm autolibs disable

Now we install the latest stable version of Ruby::

  rvm install ruby --latest

Set up a Ruby environment
^^^^^^^^^^^^^^^^^^^^^^^^^

Now setup the environment for Ruby::

  rvm --create use @bots

Get and build mumble-ruby and ruby-mpd and other dependencies
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Now we download the source code of [[Mumble-Ruby]] and build it::

  cd src

  git clone https://github.com/dafoxia/mumble-ruby.git mumble-ruby

  cd mumble-ruby

  rvm use @bots

  gem build mumble-ruby.gemspec

  rvm @bots do gem install mumble-ruby-*.gem

Install [https://github.com/archSeer/ruby-mpd/ ruby-mpd] so that the bot can control [[MPD]]::

  rvm @bots do gem install ruby-mpd

  rvm @bots do gem install crack

Download and set up celt-ruby and libcelt
-----------------------------------------

For compatibility reasons the bot uses slightly modified versions of CELT which need to be built with the following steps::

  cd ~/src

  git clone https://github.com/dafoxia/celt-ruby.git

  cd celt-ruby

  rvm use @bots

  gem build celt-ruby.gemspec

  rvm @bots do gem install celt-ruby

  cd ~/src

  git clone https://github.com/mumble-voip/celt-0.7.0.git

  cd celt-0.7.0

  ./autogen.sh

  ./configure --prefix=/home/botmaster/src/celt

  make

  make install

Download and set up opus-ruby
-----------------------------

Do the following commands::

  cd ~/src

  git clone https://github.com/dafoxia/opus-ruby.git

  cd opus-ruby

  rvm use @bots

  gem build opus-ruby.gemspec

  rvm @bots do gem install opus-ruby

Download and set up mumble-ruby-pluginbot
-----------------------------------------

Do the following commands::

  cd ~/src

  git clone https://github.com/MusicGenerator/mumble-ruby-pluginbot.git

  cd mumble-ruby-pluginbot

  git checkout -b devel origin/devel

Now we copy the config file for pluginbot to a directory which doesn't interfere with the source code::

  cp templates/override_config.yml ~/src/bot1_conf.yml

This approach has the advantage that this new config file contains only the variables you want to change. All the other variables not set in your override_config.yml are used from the ~/src/mumble-ruby-pluginbot/config/pluginbot_conf.yml file.

You should now edit the bots configuration file named "bot1_conf.yml" with your favorite editor::

  nano ~/src/bot1_conf.yml

... and adapt at least the following settings to your needs:

- mumble -> host
- mumble -> port
- mumble -> username
- mumble -> password

  - Note: This password is optional only and not needed if you want to register the bot as an admin on your server.

- mumble -> channel

  - Note: This channel name is the one your bots tries to enter when getting a .gotobed

- mumble -> bitrate

  - Note: If you set a higher bandwidth than your server can handle the bot automatically reduces its bandwidth to fit the servers needs.

The rest of the configuration file should be fine.

.. note::

  For every additional bot you need to copy the original config file and edit it, for example for bot 2 do::

    cd ~/src/mumble-ruby-pluginbot
    cp templates/override_config.yml ~/src/bot2_conf.yml

  Then edit ~/src/bot2_conf.yml and change the folowing variables:

  - main -> fifo to "/home/botmaster/mpd2/mpd.fifo", and so forth
  - plugin -> mpd -> port to 7702, and so forth

Set up MPD (Music Player Daemon)
--------------------------------

Copy the configuration file for your local MPD::

  cp ~/src/mumble-ruby-pluginbot/templates/mpd.conf ~/mpd1/mpd.conf


.. note::

  For every additional bot you must increase the number of ~/mpd1/... by one. For a second bot use::

    cp ~/src/mumble-ruby-pluginbot/templates/mpd.conf ~/mpd2/mpd.conf

  Then open the downloaded mpd.conf file and substitude every occurence of ``mpd1`` by ``mpd2``. Also increase the port from 7701 to 7702, 7703, etc.

.. note::

  For experts only: Explanations about the configuration file and additional settings you may want to have...

  - You can see the configuration file at `here`_..
  - Instead of the default sample rate of 44100 this config uses 48000 which is the sample rate Mumble clients use. And we need a mono signal.
  - The mixer type is set to software so that the volume in MPD can be changed without the need of a real soundcard.
  - You can enable `volume normalization`_ by adding the following line to the mpd config file::

      volume_normalization "yes"

  .. _here: https://github.com/MusicGenerator/mumble-ruby-pluginbot/blob/master/templates/mpd.conf
  .. _volume normalization: https://en.wikipedia.org/wiki/Audio_normalization


Set up the script to start your bot(s) and MPD instance(s)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Change into the mumble-ruby-pluginbot directory::

  cd ~/src/mumble-ruby-pluginbot

The Bash script named ``manage.sh`` in the scripts directory is used to start all your bots and your MPD instance(s).

Make it executable::

  chmod u+x ~/src/mumble-ruby-pluginbot/scripts/manage.sh

Also make the update script executable::

  chmod u+x ~/src/mumble-ruby-pluginbot/scripts/updater.sh

.. note::

  If you created more than one bot in this tutorial open the file and uncomment the needed lines to start your additional mpd instances.

You can see the script `here`__.

__ https://github.com/MusicGenerator/mumble-ruby-pluginbot/blob/master/scripts/manage.sh

Without modification the scripts starts only bot 1, for every additional bot modify the script.

Install a custom version of youtube-dl
--------------------------------------

You don't want to rely on the distributions version of an old youtube-dl so you must setup an own.

Only on Arch Linux: Install dependencies for youtube-dl
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

As root or with sudo install::

  pacman -S imagemagick ffmpeg python

Only on Debian/Ubuntu based distributions: Install the dependencies (if ffmpeg is available for your distribution)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

First install as root or via sudo the following system packages::

  apt-get install imagemagick ffmpeg python

Only on Debian/Ubuntu based distributions (OPTIONAL): Install the dependencies (if ffmpeg IS NOT available for your distribution)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

On some distributions the package ffmpeg was replaced by libav-tools; install this if ffmpeg is not available.

Install as root or via sudo the following system packages::

  apt-get install imagemagick libav-tools python

Also create the symlink so that the plugin can find it::

  ln -s /usr/bin/avconv /usr/bin/ffmpeg

Login as botmaster
^^^^^^^^^^^^^^^^^^

If not already logged in as botmaster, then do::

  su - botmaster

Install the youtube-dl script
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The youtube plugin needs youtube-dl; download it and make it executable::

  curl -L https://yt-dl.org/downloads/latest/youtube-dl -o ~/src/youtube-dl

  chmod u+x ~/src/youtube-dl

Almost done, start your bot(s) for the first time
-------------------------------------------------

You almost finished; now you can run your bot(s)::

  ~/src/mumble-ruby-pluginbot/scripts/manage.sh start

When the bot(s) appear on your server, register it/them and start working with it/them. Try ``.help`` as the first command.


.. seealso::

  If the bot does not connect refer to :ref:`knownproblems-label`.

Set up bot to start automatically on system startup
---------------------------------------------------

Start everything automatically – if your system is NOT systemd
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Add the following lines to ``/etc/rc.local`` before the ``exit...`` line to start your bot(s) when your system starts::

  su - botmaster -c "/home/botmaster/src/mumble-ruby-pluginbot/scripts/manage.sh start" &

The bot will start automatically on the next system start.

Start everything automatically – if your system is systemd
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Run the following command as root::

  cp /home/botmaster/src/mumble-ruby-pluginbot/templates/mumblerubypluginbot.service /etc/systemd/system/

  systemctl enable mumblerubypluginbot

The bot will start automatically on the next reboot.

Thats it, you are done :)

Controlling the bot(s) from your shell
--------------------------------------

To restart your bot(s) run::

  ~/src/mumble-ruby-pluginbot/scripts/manage.sh restart

To stop your bot(s) run::

  ~/src/mumble-ruby-pluginbot/scripts/manage.sh stop

To watch log files in real time run::

  ~/src/mumble-ruby-pluginbot/scripts/manage.sh log

To get the current status of your bot(s) run::

  ~/src/mumble-ruby-pluginbot/scripts/manage.sh status

Known problems
--------------

.. seealso::

  See :ref:`knownproblems-label`.
