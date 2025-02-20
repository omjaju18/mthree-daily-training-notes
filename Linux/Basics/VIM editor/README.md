# Vim Editor in Linux 

Vim is a powerful, widely used text editor in Linux and UNIX-based systems. It is highly configurable and efficient, often favored by programmers and system administrators. Below are some essential commands and tips for using Vim.

---

## **Vim Basics**

### Starting Vim

To start Vim, type the following command in the terminal:
```bash
vim filename
```
- **Explanation**: Opens `filename` in Vim. If the file doesn’t exist, it will be created.

---

### Vim Modes

Vim operates in different modes:

1. **Normal Mode**: This is the default mode when you open a file in Vim. You can navigate and manipulate the text.
2. **Insert Mode**: This mode is for entering and editing text.
3. **Command-Line Mode**: Used for executing commands like saving, quitting, etc.

---

## **Basic Navigation**

In **Normal Mode**, use the following commands to navigate within a file:

- **`h`**: Move the cursor left.
- **`j`**: Move the cursor down.
- **`k`**: Move the cursor up.
- **`l`**: Move the cursor right.
  
You can also use arrow keys to navigate.

### To Move by Word:
- **`w`**: Move the cursor to the beginning of the next word.
- **`b`**: Move the cursor to the beginning of the previous word.
- **`e`**: Move the cursor to the end of the current word.

### To Move by Line:
- **`0`**: Move to the beginning of the line.
- **`$`**: Move to the end of the line.
- **`gg`**: Move to the beginning of the file.
- **`G`**: Move to the end of the file.

---

## **Entering Text**

To enter text in **Insert Mode**, press:

- **`i`**: Insert before the cursor.
- **`I`**: Insert at the beginning of the line.
- **`a`**: Append after the cursor.
- **`A`**: Append at the end of the line.
- **`o`**: Open a new line below the current one and switch to Insert Mode.
- **`O`**: Open a new line above the current one and switch to Insert Mode.

---

## **Editing Text**

In **Normal Mode**, use these commands to edit text:

- **`x`**: Delete the character under the cursor.
- **`dd`**: Delete the current line.
- **`d{motion}`**: Delete from the cursor to the specified position.
  - Example: **`d$`** deletes from the cursor to the end of the line.
- **`y{motion}`**: Yank (copy) text from the cursor to the specified position.
  - Example: **`yy`** copies the current line.
- **`p`**: Paste after the cursor.
- **`P`**: Paste before the cursor.

---

## **Undo and Redo**

- **`u`**: Undo the last change.
- **`Ctrl + r`**: Redo the undone change.

---

## **Saving and Exiting**

In **Normal Mode**, use these commands to save and exit:

- **`:w`**: Save the file (write).
- **`:q`**: Quit Vim (exit).
- **`:wq`**: Save the file and quit.
- **`:x`**: Save and exit, similar to `:wq`.
- **`:q!`**: Quit without saving changes (force quit).
  
### Command-Line Mode:
- Press **`:`** to enter Command-Line Mode, then type the desired command (e.g., `:wq`).

---

## **Searching and Replacing**

### Searching:
- **`/search_term`**: Search for `search_term` in the file.
  - Press **`n`** to go to the next occurrence.
  - Press **`N`** to go to the previous occurrence.
  
### Replacing:
- **`:%s/old/new/g`**: Replace all occurrences of `old` with `new` in the file.
  - **`g`**: Replace all instances in each line.
  - **`c`**: Ask for confirmation before replacing each occurrence.

Example:
```bash
:%s/old/new/g
```
- Replaces all occurrences of `old` with `new`.

---

## **Working with Multiple Files**

You can open multiple files in Vim:

- **`:e filename`**: Open a new file.
- **`:bn`**: Switch to the next file.
- **`:bp`**: Switch to the previous file.
- **`:q`**: Close the current file.

---

## **Advanced Features**

### Visual Mode:
- **`v`**: Start selecting text (character by character).
- **`V`**: Start selecting text (line by line).
- **`Ctrl + v`**: Start block selection (columnar selection).

### Split Windows:
- **`:split`**: Split the window horizontally and open the same file.
- **`:vsplit`**: Split the window vertically.
- **`:close`**: Close the current window.
- **`Ctrl + w + h/j/k/l`**: Move between split windows.

---

## **Vim Tips**

- **`Ctrl + f`**: Scroll forward one page.
- **`Ctrl + b`**: Scroll backward one page.
- **`:set number`**: Display line numbers.
- **`:set nonumber`**: Hide line numbers.
- **`:set cursorline`**: Highlight the current line.
- **`:set wrap`**: Enable line wrapping.
- **`:set nowrap`**: Disable line wrapping.

---
