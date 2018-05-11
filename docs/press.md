# press

Presses a single, dash-separated key combination. It allows for easy intepretation of key combinations involving Control, Shift, and other special keys. It is meant for usage in custom functions in tandem with other operations such as [Str](Str.md).


## Usage

> **press(key_string)**
>
> key_string - String containing a single key combination, which is a dash-separated set of key names that will be held at the same time
>
> *Returns* - Function that executes the sequence of key combinations when called

When called, the key combination is executed immediately. Each key combination is a dash-separated sequence of key names that will be held during that combination. For example, 'cmd-s' would hold the Command key (⌘) and then press the 's' key.

Call the function directly with a parameter string containing a single, dash-separated key combination.


## Obtain

```python
from talon.voice import press
```


## Examples

Unlike [Key](Key.md), press is typically used in tandem with other operations in custom functions. It is not meant to be used directly in a [Context](Context.md) keymap.

### Single press

```python
press('cmd-s')
```

Immediately presses ⌘ + s, which will perform a Save operation in most apps.

### Multiple presses with other operations

This example makes additional use of [Str](Str.md).

```python
press('cmd-up')
press('enter')
press('cmd-up')
press('cmd-/')
Str('Copyright 2018')(None)
press('cmd-left')
```

This sequence would be executed as a custom function triggered by a Command. It would be something that might execute in a code editor using fairly standard keyboard shortcuts. Here's how it works:

1. ⌘ + ↑ - moves the cursor to the beginning of the first line of text
2. \n - makes a new line
3. ⌘ + ↑ - moves the cursor to the beginning of the newly created first line of text
4. ⌘ + / - inserts the comment syntax for the current language (such as '//' or '#')
5. Inserts the "Copyright 2018" string
6. ⌘ + ← - moves the cursor to the beginning of the line
