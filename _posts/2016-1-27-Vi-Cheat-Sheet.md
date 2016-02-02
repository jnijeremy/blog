---
layout: post
title: Vi Cheat Sheet

---

### Line Navigation

- `k` = up
- `j` = down
- `l` = right
- `h` = left
- `0` = go to the starting of the current line
- `$` = go to the end of the current line

### Word Navigation

- `e` = go to the end of the current word
- `b` = go to the previous (before) word
- `w` = go to the next word.

### Screen Navigation

- `H` = Go to the first line of current screen
- `M` = Go to the middle line of current screen
- `L` = Go to the last line of current screen
- `ctrl`+`f` = Jump forward one full screen.
- `ctrl`+`b` = Jump backwards one full screen
- `ctrl`+`d` = Jump forward (down) a half screen
- `ctrl`+`u` = Jump back (up) one half screen
- `gg` = Go to the beginning of the file
- `G` = Go to the end of the file
- `NG` = Go to the Nth line of the file

### Undo/Redo
- `u` = undo
- `Ctr` + `r` = redo

### Editing

- `x` = delete char
- `dd` = delete and copy the current line
- `yy` = copy the line
- `p` = paste
- `o` = add a new line below
- `O` = add a new line above

### Search & Replace
- `/pattern` = search for pattern
  - `n` = go to next pattern, `shift`+`n` = go to previous pattern

- `:%s/foo/bar/gc`
  - change each `foo` to `bar` but ask for confirmation first
  
### Setting
- `:set tabstop=2` = change tab to 2 space
- `:set nu` = enable line numbers along the left side of window
- `:set nonu` = disabling line numbers
- `:set paste` = avoid unexpected effects for copy and paste