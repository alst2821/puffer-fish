=======
 Emacs
=======

.. toctree::
   :maxdepth: 2

   emacs

.. _ref-emacs-sec1:

Useful functions
----------------

The example functions below use the prefix "pf-".

Function to copy file marked in dired to the kill-ring::

  (defun pf-copy-filename-as-kill (args)
      (interactive "P")
     (let ( (string
             (mapconcat
              (function identity) (dired-get-marked-files) " ")))
       (kill-new string)
       (message "%s" string)))
       
This gets the function above mapped to "K" in dired::

  (add-hook 'dired-load-hook
          (lambda ()
            (define-key dired-mode-map "K"
              'pf-copy-filename-as-kill)))

This function emulates vim-exec::

  (defun pf-emulate-vim-exec ()
       "Command to emulate vim's .! command"
       (interactive)
       (let (start end command result)
          (save-excursion
             (beginning-of-line)
             (setq start (point))
             (end-of-line)
             (setq end (point))
             (setq command (buffer-substring start end)) )
          (end-of-line)
          (setq result (shell-command-to-string command))
          (insert "\n")
          (setq start (point))
          (insert result)
          (setq end (point))
          (insert
           (concat
            (format "\n=== %d line(s) inserted\n" (count-lines start end))))
          ))

These functions are similar to vim's `*` command::

  (add-hook 'isearch-mode-hook 'pf-isearch-yank-word-hook)

  (defun pf-isearch-yank-word-hook ()
  (when (equal this-command 'pf-isearch-word-at-point)
    (let ((string (concat "\\<"
                          (buffer-substring-no-properties
                           (progn (skip-syntax-backward "w_") (point))
                           (progn (skip-syntax-forward "w_") (point)))
                          "\\>")))
      (if (and isearch-case-fold-search
               (eq 'not-yanks search-upper-case))
          (setq string (downcase string)))
      (setq isearch-string string
            isearch-message
            (concat isearch-message
                    (mapconcat 'isearch-text-char-description
                               string ""))
            isearch-yank-flag t)
      (isearch-search-and-update))))

  (defun pf-isearch-word-at-point ()
    (interactive)
    (call-interactively 'isearch-forward-regexp))

  (global-set-key (kbd "C-c *") 'pf-isearch-word-at-point)

.. _ref-emacs-sec2:

Emacs tips
----------

Remove empty lines::

  M-x flush-lines RET ^$ RET

  (flush-lines REGEXP &optional RSTART REND INTERACTIVE)

Delete lines containing matches for REGEXP.  When called from Lisp
(and usually when called interactively as well, see below), applies to
the part of the buffer after point.  The line point is in is deleted
if and only if it contains a match for regexp starting after point.

Keep lines::

    M-x keep-lines

Does the opposite of `flush-lines`, removes lines that don't contain
matches.

To change the tab-width of emacs, use::

    M-x eval-expression
    (setq tab-width 8)

.. _ref-emacs-sec3:

Compilation window using colours
--------------------------------

This lisp initialization allows a build on the compilation buffer to
show ansi escape codes okay::
  
  (add-hook 'compilation-filter-hook
	  (lambda ()
	    (ansi-color-apply-on-region compilation-filter-start (point))))

    
dired-x and .dired file
-----------------------

To ignore dot files in the output, set this into a ".dired" file::

  Local Variables:
  dired-omit-mode: t
  dired-actual-switches: "-l"
  End:

Spelling
--------

Add in customization the entry for ``ispell-program-name``::

  ispell-program-name "/usr/bin/hunspell"

or add this line in ``~/.emacs``::

  (setq ispell-program-name "/usr/bin/hunspell")

Convert line endings
--------------------

To convert to DOS or to Unix line endings [#fn1]_:

* Method 1: click on the indicator in the status line. Possible
  options are ":" for default encoding, (DOS) or (unix). Then save the
  file.

* Method 2: Run the command::

    C-x RET f (set-buffer-file-coding-system)
    
  and type unix/dos for unix encoding. This will change the encoding
  of newlines without changing the encoding of other characters.

  You can also change the encoding of other characters by typing
  something like utf-8-unix.

Navigate C sources
------------------
Use the commands [#fn2]_::
  
  c-backward-conditional

  c-forward-conditional

  c-up-conditional

.. rubric:: Footnotes
.. [#fn1] Source: Emacs Stack Exchange `question <https://emacs.stackexchange.com/questions/5779/>`_ from 2014 by user Charo	    
.. [#fn2] Peter Lee, `"Matching #ifdefs..." <https://lists.gnu.org/archive/html/help-gnu-emacs/2003-01/msg01000.html>`_ in help-gnu-emacs mailing list. 31 Jan 2003.
  
Tramp on remote server
----------------------

There are many tips in the `tramp page of emacs wiki
<https://www.emacswiki.org/emacs/TrampMode>`_ and there is the 
`User Manual <http://www.gnu.org/software/emacs/manual/html_node/tramp/index.html>`_.

I have a selection below:

How to use tramp to edit a file on a remote machine. Use::

  M-x find-file RET /scp:username@servername:/path/to/file

How to use tramp to edit a file as root. Use::

  M-x find-file RET /su::/etc/hosts RET

Tramp from windows using plink (tested in the past with PuTTY's plink and Pageant running)::

  C-x C-f /plink:USERNAME@SERVER:.emacs RET
  
The general syntax is::

  tramp open file syntax:
  /<user>@<host>:/path/to/file or
  /<protocol>:<user>@<host>:/path/to/file
  
Chinese chars when UTF-16 file read
-----------------------------------

This happens to me with the xml files from a program that erroneously
advertises the xml as UTF-16.

The solution, to show the xml normally (utf-8) is.

.. code:: 
	  
  M-x revert-buffer-with-coding-system

and choose ``binary`` encoding.

Windows notes
-------------

Make emacs move files to trash when deleting::

  (setq delete-by-moving-to-trash t)

(Found in `masteringemacs.com <https://www.masteringemacs.org/article/making-deleted-files-trash-can>`_).

Creating info files from sphinx content
---------------------------------------

The content of a sphinx set of documents can be made in the info
format usually by callink `make info` instead of `make html`.

The result is a texi file that can be further processed into an info.

The emacs manual `(*)
<https://www.gnu.org/software/emacs/manual/html_node/efaq/Installing-Texinfo-documentation.html>`_
explains that to browse this content as an info file in emacs, one can
invoke the info file directly using `C-u M-x info RET` followed by the
file name.

Alternatively, use `M-x Info-goto-node` and enter the info file in
brackets.

Notetaking macro
----------------

Prototype interactive function to select words and place them in a note file.::

    (defun pf-takenote ()
      (interactive)
      (let ( p1 p2 s)
        (save-excursion 
          (forward-word)
          (backward-word)
          (setq p1 (point))
          (forward-word)
          (setq p2 (point))
          (setq s (buffer-substring-no-properties p1 p2))
          (set-buffer "notes-file.txt")
          (goto-char (point-max))
          (insert s)
          (insert " \n"))
          (forward-word)))
    
    (global-set-key (kbd "<f5>") 'pf-takenote)

Emacs related links
-------------------

* `Emacs-devel mailing list archive
  <https://lists.gnu.org/archive/html/emacs-devel/>`_.
* `help-gnu-emacs mailing list archive
  <https://lists.gnu.org/archive/html/help-gnu-emacs/>`_.

Here is a link to some `emacs tips
<https://sites.google.com/site/roneau2010/computer-software/emacs>`_.

Using emacs ``M-x compile`` to generate windows targets
-------------------------------------------------------

Use a script similar to the one below. It was obtained from an
environment as populated by ``vcvars.bat`` (visual studio command line
compiler invocation batch file).  Name it "emacs-env.bat".  Then one
can use the emacs M-x compile command to invoke visual studio so::

  M-x compile RET
  X:/path/to/script/emacs-env.bat make RET

.. code:: batch
	  
 @set CommandPromptType=Native
 @set Framework35Version=v3.5
 @set FrameworkDir=C:\Windows\Microsoft.NET\Framework64
 @set FrameworkDIR64=C:\Windows\Microsoft.NET\Framework64
 @set FrameworkVersion=v4.0.30319
 @set FrameworkVersion64=v4.0.30319
 @set FSHARPINSTALLDIR=c:\Program Files (x86)\Microsoft F#\v4.0\
 @set INCLUDE=c:\Program Files (x86)\Microsoft Visual Studio 10.0\VC\INCLUDE
 @set INCLUDE=%INCLUDE%;c:\Program Files (x86)\Microsoft Visual Studio 10.0\VC\ATLMFC\INCLUDE
 @set INCLUDE=%INCLUDE%;C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\include
 @set LIB=c:\Program Files (x86)\Microsoft Visual Studio 10.0\VC\LIB\amd64
 @set LIB=%LIB%;c:\Program Files (x86)\Microsoft Visual Studio 10.0\VC\ATLMFC\LIB\amd64
 @set LIB=%LIB%;C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\lib\x64
 @set LIBPATH=C:\Windows\Microsoft.NET\Framework64\v4.0.30319
 @set LIBPATH=%LIBPATH%;C:\Windows\Microsoft.NET\Framework64\v3.5
 @set LIBPATH=%LIBPATH%;c:\Program Files (x86)\Microsoft Visual Studio 10.0\VC\LIB\amd64
 @set LIBPATH=%LIBPATH%;c:\Program Files (x86)\Microsoft Visual Studio 10.0\VC\ATLMFC\LIB\amd64
 @set path=
 @set path=%path%;c:\python27\
 @set path=%path%;c:\perl64\site\bin
 @set path=%path%;c:\perl64\bin
 @set path=%path%;c:\windows\system32
 @set path=%path%;c:\windows
 @set path=%path%;c:\windows\system32\wbem
 @set path=%path%;c:\windows\system32\windowspowershell\v1.0\
 @set path=%path%;c:\program files (x86)\microsoft sql server\100\tools\binn\
 @set path=%path%;c:\program files\microsoft sql server\100\tools\binn\
 @set path=%path%;c:\program files\microsoft sql server\100\dts\binn\
 @set path=%path%;c:\program files (x86)\subversion\bin
 @set path=%path%;c:\windows\system32
 @set path=%path%;c:\program files\tortoisesvn\bin
 @set path=%path%;c:\matlab2011b\bin
 @set path=%path%;c:\program files\matlab\r2011b\bin
 @set path=%path%;c:\program files\dell\sysmgt\oma\bin
 @set path=%path%;c:\program files\dell\sysmgt\shared\bin
 @set path=%path%;c:\program files\dell\sysmgt\idrac
 @set path=%path%;c:\anaconda
 @set path=%path%;c:\anaconda\scripts
 @set path=%path%;c:\program files (x86)\git\cmd
 @set path=%path%;c:\program files (x86)\microsoft visual studio 10.0\vc\bin\amd64
 @set path=%path%;c:\windows\microsoft.net\framework64\v4.0.30319
 @set path=%path%;c:\windows\microsoft.net\framework64\v3.5
 @set path=%path%;c:\program files (x86)\microsoft visual studio 10.0\vc\vcpackages
 @set path=%path%;c:\program files (x86)\microsoft visual studio 10.0\common7\ide
 @set path=%path%;c:\program files (x86)\microsoft visual studio 10.0\common7\tools
 @set path=%path%;c:\program files (x86)\html help workshop
 @set path=%path%;c:\program files (x86)\microsoft sdks\windows\v7.0a\bin\netfx 4.0 tools\x64
 @set path=%path%;c:\program files (x86)\microsoft sdks\windows\v7.0a\bin\x64
 @set path=%path%;c:\program files (x86)\microsoft sdks\windows\v7.0a\bin
 @set path=%path%;c:\python27\
 @set path=%path%;c:\windows\system32
 @set path=%path%;c:\windows
 @set path=%path%;c:\windows\system32\wbem
 @set path=%path%;c:\windows\system32\windowspowershell\v1.0\
 @set path=%path%;c:\program files (x86)\microsoft sql server\100\tools\binn\
 @set path=%path%;c:\program files\microsoft sql server\100\tools\binn\
 @set path=%path%;c:\program files\microsoft sql server\100\dts\binn\
 @set path=%path%;c:\program files (x86)\subversion\bin
 @set path=%path%;c:\windows\system32
 @set path=%path%;c:\program files\tortoisesvn\bin
 @set path=%path%;c:\matlab2011b\bin
 @set path=%path%;c:\program files\matlab\r2011b\bin
 @set path=%path%;c:\program files\dell\sysmgt\oma\bin
 @set path=%path%;c:\program files\dell\sysmgt\shared\bin
 @set path=%path%;c:\program files\dell\sysmgt\idrac
 @set path=%path%;c:\anaconda
 @set path=%path%;c:\anaconda\scripts
 @set path=%path%;c:\program files (x86)\gnuwin32\bin
 @set path=%path%;c:\program files (x86)\vim\vim73
 @set path=%path%;c:\program files (x86)\re2c
 @set Platform=X64
 @set VCINSTALLDIR=c:\Program Files (x86)\Microsoft Visual Studio 10.0\VC\
 @set VS100COMNTOOLS=C:\Program Files (x86)\Microsoft Visual Studio 10.0\Common7\Tools\
 @set VSINSTALLDIR=c:\Program Files (x86)\Microsoft Visual Studio 10.0\
 @set WindowsSdkDir=C:\Program Files (x86)\Microsoft SDKs\Windows\v7.0A\
 %*
 
