# Install OPAM in 2 minutes

Here is the simplest and shortest way of getting started with OPAM :

- Download a pre-compiled OPAM binary :
[opam64](http://opam.ocamlpro.com/build/opam64), or do it directly from the
shell with `wget` :

```
wget http://opam.ocamlpro.com/build/opam64      # Get a pre-compiled OPAM binary
```

- Initialize and install OPAM :

```
chmod +x opam64                                 # Make it executable
./opam64 init                                   # Initialize OPAM database locally (fresh ~/.opam)
./opam64 install opam                           # Install your own version of OPAM
eval `opam config -env`                         # Update the local environment to use OPAM
```

- You can then delete the pre-compiled binary and use the `opam` command with
your current user account.

- If you'd like the environment to be set properly to use OPAM each time you
start a new shell session, just add the `eval \`opam config -env\`` command to
your `~/.profile` or `~/.bashrc`.

- That's it! OPAM is installed and fully functional.

For further help and to learn how to use OPAM, you can either type
`opam --help` or move on to the [Tutorial](Tutorial.html).

*Note*: If using a binary to get started doesn't work for you or isn't to your
taste, you can find other bootstrapping methods in the
[Tutorial](Tutorial.html).
