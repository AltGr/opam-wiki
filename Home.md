Basic instructions for getting up and running with opam:

    <install latest opam from github.com/OCamlPro/opam>
    $ rm -rf ~/.opam
    $ opam init
    $ opam install <package-of-your-choice>

You'll also need to prepare your environment for using opam, which can be done by running.

    $ eval `opam config env`

In order to use ocaml and topfind:

    $ opam install ocamlfind
    $ ocaml -I $OCAML_TOPLEVEL_PATH
    > #use "topfind"
