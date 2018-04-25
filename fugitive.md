Instructions to use vim-fugitive

# Using the :Git command, we can run any arbitrary git command from inside Vim
# For instance:
:Git checkout -b experimental

# One can use the following. Note that '%' represents the path to current file
:Git add %

# Or the shorter, compact version:
:Gwrite

:Git checkout %
:Gread

:Git rm %
:Gremove

:Git mv %
:Gmove

# And the very important:
:Gcommit

# As well as:
:Gstatus

# And, to upload things to the server:
:Git push origin master

# Additional, valuable information may be found at:
http://vimcasts.org/episodes/fugitive-vim---a-complement-to-command-line-git/

