## Become a terminal wizard (Ubuntu terminal, with bash)

Using the arrow keys, backspace, del and enter is so mainstream.

You may stumble upon different cheat sheets on the web, so we'll quickly establish some notation:
- `C` is the same as <kbd>Ctrl</kbd>
- `M` is the [Meta] key, typically the same as <kbd>Alt</kbd>
- <kbd>Shift</kbd>, or <kbd>⇧</kbd> is the Shift key (duh) U+21E7
- `M-b`, or <kbd>Alt</kbd>+<kbd>b</kbd>, means that the two keys are pressed at the same time
- `M-2` `M-b` means that you first press <kbd>Alt</kbd>+<kbd>2</kbd>, release the keys and then presses <kbd>Alt</kbd>+<kbd>b</kbd>
- See also [bash refman, command line editing]
- I will use the `‸` symbol to denote where the caret is when we jump around in the text. U+2038
- U+2423 ␣
- U+23ce ⏎

[Meta]: https://askubuntu.com/questions/19558/what-are-the-meta-super-and-hyper-keys/19565#19565
[bash refman, command line editing]: https://www.gnu.org/software/bash/manual/html_node/Command-Line-Editing.html

### Moving around

- `C-b` move back one character
- `M-b` move back one word
---
- `C-f` move forward one character
- `M-f` move forward one word
---
- `C-a` move to the start of the line
- `C-e` move to the end of the line
---
- `C-x` `C-x` toggle between current position and beginning of line
---

- `C-h` delete the character to the left of the caret, i.e. backspace, <kbd>⌫</kbd>
- `C-d` delete the character to the right of the caret, i.e. <kbd>del</kbd>
- `M-r` delete the current line, no matter caret position
- `C-_` undo. Same as `C-x` `C-u`.

### Numeric argument

- `M-2` repeat the next arguent **2** times. You will se `(arg: 2)` at the beginning of the current line
- `M-3` `M-b` move caret **3** words **b**ack. Same as `M-b` `M-b` `M-b`
- Numeric argument can also be negative, so `M--` `3` `M-b` equals `M-3` `M-f`
- So obviously, you can choose any numeric argument

```
five four‸three two one
```

### Killing and yanking
Your terminal has something morbid called a ["kill-ring"](https://www.gnu.org/software/bash/manual/html_node/Readline-Killing-Commands.html).   
You can kill text, and it enters that ring. The ring can be filled with a number of kills.

- `C-w` kill to end of word left of caret
- `M-d` kill to end of word right of caret
- `C-u` kill from caret to start of line
- `C-k` kill from caret to end of line
- `C-y` yank (paste) back from the kill ring.   
Any number of consecutive kills save all of the killed text together, so that when you yank it back, you get it all.
- `M-y` rotate the kill ring and yank the top.

### Uppercase lowercase
- `M-u` uppercase word
- `M-l` lowercase word

### Freeze output
Sometimes, when compiling or whatever, a lot of output may be written to the terminal. Sometimes, you want to freeze the output so that you can examine it closer.
- `C-s` freeze the terminal
- `C-q` un-freeze the terminal

### Command history
What you type enters the command history. You can view the history in the file `~/.bash_history`.

- `C-r` Search command in history backwards - type the search term. Press `C-r` again to find other matches.
- `C-s` forward search (unfortunately interferes with freeze)
- `C-j` end the search at current history entry  
- `C-g` cancel the search and restore original line
- `C-p` previous command from the History
- `C-n` next command from the History
- `C-c` cancel the search and clear the line
- `M-#` comment the current text (and put it into history)
- `M-<` go to the beginning of history (and then `C-n` to go forward)
- `M->` go to the end of history (and then `C-b` to go backwards)
- `man bash` read more about history
- Start the line with a space, and it will not enter history



### Misc

- `C-l` clear the screen, reprinting the current line at the top
- `C-c` cancel almost anything
- `C-j` you can use it as <kbd>Enter</kbd>


### Jobs
Sometimes, you want to execute a command and let it run in the background, so that you can use the terminal for something else.
Some other times, you want to suspend a running process temporarily. For this, you can use [jobs](https://www.gnu.org/software/bash/manual/html_node/Job-Control.html).

- postpend a command with `&` to let it run as a background job, e.g. `firefox &`
- `C-z` suspend the current foreground job. The launched program will stop responding. (Not the same as `C-s`).
  - `fg` resume the job in the foreground.
  - `bg` resume the job in the background, as if it was launched with `&`
- `jobs` list jobs
- `%n` resume job #n, e.g. `%1` (which is synonym with `fg` or just `%`)

### Unicode

As a final note, you may wonder how I typed the ⇧ and ‸ symbols. Did i google "unicode shift symbol" and "unicode caret symbol"? Yes. Did i copy and paste them into this document? No. I discovered that
- Shift is unicode `U+21E7`
- Caret is unicode `U+2038`

Not limited to a Terminal, you can type unicode symbols with the key combination <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>u</kbd>. You will see a <ins>u</ins>, and then you type the number behind the `U+`, e.g. <ins>u263a</ins>. After you completed the code, just press <kbd>⏎</kbd>, or <kbd>Space</kbd>.

I use it some times to type æ ø å, which is `U+E6` `U+F8` `U+E5` respectively, if I'm not using a Norwegian keyboard but I need to type those symbols. 
