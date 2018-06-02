# press

Presses a single key, or a single dash-separated key combination. It is meant for usage in custom functions in tandem with other operations such as [Str](Str.md), as opposed to [Key](Key.md) that is most often used directly in a [Context's](Context.md) keymap.


## Usage

> **press(key_string)**
>
> key_string - String containing a single key or key combination
>
> *Returns* - None

When called, the provided key string, or key combination string, is executed immediately.

A single key string simply presses the corresponding key, such as the string 'k', which will press the K key.

A key combination is a dash-separated set of modifier keys followed by a single non-modifier key. For example, 'cmd-shift-s' would hold the Command key (⌘) and the Shift key (⇧), and then press the S key.

Check the [Keys List](KeysList.md) for a list of all key name strings.

### Available Modifier Keys

|     |  Modifier Key Name           |  Key String       |  Example            |
|:---:|------------------------------|-------------------|---------------------|
|  ⌃  |  Control                     |  ctrl             |  'ctrl-c'           |
|  ⌥  |  Alt/Option                  |  alt              |  'alt-tab'          |
|  ⌘  |  Command                     |  cmd              |  'cmd-s'            |
|  ⇧  |  Shift                       |  shift            |  'cmd-alt-shift-v'  |
|     |  Fn Key (Modifier)           |  fn               |  'fn-f2'            |


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

This sequence would be executed as a custom function triggered by a [Command](Commands.md). It would be something that might execute in a code editor using fairly standard keyboard shortcuts. Here's how it works:

1. ⌘ + ↑ - moves the cursor to the beginning of the first line of text
2. \n - makes a new line
3. ⌘ + ↑ - moves the cursor to the beginning of the newly created first line of text
4. ⌘ + / - inserts the comment syntax for the current language (such as '//' or '#')
5. Inserts the "Copyright 2018" string
6. ⌘ + ← - moves the cursor to the beginning of the line
