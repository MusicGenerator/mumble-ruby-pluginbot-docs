.. _systemimages-label:

Pre configured system images
============================

Banana Pi
---------

Download one of the following compressed images:

- `banana.img.gz`_
- `banana.img.xz`_
- `banana.img.zip`_

.. _banana.img.gz: https://robingroppe.de/media/mumble-ruby-pluginbot/banana.img.gz
.. _banana.img.xz: https://robingroppe.de/media/mumble-ruby-pluginbot/banana.img.xz
.. _banana.img.zip: https://robingroppe.de/media/mumble-ruby-pluginbot/banana.img.zip

Install on SD-Card
^^^^^^^^^^^^^^^^^^

####Linux
`sudo gunzip -c banana.img.gz | dd of=/dev/sdX`

or

`sudo xz -c -d banana.img.xz | dd of=/dev/sdX`

where sdX is the device for your SD-Card!

####Windows
Unzip banana.img.zip and then write with Win32DiskImager.
####Setup Bot
Set up Bot as described in [Virtual Appliance](https://wiki.natenom.com/w/VirtualBox_Appliance_for_Mumble-Ruby-Pluginbot)

- root password: bananapi
- user name:  botmaster
- user password: botmaster

##Raspberry Pi2

Download one of the following compressed images

- `image2.img.gz`_
- `image2.img.xz`_
- `image2.img.zip`_

.. _image2.img.gz: https://robingroppe.de/media/mumble-ruby-pluginbot/image2.img.gz
.. _image2.img.xz: https://robingroppe.de/media/mumble-ruby-pluginbot/image2.img.xz
.. _image2.img.zip: https://robingroppe.de/media/mumble-ruby-pluginbot/image2.img.zip

Install on SD-Card
^^^^^^^^^^^^^^^^^^

####Linux
`sudo gunzip -c image2.img.gz | dd of=/dev/sdX`

or

`sudo xz -c -d image2.img.xz | dd of=/dev/sdX`

where sdX is the device for your SD-Card!

####Windows
Unzip image2.img.zip and then write image2.img with Win32DiskImager.

###Setup Bot
Set up Bot as described in [Virtual Appliance](https://wiki.natenom.com/w/VirtualBox_Appliance_for_Mumble-Ruby-Pluginbot)

- root password: raspbian
- user name:  botmaster
- user password: botmaster

Banana Pi M2
------------

Download one of the following compressed images:

- `bananaPiM2.img.gz`_
- `bananaPiM2.img.xz`_
- `bananaPiM2.zip`_

.. _bananaPiM2.img.gz: https://robingroppe.de/media/mumble-ruby-pluginbot/bananaPiM2.img.gz
.. _bananaPiM2.img.xz: https://robingroppe.de/media/mumble-ruby-pluginbot/bananaPiM2.img.xz
.. _bananaPiM2.zip: https://robingroppe.de/media/mumble-ruby-pluginbot/bananaPiM2.zip

Install on SD-Card
^^^^^^^^^^^^^^^^^^

#####Linux
`sudo gunzip -c bananaPiM2.img.gz | dd of=/dev/sdX`

or

`sudo xz -c -d bananaPiM2.img.xz | dd of=/dev/sdX`

where sdX is the device for your SD-Card!

#####Windows
Unzip bananaPiM2.zip and then write with Win32DiskImager.
####Setup Bot
Set up Bot as described in [Virtual Appliance](https://wiki.natenom.com/w/VirtualBox_Appliance_for_Mumble-Ruby-Pluginbot)

- root password: bananapi
- user name:  botmaster
- user password: botmaster
