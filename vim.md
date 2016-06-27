# Notes on Vim

## Navigation
*   `^` Start of line
*   `$` End of line
*   `w` Start of next word
*   `e` End of next word
*   `Ctrl-d` Scroll down half a page
*   `Ctrl-f` Scroll down one page (*also* `PgDn`)
*   `Ctrl-u` Scroll up half a page
*   `Ctrl-b` Scroll up one page (*also* `PgUp`)

## Inserting text
*   `a` Insert text after cursor
*   `i` Insert text before cursor
*   `o` Insert new line below
*   `O` Insert new line above

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

## Shell commands
*   `:! bash` Run shell command 
