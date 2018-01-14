---
layout: post
title: "Discord Bots!"
date: 2018-01-14
---

## Context

I love Discord just as much as anyone else probably does if you ask them. Discord is one of the most convenient platforms for chatting on desktop (and mobile!) in my opinion, so it would only be a matter of time before I looked for ways to improve it. Bots are one of the primary features contributing to many various improvements.

## Is This a Guide to Writing a Bot?

Not really, however I'll be posting some useful code snippets throughout while discussing my latest bot, [MonikaBot](https://github.com/Hydro95/MonikaBot). At any point you can view the entire source code for the bot from the previous link as well if you're looking for a more descriptive guide of what a working bot could look like. Without further ado, I'll begin discussing some features of my bot and how I got it working.

## What do I Need to Run a Bot?

If you're reading this from a computer, great! You're likely capable of running a bot. There are many useful libraries available to create Discord bots in various different languages, but the language of choice for MonikaBot is Javascript. You can take a peek at [Discord.js](https://discord.js.org/#/) and [Node.js](https://nodejs.org/en/) to really immerse yourself in the details. Both packages are being managed by [npm](https://www.npmjs.com) on my machine. Discord.js is what allows the bot to interact with Discord and Node.js is what allows you to run Javascript applications in a terminal environment. Thankfully, networking is handled by both Node.js and Discord.js, so once you create a bot using Discord's site you only have to log it in using a few lines of code and a login key.

```javascript
var Discord = require("discord.js");
require("./tokens.js");
...
var monika = new Discord.Client();
...
monika.login(login_token);
```

The `tokens.js` file is just a file with variables containing the keys and login tokens so that I don't push them to github and allow the entire world to run my bot.

## How Does the Bot... Understand?

In most cases, you'd want your bot to pick up input by using a special "command" prefix. my bot uses `=` to signify the start of a command. An example of a command my bot can use is `=translate en | 私はモニカボットです。` When a message is sent in Discord, an event is fired that notifies the bot a message was sent and the bot is provided the message. If the message doesn't start with the prefix I tell the bot to ignore the message. Using a prefix is the best way to ensure your bot doesn't activate when it isn't wanted.

The commands follow a certain convention I set for myself:

`=[command name] < [arg 0] | [arg 1] | [arg 2] | [arg 3] | ...>`

Arguments are completely optional depending on what command is used and are separated using `|`. My reasoning behind this is that many commands use blocks of text or sentences as arguments so spaces aren't a convenient separator for arguments, and commas are also fairly common. The bot takes in the message and sorts the command name into a variable and the arguments into a list. For now, a `switch` statement is being used to provide the functionality to each command. For organizational purposes, I outsourced some of the major themes of functionalities to their own files to try and cut down the size of `index.js` (the main file) and improve readability.

## How to Not Reinvent the Wheel

The solution is npm. As far as I know, if you've ever thought of accomplishing something using a script or needed a bridge between some obscure API and the language you're using, somebody is bound to have made an npm package for it. Of course, you should always exercise caution when making use of random packages made by strangers on the internet, especially when they're larger in size + complexity or have small download counts. You can double check all of that on npm's website where it lists all the packages.

For example, my bot does image searching using an npm package that fetches data from Google images, and another that uses Google's translate API to translate text. For fun, I created a Last.fm tracker that uses an npm package to allow Javascript support for the Last.fm API. The best part about combining all these services in one place is not having to open a new browser tab to check in on anything; it can all be done right from the comfort of your Discord client.

## Read the Docs.

Read the docs before you even begin to read Google. The most comprehensive and focused bank of information is right there in the docs. If you're more of a beginner and are easily overwhelmed by all the information, definitely do make use of Google, but make an attempt to familiarize yourself with the documentation. Don't go and make a post on Stack Overflow if you haven't read the documentation. You might find your answer inside! For Discord.js, you can find the documentation [here.](https://discord.js.org/#/docs/main/stable/general/welcome)