# Learn to use OPAM in 2 minutes

This short tutorial covers the very basic use cases to get you started with
OPAM. A more lengthy introduction can be found in the
[Advanced Usage](Advanced_Usage.html) guide.

## Browsing available packages

The following commands will enable you to obtain information on available
packages:

```
opam list               # List all available packages
opam search QUERY       # List packages with QUERY in their name or description
opam info PACKAGE       # Display information about PACKAGE
```

Another option to obtain information on packages is to browse the
[Packages](../pkg/index.html) section of the [OPAM website](http://opam.ocamlpro.com/).

## Installing a package

The two commands you will probably use the most with OPAM are:

```
opam update             # Update the packages database
opam install PACKAGE    # Download, build and install the latest version of PACKAGE
```

## Upgrading your installed packages

You may want to regularly issue these commands to keep your packages up-to-date:

```
opam update             # Update the packages database
opam upgrade            # Re-install packages that were updated since last upgrade
```

## Do more with OPAM

To learn how to use more advanced features of OPAM (version pinning, multiple
repositories, multiple compilers...), move on to the
[Advanced Usage](Advanced_Usage.html) guide.