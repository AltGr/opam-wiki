## What are user preferences for installations, and why are them important?
When you request the installation of some packages, say p1...pn, opam has a lot to do: it needs to look at all the packages already installed on your machine, find all packages available from the repositories, consider your request, and then come up with a set of actions to be performed to satisfy your request.

Unfortunately, there are a lot of assumptions hidden in your mind when you tell opam that you want p1...pn installed: should it choose the latest version of the p1...pn? That seems a sensible thing to do, but sometimes installing a recent version of a package p may lead to downgrading or removing another package q, which is something you might not want. What should opam do in this case? Remove q to get the lates p, or keep q and get the most recent p that is compatible with it?
Well, the answer is: it depends! It depends on what _you_ really want, and different users may have different points of view.

User preferences, supported by CUDF-compatible solvers, are the means you can use to make the assumptions in your mind explicit and known to the solver used by opam, so that the actions performed on your machine correspond to your personalised needs.

## How do I specify my preferences?

Preferences are expressed using a simple language built by prefixing a little set of combinators with the - (minus) or + (plus) operators. The most useful combinators are the following ones:

* new  : the number of new packages
* changed : the number of packages modified
* removed : the number of packages removed
* notuptodate : the number of packages that are not at their latest version

For example, the preference  -removed  tells the solver that among all possible ways of satisfying your request, it should choose one that minimises the number of packages removed.

These combinators can be combined in a comma separated sequence, that is treated in lexicographic order by the solver.

For example, the preference  -removed,-notuptodate,-changed  tells the solver that after ensuring that removals are minimised, it should look for a solution that minimises also the number of packages wich are not at their latest version, and then reduce the changes to a minimum.

This is the default preference setting used by opam, and in practice it tries to bring _all_ your packages to the latest version available, as far as this does not implies removing too many packages.

On *nix systems, you can specify your preferences by using the OPAMCRITERIA environment variable.

For example if you are a very conservative user, you might try issueing the following command (for bash users only, other shell users will need to adapt the example to the syntax used by their shell):

`OPAMCRITERIA="-removed,-changed" opam install ... `

## Warning: there are different versions of the user preference language