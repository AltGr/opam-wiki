Basic instructions for getting up and running with opam:

    <install latest opam from github.com/OCamlPro/opam>
    $ rm -rf ~/.opam
    $ opam init
    $ opam install <package-of-your-choice>

You'll also need to prepare your environment for using opam, which can be done by running.

    $ eval `opam config -env`

Some issues to watch out for:

  - Right now, `topfind` is not installed.  This is also being worked
    on, but at the moment, you can't easily use ocamlfind and the top
    level with opam-installed packages.
  

