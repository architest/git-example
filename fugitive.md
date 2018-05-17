# Instructions to use vim-fugitive

- Using the `:Git` command, we can run any arbitrary git command from inside
Vim. For instance, let's create a new branch and move into it:
```
:Git checkout -b experimental
```

- One can use the following. Note that, in vim, '%' represents the path to
current file:
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

The command `Gstatus` is special in the sense that it opens a new window
showing the files that have been modified. In order to navigate through those
files, use `Ctrl-n` (forward) and `Ctrl-p` (backwards).

In order to stage (or unstage) a given file, just press the `-` key. This `-`
key also works in "Visual Mode", so you can select multiple files and
stage/unstage them at the same time. However, in order to add many files it is
better to use `:Git add .` (don't forget the 'dot' at the end).

Once files have been staged, one can press `cc` to invoke a commit window and
enter the commit message.

- And, to upload things to the server:
```
:Git push origin master
```

- When there is a conflict when merging, we can call
```
:Gdiff
```

  when being on the conflict file. If we want to force vertical windows, use:

```
:Gvdiff
```

- Being in the central buffer, we accept the changes from the left (target
branch/master) doing:

```
:diffget //2
```

- And, when we want the changes from the right (merge branch):

```
:diffget //3
```

  or even better, do this and at the same time update the colors in the diff
windows (it gets messed up after `diffget` or `diffput`):

```
:diffget //3 | diffupdate
```

- Shorthands for `diffget` and `diffput` are `do` and `dp`, respectively.
These mappings include `diffupdate`, so the colors will be fixed automatically

- To move to the previous hunk, use `[c`, and to jump to the next, use `]c`

- To exit _vimdiff_ mode and close all the windows except the middle one,
  containing the working copy:

```
:only
```

- After this, go through the standard procedure of `:Gstatus`, `:Gwrite` and
`:Gcommit`

- It often happens that we want to accept **all** the changes from a given
branch. In order to do that, go to the windows containing the file from the
desired branch, and use:

```
:Gwrite!
```

  The '!' sign is needed to force the writing, because Fugitive wants to be
sure that you're not going to loose previously picked up changes

- Additional, valuable information may be found at: [The Fugitive Series - a retrospective](http://vimcasts.org/blog/2011/05/the-fugitive-series/)
