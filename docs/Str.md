# Str

Constructor for function that, when invoked, outputs literal strings as key presses with minimal interpretation.

## Usage

The purpose of Str appears to be a way to output data directly with minimal interpretation. It converts `-`, `+`, `\n` and `\t` to their word equivalents and doesn't assume the input text is separated by spaces. This feature will primarily be used in custom helper functions where processing of the input data is done manually.

## Obtain

```python
from talon.voice import Str
```

## Examples

```python
Str('1234')(None)
```

Presses 1, 2, 3, 4 immediately, in sequence.
