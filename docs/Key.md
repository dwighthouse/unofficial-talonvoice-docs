# Key

Constructor for function that, when invoked, presses one or more sequences of key combinations. It allows for easy intepretation of key combinations involving Control, Shift, and other special keys.

## Usage

One or more key combinations are separated by spaces. Key combinations are constructed by a sequence of named keys separated by dashes.

Normally, Keys are created to be called by the result of detected command phrases, rather than being called directly, like [Str](Str.md).

Check the [Keys List](KeysList.md) for a list of available key names.

## Obtain

```python
from talon.voice import Key
```

## Examples

```python
Key('cmd-s')
```

When called, presses ⌘ + s, which will perform a Save operation in most apps.



```python
Key('cmd-right enter')
```

When called, presses ⌘ + → (typically moves the cursor to the end of the current line in macOS), followed by pressing the enter key. That is, "Go to the end of the line and press enter."