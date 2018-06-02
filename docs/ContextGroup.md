# ContextGroup

A ContextGroup is a grouping of [Contexts](Context.md). By default, a new [Context](Context.md) will be added to the `voice.talon` ContextGroup. Alternatively, a ContextGroup object can be passed to a new [Context](Context.md), adding it to that group.

These groupings can be enabled or disabled as a whole, which could allow for creating different modes of operation. For example, in the [speech_toggle.py script](https://github.com/talonvoice/examples/blob/master/speech_toggle.py), a ContextGroup "sleepy" is created for the [Commands](Commands.md) to enable or disable the default `voice.talon` ContextGroup. This effectively makes these [Commands](Commands.md) a toggle for recognition. Since this activity will potentially disable all normal [Command](Commands.md) recognition, these [Commands](Commands.md) have to be located in a different ContextGroup to remain active.

> **Warning:** A single spoken phrase should not contain [Commands](Commands.md) from more than a single ContextGroup. Doing so will cause Talon to ignore everything after the first [Command](Commands.md) it recognizes.
