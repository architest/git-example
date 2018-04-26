Vim Commands:
=============

This information is partially taken from [here](https://stackoverflow.com/questions/5400806/what-are-the-most-used-vim-commands-keypresses)

## References

   - [Vim documents online](http://vimdoc.sourceforge.net/htmldoc/usr_toc.html)
   - [Advanced Vim tips](http://rayninfo.co.uk/vimtips.html)
   - [More useful tips](http://www.viemu.com/a-why-vi-vim.html)
   - [Graphical cheat sheet](http://www.viemu.com/a_vi_vim_graphical_cheat_sheet_tutorial.html)
   - [Vim tutorial](http://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/)


## General

   - Nearly all commands can be preceded by a number for a repeat count. eg. `5dd` deletes 5 lines
   - `Esc` gets you out of any mode and back to command mode
   - Commands preceded by `:` are executed on the command line at the bottom of the screen
   - `:help` helps with any command


## Navigation

   - Cursor movement: ←h ↓j ↑k l→

   - By words:

     NOTE: '**words**' are letters and the underscore character, while '**WORDS**' are characters separated by blanks. For instance: in the following line:

```
      (name_1,vision_3; # this is a comment.
```

   Here the first '**word**' is `name_1`, while the first '**WORD**' is `(name_1,vision_3;`

   - `w` next **word** (by punctuation)
   - `W` next **WORD** (by spaces)
   - `b` back **word** (by punctuation)
   - `B` back **WORD** (by spaces)
   - `e` end **word** (by punctuation)
   - `E` end **WORD** (by spaces)
   - `*` goes to the next occurence of the word under the cursor
   - `#` goes to the previous occurence of the word under the cursor

   - By line:

      - `0` goes to first column
      - `^` goes to first non-blank character of the line
      - `$` end of line
      - `g_` goes to the last non-blank character of the line
      - `g;` goes to place of last insertion
      - `fX` goes to the next occurence of character _X_ on the line
         - `;` will find the next occurrence
         - `,` will find the previous occurrence
      - `3fX` finds the third occurence of character _X_ on this line
      - `tX` goes to just before the character _X_
      - `F` and `T` are like `f` and `t`, but backwards
      - `dtX` removes everything from here to just before _X_

   - By paragraph:

      - `{` previous blank line
      - `}` next blank line

   - By file:

      - `gg` goes to start of file
      - `G` goes to end of file
      - `123G` goes to specific line number ('123' in this case)

   - By marker:

      - `mx` sets bookmark x
      - `'x` goes to bookmark x
      - `'.` goes to position of last edit
      - `' '` goes back to last point before jump
      - `:marks` shows all bookmarks
      - `:delm x` deletes bookmark x
      - `:delm!` deletes all bookmarks

   - Scrolling:

      - `^F` forward full screen
      - `^B` backward full screen
      - `^D` down half screen
      - `^U` up half screen
      - `^E` scroll one line up
      - `^Y` scroll one line down
      - `zz` puts current line in the center of the screen
      - `zt` puts current line at the top of the screen
      - `zb` puts current line at the bottom of the screen


## Editing

   - `u` undo
   - `^R` redo
   - `.` repeats last editing command
   - `N<command>`  repeats <command> _N_ times (p.e. `100idesu [ESC]` inserts 'desu ' 100 times
   - `N.` repeats last editing command _N_ times


## Inserting

   All insertion commands are terminated with `Esc` to return to command mode.

   - `i` inserts text at cursor
   - `I` inserts text at start of line
   - `a` appends text after cursor
   - `A` appends text after end of line
   - `o` opens new line below
   - `O` opens new line above


## Changing

   All change commands except `r` and `R` are terminated with `Esc` to return to command mode.

   - `r` replaces single character
   - `R` replaces multiple characters
   - `s` changes single character
   - `cw` changes from the cursor to end of the word
   - `C` changes to end of line
   - `cc` changes whole line
   - `c<motion>` changes text in the direction of the motion
   - `ci(` changes inside parentheses (see text object selection for more examples)


## Deleting

   - `x` deletes char
   - `dw` deletes word
   - `D` deletes to end of line
   - `dd` deletes whole line
   - `d<motion>` deletes in the direction of the motion


## Cut and paste

   - `yy` copies line into paste buffer
   - `dd` cuts line into paste buffer
   - `p` pastes buffer **BELOW** cursor line
   - `P` pastes buffer **ABOVE** cursor line
   - `xp` swaps two characters (`x` to delete one character, then `p` to put it back after the cursor position)


## Blocks

   - `v` visual block stream
   - `V` visual block line
   - `^v` visual block column
      - most motion commands extend the block to the new cursor position
      - `o` move the cursor to the other end of the block
   - `d` or `x` cuts block into paste buffer
   - `y` copies block into paste buffer
   - `>` indents block
   - `<` unindents block
   - `gv` reselects last visual block
   - `:sort` sorts selected rows
   - `U` converts selected text to uppercase
   - `u` converts selected text to lowercase
   - `~` inverts case of selected text


## Buffers

   - `:ls` shows list of buffers
   - `:bX` changes to buffer number _X_
   - `:bn` shows next file (buffer)
   - `:bp` shows previous file (buffer)


## Global

   - `:%s/foo/bar/g` substitutes all occurrences of "foo" to "bar" **IN WHOLE FILE**
   - `:%s/foo/bar/gc` substitutes all occurrences of "foo" to "bar" **IN WHOLE FILE**, with a prompt whether to substitute or not.
   - `:#,#s/old/new/g` where _#,#_ are the line numbers of the range of lines where the substitution is to be done.
   - `%` is a range that indicates every line in the file
   - `/g` is a flag that changes all occurrences on a line instead of just the first one


## Searching

   - `/` searches forward
   - `?` searches backward
   - `*` searches forward for word under cursor
   - `#` searches backward for word under cursor
   - `n` next match in same direction
   - `N` next match in opposite direction
   - `fX` forward to next character _X_
   - `FX` backward to previous character _X_
   - `;` moves again to same character in same direction
   - `,` moves again to same character in opposite direction
   - `/word\c` ignores case for just one search command
   - `:set ic` sets the 'ignore case' option ('ignorecase')
   - `:set hls` sets highlighting of matches ('hlsearch')
   - `:set is` shows partial matching phrases ('incsearch')
   - `:nohlsearch` removes the highlighting of matches
   - Prepend "no" to switch an option off. For instance: `:set noic`


## Files

   - `:w` writes file to disk
   - `:w <name>` writes file to disk as _<name>_
   - `:x` writes file to disk and quit (only save if necessary)
   - `ZZ` writes file to disk and quit
   - `:n` edits a new file
   - `:n!` edits a new file without saving current changes
   - `:q` quits editing a file
   - `:q!` quits editing without saving changes
   - `:qa!` quits even if there are modified hidden buffers
   - `:e` edits same file again (if changed outside Vim)
   - `:e .` directory explorer
   - `:e <FILE>` opens _<FILE>_
   - `:w <FILENAME>` writes the current Vim file to disk with name _FILENAME_
   - `:saveas <path/to/file>` saves to _<path/to/file>_
   - `v <motion> :w FILENAME`  saves the visually selected lines to _FILENAME_
   - `:r FILENAME` retrieves _FILENAME_ and puts it below the cursor position
   - `:r !command` reads output of command and puts it below cursor position


## Windows

   - `^Wn` new window
   - `^Wj` down to next window
   - `^Wk` up to previous window
   - `^W_` maximises current window
   - `^W=` makes all windows equal size
   - `^W+` increases window size
   - `^W-` decreases window size


## Source Navigation

   - `%` jumps to matching parenthesis/bracket/brace, or language block if language module loaded
   - `gd` goes to definition of local symbol under cursor
   - `Ctrl-O` returns to previous position
   - `Ctrl-]` jumps to definition of global symbol (requires tags file)
   - `Ctrl-T` returns to previous position (arbitrary stack of positions maintained)
   - `Ctrl-N` (in insert mode) automatic word completion


## Other:

   - `Ctrl-j` window down
   - `Ctrl-k` window up
   - `Ctrl-l` window right
   - `Ctrl-h` window left
   - `zm` opens search result in a new window
   - `<F5>` switches between themes
   - `Ctrl-P` Super searching
   - `<leader>g` :YcmCompleter GoToDefinitionElseDeclaration<CR>
   - `<space>` (or `za`): Folding code
   - `:sp <filename>` splits the layout horizontally (:split)
   - `:vs <filename>` splits the layout vertically (:vsplit)
   - `:tabedit` opens a new empty tab
   - `:!<command>` executes an external command
   - `:help <topic>` provides help
   - `Ctrl-W Ctrl-W` jumps between windows
   - In command mode (`:e`), `Ctrl-D` shows a list of commands that start with "e"
   - Most commands can be used using the following general format:

```
      <START position><COMMAND><END position>
```

   For example, `0y$` means:

   - `0` goes to the beggining of this line
   - `y` yanks from here...
   - `$` ...up to the end of this line

   So, `ye` means '_yank from here to the end of the word_'

   Another example is `y2/foo`: '_yank up to the second occurrence of "foo"_'

   Also:

   - `gU$` changes to uppercase from here to the end of the line
   - `guw` changes to lowercase from here to the beginning of next word
   - `d3w` deletes from here to the beginnning of the third word

   - `:hardcopy` sends file to printer... but format is not very good
   - `:retab` converts tabs to spaces
   - `:shell` launches a shell console from Vim
   - `Ctrl-d` comes back from the console to Vim


## Show local changes

Vim has some features that make it easy to highlight lines that have been changed from a base version in source control. Greg Hewgill has created a small Vim script that [makes this easy](http://github.com/ghewgill/vim-scmdiff).

