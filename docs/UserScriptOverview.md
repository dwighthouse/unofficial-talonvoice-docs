# User Script Overview

The vast majority of speech/sound processing is controlled directly by Scripts in the `~/.talon/user` folder ([find out more](FolderStructure.md)), including basic features like simple dictation. This provides a lot of control over what is recognized and how it is handled. However, at the time of writing, there is almost nothing included by default.

There are several repositories containing example Scripts and tools available for copying or using as samples to build from.

* [Official Example Scripts](https://github.com/talonvoice/examples)
* [dwighthouse's scripts](https://github.com/dwighthouse/talonvoice-scripts) - mine 😉
* [tabrat's scripts](https://github.com/tabrat/talon_user)
* [tuomassalo's scripts](https://github.com/tuomassalo/talon_user)
* [tuomassalo's atom integration](https://github.com/tuomassalo/atom-talon)
* [dopey's scripts](https://github.com/dopey/talon_user)

In the future, Talon will ship with a standard phrase list and language rules into which other systems can more consistently be built. For now, however, it is largely left to the individual user to download or make the [Commands](Commands.md) and Scripts he wishes to use.

For those not wishing to start from scratch, a good place to begin is by downloading the [`std.py` file](https://github.com/talonvoice/examples/blob/master/std.py) and adding it to the `~/.talon/user` folder. Then, reading through the source code will illustrate what [Commands](Commands.md) are available and how to begin adding new ones.

To build new User Scripts, read about the [User Script Structure](UserScriptStructure.md).
