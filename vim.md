# Notes on Vim

## Navigation
*   `^` Start of line
*   `$` End of line
*   `w` Start of next word
*   `e` End of next word
*   `b` Start of previous word
*   `{` Previous blank line
*   `}` Next blank line
*   `Ctrl-d` Scroll down half a page
*   `Ctrl-f` Scroll down one page (*also* `PgDn`)
*   `Ctrl-u` Scroll up half a page
*   `Ctrl-b` Scroll up one page (*also* `PgUp`)
*   `10gg` Go to line 10

## Inserting text
*   `a` Insert text after cursor
*   `i` Insert text before cursor
*   `o` Insert new line below
*   `O` Insert new line above

### Deleting text (in Insert mode)
*   `Ctrl-w` Delete previous word
*   `Ctrl-u` Delete to first word in line

## Cutting, copying, pasting text
### Selecting text
*   `v` Select mode
*   `V` Select line mode

### Cutting text
*   `dd` Cut line
*   `x` Cut selected text

### Copying text
*   `yy` Copy line
*   `y` Copy selected text

### Pasting text
*   `p` Paste after cursor
*   `P` Paste before cursor
*   `:reg` View clipboard

## Split view
### Creating splits
*   `:vsp` Vertical split
*   `:sp` Horizontal split
*   `:sp ~/file.txt` Open file in split
*   `:q` Close split

### Switching splits
Press `Ctrl-w` to enter split select mode, then use `hjkl` to select the left,
up, down, or right of the current split.

## Tabs
*   `:tabedit {file}` Open file in new tab
*   `:tabn` Next tab
*   `:tabp` Previous tab
*   `:tabclose` Close tab

## File Explorer
*   `:Explore` Open file explorer in current window
*   `:Texplore` Open file explorer in new tab

## Shell commands
*   `:! bash` Run shell command 

## Other settings
Line numbers
* `set number`
* `set nonumber`

Line ending style
* `set ff?` Query line ending style for current document
* `set ff=dos` Use CRLF line endings
* `set ff=unix` Use LF line endings
