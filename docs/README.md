# Unofficial Talon Docs

Documenting my learning experiences with Talon, the speech-to-text system. These docs are not authorative or complete. After reading them you should be able to extend and use Talon.


## Intro

Talon is a speech-to-text system for commanding and dictating to a computer, aimed at helping programmers write code without a keyboard. It is currently in open beta and is under active development by creator Ryan Hileman as of March 2019.

You can extend Talon, for example add custom phrases. MacOS ≥ 10.11 is required; Linux is not yet supported. You can use ($150) [Dragon Naturally Speaking](https://www.nuance.com/dragon.html) or Apple’s (free) default text-to-speech engine. The Talon project also supports the [Tobii 4C](http://a.co/bILYudx) eye tracker, which can replace the mouse.





## Documentation

* Education
    - [Using Talon (voice)](UsingTalonVoice.md) - How to begin
    - [Folder Structure](FolderStructure.md) - Where Talon stores its user-accessible Scripts and logs
    - [Dictation Philosophy](DictationPhilosophy.md) - Talon's underlying philosophy of speech-to-text phrase structure
* User Scripts
    - [User Script Overview](UserScriptOverview.md) - What User Scripts are and how to obtain them
    - [User Script Structure](UserScriptStructure.md) - How to make a new User Script in which all other API calls will be made
    - [Rules](Rules.md) - Strings defining what spoken phrases can be recognized, with many options
    - [Actions](Actions.md) - One or more operations performed in response to a successful Rule recognition
* API
    - [Context](Context.md) - Containing [Rules](Rules.md) and [Actions](Actions.md), limiting scope to particular applications or windows
    - [ContextGroup](ContextGroup.md) - A grouping of [Contexts](Context.md)
    - [Key](Key.md) - Pressing sequences of key combinations
    - [press](press.md) - Pressing single key combination immediately
    - [Rep](Rep.md) - Repeating past [Actions](Actions.md)
    - [Str](Str.md) - Entering whole strings
* Data
    - [Alphabet](Alphabet.md) - Saying individual letters
    - [Keys List](KeysList.md) - String representations of all keys for use with API calls
    
    
    
    
### Links

* [Official Site](https://talonvoice.com/) - includes latest download
* [Official Docs](https://talonvoice.com/docs/index.html)
* [Official Slack Channel](https://join.slack.com/t/talonvoice/shared_invite/enQtMjUzODA5NzQwNjYzLTY1NzZjNzM4NjVhZjZhYWFlNmZkYmU2YzE2ZjQxZjcyMTgwNDk5NDg2YzhmZDRmNmEwYThkODEyYjY4ZGZmODE)
* [Creator's Twitter Account](https://twitter.com/lunixbochs)
* [Project's Patreon](https://www.patreon.com/lunixbochs/overview)
