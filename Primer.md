```
git clone git://github.com/OCamlPro/opam.git    # Get OPAM
cd opam
./configure --prefix=$HOME                      # configure and set the prefix
make && make install                            # compile and install
opam init                                       # Initialize OPAM for your system
opam install core lwt                           # Install packages
```