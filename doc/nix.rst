=====
 Nix
=====

`Nix`_ is a project (and a language) closely related to the NixOS
linux distribution.

It started as an academic research by Eelco Doljstra whose PhD Thesis
is still a reference for concepts and components of the system.

It's taking me a while to get my head around the system and I am also
interested in the related project Guix that is led by Ludovic Courtes
(Inria).

.. _`Nix`: https://nixos.org/

Nix pills
---------

A great source of information and examples are the `nix pills`_ [#f1]_ that
explain the basics and guide through producing derivations and nix expressions to build software.

.. _`nix pills`: https://nixos.org/nixos/nix-pills/index.html

Nixos FAQ
---------

`https://nixos.wiki/wiki/FAQ <https://nixos.wiki/wiki/FAQ>`_

Nix vocabulary
--------------

Derivation:
    The first step of a build based on nix expressions.

Attribute:
    I don't know yet. I think it is an element of the nix language

Environment:
    This is my terminology and it may be wrong. This is a 'generation' of
    the list one obtains with `nix-env --list-generations`

Store:
    The place where components are stored in the local storage.
    This is currently `/nix/store`
  
Channel:
    I don't know yet.

Generations:
    Variations of the environment. These are modified when one performs
    installations and removals. `Pill #11 (section 11.4) <https://nixos.org/nixos/nix-pills/garbage-collector.html>`_ shows a method to remove
    generations to help the garbage collector.

  
Nix Discourse
-------------

The site is `https://discourse.nixos.org/ <https://discourse.nixos.org/>`_.



.. rubric:: Footnotes

.. [#f1] Accessed on 4 July 2020
