# OPAM FAQ


#### How to get, install and upgrade OPAM ?

See the [Quick install guide](Quick_Install.html).


#### Where is the manual ?

OPAM has git-like, hierarchical manpages. Try `opam --help` for a starting point.

Get started with OPAM packages by reading the [Packaging Howto](Packaging.html).

See the details on the file formats and more in the [Developper
Guide](dev_manual.pdf) (pdf).


#### What changes does OPAM do to my filesystem ?

OPAM is designed to be run strictly as user (non-root), and apart for the
explicit options provided during `opam init`, only writes within `~/.opam` (and
`/tmp`). This directory -- the default "OPAM root" -- contains configuration,
various internal data, a cache of downloaded archives, and your OCaml
installations.


#### Why does `opam init` need to add stuff to my init scripts / why is `eval
     $(opam config env)` needed ?

You need two things when you install OPAM packages: to have their libraries
accessible, and to access binary programs. To provide those, OPAM needs to setup
a few ocaml-related environment variables, and to prepend to your PATH variable.

Of course, you may choose not to let OPAM change anything at `opam init`, and
run `eval $(opam config env)` yourself whenever you will be needing it.


#### What is a `switch` ?

An ocaml installation and a set of installed packages within an OPAM
installation. This can be used to keep different OCaml versions side-by-side,
or different sets of packages. See `opam switch --help`. The "prefix" for a
given installation is simply `~/.opam/<switch-name>`.

A switch is either based on a system-wide OCaml installation, or on a local
installation. In the latter case, OCaml will be downloaded and compiled on
creation of the switch. In the former case, OPAM will need to recompile all
packages when your system compiler changes.


#### Can I work on different switches at the same time in different shells ?

Yes. Use `eval $(opam config env --switch <switch>)`, or `opam config exec
--switch <switch> <command>`. This only affects the environment.


#### Can I get a new switch with the same packages installed ?

Yes. Use:
```
opam switch export file.export  # from the previous switch
opam switch <new switch>
opam switch import file.export
```

OPAM might fail if you had packages installed that are not compatible with the
OCaml version in your new switch. In that case, you'll need to remove them from
the `file.export` file by hand (the format is straight-forward, one line per
package).


#### I installed a package by hand / used `ocamlfind remove` / fiddled with the
     installed packages and OPAM is out of sync. Help !

Don't panic. OPAM assumes it's controlling what's below `~/.opam/<switch>`, but
there are several ways you can recover:
* `opam remove --force` will attempt to uninstall even if not registered as
  installed. Then `opam install`
* `opam reinstall` will try to remove an installed package, but go on to
  re-installing even if that fails.
* If all else fails, you can re-install your current set of packages from
  scratch using `opam switch reinstall`
* You can force OPAM to register an installation or removal _without actually
  performing anything_ using `opam install|remove --fake`. This is not
  recommended though, as your manual install may not be exactly equivalent to
  the one expected by other OPAM packages, and OPAM may later on trigger
  reinstallations or upgrades of the package. Don't complain if you mess up your
  installation using this! If you want to control how a package is installed or
  modify it, the right way is `opam pin`.


#### What are the minimum requirements ?

1GB of memory should be all you need. It was reported that you may run into
problems with 512MB of RAM and no swap.


#### Some package complains about missing dependencies (m4, libgtk, etc.) during
     __compilation__, and makes OPAM fail.

They probably depend on system, non-OCaml libraries: you'll need to install them
using your system package manager (apt-get, yum, pacman, homebrew, etc.). If you
have no idea what the missing system package might be:
* Check for hints printed by the failing package
* Check the output of `opam list <package> --external`
* Lookup the development packages corresponding to the error in your system's
  package repositories. If you got to this point and found the appropriate
  packages, we'd be glad if you could tell us your system details and the answer
  in [the opam-repository
  tracker](https://github.com/ocaml/opam-repository/issues), to save the others
  the trouble of searching. Thanks.


#### I have weird checksum errors: where does they come from ?

First of all, you should update your repositories (`opam update`).

If this doesn't work (or if you get the checksum errors while running `opam init`) this comes probably a badly configured proxy cache that is serving stale files. To clear your proxy cache, you can use `wget --no-cache <remote-file>` and then you can retry.

If this doesn't work as well, you can bypass the checksum checks using
`-no-checksums`.


#### I read somewhere about `opam-admin`, `opam-installer`, etc., but can't find
     them Where are they ?

You probably used a one-shot package for OPAM, containing only the main program.
Install package opam-tools within OPAM. [TODO]


#### Where do I report Bugs, Issues and Feature Requests?

Bug reports and feature requests for the OPAM tool should be reported on [OPAM's
issue-tracker](https://github.com/ocaml/opam/issues). Packaging issues or
requests for a new package can be reported on the [official repository's
issue-tracker](https://github.com/ocaml/opam-repository/issues).

General queries for both the tool and the packages can be addressed on the
[OCaml-platform mailing-list](http://lists.ocaml.org/listinfo/platform) and
insights and evolution of OPAM internals can discussed on the [OPAM-devel
mailing-list](http://lists.ocaml.org/listinfo/opam-devel).

