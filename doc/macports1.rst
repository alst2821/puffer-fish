================
Macports folders
================

This is my investigation of the folders used by macports. There is a
man page 'porthier' that shows the port files hierarchy.

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

