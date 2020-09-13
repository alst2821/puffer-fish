========
 Fedora
========

:ref:`(contents) <ref-fedora-toctree>`

Reference material
------------------

`Fedora Code of Conduct <https://getfedora.org/code-of-conduct>`_.

`Fedora Developer <https://developer.fedoraproject.org/>`_.

`Fedora magazine <http://fedoramagazine.org/>`_

`Start page: https://start.fedoraproject.org/ <https://start.fedoraproject.org/>`_

`Users' mailing list archive <https://lists.fedoraproject.org/pipermail/users/>`_

`Getting started with virtualization (fedoraproject.org)`_

.. _`Getting started with virtualization (fedoraproject.org)`: https://docs.fedoraproject.org/en-US/quick-docs/getting-started-with-virtualization/index.html

I am keeping here a link to `"Beyond Linux From Scratch"`_ which seems to
be an interesting read.  i stumbled upon the page while asking about
initramfs. Accessed okay on 20 Oct 2018.

.. _`"Beyond Linux From Scratch"`: http://www.linuxfromscratch.org/blfs/view/8.1/index.html

Locating documentation
----------------------

From around 2020 fedora are trying to put all documentation together in `docs.fedoraproject.org <https://docs.fedoraproject.org/en-US/docs/>`_.

Have a look at `apps.fedoraproject.org <http://apps.fedoraproject.org/>`_

`Fesco ticketing system <https://fedorahosted.org/fesco/wiki>`_

FESCo is the Fedora Engineering Steering Committee.

`Bugzilla <https://bugzilla.redhat.com/>`_ where reviews and bugs are entered.

Wiki documentation on the various systems (the wiki site is deprecated, so the deep links here work, but the top link takes one to `docs.fedoraproject.org <https://docs.fedoraproject.org/>`_):

Koji: `Using the koji build system <https://fedoraproject.org/wiki/Using_the_Koji_build_system>`_

`Bhodi <https://fedoraproject.org/wiki/Bodhi>`_


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

How to generate a password
--------------------------

I copied examples from `how to geek`_ on password generation::

    openssl rand -base64 32

    date +%s | sha256sum | base64 | head -c 32 ; echo

    < /dev/urandom tr -dc _A-Z-a-z-0-9 | head -c${1:-32};echo;

.. _`how to geek`:
   https://www.howtogeek.com/howto/30184/10-ways-to-generate-a-random-password-from-the-command-line/

How to find the source rpm of an installed package
--------------------------------------------------

This command outputs a source rpm for a package::

    rpm -qa --queryformat='%{NAME} %{SOURCERPM}\n' <package>

For example::

    $ rpm -qa --queryformat='%{NAME} %{SOURCERPM}\n' python3-docutils
    python3-docutils python-docutils-0.14-6.fc30.src.rpm

the list of elements that can go in the query formats comes from::

    rpm --querytags

Setting up a second monitor
---------------------------

For an all-in-one pc with a broken main display running Fedora.

The configuration below allows the pc to operate on a second monitor
ignoring the first monitor.

The configuration file is "monitors.xml" in the folder ~/.config

For gdm to operate the same way, I had to copy it to
/var/lib/gdm/.config::

  <monitors version="2">
    <configuration>
      <logicalmonitor>
        <x>0</x>
        <y>0</y>
        <scale>1</scale>
        <primary>yes</primary>
        <monitor>
          <monitorspec>
            <connector>HDMI-2</connector>
            <vendor>MED</vendor>
            <product>MD 20119</product>
            <serial>0x01010101</serial>
          </monitorspec>
          <mode>
            <width>1280</width>
            <height>1024</height>
            <rate>75.025177001953125</rate>
          </mode>
        </monitor>
      </logicalmonitor>
      <disabled>
        <monitorspec>
          <connector>HDMI-1</connector>
          <vendor>LEN</vendor>
          <product>Lenovo AIO PC</product>
          <serial>000001</serial>
        </monitorspec>
      </disabled>
    </configuration>
  </monitors>


And this is for a newer Lenovo ThinkPad laptop::

  <monitors version="2">
    <configuration>
      <logicalmonitor>
        <x>0</x>
        <y>0</y>
        <scale>1</scale>
        <primary>yes</primary>
        <monitor>
          <monitorspec>
            <connector>eDP-1</connector>
            <vendor>CMN</vendor>
            <product>0x15e5</product>
            <serial>0x00000000</serial>
          </monitorspec>
          <mode>
            <width>1680</width>
            <height>1050</height>
            <rate>59.954250335693359</rate>
          </mode>
        </monitor>
        <monitor>
          <monitorspec>
            <connector>HDMI-2</connector>
            <vendor>DEL</vendor>
            <product>DELL 2407WFP</product>
            <serial>UY5456BE10WS </serial>
          </monitorspec>
          <mode>
            <width>1680</width>
            <height>1050</height>
            <rate>59.883251190185547</rate>
          </mode>
        </monitor>
      </logicalmonitor>
    </configuration>
  </monitors>

gnome-gdm
---------

`Configure monitors for login screen <https://askbot.fedoraproject.org/en/question/36631/configure-monitors-for-login-screen/>`_

Copy the monitor configuration file from a user account where it is
configured properly to the gdm directory:

cp /<user home dir>/.config/monitors.xml /var/lib/gdm/.config/

  
Fedora Packaging
----------------

Fedora uses the `rpm <http://www.rpm.org/>`_ packaging tool.

The documentation includes a `tutorial <http://fedoranews.org/alex/tutorial/rpm/>`_ by Alexandre de Abreu (in Fedora News) [#f1]_.

This is a link to the `draft RPM guide
<https://docs.fedoraproject.org/en-US/Fedora_Draft_Documentation/0.1/html/RPM_Guide/index.html>`_
by Stuart Foster, Stuart Ellis and Ben Cotton.

These are the `Fedora Packaging Guidelines <https://docs.fedoraproject.org/en-US/packaging-guidelines/>`_ [#f2]_.

.. rubric:: Footnotes

.. [#f1] Accessed on 25 August 2019

.. [#f2] Accessed on 25 August 2019

Setting up a vnc session
------------------------

On the linux workstation::

  sudo dnf install tigervnc-server
  vncserver :1 -name <my-session-name> -geometry 1200x850

To set the password::

  vncpasswd

On the Mac OS system (client)::

  open vnc://username:passwd@host-ip:5901

Mock
----

Mock is a chroot environment to build rpms under fedora for various
distributions. This is used in koji, the build system for fedora.

User documentation:
https://github.com/rpm-software-management/mock/wiki

Miroslav Suchy's `article
<http://miroslav.suchy.cz/blog/archives/2015/05/20/why_mock_does_not_work_on_el_6_and_el7_and_how_to_fix_it/index.html>`_
from 2015 about the problem of using mock on EL6 and EL7.  It has to
do with yum being upgraded to dnf. There is a solution...  (article
link)

Find the source rpm for a package
---------------------------------

This command outputs a source rpm for a package::

  rpm -qa --queryformat='%{NAME} %{SOURCERPM}\n' <package>

For example::

   $ rpm -qa --queryformat='%{NAME} %{SOURCERPM}\n' python3-docutils
   python3-docutils python-docutils-0.14-6.fc30.src.rpm

the list of elements that can go in the query formats comes from::

  rpm --querytags

There were 243 entries when I tried it::

  ARCH
  ARCHIVESIZE
  BASENAMES
  BUGURL
  BUILDARCHS
  BUILDHOST
  BUILDTIME
  C
  CHANGELOGNAME
  CHANGELOGTEXT
  CHANGELOGTIME
  CLASSDICT
  CONFLICTFLAGS
  CONFLICTNAME
  CONFLICTNEVRS
  CONFLICTS
  CONFLICTVERSION
  COOKIE
  DBINSTANCE
  DEPENDSDICT
  DESCRIPTION
  DIRINDEXES
  DIRNAMES
  DISTRIBUTION
  DISTTAG
  DISTURL
  DSAHEADER
  E
  ENCODING
  ENHANCEFLAGS
  ENHANCENAME
  ENHANCENEVRS
  ENHANCES
  ENHANCEVERSION
  EPOCH
  EPOCHNUM
  EVR
  EXCLUDEARCH
  EXCLUDEOS
  EXCLUSIVEARCH
  EXCLUSIVEOS
  FILECAPS
  FILECLASS
  FILECOLORS
  FILECONTEXTS
  FILEDEPENDSN
  FILEDEPENDSX
  FILEDEVICES
  FILEDIGESTALGO
  FILEDIGESTS
  FILEFLAGS
  FILEGROUPNAME
  FILEINODES
  FILELANGS
  FILELINKTOS
  FILEMD5S
  FILEMODES
  FILEMTIMES
  FILENAMES
  FILENLINKS
  FILEPROVIDE
  FILERDEVS
  FILEREQUIRE
  FILESIGNATURELENGTH
  FILESIGNATURES
  FILESIZES
  FILESTATES
  FILETRIGGERCONDS
  FILETRIGGERFLAGS
  FILETRIGGERINDEX
  FILETRIGGERNAME
  FILETRIGGERPRIORITIES
  FILETRIGGERSCRIPTFLAGS
  FILETRIGGERSCRIPTPROG
  FILETRIGGERSCRIPTS
  FILETRIGGERTYPE
  FILETRIGGERVERSION
  FILEUSERNAME
  FILEVERIFYFLAGS
  FSCONTEXTS
  GIF
  GROUP
  HDRID
  HEADERCOLOR
  HEADERI18NTABLE
  HEADERIMAGE
  HEADERIMMUTABLE
  HEADERREGIONS
  HEADERSIGNATURES
  ICON
  INSTALLCOLOR
  INSTALLTID
  INSTALLTIME
  INSTFILENAMES
  INSTPREFIXES
  LICENSE
  LONGARCHIVESIZE
  LONGFILESIZES
  LONGSIGSIZE
  LONGSIZE
  MODULARITYLABEL
  N
  NAME
  NEVR
  NEVRA
  NOPATCH
  NOSOURCE
  NVR
  NVRA
  O
  OBSOLETEFLAGS
  OBSOLETENAME
  OBSOLETENEVRS
  OBSOLETES
  OBSOLETEVERSION
  OLDENHANCES
  OLDENHANCESFLAGS
  OLDENHANCESNAME
  OLDENHANCESVERSION
  OLDFILENAMES
  OLDSUGGESTS
  OLDSUGGESTSFLAGS
  OLDSUGGESTSNAME
  OLDSUGGESTSVERSION
  OPTFLAGS
  ORDERFLAGS
  ORDERNAME
  ORDERVERSION
  ORIGBASENAMES
  ORIGDIRINDEXES
  ORIGDIRNAMES
  ORIGFILENAMES
  OS
  P
  PACKAGER
  PATCH
  PATCHESFLAGS
  PATCHESNAME
  PATCHESVERSION
  PAYLOADCOMPRESSOR
  PAYLOADDIGEST
  PAYLOADDIGESTALGO
  PAYLOADFLAGS
  PAYLOADFORMAT
  PKGID
  PLATFORM
  POLICIES
  POLICYFLAGS
  POLICYNAMES
  POLICYTYPES
  POLICYTYPESINDEXES
  POSTIN
  POSTINFLAGS
  POSTINPROG
  POSTTRANS
  POSTTRANSFLAGS
  POSTTRANSPROG
  POSTUN
  POSTUNFLAGS
  POSTUNPROG
  PREFIXES
  PREIN
  PREINFLAGS
  PREINPROG
  PRETRANS
  PRETRANSFLAGS
  PRETRANSPROG
  PREUN
  PREUNFLAGS
  PREUNPROG
  PROVIDEFLAGS
  PROVIDENAME
  PROVIDENEVRS
  PROVIDES
  PROVIDEVERSION
  PUBKEYS
  R
  RECOMMENDFLAGS
  RECOMMENDNAME
  RECOMMENDNEVRS
  RECOMMENDS
  RECOMMENDVERSION
  RECONTEXTS
  RELEASE
  REMOVETID
  REQUIREFLAGS
  REQUIRENAME
  REQUIRENEVRS
  REQUIRES
  REQUIREVERSION
  RPMVERSION
  RSAHEADER
  SHA1HEADER
  SHA256HEADER
  SIGGPG
  SIGMD5
  SIGPGP
  SIGSIZE
  SIZE
  SOURCE
  SOURCEPACKAGE
  SOURCEPKGID
  SOURCERPM
  SUGGESTFLAGS
  SUGGESTNAME
  SUGGESTNEVRS
  SUGGESTS
  SUGGESTVERSION
  SUMMARY
  SUPPLEMENTFLAGS
  SUPPLEMENTNAME
  SUPPLEMENTNEVRS
  SUPPLEMENTS
  SUPPLEMENTVERSION
  TRANSFILETRIGGERCONDS
  TRANSFILETRIGGERFLAGS
  TRANSFILETRIGGERINDEX
  TRANSFILETRIGGERNAME
  TRANSFILETRIGGERPRIORITIES
  TRANSFILETRIGGERSCRIPTFLAGS
  TRANSFILETRIGGERSCRIPTPROG
  TRANSFILETRIGGERSCRIPTS
  TRANSFILETRIGGERTYPE
  TRANSFILETRIGGERVERSION
  TRIGGERCONDS
  TRIGGERFLAGS
  TRIGGERINDEX
  TRIGGERNAME
  TRIGGERSCRIPTFLAGS
  TRIGGERSCRIPTPROG
  TRIGGERSCRIPTS
  TRIGGERTYPE
  TRIGGERVERSION
  URL
  V
  VCS
  VENDOR
  VERBOSE
  VERIFYSCRIPT
  VERIFYSCRIPTFLAGS
  VERIFYSCRIPTPROG
  VERSION
  XPM
