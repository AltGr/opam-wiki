# OPAM FAQ

***

### How to upgrade OPAM itself to its latest version ?

In summary: upgrade the OPAM binary to the latest and run `opam update` to update your package descriptions. You won't see this message again.

Some more detail: In the heady days of early OPAM when it had no users, we thought auto-updating via OPAM would be a good strategy. It turned out not to be such a great idea, as there are lots of corner cases with bootstrapping it, and particularly during repository format changes.

Nowadays, OPAM has settled down in terms of features and interfaces, and starting to get packaged up in upstream distributions. This means that you should be able to upgrade via that OS-specific process and get the latest OPAM binary.

Current options:

* Upgrade from source: fetch the latest sources and ./configure && make && sudo make install. If you run into odd build errors from old trees, you may find a make distclean will help before the configure.

* On MacOS X, we keep the Homebrew packages up-to-date, so `brew update && brew upgrade opam` will do the trick. I believe there are MacPorts packages also, but I don't track them closely.

* On Debian, we have dpkg descriptions, but the NEW queue is blocked due to the Wheezy release. There are unofficial binary packages, but I'd recommend a source installation for the moment.

* On the various BSDs, we should have ports when shortly (OPAM mostly works, but many packages are a little broken on the BSDs due to GNU make vs BSD make problems. Easy to fix, but there are a lot of packages to test now).


#### I have weird checksum errors: where does they come from ?

First of all, you should update your repositories (`opam update`).

If this doesn't work (or if you get the checksum errors while running `opam init`) this comes probably a badly configured proxy cache that is serving stale files. To clear your proxy cache, you can use `wget --no-cache <remote-file>` and then you can retry.

If this doesn't work as well, you can bypass the checksum checks using `-no-checksums`.

#### Is there a way to tell OPAM to install from INRIA's SVN repository (either the trunk or a specific branch), and to update on demand?

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

#### Now I want to create my first package.  I've followed the instructions from http://opam.ocamlpro.com/doc/Packaging.html but I don't know where to find opam-mk-repo (I've installed opam from the amd64 linux binary).

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