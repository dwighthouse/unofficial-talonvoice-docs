# Key

Constructor for function that, when invoked, presses one or more key combination sequences. It is intended to be placed directly in a [Context's](Context.md) keymap, rather than being called directly, which [press](press.md) is more suited to.


## Usage

> **Key(key_string)**
>
> key_string - String containing one or more space-separated keys or key combinations
>
> *Returns* - Function that executes the key combination sequences when called

When the return value of Key is called, it executes each space-separated keys or key combinations in sequence.

A single key string simply presses the corresponding key, such as the string 'k', which will press the K key.

A key combination is a dash-separated set of modifier keys followed by a single non-modifier key. For example, 'cmd-shift-s' would hold the command key (⌘) and the Shift key (⇧), and then press the S key.

These can be combined in any order, and in any quantity, when separated by spaces. For example, the `key_string` 'cmd-p enter' would hold the command key (⌘) and press the P key, then release both, then it would press the Enter key.

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
from talon.voice import Key
```


## Examples

These examples are used within a [Context](Context.md), either defined with a keymap, or called directly from a function. Calling Key directly from a function is discouraged in favor of using [press](press.md).

### Within a Context's keymap

```python
context.keymap({
    'save': Key('cmd-s'),
})
```

When saying `🔊 save`, presses ⌘ + s, which will perform a Save operation in most apps.

### Called directly in a function

```python
def end_of_line_enter(m):
    Key('cmd-right enter')(None)

context.keymap({
    'make next line': end_of_line_enter,
})
```

When saying `🔊 make next line`, calls a function that presses ⌘ + → (typically moves the cursor to the end of the current line in macOS), followed by pressing the enter key. That is, "Go to the end of the line and press enter."

Normally, if calling a key combination directly via a function, the [press](press.md) function is preferred over Key.

The main difference between Key and [press](press.md) is that [press](press.md) only accepts a single key combination, when Key allows space-separated sequences of key combinations. Otherwise, the only difference is that [press](press.md) can be called directly, it is not a constructor for a function as Key is.
