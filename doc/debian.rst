=======================================
 Notes on debian system administration
=======================================

Notes taken over 10 years ago, when I used to work with Debian
systems.

How to get the list of packages installed
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::
   
   dpkg --list

To remove subversion::

  apt-get remove subversion
  apt-get remove libsvn0

How to know which packages may be upgraded
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
::

   apt-show-versions -u

Raid disk stuff
^^^^^^^^^^^^^^^

RAID-1 mirror reconstruction notes. These I have not used since 2008,
so ``man mdadm`` may have much better information!

Mark as failed::

  mdadm /dev/md0 -f /dev/hda1

Remove from array::

  mdadm /dev/md0 -r /dev/hda1

Add to array as spare::

  mdadm -a /dev/hda1

Debian sources.list for apt
^^^^^^^^^^^^^^^^^^^^^^^^^^^

The `sources list page`_ on the debian wiki explains what one has to
add to the apt/sources.list file to use contrib non-free

.. _`sources list page`: https://wiki.debian.org/SourcesList


Notes about debian packaging
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* Per Abrahamsen, `"Distribute a single executable as a .deb file"`_.
  Per Abrahamsen's blog. March 2016.  Notes from packaging an
  executable in a debian package. [#fn1]_

* Lucas Nussbaum, `"Debian packaging tutorial"`_ (pdf). debian.org
  site. 89 slides.  Aug 2017. [#fn2]_

Slide 7 explains that a .deb archive is an "ar" (archive, as processed
by the library tool ar)::
  
  $ ar tv wget_1 .12 -2.1 _i386.deb
  
The command above wil extract the components, a binary, a control and
a data component.

* `Building tutorial`_. Debian Wiki. [#fn1]_

.. _`"Distribute a single executable as a .deb file"`: http://per-abrahamsen.blogspot.co.uk/2016/03/distribute-single-executable-as-deb-file.html

.. _`"Debian packaging tutorial"`: https://www.debian.org/doc/manuals/packaging-tutorial/packaging-tutorial.en.pdf

.. _`Building tutorial`: https://wiki.debian.org/BuildingTutorial


.. rubric:: Footnotes

.. [#fn1] Accessed Aug 2019
	     
.. [#fn2] Accessed March 2018
          
