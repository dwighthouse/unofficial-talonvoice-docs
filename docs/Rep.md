# Rep

Constructor for function that, when invoked, repeats the last Action. That could include a Command Action, a Data Entry task, or even a previous repetition Action.


## Usage

> **Rep(repeat_count)**
>
> repeat_count - Integer indicating the number of times to repeat the previous Action
>
> *Returns* - Result of the execution of Rep, which is needed by Talon to prevent infinite recursion

The Rep function constructor takes a number argument indicating how many times to repeat the previous Action or task.

Like [Key](Key.md), Rep can be used in response to a spoken Command phrase, or called directly in a custom function. However, when called directly, it must be carefully constructed as described below.


## Obtain

```python
from talon.voice import Rep
```


## Examples

These examples are used within a [Context](Context.md), either defined with a keymap, or called directly from a function.

### Within a Context's keymap

```python
context.keymap({
    'twice': Rep(1),
})
```

When saying `🔊 twice`, whatever happened immediately before will be repeated once. For example, saying `🔊 phrase hello world twice` would result in "hello worldhello world" being printed because the first part (`🔊 phrase hello world`) enters "hello world", and the second part (`🔊 twice`) enters it again.

> **Warning:** The number argument passed to Rep is one less than the number of output values, not equal to it. Rep cannot retroactively remove the result of the previous Action, so this off-by-one must be taken into account.

### Called directly in a function

This example function does the same thing as the previous example, but using a direct call.

```python
def repeat_twice(m):
    from talon.voice import talon

    repeater = Rep(1)
    repeater.ctx = talon
    return repeater(None)

context.keymap({
    'twice': repeat_twice,
})
```

> **Warning:** The constructed Rep function, `repeater` in this case, must have its `ctx` attribute set to `talon`, which is imported from `talon.voice`. Additionally, the result of calling `repeater` must be returned. Failing to do either will result in a Talon error.

A general-purpose repetition Command can be built by parsing numbers in a phrase, then using the detected integer as input to the Rep constructor. An implementation of this is [repeater.py](https://github.com/dwighthouse/talonvoice-scripts/blob/master/repeater.py).