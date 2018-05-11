# Key

Constructor for function that, when invoked, presses one or more sequences of key combinations. It allows for easy intepretation of key combinations involving Control, Shift, and other special keys.


## Usage

> **Key(key_string)**
>
> key_string - String containing one or more space-separated key combinations, each of which are dash-separated sets of key names that will be held at the same time
>
> *Returns* - Function that executes the sequence of key combinations when called

When the return value of Key is called, it executes each space-separated key combination in sequence. Each key combination is a dash-separated sequence of key names that will be held during that combination. For example, 'cmd-s' would hold the Command key (⌘) and then press the 's' key.

Normally, Keys are created to be called by the result of detected Command phrases in a [Context's](Context.md) keymap, rather than being called directly, like [Str](Str.md) or [press](press.md).

Check the [Keys List](KeysList.md) for a list of available key name strings.


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
