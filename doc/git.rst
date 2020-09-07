===========
 Git notes
===========

* `Git Everyday <https://mirrors.edge.kernel.org/pub/software/scm/git/docs/giteveryday.html>`_

* `Git user manual <https://mirrors.edge.kernel.org/pub/software/scm/git/docs/user-manual.html>`_

* `A successful git branching model
  <https://nvie.com/posts/a-successful-git-branching-model/>`_ by
  Vincent Driessen

* `Git magic`_ is a book that is kept in a git repo and `also in github <https://github.com/blynn/gitmagic>`_
  
.. _`Git magic`: http://www-cs-students.stanford.edu/~blynn/gitmagic/


Links about rewriting history:

`Section 7.6`_ of the `Pro Git book`_ by git evangelist Scott Chacon
and Ben Straub talks about rewriting history.

In essence, the command one wants is::

  git commit --amend

I also found a variant (from `ref 1`_)::

  git commit --amend -author="Author Name <email@address.com>"


.. _`Section 7.6`: https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History

.. _`Pro Git book`: https://git-scm.com/book/en/v2

.. _`ref 1`: https://confluence.atlassian.com/bitbucketserverkb/how-do-you-make-changes-on-a-specific-commit-779171729.html

=======
 Magit
=======

Magit is an emacs based git package. I use magit_ and I sometimes find
it convenient.

.. _magit: https://magit.vc/manual/magit/index.html

The user manual gets installed as info pages in emacs, but there is a
version online `too <https://magit.vc/manual/magit/index.html>`_

Installation
------------

The melpa method is::

  (require 'package)
  (add-to-list 'package-archives
             '("melpa" . "http://melpa.org/packages/") t)

  M-x package-refresh-contents RET
  M-x package-install RET magit RET

