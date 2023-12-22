===========
 OSX notes
===========

When using a terminal from the 'Terminal' app on a Mac, I noticed
quickly that the meta key used in emacs and readline at linux
terminals does not operate as expected.

The solution is a checkbox labelled 'Use option as meta key'.

This is available from the app preferences menu, in the keyboard tab.

A `nice description with screenshots in osxdaily
<http://osxdaily.com/2013/02/01/use-option-as-meta-key-in-mac-os-x-terminal/>`_ [#f1]_
taught me that. Thanks!

However when using a terminal, this gets in the way of typing
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

.. [#f1] Accessed on 27 July 2019.
	
