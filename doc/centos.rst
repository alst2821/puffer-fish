========
 CentOS
========

`CentOS - how to rebuild a source RPM`_. (from the CentOS wiki,
accessed July 2019)

.. _`CentOS - how to rebuild a source RPM`:
   https://wiki.centos.org/HowTos/RebuildSRPM

Link to instructions on `how to set up the environment`_. (Also from
the CentOS wiki, accessed July 2019)

.. _`how to set up the environment`:
    https://wiki.centos.org/HowTos/SetupRpmBuildEnvironment
    
Building an RPM for emacs
^^^^^^^^^^^^^^^^^^^^^^^^^

16 Sep 2018

I wrote about creating an emacs rpm :ref:`before
<ref-emacs_rpm_for_centos>`. I was trying to copy it over to a rhel7
system and crashed screen (gnu screen) spectacularly.

It seems that screen is buggy after all. I found a reference to a bug
report that shows the state of screen during a crash [#fn1]_.

The bug report was very interesting, because it mentions that the user
attaches to the running screen session with gdb to obtain a stack
trace. This is very useful, because the screen process was showing
100% cpu usage and I could list it among the processes.

So I enquired how to attach to the running process and found [#fn2]_
that gdb allows the call with the process ID, e.g.

gdp -p <process-id>

Except that it did not work. The error was "ptrace: operation not
permitted" This works okay on my fedora system. A search on the
subject revealed [#fn3]_ that it has to do with a kernel "yama"
security option. An answer by "jesup" further links to a fedora 22
article [#fn4]_ that suggests two solutions.

The temporary solution is to execute (as root)::

  echo 0 > /proc/sys/kernel/yama/ptracescope

Also, the author says,

To enable that permanently, do::

  echo kernel.yama.ptracescope = 0 > /etc/sysctl.d/10-ptrace.conf

The etc/sysctl.d does not exist in fedora 28 anymore and there is a
note pointing to other locations: /usr/lib/sysctl.d, run/sysctl.d, and
etc/sysctl.d.

The first folder does include a 10-default-yama-scope.conf file
setting the ptrace_scope value to zero.

Back to the rpm
^^^^^^^^^^^^^^^

There are clashes with other files, detected by the rpm database.

gctags.1.gz and info.gz

It turns out that info.gz is a solution to bugzilla bug 927996 [#fn5]_
but it does not solve the problem in my case. I don't know why and I'm
not worried about erasing info.gz, so I have done that.

dnf diversion
^^^^^^^^^^^^^

It turns out that dnf can query packages in a repository without
downloading the package. The method is to use 'dnf repoquery -l'.

Conclusion
^^^^^^^^^^

I created a packaged version of emacs 25.3 on a rhel7 system.

.. rubric:: Footnotes

.. [#fn1] Bug 42342 "screen hangs irretrievably" url: https://savannah.gnu.org/bugs/?42342 accessed on 16 Sep 2018

.. [#fn2] Stackoverflow question from 17 Jan 2013 url:
         https://stackoverflow.com/questions/14370972/how-to-attach-a-process-in-gdb
         accessed on 16 Sep 2018

.. [#fn3] Stackoverflow question from 6 Oct 2013 url:
         https://stackoverflow.com/questions/19215177/how-to-solve-ptrace-operation-not-permitted-when-trying-to-attach-gdb-to-a-pro
         accessed on 16 Sep 2018
   
.. [#fn4] Attaching debugger and ptrace_scope 16 July 2015 url:
          https://rajeeshknambiar.wordpress.com/2015/07/16/attaching-debugger-and-ptrace_scope/
          accessed on 16 Sep 2018

.. [#fn5] Bug 927996 url:
          https://bugzilla.redhat.com/show_bug.cgi?id=927996 accessed
          on 16 Sep 2018
