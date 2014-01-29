> With 1.1.1, OPAM is getting quite stable, and earning a wider and wider
acceptation from the community. This is just the beginning, and we now have
opportunities to build on this success in many directions.

> This document aims to summarise all those directions, and give an overview of their current status. Some belong to the core and are handled by OCamlPro, some others are more platform-related and are being worked on by OCaml Labs and the community. Lots do already have prototypes but need work to be put into production

# The Platform

First is the Platform, to make the life of OCaml hackers easier, and make
jumping in for new users a breeze.

## OPAM must interact with many other tools:

   - [opam-doc](https://github.com/ocamllabs/opam-doc) to have a nice browsable, consistent and relevant API
     documentation at hand. This is working, but still in progress.
     To get better integration, this would need build tool support, which is related to the points below.

   - [opam2web](https://github.com/ocaml/opam2web) to give easy access to what is available and up-to-date
     information.
     This has already been up for a while. An obvious major improvement would be opam-doc documentation readily available.

   - build systems to get better integration, easier packaging and consistent
     install/uninstall.
     
     We have started an attempt to bridge the gap with opam-installer, but OPAM needs to get a better understanding/integration with 
     ocamlfind, which is the one well-established tool in this area (note: that should be done as a plugin not to contradict the "agnostic" point below).
     With time and proper support from OPAM, we hope to have the build tools properly integrate.

## Build and deployment

   - opam-in-a-box, a first glimpse of the platform: simplified architecture
     giving access to all needed components. Easy to build custom images,
     trivial to deploy ; does not yet give the best integration and ease of use.
     
     This is currently the only viable option on Windows.
     There are a few prototypes of this using [Docker](https://github.com/avsm/docker-opam) or [Vagrant](https://github.com/avsm/vagrant-opam).
     We need to make them easier to customise and build, and more stable.

   - binary packages for easier and quicker deployment. For those, there are
     several different approaches:

     * generate external binary packages (eg. .deb) from opam packages. Doing
       this individually would be crazy, but parts of the platform may be
       packaged like this for better integration.
       [Opam2debian](https://github.com/gildor478/opam2debian) is an interesting prototype that builds a debian package with the same idea as opam-in-a-box.

     * keep a cache of pre-built packages with their specific dependencies, to
       avoid recompilation. Very handy within a company, or for setting up a
       classroom for example.
       [ocp-bin](http://www.ocamlpro.com/blog/2013/12/02/monthly-11.html) is a working prototype of this.

     * generate binary OPAM repositories mechanically from a standard OPAM
       repository. Indeed, nothing in the current OPAM format forbids binary
       packages: a tool could build all packages, rewrite their definitions,
       straighten their dependencies, and create a new repository for a given
       OS/architecture. This could prove particularly useful for Windows
       repositories which could install on systems without a proper toolchain
       available. This approach could even allow for cross-compiling a whole repository.
       Not much have been attempted yet in this area, but [ocp-reloc](https://github.com/AltGr/ocp-reloc) is a needed basic building block.
       
       It is well worth trying as it probably won't need much changes from OPAM itself, but works by adding tooling that works on the repository.
       This is lighter, likely to prove of more general use, and won't add weight to OPAM's core codebase.

# Attract new users

There is much to be done on that front as well, and several directions to explore:

   - proper Windows support: this is a mandatory step to take,
     because it keeps us away from the main pool of potential users. It is
     tricky because of the slight incompatibilities and lack of proper tooling
     infrastructure.
     The first step is a working Cygwin port of OPAM: we can currently compile,
     but the hoard of small bugs makes it non-working at the moment. This will
     need a bit of time and attention but shouldn't be a huge challenge.
     
     It could be worth starting by attempting cross-compilation also, as this may prove
     the quickest route to get there.
     
     The longer-term objective is to have native Windows executables, possibly using mingw.

   - making OPAM more agnostic, and using it for different languages, will
     attract users, make publicity and gain traction. We have a [working
     prototype](https://github.com/AltGr/opam/commits/experimental-compiler-packages) that removes most OCaml-specific operations from OPAM and makes
     it much easier to use in a different setting. This represents large changes
     in the repository itself, but doesn't actually change OPAM itself very
     deeply.

   - this is already [well underway](https://github.com/braibant/opam-coq-repo)  for Coq, which is a nice middle-ground since
     it builds on OCaml but has a largely different user base.

# Stability and UI

Ongoing work to improve code quality and stability, as well as polish the user interface and improve error messages, must also be mentionned. Also, features like per-switch remotes would be quite valuable but don't fit in the above picture, for example.

# Plans

1.1.1 is focusing on opam-in-a-box, which we need to get as nice to use as possible.

For 1.2, the main objective is to generalise the build, install and interaction of packages, which will in turn make deployment smoother.
