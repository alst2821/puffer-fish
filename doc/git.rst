===========
 Git notes
===========

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

