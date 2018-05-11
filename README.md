# Unofficial Talon Docs

Documenting my learning experiences with Talon, the speech-to-text system. These docs are not authorative or complete, but instead represent an 80/20 view of the API sufficient for getting started making extensions and using the system.


## Intro

Talon is a next-generation speech-to-text system for coding, commanding, and dictating to a computer. It is currently in open beta and is under active development by creator, Ryan Hileman, as of April 2018.

Talon provides very good recognition and a still-developing set of APIs for extending it and adding commands. Current versions require the use of [Dragon Naturally Speaking](https://www.nuance.com/dragon.html) and macOS at this time. The Talon project also includes support for the [Tobii 4C](http://a.co/bILYudx) eye tracker, which can allow the replacement of a mouse.

These docs aim to provide a quick documentation experience on the use of various APIs, best practices, and example extensions and commands.

### Links

* [Official Site](https://talonvoice.com/) - includes latest download
* [Official Docs](https://talonvoice.com/docs/index.html)
* [Official Slack Channel](https://join.slack.com/t/talonvoice/shared_invite/enQtMjUzODA5NzQwNjYzLTY1NzZjNzM4NjVhZjZhYWFlNmZkYmU2YzE2ZjQxZjcyMTgwNDk5NDg2YzhmZDRmNmEwYThkODEyYjY4ZGZmODE)
* [Creator's Twitter Account](https://twitter.com/lunixbochs)
* [Project's Patreon](https://www.patreon.com/lunixbochs/overview)


## Documentation

* Education
    - [Using Talon (voice)](docs/UsingTalonVoice.md) - How to start up and begin using Talon for voice control
    - [Folder Structure](docs/FolderStructure.md) - Where Talon stores its user-accessible Scripts and logs
    - [User Script Overview](docs/UserScriptOverview.md) - What User Scripts are and how to obtain them
    - [Dictation Philosophy](docs/DictationPhilosophy.md) - Talon's underlying philosophy of speech-to-text phrase structure
* API
    - [User Script Structure](docs/UserScriptStructure.md) - How to make a new User Script in which all other API calls will be made
    - [Context](docs/Context.md) - Containing Commands and Actions, limiting scope to particular applications or windows
    - [Key](docs/Key.md) - Pressing sequences of key combinations
    - [press](docs/press.md) - Pressing single key combination immediately
    - [Rep](docs/Rep.md) - Repeating past Actions
    - [Str](docs/Str.md) - Entering whole strings
* Data
    - [Alphabet](docs/Alphabet.md) - Saying individual letters
    - [Keys List](docs/KeysList.md) - String representations of all keys for use with API calls