# Vim

## Useful vim command

### insert
1. o: open a line below
2. O: open a line above
3. a: append a word after the cursor.
4. A: append a word after the line.i
5. :r file/command : insert the content to current file

### delete
1. x: delete a character
2. dw: delete until the start of the next world
3. de: delete until the end of the word.
4. d$: delete to the end of the line.
5. dd: delete a whole line.

###split window
1. :Ve : open current file explore and split vertical window
2. vim -On file1 file2 : split vertically to open files
3. vim -on file1 file2 : split horizontally to open files
4. ctrl+w v: split vertically current file
5. ctrl+w s: split horizontally current file
6. :vsp filename : split vertically and open a new file
7. ctrl+w (h/j/k/l) : switch focus among windows
8. ctrl+w (H/J/K/L) : move the window
9. ctrl+w = : make all the windows has the same height
10. ctrl+w [n] + / - : adjust the height of current window
11. ctrl+w [n] < / > : adjust the width of current window
12. :resize N : resize the height of the current window to size N
13. :vertical resize N : resize the width of the current window to size N.

### move
1. e: to the end of the word forward
2. w: to the start of the word forward
3. 2w, 3e, move the word faster
4. 0: move to the start of a line
5. $: move to the end of a line
6. j$: move to the end of the next line

### undo / redo
1. u: undo previous action
2. U: undo all the changes on a line
3. CTRL-R: undo the undo's

### change words
1. ce: similar to de, but ce will be in the insert mode.
2. r: replace current word
3. c$:

### substitute words
1. :s/old/new : substitute the first word in the current line.
2. :s/old/new/g : substitute all words in the current line.
3. :%s/old/new/gc: substitute every occurrence in the file with a prompt whether to substitute or not.

### cursor location
1. CTRL-G: show status
2. G: move to bottom of file
3. gg: move to start of file
4. [N]G: move to Nth line
5. %: match (,),[,],{,}

### search
1. /[pattern]: search words that match the pattern
2. /[pattern]: search words that match the pattern backword
3. n: search the next match
4. N: seach the previous match
5. :set ic :ignore the case
6. :set hls is (highlightsearch increase search)
7. prepend no to switch an option off, i.e. :set noic
8. /ignore\c to ignore case for just one search

### copy/paste
1. p: paste below
2. y: yank (copy)
3. yw: copy a wordi
*Trick* Press V to enter visual mode to selete words andcopy

### save file
1. :w "file name": save the file as "file name"
2. V :w "file name": save the selected part of the file.

### execute external command
1. :!<command>
