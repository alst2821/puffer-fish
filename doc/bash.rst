======
 Bash
======

Colouring the bash prompt
-------------------------

I am entering this to document a favourite sequence for PS1::

  PS1="\[\033[1;34m\][\D{%a %d.%m.%y} \t \u@\h \w]$\[\033[0m\] "
  export PS1

The colours are shown in `section 6.1
<https://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/x329.html>`_ of the
`Bash Prompt HOWTO`_.

.. _`Bash Prompt HOWTO` : https://www.tldp.org/HOWTO/Bash-Prompt-HOWTO/index.html

Style
-----

* `bashate
  <http://docs.openstack.org/developer/bashate/readme.html>`_, also in
  `pypi <https://pypi.python.org/pypi/bashate>`_ is an automated style
  checker for bash scripts to fill the same part of code review that
  pep8 does in (python).

* `shellcheck <https://www.shellcheck.net/>`_
  "It's really useful for keeping bash scripts a little more consistent"
  (This one is packaged for Fedora).

::
   
   $ sudo dnf install ShellCheck
   $ shellcheck myscript.sh

Stderr in red
-------------

`Methods to show stderr in red <https://serverfault.com/questions/59262/bash-print-stderr-in-red-color>`_

Method 1: Use process substitution::

  command 2> >(sed $'s,.*,\e[31m&\e[m,'>&2)

Method 2: Create a function in a bash script::

  color()(set -o pipefail;"$@" 2>&1>&3|sed $'s,.*,\e[31m&\e[m,'>&2)3>&1

Use it like this::

  $ color command

Both methods will show the command's stderr in red.
