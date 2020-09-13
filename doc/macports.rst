========
Macports
========

The macports page is `macports <https://www.macports.org/>`_.

To install a port, use::

  sudo port install <name-of-port>

For example::

  sudo port install py37-sphinx

The list of ports is available in the `macports pages
<https://www.macports.org/ports.php>`_.

To find the list from the console, type::

  port list

  $ port list | wc
  21635   64905 1427449

It is a long list of over 21000 ports as of July 2019.

The python related ports are almost 7000!

There is a `guide <https://guide.macports.org/>`_ and a `wiki
<https://guide.macports.org/>`_.  The mailing list is somewhat active
and the ports are relatively up to date. For example emacs 26 is
avavailable.

Commands sometimes used
-----------------------

To get a list of updates::

  port list outdated

Investigation of the folders used by macports
---------------------------------------------

There is a man page 'porthier' that shows the port files hierarchy.

Under the location /opt/local/var/macports/registry/portfiles I found
a hierarchy of files for every port installed.

This is quite interesting. The Portfile for the sphinx port installed
on this laptop has interesting information that was possibly displayed
when I was installing it, but I had not payed attention to.

It is the 'notes' section of the portfile. It has dollar substitutions
too.

    To make the Python ${python.branch} version of Sphinx the one that
    is run when you execute the commands without a version suffix,
    e.g. 'sphinx-build', run:

    port select --set ${select.group} [file tail ${select.file}]

And the select.group and select.file entries are defined somewhere
else in the Portfile.

    select.group    sphinx
    select.file     ${filespath}/py${python.version}-sphinx

Now, where is the docutils and sphinx documentation?

The ports documentation is in a useful man page that shows examples of
the commands to select the default python and sphinx::

  port select --list python
  port select --set python python37
  sudo port select --set python python37
  port select --list python
  port select --summary
  sudo port select --set sphinx py37-sphinx

