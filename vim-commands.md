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

   - Nearly all commands can be preceded by a number for a repeat count. eg. `5dd` delete 5 lines
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

      - `0` go to first column
      - `^` go to first non-blank character of the line
      - `$` end of line
      - `g_` go to the last non-blank character of the line
      - `g;` go to place of last insertion
      - `fX` go to the next occurence of character _X_ on the line
         - `;` will find the next occurrence
         - `,` will find the previous occurrence
      - `3fX` find the third occurence of character _X_ on this line
      - `tX` go to just before the character _X_
      - `F` and `T` are like `f` and `t`, but backwards
      - `dtX` remove everything from here to just before _X_

   - By paragraph:

      - `{` previous blank line
      - `}` next blank line

   - By file:

      - `gg` start of file
      - `G` end of file
      - `123G` go to specific line number ('123' in this case)

   - By marker:

      - `mx` set bookmark x
      - `'x` go to bookmark x
      - `'.` go to position of last edit
      - `' '` go back to last point before jump
      - `:marks` show all bookmarks
      - `:delm x` delete bookmark x
      - `:delm!` delete all bookmarks

   - Scrolling:

      - `^F` forward full screen
      - `^B` backward full screen
      - `^D` down half screen
      - `^U` up half screen
      - `^E` scroll one line up
      - `^Y` scroll one line down
      - `zz` put current line in the center of the screen
      - `zt` put current line at the top of the screen
      - `zb` put current line at the bottom of the screen


## Editing

    u undo
    ^R redo
    . repeat last editing command
    N<command>  repeat <command> N times (p.e. 100idesu [ESC] inserts
         'desu ' 100 times
    N. repeats last editing command N times


## Inserting

    All insertion commands are terminated with <Esc> to return to command mode.

    i insert text at cursor
    I insert text at start of line
    a append text after cursor
    A append text after end of line
    o open new line below
    O open new line above

## Changing

    All change commands except r and R are terminated with <Esc> to return to
    command mode.

    r replace single character
    R replace multiple characters
    s change single character
    cw change from the cursor to end of the word
    C change to end of line
    cc change whole line
    c<motion> changes text in the direction of the motion
    ci( change inside parentheses (see text object selection for more examples)

## Deleting

    x delete char
    dw delete word
    D delete to end of line
    dd delete whole line
    d<motion> deletes in the direction of the motion

## Cut and paste

    yy copy line into paste buffer
    dd cut line into paste buffer
    p paste buffer BELOW cursor line
    P paste buffer ABOVE cursor line
    xp swap two characters (x to delete one character, then p to put it back
                            after the cursor position)

## Blocks

    v visual block stream
    V visual block line
    ^v visual block column
        most motion commands extend the block to the new cursor position
        o move the cursor to the other end of the block
    d or x cut block into paste buffer
    y copy block into paste buffer
    > indent block
    < unindent block
    gv reselect last visual block
    :sort sort selected rows
    U convert selected text to uppercase
    u convert selected text to lowercase
    ~ invert case of selected text

## Buffers

    :ls  shows list of buffers
    :bX change to buffer number 'X'
    :bn show next file (buffer)
    :bp show previous file (buffer)

## Global

    :%s/foo/bar/g substitute all occurrences of "foo" to "bar" IN WHOLE FILE
    :%s/foo/bar/gc substitute all occurrences of "foo" to "bar" IN WHOLE FILE,
        with a prompt whether to substitute or not.
    :#,#s/old/new/g    where #,# are the line numbers of the range of lines
        where the substitution is to be done.
    % is a range that indicates every line in the file
    /g is a flag that changes all occurrences on a line instead of just the
       first one

## Searching

    / search forward
    ? search backward
    * search forward for word under cursor
    # search backward for word under cursor
    n next match in same direction
    N next match in opposite direction
    fx forward to next character x
    Fx backward to previous character x
    ; move again to same character in same direction
    , move again to same character in opposite direction
    /word\c ignore case for just one search command
    :set ic sets the 'ignore case' option ('ignorecase')
    :set hls sets highlighting of matches ('hlsearch')
    :set is shows partial matching phrases ('incsearch')
    :nohlsearch removes the highlighting of matches
    Prepend "no" to switch an option off. For instance:  :set noic

## Files

    :w write file to disk
    :w <name> write file to disk as <name>
    :x write file to disk and quit (only save if necessary)
    ZZ write file to disk and quit
    :n edit a new file
    :n! edit a new file without saving current changes
    :q quit editing a file
    :q! quit editing without saving changes
    :qa! quit even if there are modified hidden buffers
    :e edit same file again (if changed outside vim)
    :e . directory explorer
    :e <FILE> opens <FILE>
    :w FILENAME  writes the current Vim file to disk with name FILENAME
    :saveas <path/to/file>  save to <path/to/file>
    v <motion> :w FILENAME  saves the visually selected lines to FILENAME
    :r FILENAME  retrieves FILENAME and puts it below the cursor position
    :r !command  reads output of command and puts it below cursor position

## Windows

    ^Wn new window
    ^Wj down to next window
    ^Wk up to previous window
    ^W_ maximise current window
    ^W= make all windows equal size
    ^W+ increase window size
    ^W- decrease window size

## Source Navigation

    % jump to matching parenthesis/bracket/brace, or language block if language
      module loaded
    gd go to definition of local symbol under cursor
    ^O return to previous position
    ^] jump to definition of global symbol (requires tags file)
    ^T return to previous position (arbitrary stack of positions maintained)
    ^N (in insert mode) automatic word completion

## Other:

    - Ctrl-j: Window down
    - Ctrl-k: Window up
    - Ctrl-l: Window right
    - Ctrl-h: Window left
    - zm: Open search result in a new window
    - <F5>: Switch between themes
    - Ctrl-P:  Super searching
    - <leader>g  :YcmCompleter GoToDefinitionElseDeclaration<CR> (???)
    - <space> (or za): Folding code
    - :sp <filename>: Split the layout horizontally (:split)
    - :vs <filename>: Split the layout vertically (:vsplit)
    - :tabedit  Open a new empty tab
    - :!command  executes an external command
    - :help <topic> provides help. CTRL-W CTRL-W to jump between windows
    - In command mode (:e), Ctrl-D shows a list of commands that start with "e"
    - Most commands can be used using the following general format:

        <START position><COMMAND><END position>

      For example, '0y$' means:

        - 0 -> go to the beggining of this line
        - y -> yank from here...
        - $ -> ...up to the end of this line

      So, 'ye' means 'yank from here to the end of the word'
      Another example is 'y2/foo': 'yank up to the second occurrence of "foo"'
      Also:
        - gU$ -> change to uppercase from here to the end of the line
        - guw -> change to lowercase from here to the beginning of next word
        - d3w -> delete from here to the beginnning of the third word
    - :hardcopy send file to printer... but format is not very good
    - :retab convert tabs to spaces
    - :shell to launch a shell console from Vim
    - Ctrl-d to come back from the console to Vim


## Show local changes

Vim has some features that make it easy to highlight lines that have been
changed from a base version in source control. I have created a small vim
script that makes this easy: http://github.com/ghewgill/vim-scmdiff

