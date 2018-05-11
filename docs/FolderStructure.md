# Folder Structure

Talon's user-facing API and scripts are written in Python. It hooks into speech recognition engines such as Dragon Naturally Speaking. In future versions, it will likely come bundled with its own speech recognition engine.

Once installed, all of Talon's extensions and monitoring are in the folder `~/.talon`. That is, in a hidden `.talon` folder in the user folder on macOS, adjacent to the Desktop and Downloads folders.

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
