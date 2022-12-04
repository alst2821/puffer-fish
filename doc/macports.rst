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

  port upgrade outdated

