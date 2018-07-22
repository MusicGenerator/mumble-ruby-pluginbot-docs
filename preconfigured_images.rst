.. _systemimages-label:

Pre configured system images
============================

.. note::

    We do not rebuild these images for every patchlevel update, so please run the updater once after installing the image.

    The updater is located in ``~/src/mumble-ruby-pluginbot/scripts/updater.sh``.


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

.. note::

    On Windows you need to download `Win32 Disk Imager`_ to write the images to an sdcard.

    .. _Win32 Disk Imager: https://sourceforge.net/projects/win32diskimager/

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
