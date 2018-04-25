# Instructions to use vim-fugitive

- Using the `:Git` command, we can run any arbitrary git command from inside Vim
For instance:
```
:Git checkout -b experimental
```

- One can use the following. Note that '%' represents the path to current file
```
:Git add %
```

- Or the shorter, compact version:
```
:Gwrite
```

- Other equivalent commands are:
```
:Git checkout %
:Gread

:Git rm %
:Gremove

:Git mv %
:Gmove
```

- And the **_very_** important:
```
:Gcommit
```

- As well as the very used:
```
:Gstatus
```

- And, to upload things to the server:
```
:Git push origin master
```

- Additional, valuable information may be found at: [The Fugitive Series - a retrospective](http://vimcasts.org/blog/2011/05/the-fugitive-series/)
