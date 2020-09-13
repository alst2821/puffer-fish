.. _ref-matplotlib:

============
 matplotlib
============

Documentation links are:

* `Matplotlib developers' guide`_ (Accessed July 2019)
* `Matplotlib usage guide`_ 

.. _`Matplotlib developers' guide`: https://matplotlib.org/devel/index.html#developers-guide-index
.. _`Matplotlib usage guide`: https://matplotlib.org/faq/usage_faq.html


There are two methods to interface matplotlib:

* The `pyplot API`_, that has a subsection of the `examples`_ and a `tutorial`_.
  Details are shown in a `separate page`_. The documentation says:

    pyplot is mainly intended for interactive plots and simple cases
    of programmatic plot generation
  
The main parts of the object oriented API mentioned are the `axes`_
and `figure`_ documentation references.

.. _`axes`: https://matplotlib.org/3.1.1/api/axes_api.html#matplotlib.axes.Axes

.. _`figure`: https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.figure.Figure.html#matplotlib.figure.Figure

.. _`pyplot API`: https://matplotlib.org/3.1.1/api/index.html#the-pyplot-api
.. _`separate page`: https://matplotlib.org/3.1.1/api/_as_gen/matplotlib.pyplot.html
.. _`examples`: https://matplotlib.org/3.1.1/gallery/index.html#pyplots-examples
.. _`tutorial`: https://matplotlib.org/3.1.1/tutorials/introductory/pyplot.html


* The object-oriented API.
  This is described further down on the `API page`_
  
.. _`API page`:  https://matplotlib.org/3.1.1/api/index.html#the-object-oriented-api


* `The matplotlib FAQ <https://matplotlib.org/3.1.1/faq/index.html>`_

* `The Matplotlib Developer's guide`_ 

* `John Hunter excellence in plotting contest`_

.. _`The Matplotlib Developer's guide` : https://matplotlib.org/devel/coding_guide.html
.. _`John Hunter excellence in plotting contest` : https://jhepc.github.io/index.html


Simple bar plotting example that colours bars in two colours.

This is based on the example from the documentation
`'Scores by group and gender' <https://matplotlib.org/3.1.1/gallery/lines_bars_and_markers/barchart.html#sphx-glr-gallery-lines-bars-and-markers-barchart-py>`_::

  import matplotlib
  import matplotlib.pyplot as plt
  import numpy as np
  
  labels = [    "G1", "G2", "G3", "G4",
                "G5", "G6", "G7", "G8"]
  controls = [ False, True, False, True,
               True, True, False, False]
  no_members = [30, 25, 22, 16, 15, 12, 5, 3]
  
  x = np.arange(len(labels))  # the label locations
  width = 0.35  # the width of the bars
  
  fig, ax = plt.subplots()
  rects1 = ax.bar(x, no_members, width)
  
  # Add some text for labels, title and custom x-axis tick labels, etc.
  ax.set_ylabel('No of members')
  ax.set_title('Head Count')
  ax.set_xticks(x)
  ax.set_xticklabels(labels)
  ax.legend()
  
  
  def autolabel(rects):
      """Attach a text label above each bar in *rects*, displaying its height."""
      count = 0
      for rect in rects:
          if controls[count]:
              rect.set_color('r')
          height = rect.get_height()
          ax.annotate('{}'.format(height),
                      xy=(rect.get_x() + rect.get_width() / 2, height),
                      xytext=(0, 3),  # 3 points vertical offset
                      textcoords="offset points",
                      ha='center', va='bottom')
          count = count + 1
  
  
  autolabel(rects1)
  
  fig.tight_layout()
  
  plt.show()

