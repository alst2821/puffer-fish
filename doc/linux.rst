================
 Linux material
================

* Intel Active Management Interface

  This is the linux specific info in `kernel.org <https://www.kernel.org/doc/html/latest/driver-api/mei/index.html>`_ (Accessed Sep 2020)

  This is the information from `Intel <https://www.intel.com/content/www/us/en/architecture-and-technology/implementation-of-intel-active-management-technology.html>`_ (Accessed Sep 2020)

  Setup guide `video <https://www.intel.com/content/www/us/en/support/articles/000026592/technologies.html>`_ (Accessed Sep 2020)
  


* `LWN Guest articles list <https://lwn.net/Archives/GuestIndex/>`_,
  organised by author.

Video of Rob Landley's tutorial `"Building the Simplest Possible Linux
System" <https://www.youtube.com/watch?v=Sk9TatW9ino>`_ [#f1]_.

Rob Landley has a `website <http://landley.net>`_ with writings about
early BSD/Linux developments.  For example one `from 2014
<http://landley.net/notes-2014.html#04-09-2014>`_ [#f2]_ which
discusses the motivation of systemd.

* `The linux kernel user's and administrator's guide <https://www.kernel.org/doc/html/latest/admin-guide/index.html>`_ (kernel.org)

* `The tragedy of systemd <https://www.youtube.com/watch?v=o_AIw9bGogo>`_ talk by Benno Rice at linux.conf.au in Jan 2019.

* The talk above references this article: `Contempt culture <http://blog.aurynn.com/2015/12/16-contempt-culture>`_ 
  
.. rubric:: Footnotes
	    
.. [#f1] Accessed on 12 August 2019

.. [#f2] Accessed on 12 August 2019	 


Lost password on virtual machine
--------------------------------

I recently lost the password of 'root' on a debian virtual machine.
I found some `pointers <https://coderwall.com/p/vibura/reset-a-lost-password-on-an-ubuntu-vm>`_ to recover and I am grateful.

The things that I had to do were:

* Go into a root shell on startup. This needed to modify the grub line
  to add ::
    
    init=/bin/bash
* Remount the root folder as read-write. This is because it was
  read-only when the machine booted::
    
    mount -rw -o remount /

* I was then able to reset the password::
    passwd


NX Nomachine
------------

* `NX Enterprise Client downloads <https://www.nomachine.com/product&p=NoMachine%20Enterprise%20Client>`_
  
* `List per architecture <https://www.nomachine.com/download-enterprise#NoMachine-Enterprise-Client>`_ [Accessed Dec 2019]

* `Linux packages for Fedora/Ubuntu/Tar <https://www.nomachine.com/download/linux&id=4>`_

* `Update to version 6.9.2-1 [Dec 2019] <https://www.nomachine.com/download/download&id=11>`_

Logs of the installation::
  
    $ rpm -qa noma*
    nomachine-enterprise-client-6.7.6-13.x86_64

    $ sudo rpm -e nomachine-enterprise-client-6.7.6-13.x86_64
    [sudo] password for <user>: 
    NX> 702 Starting uninstall at: Sat Dec 28 10:12:56 2019.
    NX> 702 Uninstalling: nxplayer version: 6.7.6.
    NX> 702 Uninstall log is: /usr/NX/var/log/nxuninstall.log.
    NX> 702 Uninstalling: nxclient version: 6.7.6.
    NX> 702 Uninstall log is: /usr/NX/var/log/nxuninstall.log.
    NX> 702 Client uninstall completed with warnings.
    NX> 702 Please review the uninstall log for details.
    NX> 702 Uninstall completed at: Sat Dec 28 10:14:04 2019.

    $ sudo dnf install nomachine-enterprise-client_6.9.2_1_x86_64.rpm
    [sudo] password for <user>:
    Updating Subscription Management repositories.
    Last metadata expiration check: 1:18:54 ago on Sat 28 Dec 2019 09:47:08 GMT.
    Dependencies resolved.
    ...
    Install  1 Package
    
    Total size: 36 M
    Installed size: 43 M
    Is this ok [y/N]: y
    Downloading Packages:
    Running transaction check
    Transaction check succeeded.
    Running transaction test
    Transaction test succeeded.
    Running transaction
    Preparing        :                                                        1/1
    Running scriptlet: nomachine-enterprise-client-6.9.2-1.x86_64             1/1
    Installing       : nomachine-enterprise-client-6.9.2-1.x86_64             1/1
    Running scriptlet: nomachine-enterprise-client-6.9.2-1.x86_64             1/1
    NX> 700 Starting install at: Sat Dec 28 11:06:15 2019.
    NX> 700 Installing: nxclient version: 6.9.2.
    NX> 700 Using installation profile: Fedora.
    NX> 700 Install log is: /usr/NX/var/log/nxinstall.log.
    NX> 700 Compiling the USB module.
    NX> 700 Installing: nxplayer version: 6.9.2.
    NX> 700 Using installation profile: Fedora.
    NX> 700 Install log is: /usr/NX/var/log/nxinstall.log.
    NX> 700 To connect the remote printer to the local desktop,
    NX> 700 the user account must be a member of the CUPS System Group: sys.
    NX> 700 Install completed at: Sat Dec 28 11:06:55 2019.
    
    Verifying        : nomachine-enterprise-client-6.9.2-1.x86_64             1/1
    Installed products updated.
    
    Installed:
      nomachine-enterprise-client-6.9.2-1.x86_64
    
    Complete!
    
    $ rpm -ql nomachine-enterprise-client-6.9.2-1.x86_64
    /etc/NX
    /etc/NX/player
    /etc/NX/player/localhost
    /etc/NX/player/localhost/player.cfg.sample
    /etc/NX/player/packages
    /etc/NX/player/packages/nxclient.tar.gz
    /etc/NX/player/packages/nxplayer.tar.gz
    /usr/NX

         
