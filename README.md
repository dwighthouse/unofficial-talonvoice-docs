# Unofficial Talon Docs

Documenting my learning experiences with Talon, the speech-to-text system.

## Intro

Talon is a next-generation speech-to-text system for coding, commanding, and dictating to a computer. It is currently in open beta and is under active development by its lead developer, Ryan Hileman, as of April 2018.

Talon provides very good recognition and a still-developing set of APIs for extending it and adding commands. Current versions require the use of [Dragon Naturally Speaking](https://www.nuance.com/dragon.html) and Mac OS X at this time. The Talon project also includes support for the [Tobii 4C](http://a.co/bILYudx) eye tracker, which can allow the replacement of a mouse.

These docs aim to provide a quick documentation experience on the use of various APIs, best practices, and example extensions and commands.

### Links

* [Official Site](https://talonvoice.com/) - includes latest download
* [Official Docs](https://talonvoice.com/docs/index.html)
* [Official Slack Channel](https://join.slack.com/t/talonvoice/shared_invite/enQtMjUzODA5NzQwNjYzLTY1NzZjNzM4NjVhZjZhYWFlNmZkYmU2YzE2ZjQxZjcyMTgwNDk5NDg2YzhmZDRmNmEwYThkODEyYjY4ZGZmODE)
* [Creator's Twitter Account](https://twitter.com/lunixbochs)
* [Project's Patreon](https://www.patreon.com/lunixbochs/overview)

## Installation Structure

Talon is written primarily in Python. It hooks into speech recognition engines such as Dragon Naturally Speaking.

Once installed, all of Talon's extensions and monitoring are in the folder `~/.talon`. That is, in a hidden `.talon` folder in your user folder on Mac OS X, adjacent to the Desktop and Downloads folders.

**Note: To access this hidden folder via Finder, choose "Go > Go to Folder..." from the Menu Bar, or press ⌘+⇧+G, then enter the folder path `~/.talon`**

Inside the `.talon` folder are two things to take note of.

* `talon.log`
    - Open this file in the Console utility (`/Applications/Utilities/Console.app`) to see live updates from Talon
    - Updates include:
        - Speech recognition debug information
        - Script compilation failures for user scripts
        - Anything printed to the command line in user scripts
        - Other debug information
* The `user` folder
    - Any `*.py` files in this folder will be loaded by Talon as user scripts for handling detected speech/sounds when Talon loads. While Talon is running, it will detect any changes to these scripts and re-import them immediately, reporting errors in compilation via system notifications, if necessary.

## User Scripts Overview

The vast majority of speech/sound processing is controlled directly by scripts in the `user` folder, including basic features like simple dictation. This provides a lot of control over what is recognized and how it is handled. However, at the time of writing, there is almost nothing included by default.

There are several repositories containing example scripts and tools available for copying or using as samples to build from.

* [Official Example Scripts](https://github.com/talonvoice/examples)
* [tabrat's scripts](https://github.com/tabrat/talon_user)
* [tabrat's atom integration](https://github.com/tuomassalo/atom-talon)
* [tuomassalo's scripts](https://github.com/tuomassalo/talon_user)
* [dopey's scripts](https://github.com/dopey/talon_user)

In the future, Talon will ship with a standard phrase list and language rules into which other systems can more consistenly be built. For now, however, it is largely left to the individual user to download or make the commands and scripts he wishes to use.

For those not wishing to start from scratch, a good place to begin is by downloading the [`std.py` file](https://github.com/talonvoice/examples/blob/master/std.py) and adding it to the `~/.talon/user` folder. Read through the source code understand the basic commands that will then become available.


## Using Talon (voice)

If using Dragon Naturally Speaking as the speech detection engine, start up that program first. Make sure that the microphone mode is set to "Sleep" mode (blue with moon icon), not Active or Disabled. In this mode, Dragon is only listening for its microphone activation command, which is normally `🔊 wake up`.

**Warning: Avoid saying `🔊 wake up` when using Talon to avoid enabling Dragon Naturally Speaking.**

Once Dragon is running, start Talon. It will use system notifications to indicate when both the eye tracking and voice recognition systems are ready, or whether a system is unable to start and why.
