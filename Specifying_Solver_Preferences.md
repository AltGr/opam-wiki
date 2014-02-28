# Specifying user Preferences for the external Solvers

A fundamental distinguishing feature of the `opam` package manager is the fact that it is designed to reuse state-of-the-art dependency solving technology that gives the users the possibility to express their preferences regarding the operations to be performed during an installation, instead of being bound to an hard-coded strategy.
This section provides basic documentation on this feature, and its usage.

## What are user preferences for installations, and why are them important?
When you request the installation of some packages, say p1...pn, `opam` has a lot to do: it needs to look at all the packages already installed on your machine, find all packages available from the repositories, consider your request, and then come up with a set of actions to be performed to satisfy your request.

Unfortunately, there are a lot of assumptions hidden in your mind when you tell `opam` that you want p1...pn installed: should it choose the latest version of the p1...pn? That seems a sensible thing to do, but sometimes installing a recent version of a package p may lead to downgrading or removing another package q, which is something you might not want. What should `opam` do in this case? Remove q to get the lates p, or keep q and get the most recent p that is compatible with it?
Well, the answer is: it depends! It depends on what _you_ really want, and different users may have different points of view.

User preferences, supported by `CUDF`-compatible solvers, are the means you can use to make the assumptions in your mind explicit and known to the solver used by `opam`, so that the actions performed on your machine correspond to your personalised needs.

## How do I specify my preferences?

Preferences are expressed using a simple language built by prefixing a little set of combinators with the `-` (minus) or `+` (plus) operators. The most useful combinators are the following ones:

* `new`  : the number of new packages
* `changed` : the number of packages modified
* `removed` : the number of packages removed
* `notuptodate` : the number of packages that are not at their latest version

For example, the preference  `-removed`  tells the solver that among all possible ways of satisfying your request, it should choose one that minimises the number of packages removed.

These combinators can be combined in a comma separated sequence, that is treated in lexicographic order by the solver.

For example, the preference  `-removed,-notuptodate,-changed`  tells the solver that after ensuring that removals are minimised, it should look for a solution that minimises also the number of packages wich are not at their latest version, and then reduce the changes to a minimum.

This is the default preference setting used by opam, and in practice it tries to bring _all_ your packages to the latest version available, as far as this does not implies removing too many packages.

On *nix systems, you can specify your preferences by using the `OPAMCRITERIA` environment variable.

For example if you are a very conservative user, you might try issueing the following command (for `bash` users only, other shell users will need to adapt the example to the syntax used by their shell):

`OPAMCRITERIA="-removed,-changed" opam install ... `

## Yes, there are different versions of the user preference language

The `opam` package manager is an instance of the approach described in the article "[A modular package manager architecture](http://dl.acm.org/citation.cfm?id=2401012)", which was one of the outcomes of the [Mancoosi](http://www.mancoosi.org) research project. This architecture relies on external dependency solvers for package managers, that communicate with the package manager front-end via the [CUDF format](http://www.mancoosi.org/cudf/).
We have now several CUDF-compatible solvers, developed by a variety of research teams during the [MISC competitions](http://www.mancoosi.org/misc/) run yearly from 2010 to 2012:

* [aspcud](http://www.cs.uni-potsdam.de/wv/aspcud/)
* [Mccs](http://www.i3s.unice.fr/~cpjm/misc/mccs.html)
* [Packup](http://sat.inesc-id.pt/~mikolas/sw/packup/)
* [P2Cudf](https://wiki.eclipse.org/Equinox/p2/CUDFResolver)

Each of these competitions led to improving the preferences language, by allowing the user progressively more flexibility.

As of today, the preferences language described in the previous section, which corresponds to the one used in the 2010 competition, should be supported by all external solvers, but if you happen to use as external solver one of the entrants of the 2012 competition, like recent versions of `aspcud`, then you have access to a more sophisticated set of preferences, described in [the 2012 MISC competition rules](http://www.mancoosi.org/misc-2012/criteria/). 
For example, you could use

 `-count(removed), -count(down),-sum(solution,installedsize),-notuptodate(solution),-count(changed)`

to instruct a solver to minimise downgrades, and mininise the installed size, among other criteria.

The `aspcud` solver supports this extended language starting from its version 1.8.0, which unfortunately is not the version shipped by default with Ubuntu precise or Debian Wheezy.