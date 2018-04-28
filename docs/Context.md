# Context

TODO: In progress

Basic usage:

```python
ctx = Context('CONTEXT_NAME')
```

Key commands are added to the context.

```python
ctx.keymap({ ...KEYMAP_DATA... })
```

Make sure it doesn't conflict. Future updates will have a way of merging context commands instead of overwriting them.


Can allow its commands to be limited to specific apps or window names.

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


```python
ctx = Context('spotify', bundle='com.spotify.client')
```

https://github.com/tabrat/talon_user/blob/master/spotify.py
