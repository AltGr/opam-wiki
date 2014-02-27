## What are user preferences for installations, and why are them important?
When you request the installation of some packages, say p1...pn, opam has a lot to do: it needs to look at all the packages already installed on your machine, find all packages available from the repositories, consider your request, and then come up with a set of actions to be performed to satisfy your request.

Unfortunately, there are a lot of assumptions hidden in your mind when you tell opam that you want p1...pn installed: should it choose the latest version of the p1...pn? That seems a sensible thing to do, but sometimes installing a recent version of a package p may lead to downgrading or removing another package q, which is something you might not want. What should opam do in this case? Remove q to get the lates p, or keep q and get the most recent p that is compatible with it?
Well, the answer is: it depends! It depends on what _you_ really want, and different users may have different points of view.

User preferences, supported by CUDF-compatible solvers, are the means you can use to make the assumptions in your mind explicit and known to the solver used by opam, so that the actions performed on your machine correspond to your personalised needs.
 
## How do I specify my preferences?
## Warning: there are different versions of the user preference language