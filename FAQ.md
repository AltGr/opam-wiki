# OPAM FAQ

***

### Is there a way to tell OPAM to install from INRIA's SVN repository (either the trunk or a specific branch), and to update on demand?

`opam switch 4.01.0dev+trunk` has been added recently, which will grab the latest trunk snapshot.
To reinstall it and refresh to a newer snapshot, just do `opam switch reinstall 4.01.0dev+trunk`, which will also attempt to recompile any packages you had in there before.

It's also pretty easy to add your own branches; see
https://github.com/OCamlPro/opam-repository/blob/master/compilers/4.01.0dev%2Btrunk.comp
...for the trunk description, and there are several others out there.

For instance, Pierre Chambart is maintaining his various optimisation patches in his repository as an example, so you can see how to maintain custom branches as normal OPAM remotes (just like for packages).
https://github.com/chambart/opam-compilers-repository

Note that SVN isn't directly supported by OPAM (only Darcs and Git), so all of these are using the SVN->Git mirror at http://github.com/ocaml/ocaml, which is updated every hour via our friendly double-humped Bactrian Github bot.  Let us know how you get along with this!

The compiler description isn't simply called "trunk", without a reference to a version number, because OPAM also has compiler version constraints, so that you can mark a package as requiring `{>=4.00}` for example.  If the package is just marked trunk, then we need to manually record the version number somewhere.

One option is to have a very high version, so that any packages with a lower bound will continue to work.  The other option (which I chose) is to pick the current working version, since compiler releases only happen a couple of times a year.  We can improve on this...

***

### Now I want to create my first package.  I've followed the instructions from http://opam.ocamlpro.com/doc/Packaging.html but I don't know where to find opam-mk-repo (I've installed opam from the amd64 linux binary).

(that binary is hopefully just a stopgap until the OPAM binary packages become more widely available)

`opam-mk-repo` is installed as part of OPAM, so you'll need to install from source.  However, you don't actually need to create a repository unless you want to host a mirror of the tarballs. Simply try this:

````
$ mkdir -p my-repo/packages
$ opam remote add localdev my-repo
<create your package inside my-repo/packages/>
$ opam update
<the new packages will be available>
$ opam install <new-package>
```

The same applies for compilers.

If you specify a git:// or darcs:// URL in the package `url` file, a subsequent `opam update` will refresh the working copy from the remote source.

If you want to work with a local copy of that package, just do `opam pin <package> <dir>`.

If you want the bleeding edge version of a stable package, you can even do `opam pin <package> git://foo/bar`.

Quite the swiss-army knife, but each of those scenarios has come in useful at one point or another, particularly when hacking on Mirage which requires rebuilding lots of forward dependencies if (e.g.) a network driver library is being modified.