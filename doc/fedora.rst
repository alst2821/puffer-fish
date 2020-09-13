========
 Fedora
========

:ref:`(contents) <ref-fedora-toctree>`
     
General links
-------------

`Fedora magazine <http://fedoramagazine.org/>`_

`Start page: https://start.fedoraproject.org/ <https://start.fedoraproject.org/>`_

`Users' mailing list archive <https://lists.fedoraproject.org/pipermail/users/>`_

`Getting started with virtualization (fedoraproject.org)`_

.. _`Getting started with virtualization (fedoraproject.org)`: https://docs.fedoraproject.org/en-US/quick-docs/getting-started-with-virtualization/index.html

MP4 video codecs
----------------

The solution below requires rpmfusion packages. The ipod touch I have
saves "\*mov" files that are MP4 H.264 AAC encoded files.

I found out because I could not play them with the standard "totem" in Fedora 24.

This was cured with these commands::

   dnf install h264enc.noarch
   dnf install faac
   dnf install gstreamer-plugins-ugly
   dnf install gstreamer-plugins-bad
   dnf install gstreamer-plugins-bad-free
   dnf install gstreamer-ffmpeg
   dnf install gstreamer1
   dnf install gstreamer1-plugins-good
   dnf install gstreamer1-plugins-bad-freeworld
   dnf install gstreamer1-plugins-ugly
   dnf install gstreamer1-libav

Systemd
-------

This is an article by Jon Stanley about converting sysv-init scripts to systemd in fedora magazine (2015).
`systemd: Converting sysvinit scripts <https://fedoramagazine.org/systemd-converting-sysvinit-scripts/>`_

And here is a link to the man page of the systemd service: `systemd.service <https://www.freedesktop.org/software/systemd/man/systemd.service.html>`_ (Freedesktop dot org)


Version
-------

One of the possibly many ways to determine which fedora version you are running::
  
   rpm -E %fedora

On my current machine, it gives me "24" (July 2016).

On a redhat system, this is possible too::

  rpm -E %rhel

The result is "7" on a RHEL7 machine.

This was noticed first in the recipe from rpmfusion.

Other things can be gleaned at from `rpm --showrc` that shows many,
many entries (about 1400 lines on the redhat system I tried it on).
