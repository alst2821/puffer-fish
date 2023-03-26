
==========
 Gnu make
==========

Two blog posts by John Graham-Cumming, author of the `GNU Make Book`_.

* `The one line you should add to every makefile`_

* `One weird trick that will give you makefile X-ray vision`_

*  `Debugging Makefiles`_ by John Graham-Cumming. Feb 2007. An even older article in Dr Dobbs, now linked through the web-archive. [#fn1]_

* `The GNU Make Debugger` http://gmd.sourceforge.net/

.. _`GNU Make Book`: https://nostarch.com/gnumake

.. _`The one line you should add to every makefile` : https://blog.jgc.org/2015/04/the-one-line-you-should-add-to-every.html

.. _`One weird trick that will give you makefile X-ray vision` : https://blog.jgc.org/2015/04/one-weird-trick-that-will-give-you.html


.. _`Debugging Makefiles`: https://web.archive.org/web/20131005160756/http://www.drdobbs.com/tools/debugging-makefiles/197003338

.. rubric:: Footnotes
.. [#fn1] Accessed on 28 Aug 2019
	  
This is a note of a command I used to find the targets from a make::

   make -qp | awk -F':' '/^[a-zA-Z0-9][^$#\/\t=]*:([^=]|$)/ {split($1,A,/ /);for(i in A)print A[i]}' | sort -u

(copied from Marc 2377's answer in `stack overflow <https://stackoverflow.com/questions/4219255>`_ on 26 March 2023)
