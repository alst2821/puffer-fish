======
 mock
======

Notes about building a package in mock using fedora.

Running mock
------------
::
   
  mock -r epel-7-x8664 –init

Now I need to grab a source rpm from centos to try building.

The `guide <https://wiki.centos.org/Sources>`_ to obtain the sources
from centos explains that I should use the script "getsources.sh" to
download sources from the lookaside repository. The script is part of
the `centos git common repository <https://git.centos.org/r/centos-git-common.git>`_.

I chose to build emacs. I cloned the `emacs centos rpm <https://git.centos.org/git/rpms/emacs.git>`_ project in a local folder.

The commands are::
  
  SCRIPTDIR=/home/polka/centos/centos-git-common ${SCRIPTDIR}/getsources.sh rpmbuild –nodeps –define "%topdir /home/polka/centos/sources/emacs" -bs SPECS/emacs.spec

The result of this last step was a src rpm file emacs-24.3-20.fc28.src.rpm

Building the rpm under mock
---------------------------

I invoked the mock command::

  mock -r epel-7-x8664 emacs-24.3-20.fc28.src.rpm

Mock started fetching rpms from the repositories as per its
configuration [#]_. It turns out that the yum cache is not enabled. The
documentation of the yum plugin [#]_ indicates what entries there
should be for the yum cache to be active.

   
The `documentation <https://github.com/rpm-software-management/mock/wiki>`_ [#]_ shows that there are four places where the mock configuration could go. The yum plugin could be configured for the local user using ~/.mock/user.cfg


.. [#] epel 7 mock configuration path: /etc/mock/epel-7-x86_64.cfg
       
.. [#] plugin yum cache user documentation url: https://github.com/rpm-software-management/mock/wiki/Plugin-YumCache accessed 15 Sep 2018

.. [#] The locations are /etc/mock/site-defaults.cfg etc/mock/<buildroot>.cfg ~.mock/user.cfg ~/.config/mock.cfg (since mock-1.2.15)

::
   
  config_opts['pluginconf']['yumcacheenable'] = True
  config_opts['pluginconf']['yumcacheopts'] = {}
  config_opts['pluginconf']['yumcacheopts']['maxagedays'] = 30
  config_opts['pluginconf']['yumcacheopts']['maxmetadataagedays'] = 30
  config_opts['pluginconf']['yumcacheopts']['dir'] = "%(cachetopdir)s/%(root)s/%(packagemanager)scache/"
  config_opts['pluginconf']['yumcacheopts']['targetdir'] = "var/cache/%(packagemanager)s"
  config_opts['pluginconf']['yumcacheopts']['online'] = True

mock yum cache
--------------

With the configuration modified as in the previous section, mock is
saving the rpm files locally under /var/cache/mock

The packages will occupy space in the /dev/mapper/fedora-root partition, currently 34% full and with 31G available.

After building the package the disk usage is 38% in
/dev/mapper/fedora-root and there are 30G available.

Result
------

The result of the mock invocation was a set of rpm packages and a
source rpm package. All were placed in a 'results' folder [#]_. 

.. [#] mock result folder. path: /var/lib/mock/epel-7-x86_64/result 

       
