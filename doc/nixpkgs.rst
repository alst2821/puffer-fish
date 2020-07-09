=========
 Nixpkgs
=========

The repository nixpkgs also defines many of the functions used to
generate derivations.

For example the sources to process `fetchFromGithub` are in the file all-packages.nix,
defined so::

  fetchFromGitHub = callPackage ../build-support/fetchgithub {};

