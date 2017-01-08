.. _systemimages-label:

Pre configured system images
============================

.. _note::

    On Windows you need to download `Win32 Disk Imager`_ to write the images to an sdcard.

    Linux has all the tools onboard :)

    .. _Win32 Disk Imager: https://sourceforge.net/projects/win32diskimager/


Login credentials for all images
--------------------------------

- root : root
- botmaster : botmaster

Installaltion on SD-Card
------------------------

Linux
^^^^^

::

    sudo gunzip -c pluginbot.arch.img.ARCHITECTURE.gz | dd of=/dev/sdX

Where sdX is the device for your SD-Card.

Windows
^^^^^^^

Unzip pluginbot.arch.img.ARCHITECTURE.zip and then write image2.img with Win32DiskImager.

Downloads
---------

Banana Pi
^^^^^^^^^

Download one of the following compressed images:

- `pluginbot.arch.img.bananapi.gz`_
- `pluginbot.arch.img.bananapi.zip`_

.. _pluginbot.arch.img.bananapi.gz: https://www.robingroppe.de/media/mumble-ruby-pluginbot/0.10/armboards/pluginbot.arch.img.bananapi.gz
.. _pluginbot.arch.img.bananapi.zip: https://www.robingroppe.de/media/mumble-ruby-pluginbot/0.10/armboards/pluginbot.arch.img.bananapi.zip

Raspberry Pi2
^^^^^^^^^^^^^

Download one of the following compressed images

- `pluginbot.arch.img.pi2.gz`_
- `pluginbot.arch.img.pi2.zip`_

.. _pluginbot.arch.img.pi2.gz: https://www.robingroppe.de/media/mumble-ruby-pluginbot/0.10/armboards/pluginbot.arch.img.pi2.gz
.. _pluginbot.arch.img.pi2.zip: https://www.robingroppe.de/media/mumble-ruby-pluginbot/0.10/armboards/pluginbot.arch.img.pi2.zip

Raspberry Pi3
^^^^^^^^^^^^^

Download one of the following compressed images

- `pluginbot.arch.img.pi3.gz`_
- `pluginbot.arch.img.pi3.zip`_

.. _pluginbot.arch.img.pi3.gz: https://www.robingroppe.de/media/mumble-ruby-pluginbot/0.10/armboards/pluginbot.arch.img.pi3.gz
.. _pluginbot.arch.img.pi3.zip: https://www.robingroppe.de/media/mumble-ruby-pluginbot/0.10/armboards/pluginbot.arch.img.pi3.zip


.. note::

  On newer distributions instead of editing the file you need to disable the MPD service by running the following command as root or with sudo::

    systemctl disable mpd

    systemctl stop mpd
