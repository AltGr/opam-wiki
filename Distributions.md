This page tracks the state of binary packaging of OPAM on upstream distributions.  If you do package up OPAM for your various OS, please feel free to add it below, and mail <opam-devel@lists.ocaml.org> to let us know.

| Distribution   | Latest revision   | Maintainer | Solver | Notes  |
| ------------- |-------------| -----|-----|-----|
| Debian Linux (sid)  | 1.1.1 | Mehdi Dogguy| aspcud recommended | [sid page](http://packages.debian.org/sid/opam)
| Ubuntu Linux (PPA)  | 1.1.1  |  Anil Madhavapeddy | aspcud recommended | [PPAs](https://launchpad.net/~avsm) [Travis notes](http://anil.recoil.org/2013/09/30/travis-and-ocaml.html)
| Homebrew (MacOS X) | 1.1.1 | Anil Madhavapeddy | aspcud [recommended](https://github.com/Homebrew/homebrew/blob/master/Library/Formula/aspcud.rb) | [1.1.1 pull req](https://github.com/Homebrew/homebrew/pull/26282), [1.1.0 pull req](https://github.com/Homebrew/homebrew/pull/24086)
| Macports (MacOS X) | 1.1.1 |  | builtin | [trac to Portfile](https://trac.macports.org/browser/trunk/dports/sysutils/opam/Portfile) has wrong homepage
| Arch Linux | 1.1.1 | Vincent Bernardoff | builtin | [package info](https://aur.archlinux.org/packages.php?ID=62127)
| Exherbo Linux | 1.1.1 | @nbraud | builtin | [unofficial ocaml repo](https://github.com/Exherbo/ocaml-unofficial/)
| Mageia Linux | 1.1.0 | | builtin | [cauldron rpm spec file](http://svnweb.mageia.org/packages/cauldron/opam/current/SPECS/opam.spec?view=markup)
| NixOS | 1.1.1 | Malcolm Matalka | builtin | [github](https://github.com/NixOS/nixpkgs/tree/master/pkgs/development/tools/ocaml/opam), NixOS/nixpkgs#1810
| FreeBSD | from source | Vsevolod Stakhov | [aspcud port](http://www.freshports.org/math/aspcud/) | |
| CentOS | from source | | | | [need spec file](https://github.com/ocaml/opam/issues/409)
| Fedora | from source | | | |  [need spec file](https://github.com/ocaml/opam/issues/409)
| OpenBSD | from source | | | | [old port submitted to list](http://openbsd.7691.n7.nabble.com/new-opam-1-0-0-td225057.html)
| Windows | not supported as of 1.1.1 | | | | 