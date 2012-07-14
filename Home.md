Basic instructions for getting up and running with opam:

    <install latest opam from github.com/OCamlPro/opam>
    $ rm -rf ~/.opam
    $ opam init default http://mirage.github.com/opam
    $ opam install <package-of-your-choice>
    $ opam upgrade

You'll also need to prepare your environment for using opam, which can be done by running.

    $ eval `opam config -env`

or 
    
    $ export `opam config -env`

depending on your shell.

Some issues to watch out for:

  - The extra call to  `opam upgrade` is necessary to deal with some
    incorrect version choices, but that is being fixed soon.
  - installing a package as a dependency doesn't always give the same
    version as installing directly --- the direct-installed packages
    generally being more recent.  You can work around this by doing
    the direct install in a shell loop, but it's obviously not ideal.
  - Right now, `topfind` is not installed.  This is also being worked
    on.
  

