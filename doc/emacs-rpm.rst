.. _ref-emacs_rpm_for_centos:

====================================
 Notes on creating an emacs package
====================================

16 Sep 2018

The plan is to grab a new version of emacs and package it for rhel7

Not sure if emacs 25 is possible.

I found the location of the emacs mirror [#fn1]_. I then found the
location of the packaging folder where I was working [#fn2]_.

I remember there were problems compiling emacs 26, because in one of
the updates, the minimum version of autoconf had to be higher autoconf
available on rhel7. I skimmed through the "news" [#fn3]_ of the
releases and could not find a mention.

Next: download emacs 25.3 to try compiling it.

Diversion into autoconf version
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

I found a method to chroot into the buildroot for epel to enquire the
version of autoconf used. ::

  mock -r epel-7-x86_64 –shell rpm -qa | grep autoconf

The result was that I am using autoconf 2.69

Baring spec
^^^^^^^^^^^

I am removing all the patches and additional source files to get a
"clean" rpm that reflects emacs sources.

I would like to compare the spec file to the spec file used in
fedora. What was the dnf command to obtain the source rpm?

Even better, one could get the git repo from the fedora equivalent of
git.centos.org using fedpkg.

As I write this piece there are problems using fedpkg to clone "emacs"
unless done anonymously. I found this thanks to a message to the
fedora developers list from user Martin Gansser [#fn4]_. He reported the
error I saw, that even though I can connect to fedorapeople.org using
an ssh-key, the cloning using fedpkg fails with a message "Permission
denied".

Pavel Zhukov diagnosed the problem as something to do with the
versions of the ssh server and the client and pointed to a bug report
in the archlinux domain [#fn5]_. It seems that my ssh client is too new on
this fedora 28 workstation. I am using version 7.8p1-2. There are also
two related bug reports in bugzilla [#fn6]_ , [#fn7]_.

Mock build
^^^^^^^^^^

The build in mock failed because I failed to include the packaged
files in the %files section of the spec file.

After adding the several thousand(!) files in the build, the creation
of the rpm worked okay.

I thought it was an odd thing in the rpm generated that the
description would be followed by the list of files, but it turns out
that the query command I typed on the generated rpm included the "-l"
switch.::

  rpm -qipl /var/lib/mock/epel-7-x86_64/result/emacs-25.3-1.el7.x86_64.rpm

Now I have to test this on a rhel7 system.

.. rubric:: References

.. [#fn1] Example emacs mirror url:
         http://ftp.snt.utwente.nl/pub/software/gnu/emacs/ accessed 16
         Sep 2018
	 
.. [#fn2] Centos source folder path: /home/polka/centos/sources/emacs
	  
.. [#fn3] Release notes in emacs page url:
          https://www.gnu.org/software/emacs/ accessed 16 Sep 2018
	  
.. [#fn4] Thread started by Martin Gansser "fedpkg clone doesn*t work"
          Fedora developers mailing list 10 Sep 2018 archive at url:
          https://lists.fedoraproject.org/archives/list/devel@lists.fedoraproject.org/thread/UBBJCEK5Y7SVZ3EVNGKBIPGJFRHACF7N/#3AE3BW6K62OVEG6LU453QZYHK3Z7V3RC
          accessed 16 Sep 2018

.. [#fn5] OpenSSH client cannot connect to server after client upgrade
          url: https://bugs.archlinux.org/task/59838 accessed 16 Sep
          2018

.. [#fn6] Bugzilla report 1627875 url:
          https://bugzilla.redhat.com/show_bug.cgi?id=1627875

.. [#fn7] Bugzilla report 1623929 url:
          https://bugzilla.redhat.com/show_bug.cgi?id=1623929
