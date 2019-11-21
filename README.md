# alarm-images
Arch Linux Arm Base Images for Raspberry Pi


This repository contains automated image builds of Arch Linux ARM for Raspberry Pi 2, 3, and 4.  

Each image is built from [upstream tarballs](https://archlinuxarm.org/about/downloads) distributed by the Arch Linux ARM project, but written to an 8GB image file. This image file can then be written to any SD Card 8GB+. The remaining space  of the SD Card can be used as desired (expand partition and filesystem to fit, or create additional partitions).

## Background
It's hard to buy small SD Cards these days. While you can still find 8GB and 16GB cards on the market, the conventional starting point is a 32 GB SD Card. It's trivial to prepare and install Arch Linux ARM on an SD Card, but sometimes its nice to just have a simple, base image you can copy over and over as needed.

In my case, I was doing a some work for a client with an older version Arch Linux ARM that they had been imaging with their application, and needed to test an upgrade script. Creating an image directly from their 32GB card wasted a lot of space on my laptop, and re-writing it every time I needed to boot clean was a four-hour job. I didn't have a duplicator at the time, and futzing around with sparse image files on macOS to support Linux partitions and Ext4 filesystems to copy <8GB of data from a 32GB image just to save time was challenging, at best.

So, building on the work documented by [disconnected.systems](https://disconnected.systems) in [this blog post](https://disconnected.systems/blog/raspberry-pi-archlinuxarm-setup/) and [this other blog post](https://disconnected.systems/blog/custom-rpi-image-with-github-travis//), I now have a set of default images that are 8GB in size that I can quickly write [and customize] as needed. And since they're generic Arch Linux ARM builds with *nothing else* added, you can use them too.

Just download, burn, and boot!

## Releases
If you just want the downloads, head over to [Releases](https://github.com/andrewboring/alarm-images/releases) and get the appropriate one for your Raspberry Pi. Or select the latest version from the Files section below.

Then follow the standard instructions for your operating system to burn the image to your SD Card.


### Latest Files
- [rpi-2-archlinux.img.zip](https://github.com/andrewboring/alarm-images/releases/latest/download/rpi-2-archlinux.img.zip): For ARMv7, with the Raspberry Pi firmware. Also works on Raspberry Pi 3 series. Use this if you need VC4 stuff (like the GPU).
  - Upstream: https://archlinuxarm.org/platforms/armv7/broadcom/raspberry-pi-2

- [rpi-3-archlinux.img.zip](https://github.com/andrewboring/alarm-images/releases/latest/download/rpi-3-archlinux.img.zip): For ARMv8/Aarch64, with Uboot and Mainline Linux kernel. Almost full support for the board itself, but you get zero GPU. Experimental 64-bit Raspberry Pi firmware package is available, if you really want 64-bit and GPU.
  - Upstream: https://archlinuxarm.org/platforms/armv8/broadcom/raspberry-pi-3

- [rpi-4-archlinux.img.zip](https://github.com/andrewboring/alarm-images/releases/latest/download/rpi-3-archlinux.img.zip): Supplies ARMv7 kernel and RPi firmware, at the moment. Use RPI-3 above if you want aarch64 support.
  - Upstream: https://archlinuxarm.org/platforms/armv8/broadcom/raspberry-pi-4

[ to do: add more details on ARMv7 vs ARMv8 vs aarch32 vs aarch64 ]

### Frequency
The Arch Linux ARM project will release updated tarballs, but not with the same frequency as Arch Linux. Therefore, these images may not be aligned with the latest tarball from Arch Linux ARM.

[ to do: add script to master control to check for upstream updates and trigger a new release on demand]

## Source
The source includes a Vagrant file to boot Arch Linux, which then automatically downloads and builds the three releases. You'll need [Vagrant](https://www.vagrantup.com) and [Virtualbox](https://virtualbox.org).

If you'd like to build these yourself (eg, to change the image size or add additional software to the image), just edit the Vagrant file and comment out the shell stuff. The create-image file will be available in /tmp/vagrant for you to run manually, to create a single image. Use pacstrap to install additional packages into your image before unmounting and compressing.

[ to do: add instructions for customizing images, linking to ArchWiki and other resources ]

Once built, you'll need to copy the appropriate image out of the Vagrant box before deleting it.
