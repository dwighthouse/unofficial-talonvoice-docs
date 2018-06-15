# Rules

A Rule is a string that defines what spoken phrases Talon can recognize. Rules are usually paired with [Actions](Actions.md) in a [Context](Context.md) `keymap` to create Voice Commands. Rules can be limited in scope by their [Context](Context.md). Rules can specify not just simple words and numbers, but also groupings, optional phrases, lists, and other options.

A given Rule is made up of one or more Structural Items. Most Structural Items can be combined where it is logical do to so. In the future, more complex nesting and creating custom Structural Items will be possible.


## Structural Items

### Word or Number

Any standard word or numerical digit. Variants in spelling are usually acceptable.

**Examples:** `save`, `apple`, `3`, `their`

### Phrase

A sequence of standard words and or numerical digits, separated by spaces.

**Examples:** `save new`, `apple 2`, `three blind mice`

### Optional Partial Phrase

TODO []

### Grouping

TODO ()

### Alternatives

TODO |

### Zero or More of Grouping

TODO *

### One or More of Grouping

TODO +

### Arbitrary Word

TODO `<dgnwords>`

### Arbitrary Phrase

TODO `<dgndictation>`

### Value from Context Set List

TODO {}


## Examples

TODO