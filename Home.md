Basic instructions for getting up and running with opam:

    <install latest opam from github.com/OCamlPro/opam>
    $ rm -rf ~/.opam
    $ opam init default http://mirage.github.com/opam
    $ opam install <package-of-your-choice>
    $ opam upgrade

Some issues to watch out for:

  - The extra call to  `opam upgrade` is necessary to deal with some
    incorrect version choices, but that is being fixed soon.
  - you'll occasionally get errors on individual packages.  If you
    just retry `opam install` on the dependency that failed, that
    seems to clear it up.
  - Right now, `topfind` is not installed.  This is also being worked
    on.
  

