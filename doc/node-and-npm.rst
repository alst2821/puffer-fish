====
Node
====

References that I gather as I start using node.

* website: https://nodejs.org/

===
npm
===

Links related to npm.

* website https://www.npmjs.com/

* port of npm https://ports.macports.org/port/npm10/details/

The stack overflow question `here
<https://stackoverflow.com/questions/18088372>`_ gives indications on
how to overcome the limitation to install npm globally.

The recipe is to use::

  npm config set prefix '~/.local/'

  mkdir -p ~/.local/bin

  echo 'export PATH="$HOME/.local/bin/:$PATH"' >> ~/.zshrc


This is assuming that the machine/account is using zsh, otherwise
change .zshrc for .bashrc or similar.

