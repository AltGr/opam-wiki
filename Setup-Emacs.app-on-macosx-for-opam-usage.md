Setting up environment variables for GUI programs on macosx has been [a mess](http://emacswiki.org/emacs/EmacsApp#toc2) for quite some time now. 

If you are using compilation mode in `Emacs.app` it is likely that you won't have a correct environment (this can simply be checked by issuing `env` as the compilation command). There are various tips that will tell you how to adjust your `$PATH`, but it's not enough, there are other environment variables setup by `opam`. 

A simple solution to this problem is to invoke the compilation mode shell as an interactive shell; this will read your `.profile` or `.bash_profile` file and everything should be setup correctly. This can be achieved by adding the following lines to your `.emacs`. 

```elisp
(cond 
 ((eq window-system 'ns) ; macosx
  ;; Invoke interactive shells, so that .profile or .bash_profile is read
  (setq shell-command-switch "-ic")))
```
