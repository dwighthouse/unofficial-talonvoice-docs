# Context

A Context is a named structure containing mappings from Command phrases to [Key](Key.md) Actions, [Str](Str.md) Actions, [Rep](Rep.md) Actions, and custom functions. It also defines the application or window context in which this list of Command/Action combinations will or will not be recognized. By limiting the context of some phrases, the same Command can mean and do different things in different applications, for example.


## Usage

> **Context(name[, app[, exe[, bundle[, title[, func[, group]]]]]])**
>
> name - Required string name for the Context
>
> app - (Optional) TODO
>
> exe - (Optional) TODO
>
> bundle - (Optional) String that limits the Context to apps with the same bundle name
>
> title - (Optional) String that limits the Context to windows with the same window title
>
> func - (Optional) Function that is called with an app and window object passed, returning `True` from which activates the Context
>
> group - (Optional) TODO
>
> *Returns* - Context object

A Context is usually created at the beginning of a User Script and then one or more keymaps (Command/Action pairing objects) are applied to it via its `keymap` member function.

In its default usage, where it provides a universal Command/Action mappings to every application at all times, a Context serves little more than a way to pipe these mappings into Talon.

Where it becomes more complicated and interesting is when a Context is limited in various ways to a specific application, window name, or some other data.

> **Warning:** If two different Contexts with the same name are loaded in Talon at the same time, the Context loaded most recently will take precedence. Future updates to Talon will have a way of merging Context Commands instead of overwriting them.


## Obtain

```python
from talon.voice import Context
```


## Examples

### Basic Universal Context

Create a universal Save command that presses ⌘ + s when saying `🔊 save`. This will happen in every app.

```python
from talon.voice import Context, Key

context = Context('MyExampleContext')

context.keymap({
    'save': Key('cmd-s'),
})
```

### Context Limited by App Bundle Name

Limit this context only to Google Chrome by using the optional named bundle parameter with Google Chrome's app bundle. This Context's keymap will only apply when Google Chrome is active. This Command focuses the address bar when saying `🔊 address bar` by pressing the key combination ⌘ + l.

```python
from talon.voice import Context, Key

context = Context('GoogleChrome', bundle='com.google.Chrome')

context.keymap({
    'address bar': Key('cmd-l'),
})
```

> **Note:** The app bundle name can be determined by running `osascript -e 'id of app "APP_NAME"'` in Terminal, where `APP_NAME` is the name of the app, such as 'Slack' or 'Google Chrome'. Alternatively, the app bundle name can be found by exploring inside the app's Package Contents. Access the Package Contents by right-clicking the app's executable in the Applications directory (usually at `/Applications`), and then choosing "Show Package Contents. Inside the Package, look inside the `Contents/Info.plist` file to see the Bundle Identifier.

### Context Limited by Window Title

TODO


### Context Limited by Dynamic Function

TODO

---

```python
ctx = Context('crawl', bundle='com.apple.Terminal', func=lambda app, win: 'crawl' in win.title)
```

https://github.com/talonvoice/examples/blob/master/crawl.py


That limitation can be programmatically determined

```python
ctx = Context('code', func=lambda app, win:
              any(app.bundle == b for b in bundles)
              or any(win.doc.endswith(l) for l in languages)
              )
```


One can attach data to a context to make use of it during commands or to influence what commands are possible at any given time.

https://github.com/talonvoice/examples/blob/master/switcher.py

### More examples

```python
ctx = Context('vim', bundle='com.apple.Terminal', func=lambda app, win: 'vim' in win.title)
```

https://github.com/talonvoice/examples/blob/master/vim.py
