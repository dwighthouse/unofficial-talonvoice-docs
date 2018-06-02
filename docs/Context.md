# Context

A Context is a named structure containing mappings from [Commands](Commands.md) to [Actions](Actions.md). It also defines the application or window context in which this list of Command/Action combinations will or will not be recognized. By limiting the Context, the same [Commands](Commands.md) can mean and do different things in different applications, for example.


## Usage

> **Context(name[, app[, exe[, bundle[, title[, func[, group]]]]]])**
>
> name - Required string name for the Context
>
> app - (Optional) String name of the focused application to match for Context activation
>
> exe - (Optional) String full path of the focused application to match for Context activation
>
> bundle - (Optional) String bundle name of the focused application to match for Context activation
>
> title - (Optional) String window title of the focused window to match for Context activation
>
> func - (Optional) Function that receives a reference to both the active application object and the active window object; returning `True` from this function will activate the Context for the focused application and window
>
> group - (Optional) [ContextGroup](ContextGroup.md) object to apply the Context to, defaults to `voice.talon` Context
>
> *Returns* - Context object

A Context is usually created at the beginning of a [User Script](UserScriptStructure.md), then one or more keymaps (Command/Action pairing objects) are applied to it via its `keymap` member function.

In its default usage, where it provides a universal Command/Action mappings to every application at all times, a Context serves little more than a way to pipe these mappings into Talon.

However, using the various data strings and the `func` function, a Context can be significantly limited to only apply to certain applications, certain windows, or any arbitrary situation some custom code can determine. Doing so will allow for logical or memorable [Commands](Commands.md) in different applications without worrying about clobbering the meaning and functionality of the same [Commands](Commands.md) in other applications or Contexts.

Any optional parameters can be used in any combination. For example, a Context could be limited both by `bundle` and `title`, but not the `exe`, `app`, or `func`.

> **Warning:** If two different Contexts with the same name are loaded in Talon at the same time, the Context loaded most recently will take precedence. Future updates to Talon will have a way of merging Context [Commands](Commands.md) instead of overwriting them.


## Obtain

```python
from talon.voice import Context
```


## Examples

### Basic Universal Context

Create a universal Save operation that presses ⌘ + s when saying `🔊 save`. This will happen in every app.

```python
from talon.voice import Context, Key

context = Context('MyExampleContext')

context.keymap({
    'save': Key('cmd-s'),
})
```

### Context Limited by App Title

Limit this Context only to TextEdit by using the optional application title parameter (`app`) with TextEdit's name. This Context's keymap will only apply when TextEdit is active. This [Command](Commands.md) will toggle the document between Rich Text and Plain Text modes when saying `🔊 toggle doc` py programmatically pressing the key combination ⌘ + ⇧ + T

```python
from talon.voice import Context, Key

context = Context('TextEdit', app='TextEdit')

context.keymap({
    'toggle doc': Key('cmd-shift-t'),
})
```

### Context Limited by App Binary Full Path

Limit this Context only to Finder by using the optional full path to binary parameter (`exe`) with the full path to Finder's binary. This Context's keymap will only apply when Finder is active. This [Command](Commands.md) will move up one level in the folder hierarchy when saying `🔊 upward` by programmatically pressing the key combination ⌘ + ↑.

```python
from talon.voice import Context, Key

context = Context('Finder', exe='/System/Library/CoreServices/Finder.app/Contents/MacOS/Finder')

context.keymap({
    'upward': Key('cmd-up'),
})
```

### Context Limited by App Bundle Name

Limit this Context only to Google Chrome by using the optional named bundle parameter (`bundle`) with Google Chrome's app bundle name. This Context's keymap will only apply when Google Chrome is active. This [Command](Commands.md) focuses the address bar when saying `🔊 address bar` by programmatically pressing the key combination ⌘ + L.

```python
from talon.voice import Context, Key

context = Context('GoogleChrome', bundle='com.google.Chrome')

context.keymap({
    'address bar': Key('cmd-l'),
})
```

> **Note:** The app bundle name can be determined by running `osascript -e 'id of app "APP_NAME"'` in Terminal, where `APP_NAME` is the name of the app, such as 'Slack' or 'Google Chrome'. Alternatively, the app bundle name can be found by exploring inside the app's Package Contents. Access the Package Contents by right-clicking the app's executable in the Applications directory (usually at `/Applications`), and then choosing "Show Package Contents". Inside the Package, look inside the `Contents/Info.plist` file to see the Bundle Identifier.

### Context Limited by Window Title

Limit this Context only to windows with the name 'journal.md'. This Context's keymap may apply in multiple applications, so long as the window name matches. This [Command](Commands.md) starts a new log entry at the top of the file, with the current date, then starts the next line, when saying `🔊 new log`.

```python
from talon.voice import Context, press, Str
import datetime

context = Context('Journal', title='journal.md')

def new_entry(m):
    press('cmd-up') # Go to beginning of first line of the file
    Str(str(datetime.datetime.now()))(None) # Add the current date

    # Create spacing from any previous entries
    press('return')
    press('return')
    press('return')

    # Return to just after the date entry
    press('up')
    press('up')

    # Enter start of new list item
    Str('* ')(None)

context.keymap({
    'new log': new_entry,
})
```

> **Warning:** Since this is not an application limitation, but a limitation based on window name, this Context could theoretically apply to multiple applications. Generally speaking, it's a good idea to specify an application in addition to a window title, or better yet, use the `func` parameter to more intelligently work with application and window values.


### Context Limited by Function

Limit this Context by an arbitrary function. If the `func` function returns `True`, the Context will be active, otherwise it will not be. The app and window objects are passed in for use, but any arbitrary code and data source can be used.

This [Command](Commands.md) starts a blockquote entry on a new line, when saying `🔊 quoted`, but only in files with the ".md" extension in the title.

```python
from talon.voice import Context, press, Str

def is_markdown(app, window):
    return '.md' in window.title

context = Context('Markdown', func=is_markdown)

def new_blockquote(m):
    press('return') # Make new line
    Str('> ')(None) # Add the blockquote symbol

context.keymap({
    'quoted': new_blockquote,
})
```

For more examples of this dynamic Context activation, consider these examples:

* [Context for Terminal when VIM is running](https://github.com/talonvoice/examples/blob/master/vim.py)
* [A slightly more robust language-specific window detecting Context](https://github.com/tabrat/talon_user/blob/master/java.py)
* [Context activating for one of multiple app bundle names](https://github.com/tabrat/talon_user/blob/master/jetbrains.py)
