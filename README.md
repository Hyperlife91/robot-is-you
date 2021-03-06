# About

A fun Discord bot based on the indie game [Baba Is You](https://store.steampowered.com/app/736260/Baba_Is_You/) (by Arvi Teikari). This bot was written with the [discord.py](https://discordpy.readthedocs.io/en/latest/) library for Python 3.x.

# Functionality

A list of all commands can be seen using the `help` command. (By default, the bot has a prefix of `+`.)

This bot primarily features rendering and animation of
tiles in *Baba Is You* (through the `tile` and `rule` commands), 
as well as *Baba Is You* levels (using the `level` command).

*Example command:*

![Example command](https://cdn.discordapp.com/attachments/420095557231443988/596606587800387594/unknown.png)

*Example output:*

![Example command output](https://cdn.discordapp.com/attachments/420095557231443988/596606636215500816/unknown.png)

**NOTE: Output is in the form of an animated gif. Try the commands yourself for the best experience.**

# Invite

[Invite the bot to your server!](https://discordapp.com/api/oauth2/authorize?client_id=480227663047294987&scope=bot&permissions=388160)

# Support server

Leave any suggestions, bug reports or questions in the official [support Discord server](https://discord.gg/rMX3YPK).

# To Host This Yourself

Please follow the terms of the license!

Install the requirements: `pip install -r requirements.txt`.

Run the bot using `python3 ROBOT.py`.

(The bot may not work properly on Windows, as it makes use of some unix-ish shell commands for the convenience of the programmer.)

## Required files

Bot configuration is in `config/setup.json`. It contains the following fields:

* `auth_file` Should point to a JSON file with a `token` field with your bot token.
* `activity` A "playing" message to set at login.
* `description` A description to use in the help command.
* `prefixes` A list of strings that can be used to trigger commands.
* `trigger_on_mention` A boolean dictating whether bot @mentions will behave as a command prefix.
* `webhook_id` The ID of a webhook to report command errors to. Requires the `manage webhooks` permission in the webhook's channel.
* `owner_id` The ID of the bot owner.
* `embed_color` The color of embedded messages.
* `log_file` The file to report logs to.
* `cogs` A list of strings -- cogs to load into the bot.

If the bot complains about missing files or directories in `cache/` or `target/`, create them. Specifically, you should have the following paths created:
* `cache/tiledata.json` A JSON file defaulting to the empty object `{}`. Contains tile data for rendering objects.
* `cache/blacklist.json` A JSON file defaulting to the empty object `{}`. Contains the IDs of blocked users.
* `cache/leveldata.json` A JSON file defaulting to the empty object `{}`. Contains level metadata.
* `cache/debug.json` A JSON file defaulting to the empty object `{}`. Contains debug data about bot restarts. 
* `target/renders/vanilla/` An empy directory. Contains levels rendered into animated GIFs.
* `target/letters/big/` An empty directory. Contains sprites for "tall" letters (like `IS`) scraped from vanilla sprites.
* `target/letters/small/` An empty directory. Contains sprites for "short" letters (like `BABA`) scraped from vanilla sprites.
* `target/letters/thick/` An empty directory. Contains sprites for "individual" letters (like `BA`) scraped from vanilla sprites.

## Setup commands (bot owner only)

`<>` denotes a required argument, and `[]` denotes an optional argument.

* `loaddata` Collects tile metadata from `values.lua`, `editor_objectlist.lua`, `data/worlds/vanilla/*.ld` files and `data/custom/*.json` files, and saves it to disk. The following commands are also available, but it is **strongly recommended** to use `loaddata`.
* * `loadchanges` Collects tile metadata only from `.ld` files.
* * `loadcolors` Collects tile metadata only from `values.lua`.
* * `loadcustom` Collects tile metadata only from custom `.json` files.
* * `loadeditor` Collects tile metadata only from `editor_objectlist.lua`.
* * `dumpdata` Dumps collected tile metadata into `cache/tiledata.json`.
* `loadletters` Scrapes individual letter sprites from image sprites in `data/sprites/*`, as well as pre-made letters from `data/letters/**/*` and places the results in `target/letters/`.
* `loadmap <world_name> <level_id> [include_metadata?]` Reads and renders an animated GIF of the provided level. `world_name` should be `vanilla` in most cases. If `include_metadata` is `True`, the level metadata is stored as well. Useful for re-rendering levels changed in an update without re-doing everything.
* `loadmaps` Reads and renders every single level in `data/levels/vanilla/`. Also collects metadata.

* To load tile data, run the `loaddata` command. To load letter data (for custom text), run the `loadletters` command. To load and pre-render levels, run the `loadmaps` command.

## Adminstrative commands (bot owner only)

`<>` denotes a required argument, and `[]` denotes an optional argument.

* `load [cog]`(aliases: `reload`, `reloadcog`) Reloads a cog. Useful to hot-reload modules of the bot. If the argument is omitted, all cogs are reloaded.
* `restart` Exits the bot with a return code of 1. (I use this with a process manager that restarts failed tasks.)
* `logout` (aliases: `kill`, `yeet`) Exits the bot with a return code of 0. 
* `debug` Gives some debug information about the bot health, including the number of IDENTIFY and RESUME payloads in the past 24 hours.
* `ban <user_id>` Adds a user ID to the list of blacklisted users. (This might actually be broken, haven't tested properly)
* `leave <guild_id>` Leaves a guild.
* `hidden` Lists all hidden commands.
* `doc <command>` Displays the docstring for a command.

The bot additionally uses [Jishaku](https://github.com/Gorialis/jishaku/) to interface with `git`, run shell commands and evaluate python. Read more about the `jsk` command at [Jishaku's documentation](https://jishaku.readthedocs.io/en/latest/).

