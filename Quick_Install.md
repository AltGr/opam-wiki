# Install OPAM in 2 minutes

This page describes how to install and configure OPAM.
For further help and to learn how to use OPAM, you can either type
`opam --help` or move on to the [Basic Usage](Basic_Usage.html) guide.

## Installing OPAM with your distribution

You can use the OPAM package of your distribution if
available. Here is a list of supported distributions:

#### Archlinux

The [opam](http://aur.archlinux.org/packages.php?ID=62127) and [opam-git](http://aur.archlinux.org/packages.php?ID=62387) packages are available in the [AUR](https://wiki.archlinux.org/index.php/AUR). Replace `opam` with `opam-git` in the following instruction to get the development version:

```
  yaourt -S opam
```

#### Debian and Ubuntu

```
  echo "deb [arch=amd64] http://www.recoil.org/~avsm/ wheezy main" >> /etc/apt/sources.list
  apt-get update
  apt-get install opam
```

#### OSX

OPAM packages for [homebrew](http://mxcl.github.com/homebrew/) and [MacPorts](http://www.macports.org/) are available:

```
  brew install opam # using Homebrew
  port install opam # using MacPort
```

See also [howto setup Emacs.app](macosx_emacs_app.html) for opam usage.

## Binary installer

*Warning: This method only works with Darwin and Linux 64bits architecture.*

If your platform is of a different kind or if using a pre-compiled binary isn't to your
taste, use another method.

To install the latest stable opam in `/usr/local/bin` (you can change the path) and install the latest version of OCaml as well, you just need to download the binary auto-installed and run it:

```
  wget http://www.ocamlpro.com/pub/opam_installer.sh
  sh ./opam_installer.sh /usr/local/bin
```

You can also specify which version of OCaml you want to install:

```
  sh ./opam_installer.sh /usr/local/bin 3.12.1 # Install the latest OPAM and OCaml 3.12.1
  sh ./opam_installer.sh /usr/local/bin system # Install the latest OPAM using the system compiler (if any)
```

## From Sources

#### Getting the Sources

Sources of the latest stable version of OPAM are available [here](https://github.com/OCamlPro/opam/archive/latest.tar.gz).

Once the archive downloaded and extracted, you can then run the usual commands:

```
./configure && make && make install
```

See [Advanced Install](Advanced_Install.html) guide for more information.

#### Using ocamlbrew

[ocamlbrew](https://github.com/hcarty/ocamlbrew) is a script that can bootstrap an OCaml environment including OPAM, from source.  This option does not require an existing OCaml installation, or a pre-compiled OPAM binary for your platform.  To bootstrap a new OCaml environment including OPAM, make sure that you have the necessary pre-requisites installed to run ocamlbrew, and then run:

```
curl -kL https://raw.github.com/hcarty/ocamlbrew/master/ocamlbrew-install | env OCAMLBREW_FLAGS="-r" bash
```