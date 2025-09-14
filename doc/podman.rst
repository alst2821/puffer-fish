========
 Podman
========

Links related to podman:

* Why you should use docker ignore (bookmarked 30 Dec 2022 `howtogeek <https://www.howtogeek.com/devops/understanding-the-docker-build-context-why-you-should-use-dockerignore/>`_)
* Podman machine on MacOS (bookmarked 30 Dec 2022 `stack overflow link 1 <https://stackoverflow.com/questions/70564828/podman-machine-cannot-connect-to-podman-on-macos>`_)

* Podman pull error (bookmarked 30 Dec 2022 `stack overflow link 2 <https://stackoverflow.com/questions/67100094/podman-pulling-image-error-dial-tcp-18000-connect-connection-refused>`_)

* Tutorial, how to create a docker image (bookmarked 30 Dec 2022 `linux.com <https://www.linux.com/training-tutorials/how-create-docker-image/>`_).
  
Podman workflow on macos
~~~~~~~~~~~~~~~~~~~~~~~~

Initialise the podman machine (only once):

  podman machine init <name>

Start the podman machine:

  podman machine start 


The objective I have is to run a devcontainer to use from emacs.  The
instructions I plan to follow are in the `blog post
<https://happihacking.com/blog/posts/2023/dev-containers-emacs/>`_ by
`happihacking <https://happihacking.com/>`_ from 2023 (accessed Sep 2025).

The modifications I want to make are related to *not* wishing to use
docker, but use podman instead, because it is rootless.

The setup should still use the `devcontainer cli <https://github.com/devcontainers/cli>`_.

Start
~~~~~

As per the guide:

  mkdir rust-dev-container && cd rust-dev-container
  mkdir .devcontainer && touch .devcontainer/Dockerfile && touch .devcontainer/devcontainer.json

  <Fill in Dockerfile>

  <Fill in devcontainer.json>

Now the guide expects devcontainer to be running to call:

  devcontainer up --workspace-folder .

I realise I don't have devcontainer running.

Getting devcontainer
~~~~~~~~~~~~~~~~~~~~

The `devcontainer pages <https://github.com/devcontainers/cli>`_ say that it can be installed using npm or from source using yarn.

As I am using macports, it was okay to install nodejs and npm.

As I am writing this (Sep 2025) the macport versions that are current
are npm10 and nodejs22 (even though there is nodejs24).

The installation of npm came with a note that it is not adviseable to
install packages globally, but the devcontainer instructions use the
"-g" switch to install it globally.

The work-around was to change the npm configuration to set a prefix to ~/.local

Errors launching podman
~~~~~~~~~~~~~~~~~~~~~~~

Yes. Particularly with macos.

I will try on linux to see if the errors go away.

It turns out that the podman machine needs to mount the file system
from the host. I haven't figured out the problem. I get errors like::

  [240967 ms] Start: Run: docker run --sig-proxy=false -a STDOUT -a STDERR
  --mount type=bind,source=/Users/xxx/dev/rust-dev-container,target=/workspaces/rust-dev-container,consistency=cached -l devcontainer.local_folder=/Users/xxx/dev/rust-dev-container
  -l devcontainer.config_file=/Users/xxx/dev/rust-dev-container/.devcontainer/devcontainer.json
  --cap-add SYS_PTRACE --security-opt seccomp=unconfined
  --entrypoint /bin/sh vsc-rust-dev-container-21ec84f9b64e1ccd13b54793d3296e096487e38be5089ee473d0727bd024d8c8
  -c echo Container started

Followed by::

  Error: statfs /Users/xxx/dev/rust-dev-container: no such file or directory
  Error: Command failed: <copy of command above>
  


