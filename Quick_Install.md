# Install OPAM in 2 minutes

Here is the simplest and shortest way of getting started with OPAM:

*Warning: This method only works with a Linux 64bits architecture.* If your
platform is of a different kind or if using a pre-compiled binary isn't to your
taste, you can find other bootstrapping methods in the
[Advanced Install](Advanced_Install.html) guide.

- Download a pre-compiled OPAM binary (the current version is 0.9):
[opam64](http://opam.ocamlpro.com/build/opam64), or do it directly from the
shell with `wget`:

```
wget http://opam.ocamlpro.com/build/opam64      # Get a pre-compiled OPAM binary
```

- Initialize and install OPAM:

```
chmod +x opam64                                 # Make it executable
sudo cp opam64 /usr/local/bin/opam              # Copy the binary in your path
opam init                                       # Initialize OPAM database locally (fresh ~/.opam)
eval `opam config env`                          # Update the local environment to use OPAM
```

- If you don't have OCaml installed on your system, you can initialize OPAM with
a given compiler version:

```
opam init --comp 4.00.1                        # Initialize OPAM with OCaml 4.00.1
```

- If you'd like the environment to be set properly to use OPAM each time you
start a new shell session, just add the `eval \`opam config env\`` command to
your `~/.profile` or `~/.bashrc`.

- That's it! OPAM is installed and fully functional.

For further help and to learn how to use OPAM, you can either type
`opam --help` or move on to the [Basic Usage](Basic_Usage.html) guide.