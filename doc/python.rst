.. _ref-python:

======================
 Python related links
======================

* `Advanced python`_. Lecture on python by Thomas Wouters at Google. 21 Feb 2007 [#fn1]_
* `reddit channel for python`_
* `Numpy for Matlab users`_ (Accessed July 2019)

* `pandas dataframe reference`_

.. _`Advanced python`: https://www.youtube.com/watch?v=HlNTheck1Hk
.. _`reddit channel for python`: http://www.reddit.com/r/python
.. _`Numpy for Matlab users`: https://docs.scipy.org/doc/numpy/user/numpy-for-matlab-users.html
.. _`pandas dataframe reference`: https://pandas.pydata.org/pandas-docs/stable/reference/api/pandas.DataFrame.html?highlight=dataframe#pandas.DataFrame

.. rubric:: Footnotes

.. [#fn1] Accessed on 28 Aug 2019

:ref:`Matplotlib <ref-matplotlib>` (separate page).


`Managing dependencies — Reinout van Rees's website <http://reinout.vanrees.org/weblog/2009/12/17/managing-dependencies.html>`_
Article from 2009 about Managing dependencies.
     
`PyFormat <https://pyformat.info/>`_: Examples of using format() in python

Old talk by Aaron Meurer:
`10 awesome features of Python you cannot do because you are still using Python 2 <https://asmeurer.github.io/python3-presentation/slides.html>`_
9 April 2014 at APUG

`Python documentation in info format <https://sites.google.com/site/roneau2010/computer-software/emacs/python-documentation>`_ (useful with a powerful info reader like emacs).

Example using datetime
----------------------

The documentation of the `datetime module
<https://docs.python.org/3.7/library/datetime.html>`_ indicates that
there are these objects:
* datetime
* time
* timezone

.. code:: python

    import datetime
    import time
    b= 1261228562.0
    print(b)
    a = datetime.datetime.fromtimestamp(b)
    print(a)

Style guide
-----------


* `Google python style guide`_ (part of the general `style guides`_).
  These guides are kept in a "styleguide" `github repo`_.

.. _`Google python style guide`: https://google.github.io/styleguide/pyguide.html
.. _`style guides`: https://google.github.io/styleguide/
.. _`github repo`: https://github.com/google/styleguide

* `Fluent python book by Luciano Ramalho (O'Reilly 2015) <http://shop.oreilly.com/product/0636920032519.do>`_.
  The `example code <https://github.com/fluentpython/example-code>`_ is in github.
  

Virtualenv
----------

Turns out that virtualenv_ is not the same as venv_

I finally read a `stack overflow article/question <https://stackoverflow.com/questions/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe>`_ (Jan 2017) that clarifies what
is what and there's a good `link to explain pipenv <https://realpython.com/pipenv-guide/#problems-that-pipenv-solves>`_ in realpython.com

I think I like the answer from Rias Rizvi suggesting that one should
generally use venv for python 3.3 and newer. Since python 2 is
deprecated, it sounds like there is no need to use virtualenv.

Then there also is pipenv_. And pipenv uses virtualenv instead of venv. 

.. _virtualenv : https://virtualenv.pypa.io/en/latest/
.. _venv: https://docs.python.org/3/library/venv.html
.. _pipenv: https://pipenv.pypa.io/en/latest/

