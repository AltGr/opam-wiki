# About OPAM

OPAM stands for OCaml PAckage Manager. It aims to suit to a vast
number of users and use cases, and has unique features:

* Powerful handling of dependencies: versions constraints,
  optional dependencies, conflicts, etc.

* Multiple repositories backends: HTTP, rsync, git

* Ease to create packages and repositories

* Ability to switch between different compiler versions

The fine grained handling of dependencies is made possible by the use
of the [CUDF](http://mancoosi.org/cudf/) library and the
[dose3](http://mancoosi.org/software/#index2h1) solver developed by
the [Mancoosi](http://www.mancoosi.org/) project, which is, among
other things, used by Debian to manage their packages.

Typically, OPAM will probably make your life easier if you recognize
yourself in at least one of these profiles:

* You use multiple versions of the OCaml compiler, or you hack the
  compiler yourself and needs to frequently switch between compiler
  versions.

* You use or develop software that needs a specific and/or modified
  version of the OCaml compiler to be installed.

* You use or develop software that depends on a specific version of
  an OCaml library, or you just want to install a specific version of
  a package, not just the latest one.

* You want to create your own packages yourself, put them on your own
  repository, with minimal effort.

A specific tutorial will be devoted to these use cases. In the
meantime, let’s learn the basics. You can get started with the [Quick
Install](Quick_Install.html) guide.
