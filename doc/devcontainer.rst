Dev containers
==============

I am reading through several documents and guides about dev containers
( `1 <https://happihacking.com/blog/posts/2023/dev-containers/>`_,
`2 <https://happihacking.com/blog/posts/2023/dev-containers-emacs/>`_,
`3 <https://code.visualstudio.com/docs/devcontainers/create-dev-container>`_,
`4 <https://blog.wille-zone.de/post/run-devcontainer-outside-of-visual-studio-code/>`_,
`5 <https://www.reddit.com/r/emacs/comments/iqrze0/work_with_vscodes_dev_containers/>`_,
`6 <https://developers.redhat.com/articles/2023/02/14/remote-container-development-vs-code-and-podman#install_podman_desktop_on_the_local_machine>`_).
I am trying to avoid having to use vscode.

There is one emacs extension (`devcontainer-mode <https://github.com/johannes-mueller/devcontainer-mode/>`_ recently available (Feb 2025?) that I may
look at too. One other extension referenced is `lsp-docker <https://github.com/emacs-lsp/lsp-docke>`_, but that might
be useful only for language servers? I will have to understand or find out.

Other preferences I have are that I want to use podman instead of docker.
I don't understand well the place of 'docker compose'. That is where a
dose of reading the `docs <https://docs.docker.com/compose/>`_ might help.

I should also check the page of `dev container cli <https://github.com/devcontainers/cli>`_ (also `here <https://containers.dev/supporting#devcontainer-cli>`_) which is a reference implementation to use devcontainer.json without using vscode. 
