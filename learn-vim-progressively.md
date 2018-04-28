LEARN VIM PROGRESSIVELY
=======================


The following text is based on the tutorial **_Learn Vim Progressively_** that can be found [here](http://yannesposito.com/Scratch/en/blog/Learn-Vim-Progressively/)


## 1ST LEVEL:

Vim starts by default in NORMAL mode. Use `i` to change to INSERT mode. To get back to NORMAL mode just press the `ESC` key.

- `i` -> Go to **INSERT** mode. Inserts in the place where the cursor is
- `ESC` -> Back to **NORMAL** mode
- `x` -> Delete the character under the cursor
- `:wq` -> Save (`:w`) and Quit (`:q`)
- `dd` -> Delete (and copy to clipboard) the current line
- `p` -> Paste what is in clipboard
- `hjkl` -> Move Left, Down, Up, Right (`j` looks like a down arrow)
- `:help <command>` -> Show help about _command_. `:help` provides general help


## 2ND LEVEL:

1. Insert mode variations:

    - `i` -> insert **IN** the cursor
    - `a` -> insert **AFTER** the cursor
    - `I` -> insert at the **BEGINNING** of the current line
    - `o` -> insert a new line **AFTER** the current one
    - `O` -> insert a new line **BEFORE** the curren one
    - `cw` -> replace from the cursor to the end of the word

2. Basic moves:

    - `0` -> (Zero) go to the first column
    - `^` -> go to the first **NON-BLANK** character of the line
    - `$` -> go to the end of the line
    - `g_` -> go to the last **NON-BLANK** character of the line
    - `/pattern` -> search for _pattern_

3. Copy/Paste:

    - `P` -> paste **BEFORE** current position
    - `p` -> paste **AFTER** current position
    - `yy` -> copy the current line

4. Undo/Redo:

    - `u` -> undo
    - `Ctrl-r` -> redo

5. Load/Save/Quit/Change File (Buffer):

    - `:e <path/to/file>` -> open _path/to/file_
    - `:w` -> save
    - `:saveas <path/to/file>` -> save to _path/to/file_
    - `:wq`, `:x` or `ZZ` -> save and quit (`:x` only save if necessary)
    - `:q!` -> quit without saving
    - `:qa!` -> quit without saving even if there are modified hidden buffers
    - `:bn` -> show **NEXT** file (buffer)
    - `:bp` -> show **PREVIOUS** file (buffer)


## 3RD LEVEL:

- `.` -> (dot) will repeat the last command
- `N<command>` will repeat <command> _N_ times

  For example:

  - `100idesu [ESC]` -> will write "_desu_ " 100 times
  - `.` (dot) -> just after last command will write again 100 times "_desu_ "
  - `3.` -> will write 3 times "_desu_ " (and not 300 times)

- `NG` -> go to line _N_
- `gg` -> go to **start of file** (shortcut for `1G`)
- `G` -> go to **last** line of file

Mind that '**words**' are composed of letters and underscore character, while '**WORDS**' are a group of characters separated by blank characteres. Thence, in the following string:

```
    (name_1,vision_3); # this is a comment.
```

the first '**word**' is `name_1`, while the first '**WORD**' is `(name_1,vision_3);`

- `w` -> go to the **START** of the following '**word**'
- `W` -> go to the **START** of the following '**WORD**'
- `e` -> go to the **END** of this '**word**'
- `E` -> go to the **END** of this '**WORD**'

- `%` -> go to the correspondig (, {, [
- `*` -> go to the **NEXT** occurence of the word under the cursor
- `#` -> go to the **PREVIOUS** occurence of the word under the cursor

Most commands can be used using the following general format:

```
    <START-position><COMMAND><END-position>
```

  For example, `0y$` means:

  - `0` -> (Zero) go to the beginning of this line
  - `y` -> yank from here...
  - `$` -> ...up to the end of this line

  Other examples are:

  - `ye` -> yank to the end of this word
  - `y2/foo` -> yank up to the second occurence of _foo_


## 4TH LEVEL:


1. General:

   - `fX` -> go to the next occurence of character _X_ on this line

     For instance:
     - `3fX` -> find the 3rd occurence of character _X_ in this line

     - `F` -> like `f`, but backwards
     - `;` -> find the **NEXT** occurrence
     - `,` -> find the **PREVIOUS** occurrence

   - `tX` -> go to just **BEFORE** the character _X_
     - `T` -> like `t`, but backwards
   - `dtX` -> remove everything up to _X_, without including it


2. Zone selection:

   This follows the patterns:

```
    <action>a<object>  and  <action>i<object>
```

   Where action can be `d` (delete), `y` (yank), `v` (select in visual mode),etc. The object can be: w (**word**), W (**WORD**), s (sentence), p (paragraph), but also natural characters like `"`, `'`, `)`, `}`, `]`.

   Let's suppose the cursor is on the first 'o' of `(map (+) ("foo"))`:

   - `vi"` -> will select `foo`
   - `va"` -> will select `"foo"`
   - `vi)` -> will select `"foo"`
   - `va)` -> will select `("foo")`
   - `v2i)` -> will select `map (+) ("foo")`
   - `v2a)` -> will select `(map (+) ("foo"))`


3. Rectangular blocks:

   They are very useful for commenting many lines of code. For instance:

```
    ^<Ctrl-v><Ctrl-d>I-- [ESC][ESC]
```

   - `^` -> go to the first non-blank character of the line
   - `Ctrl-v` -> start of block selection (_ATTENTION!_, it is **_CTRL_**!!!)
   - `Ctrl-d` -> move down (could also be `jjj`, `%`, etc.)
   - `I-- [ESC][ESC]` -> write `-- ` to comment each line
   - `o` -> in Visual Block Mode, toggles selection cursor to **OPPOSITE** corner

     Note #1: Instead of `I` we can use `i`, `A`, `a`, `c`, `r`, etc.

     Note #2: Don't confuse `Ctrl-v` (Visual Block Mode) with `V` and `v` modes

   To add something at the end of all visually selected lines:

   - `Ctrl-v` -> gets into Visual Block Mode
   - go to the desired line (with `j`, `Ctrl-d`, `/pattern`, etc)
   - `$` -> go to the end of the line
   - `A` + write text + `ESC`

   A fabulous video about the Visual Block Mode can be found at [Vimcasts](http://vimcasts.org/episodes/selecting-columns-with-visual-block-mode/).

4. Completion:

   - `Ctrl-p` -> call the autocompletion feature


5. Macros:

   - `qa` -> records your actions in register '_a_'
   - `@a` -> this will call the macro saved in register '_a_'
   - `@@` -> calls the last executed macro

   Example: On a line containing only the number 1, type:

   - `qaYp<Ctrl-a>q`
     - `qa` -> starts recording the macro
     - `Yp` -> duplicates this line
     - `Ctrl-a` -> increments the number
     - `q` -> stops recording the macro
   - `@a` -> writes 2 under 1
   - `@@` -> writes 3 under 2
   - `100@@` -> writes increasing numbers up to 103

6. Visual selection: `v`, `V` and `Ctrl-v`

   Once the selection has been made:

   - `J` -> joins all the lines together
   - `<` -> indent to the left
   - `>` -> indent to the right
   - `=` -> autoindent

7. Splits:

   - `:split` -> create a (horizontal) split (shorthand: `:sp`)
   - `:vsplit` -> create a vertical split (shorthand: `:vs`)
   - `Ctrl-w <direction>` -> (where _direction_ is `hjkl`) to change split
   - `Ctrl-w_` -> Maximise the size of the (horizontal) split
   - `Ctrl-w |` -> Maximise the size of the vertical split
   - `Ctrl-w +` -> Grow the split
   - `Ctrl-w -` -> Shrink the split

8. The manuals:

   - `:help usr_01.txt` -> Start the User Manual
   - `Ctrl-]` -> jumps to the subject under the cursor
   - `Ctrl-o` -> jumps back

