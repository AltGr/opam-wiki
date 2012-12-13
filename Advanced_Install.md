# Installing OPAM

This tutorial is a complement to the [Quick Install](Quick_Install.html)
tutorial and provides you alternative methods to install OPAM beyond the
simpler but restrictive boostrapping with a pre-compiled binary.

## Installing OPAM using a pre-compiled binary

This is the simplest and recommended method if you're running *Linux 64bits*.
This method is described in the [Quick Install](Quick_Install.html) tutorial.

## Installing OPAM with your distribution

You can use the OPAM package of your distribution if
available. Here is a list of supported distributions:

* Archlinux: [opam](http://aur.archlinux.org/packages.php?ID=62127),
  [opam-git](http://aur.archlinux.org/packages.php?ID=62387)

* Mac OS X: `opam` via [homebrew](http://mxcl.github.com/homebrew/)

## Installing OPAM from source

### Prerequisites:

* ocaml
* curl or wget
* git (optional, to use the git backend)
* rsync (optional, to use the rsync backend)

### Obtaining OPAM

Download OPAM 0.8 at <https://github.com/OCamlPro/opam/archive/0.8.1.tar.gz>

If you want to try the development (unstable) version of OPAM, clone
 the git repository: `git clone
 git://github.com/OCamlPro/opam.git`. Please keep in mind that this
 version may not work as expected.

### Compiling OPAM

To compile opam (binaries will be installed in `/usr/local/bin`),
simply run:

```
./configure
make
```

To have OPAM installed in a specific location, please do

```
./configure --prefix=/the/opam/path
make
```

This will fetch the necessary archives if they are not already
downloaded and then build OPAM. If you just want to get the necessary
dependencies without compiling the project, run `make clone`.

If you don't have *curl* installed on your system, you can run `make
FETCH=wget clone` before `make`.

####

On *BSD systems, you need to use `gmake` instead of `make`. Moreover, the
default path for installing the manual pages needs to be changed:

```
./configure --mandir /usr/local/man
gmake
```

### Installing OPAM

To install opam simply run:

```
sudo make install
```

OPAM will be installed under `$prefix`, that is under `/usr/local` if
you did not specify a prefix in the configure phase, or whatever
location you specified.

# Initializing OPAM

Before using OPAM, you need to initialize its state. Start by doing:

```
opam init
eval `opam config env`
```

This will:

* Create OPAM configuration files in `~/.opam`

* Add the default remote repository at URL `http://opam.ocamlpro.com`
  using opam’s HTTP repository backend.

* Update your local environment to be able to use OPAM packages and compilers.

It is recommanded that you add ``eval `opam config env` `` in the
configuration file of your shell (most likely `~/.bashrc` or
`~/.profile`).

To learn more about these two commands, try `opam --help init` and
`opam --help config`.