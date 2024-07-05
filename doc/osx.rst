===========
 OSX notes
===========

Links for the Mac OS user guide [#f1]_:

* `Monterrey (12) <https://support.apple.com/en-gb/guide/mac-help/welcome/12.0/mac>`_

* `Sonoma (14) <https://support.apple.com/en-gb/guide/mac-help/mchld1690538/14.0/mac/14.0>`_
  

Notes on using the terminal
^^^^^^^^^^^^^^^^^^^^^^^^^^^

When using a terminal from the 'Terminal' app on a Mac, the key
labelled "alt" can be configured to be the "meta key" for convenient
use in emacs and for readline at the command prompt.

To do this select "use option as meta key".

Navigation is Preferences >> Tab "profiles" >> Sub tab "keyboard" and
check the box at the bottom labelled 'Use option as meta key'. [#f2]_

HOWEVER, when using a terminal, this gets in the way of typing
accented characters using the option key.
The configuration of emacs to use the modifier can be added to the .emacs file
::
   
     (setq ns-right-alternate-modifier (quote none))

Notes on tmux and terminfo
^^^^^^^^^^^^^^^^^^^^^^^^^^

I found that MacOS 12 (Monterrey) comes with an old version of ncurses (5.7).
The terminal gets confused when using macports applications that are compiled
against a newer version of curses.
This is particularly noticeable when using tmux.
Tmux uses the TERM type tmux-256color.

The faboulous `guide <https://gpanders.com/blog/the-definitive-guide-to-using-tmux-256color-on-macos/>`_ by Gregory Anders shows a method to copy the terminfo
from the new version of ncurses to the built-in version of ncurses.

What I used on my system was::

  $ /opt/local/bin/infocmp -x tmux-256color > ~/tmux-256color.src

Now, modify the tmux-256color.src file to change the `pairs` value from
65536 to 32767. This must be done because of a bug in ncurses 5.7 that
interprets pairs#65536 as pairs#0.

Then load this to the terminfo database::

  $ /usr/bin/tic -x -o $HOME/.local/share/terminfo tmux-256color.src

And I added TERMINFO_DIRS to .zshrc::

  if [[ -v TERMINFO_DIRS ]]; then
   TERMINFO_DIRS=$TERMINFO_DIRS:$HOME/.local/share/terminfo
  else
    TERMINFO_DIRS=$HOME/.local/share/terminfo
  fi
  export TERMINFO_DIRS


.. rubric:: Footnotes

.. [#f1] (accessed 5 July 2024)
         
.. [#f2] Thanks to `osxdaily <http://osxdaily.com/2013/02/01/use-option-as-meta-key-in-mac-os-x-terminal/>`_,
         (accessed 27 July 2019)
	
