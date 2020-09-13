========
 Kernel
========

Ftrace
------

This is a good write-up from 2009 by Steven Rostedt, describing the
use of ftrace

`Debugging the kernel using Ftrace - part 1 <https://lwn.net/Articles/365835/>`_

`Debugging the kernel using Ftrace - part 2 <https://lwn.net/Articles/366796/>`_   (22 Dec 2009) lwn.net

Here is an example for find_debugfs (also from `lwn.net <https://lwn.net/Articles/366800/>`_)
::
   
    #define MAX_PATH 256
    #define _STR(x) #x
    #define STR(x) _STR(x)
    static const char *find_debugfs(void)
    {
	    static char debugfs[MAX_PATH+1];
	    static int debugfs_found;
	    char type[100];
	    FILE *fp;

	    if (debugfs_found)
		    return debugfs;

	    if ((fp = fopen("/proc/mounts","r")) == NULL)
		    return NULL;

	    while (fscanf(fp, "%*s %"
			  STR(MAX_PATH)
			  "s %99s %*s %*d %*d\n",
			  debugfs, type) == 2) {
		    if (strcmp(type, "debugfs") == 0)
			    break;
	    }
	    fclose(fp);

	    if (strcmp(type, "debugfs") != 0)
		    return NULL;

	    debugfs_found = 1;

	    return debugfs;
    }


