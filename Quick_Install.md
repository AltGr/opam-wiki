# Install OPAM in 2 minutes

This page describes how to install and configure OPAM.
For further help and to learn how to use OPAM, you can either type
`opam --help` or move on to the [Basic Usage](Basic_Usage.html) guide.

## Installing OPAM with your distribution

You can use the OPAM package of your distribution if
available. Here is a list of supported distributions:

* Archlinux: [opam](http://aur.archlinux.org/packages.php?ID=62127),
  [opam-git](http://aur.archlinux.org/packages.php?ID=62387)
  ```
  pacman -S opam
  ```

* Debian and Ubuntu packages are available.
  ```
  echo "deb http://www.recoil.org/~avsm/ wheezy main" >> /etc/apt/sources.list`
  apt-get update
  apt-get install opam
  ```

* OSX: packages for [homebrew](http://mxcl.github.com/homebrew/) and [MacPorts](http://www.macports.org/).
  ```
  brew install opam # using Homebrew
  port install opam # using MacPort
  ``` 

## Binary installer

*Warning: This method only works with Darwin and Linux 64bits architecture.* If your
platform is of a different kind or if using a pre-compiled binary isn't to your
taste, use another method.

- Download the binary auto-installed and run it:

```
wget http://www.ocamlpro.com/pub/opam_installer.sh
sh ./opam_installer.sh /usr/local/bin
```

- This will install the latest stable opam in `/usr/local/bin`. You can change
the path to install it in an other place.

- By default, this will download and install the latest version of OCaml as well.
You can specify which version of the OCaml you want to install:

```
sh ./opam_installer.sh /usr/local/bin 3.12.1 # Install the latest OPAM and OCaml 3.12.1
sh ./opam_installer.sh /usr/local/bin system # Install the latest OPAM using the system OCaml
```

- If you'd like the environment to be set properly to use OPAM each time you
start a new shell session, just add the `eval \`opam config env\`` command to
your `~/.profile` or `~/.bashrc`.

## Getting OPAM from sources

Sources of OPAM 0.9.1 are available [here](https://github.com/OCamlPro/opam/archive/0.9.1.tar.gz).
Once the archive downloaded and extracted, you can then run the usual commands:

```
./configure && make && make install
```

See [Advanced Install](Advanced_Install.html) guide for more information.

## Installing OPAM and OCaml from source using ocamlbrew

[ocamlbrew](https://github.com/hcarty/ocamlbrew) is a script that can bootstrap an OCaml environment including OPAM, from source.  This option does not require an existing OCaml installation, or a pre-compiled OPAM binary for your platform.  To bootstrap a new OCaml environment including OPAM, make sure that you have the necessary pre-requisites installed to run ocamlbrew, and then run:

```
curl -kL https://raw.github.com/hcarty/ocamlbrew/master/ocamlbrew-install | env OCAMLBREW_FLAGS="-r" bash
```