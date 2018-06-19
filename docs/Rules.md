# Rules

A Rule is a string that defines what spoken phrases Talon can recognize. Rules are usually paired with [Actions](Actions.md) in a [Context](Context.md) `keymap` to create Voice Commands. Rules can be limited in scope by their [Context](Context.md). Rules can specify not just simple words and numbers, but also groupings, optional phrases, lists, and other options.

A given Rule is made up of one or more Structural Items. Most Structural Items can be combined and nested where it is logical do to so. In the future, more complex nesting will be available, as well as the ability to create custom Structural Items.



## Structural Items

### Word or Number

Any standard word or numerical digit. Variants in spelling are usually acceptable.

* `save` - Recognizes "save"
* `apple` - Recognizes "apple"
* `3` - Recognizes "three"
* `their` - Recognizes "there", "their", and "they're"



### Phrase

A sequence of standard words and or numerical digits, separated by spaces.

* `save new` - Recognizes "save new"
* `apple 2` - Recognizes "apple two"
* `three blind mice` - Recognizes "three blind mice"



### Alternatives

Alternative words and phrases can be recognized as the same Rule by separting the options with a pipe ("|"). For now, Alternatives have to be contained within a Grouping set of parentheses (see below).

This is mostly used when there is more than one common way to describe an [Action](Actions.md), or to provide a shorthand verbal syntax while retaining the more verbose and understandable original.

This can also be useful if there are alternate spellings, or very similar sounding words, for a word that is harder to recognize.

* `(enter | return)` - Recognizes either "enter" or "return"
* `(dubquote | double quote)` - Recognizes either "dubquote" or "double quote"
* `(tilde | till duh | till day)` - Recognizes "tilde", in spite of alternative pronounciations



### Optional Partial Phrase

A sequence of Structural Items inside square brackets that will be counted as optional to the recognition of the phrase. The bracketed sequences can be nested.

* `[show] console` - Recognizes both "show console" and "console"
* `close [[the] window]` - Recognizes "close", "close window", and "close the window", but not "close the"

#### Usage for Ambiguity Reduction

Optional Partial Phrases can sometimes also be useful in providing Talon with some help recognizing spoken phrases with ambigious length by adding an optional final terminating word or phrase. For example, if using the (later explained) `<dgndictation>` to recognize an arbitrary phrase, adding an optional `[over]` ending phrase will help Talon deliniate when to stop that particular Rule recognition. Without using the optional phrase, Talon will have to rely on an auditory pause.

> **Note:** If the entire Rule is entirely made up of an Optional Partial Phrase (ex. `[wholely optional]`), Talon will treat the Rule as if it does not have the brackets, aka, not optional. Avoid this construction as it serves no purpose and might lead to confusion.hello worldhello world movementhello world movement



### Grouping

A sequence of Structural Items that are logically separate from other parts of the Rule using parentheses. It is primarily used for grouping Alternatives within a larger Rule, or to provide a hook for other Structural Items to apply to.

* `run make (durr | dear)` - Recognizes either "run make durr" or "run make dear"
* `(bang | exclamation point)` - Recognizes either "bang" or "exclamation point"
* `(ok)+` - Recognizes one or more "ok" verbal phrases in quick succession (see "One or More")



### Zero or More

When following a word or Grouping with a star ("*"), the word or Grouping contents can be recognized zero or more times. It is recommended to always use the Grouping style.

* `my (super | quantum)* computer` - Recognizes "my computer", "my super computer", "my quantum computer", "my super quantum computer", "my quantum super computer", "my quantum quantum computer", etc.
* `really* good` - Recognizes "good", "really good", "really really good", etc.
  - **This style is not recommended.**



### One or More

When following a word or Grouping with a plus ("+"), the word or Grouping contents will be recognized one or more times. It is recommended to always use the Grouping style.

* `(eye | mighty | apple)+ mouse` - Recognizes "iMouse", "Mighty Mouse", "Apple Mouse", "Apple iMouse", etc.
  - Does **NOT** recognize "mouse"
* `simply being loved+` - Recognizes "simply being loved", "simply being loved loved", ["simply being loved loved loved"](https://www.youtube.com/watch?v=VGqBGdHcbd8), etc.
  - **This style is not recommended.**

> **Note:** `(...)*` is not the equivalent of `[...]+`. `[...]+` is a syntax error.



### Arbitrary Phrase

A sequence of one or more words that will be recognized as a whole, without explicitly defining what words those are. This is defined in Rule strings as `<dgndictation>`.

> **Note:** The Arbitrary Phrase Structural Item will often, but not always, intrepret other Rules inside the Arbitrary Phrase. This can lead to unexpected output.

> **Warning:** The Arbitrary Phrase Structural Item is not yet fully implemented, please use it sparingly.

* `phrase <dgndictation>` - Recognizes "phrase (ANY_NUMBER_OF_WORDS) (AUDITORY_PAUSE)"
* `say <dgndictation> [over]` - Recognizes "say (ANY_NUMBER_OF_WORDS) (AUDITORY_PAUSE)" or "say (ANY_NUMBER_OF_WORDS) over"
  - Using an optional word at the end to signal the end of a phrase recognition can sometimes improve Talon's ability to recognize.
  - However, this only applies sometimes, in relation to a subsequent recognized Rule. The implementation is currently incomplete, so do not rely on this feature.



### Value from Context Set List

A named set of values that can be dynamically controlled by the [Context](Context.md). This is defined in Rules strings as `{CONTEXT_NAME.LIST_NAME}`.

A [Context](Context.md) can recieve a dynamic list of values using its member function `set_list`. `set_list` takes a string (the LIST_NAME), and a list of strings (DYNAMIC_LIST).

The DYNAMIC_LIST, when used in a Rule, is effectively equivalent to an Alternatives Grouping.

For example:

1. If the [Context](Context.md) name was "computer"
2. And if the DYNAMIC_LIST name was "os"
3. And if the DYNAMIC_LIST currently contained
   - `['mac os', 'linux', 'windows', 'free bsd', 'minux']`

Then when a Rule contains `{computer.os}`, it would effectively be the same as writing `(mac os | linux | windows | free bsd | minux)` in the rule.

The reason this might be useful is because the DYNAMIC_LIST can be dynamically updated at any time, as is its namesake.

To see a practical example, read the [source of the `switcher.py` script](https://github.com/talonvoice/examples/blob/master/switcher.py). This script dynamically recognizes when applications are opened and closed. By updating a list of application names when anything changes, the script allows the user to switch to any open application, even as the set of available applications changes.

> **Warning:** This is not well defined and there is some subtlety missing in this description that can become important. Please use with care.



## Combining Structural Items

Structural Items can be combined and nested where it makes sense. Here are a few examples.

* `(upper | title | string)+ [<dgndictation>]` - Recognizes any combination and quantity of "upper", "title", and "string" followed by (ANY_NUMBER_OF_WORDS)
* `(op | is) greater [than]` - Recognizes "op greater", "is greater", "op greater than", and "is greater than"



## Future Structural Items

Some Structural Items are not yet fully implemented or available.

**These are placeholders. Do not use.**

### Arbitrary Word

A single, arbitrary word. Useful for recognizing certain words that are defined as Rules in other Voice Commands, so the word can be entered literally or used directly, rather than triggering the Voice Command associated with it. This is defined in Rule strings as `<dgnwords>`.

* `word <dgnwords>` - Recognizes "word star", "word book", etc.
  - Does **NOT** recognize "word"
  - Saying any words after the `<dgnwords>` word will cause Talon to start its recognition system anew after it.

### Custom Structural Item

Future versions will support some form of user-defined Structural Item, where a the `<x>` syntax can be used in the Rule string, and the recognition of "x" will be left to user-defined functions.

For example, one could conceivably make a `<numbers>` Custom Structural Item, wherein an arbitrarily large but valid number, spoken in parts (one million five hundred sixty thousand four hundred and fourty five), could be recognized as a single number value (1560445).
