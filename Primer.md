```
git clone git://github.com/OCamlPro/opam.git    # Get OPAM
cd opam
./configure                                     # configure and set the prefix
make && sudo make install                       # compile and install
opam init                                       # Initialize OPAM for your system
eval `opam config -env`                         # Update your environment for OPAM
echo "eval `opam config -env`" >> ~/.bashrc     # Make your shell ready for OPAM
opam install core lwt                           # Install packages
```