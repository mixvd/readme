# Squadron

### Description

Originally created as a personal tool for my own server, Squadron has now evolved into something bigger than I ever anticipated. Obviously, I could have used any of the other Administration Addons, like ULX, SAM, ServerGuard, etc. However, they all had issues. Some were conflicting with Helix, others were bloated with features I did not need or were lacking features I wanted, some had a bad reputation, and others costed money. So I took it upon myself to make my own administration solution which only contained useful features for a SeriousRP server, no bloat, and one that integrated with Helix like a glove.

### Conflicts

At this time, Squadron does not natively support other Administration Mods (ULX, SAM, ServerGuard, etc), and will conflict with them. You are free to attempt to use them alongside it, but unintended behavior may occur. You have been warned.

### Features

Squadron comes with a large assortment of features to help Server Owners administrate their server, including but not limited to:

* Advanced Admin ESP system
    * Detailed player information
    * Misc Entity ESP
    * Easy custom entity ESP registration
* Anti-Bunny-Hop
* Anti-Money-Duping (notifies staff when large amounts of cash is transferred)
* Death Tracking
* Dedicated Server Administration Faction
    * Automatic flag administration on spawn
    * Automatic staff character creation on rank set
    * Command to toggle Staff Tools (Physics Gun, Toolgun) on and off
    * Command to quickly switch between Staff Character and normal character
* Family Sharing Protection (Requires Steam API key)
* IC-Chat logging
* Kick/Ban System
* Localization/Language support
* Logging System
* Mid-Air spawn failsafe
* Option to hide config changes from Non-Staff
* Option to show or hide connect and disconnect messages
* Player Notes
* Player Physgun Freezing
* Prop Blacklisting
    * Easy blacklisting through the spawnmenu & the context menu
    * Search feature
* Prop Owner Tracking
* Rank System using CAMI
    * Proper inheritance
    * Tool, command, and spawning permissions
    * Command integration
* Scoreboard & Context Menu command shortcuts
* Server Whitelist System
* Spectating System
* Ticket System
    * Including auxiliary /Help and /Respond commands
* Toolgun Improvements
    * Option to hide Toolgun effects
    * Option to silence Toolgun
    * Prop/Entity Persist/Unpersist tools
* Various Administration commands
    * Godmode
    * Tying
    * Forced Char-Switching
    * Teleporting
    * Respawning
    * Freezing
    * Health/Armor setting
    * Killing
    * Clearing Decals
    * Stopping Sounds
    * Server Announcements
    * Etc.
* Version Control (Notifications when Squadron receives an update)
* Warning System
* Etc.

### Installing & Configuring

The installation process for Squadron is quite simple:

1. Place the Squadron folder inside your **Schema's** plugin folder.
2. Ensure that the Squadron plugin folder is named "squadron" (not "SQUADRON" or "Squadron-Main" or anything else).
3. Navigate to Squadron's main plugin folder and create a file named `sh_squadron_overrides.lua`.
4. In that file, put `SQUADRON.owner = "STEAM_0:0:00000000"`, where the SteamID represents your own SteamID. If you wish to add more than one owner, you can do so by putting `SQUADRON.owner = {"STEAM_0:0:00000000", "STEAM_0:0:00000000"}`. You can add as many owners as you wish.

That's it. Most other options can be configured in-game. Additionally, if you wish to create your own Staff Ranks or modify the default ones, put the rank table in `sh_squadron_overrides.lua`, as such:

	SQUADRON.ranks["customrank"] = {
		Name = "customrank", -- The internal name of the rank.
		DisplayName = "Custom Rank", -- The display name of the rank.
		NoTitle = false, -- Whether the rank's display name should not show (eg when connecting or disconnecting).
		ShortName = "CR", -- The short name of the rank.
		FunctionName = "IsCustomRank", -- The name of the function to be created to check if the player is this rank, similar to IsAdmin().
		ClassInfo = {"Custom Rank", "Custom Rank", "Cr", Color(255, 255, 0), true}, -- The information of the chat class and command to be created in order to communicate to players with this rank. Name, Display Name, Alias, Color & Log bool.
		RankColor = Color(255, 255, 0), -- The color of the rank.
		Icon = "icon16/bomb.png", -- The icon of the rank.
		IsStaff = true, -- Whether this is a staff rank.
		Flags = "pet", -- The flags this rank is entitled to.
		Permissions = {
		    ["PlayerSpawnSWEP"] = true
		}, -- The permissions that this rank is entitled to.
		Tools = {
		    ["dynamite"] = true,
		}, -- What tools this rank has access to.
		Order = 90, -- The order of the rank, compared to other ranks.
		Inherits = "user" -- What rank's permissions this rank inherits.
	},

Look at the top of `sh_plugin.lua` for examples of rank creation.

Furthermore, you can add your own ticket dismiss templates in `sh_squadron_overrides.lua`, as such:

    -- These are the default dismiss reasons.
    SQUADRON.dismissReasons = {
		["No Response"] = "No Response - Your ticket was considered out of staff hands, nonsensical, self-explanatory or is not an actual question or issue.",
		["IC Issue"] = "IC Issue - This issue has been deemed an IC (In-Character) issue, and will not be handled by Staff.",
		["Being Handled"] = "Being Handled - This issue is already being dealt with.",
		["Resolved"] = "Resolved - This issue has already been resolved."
	}

In addition, with the Advanced Admin ESP system, you can register your own entities with ease using the following function in `sh_squadron_overrides.lua`:

    SQUADRON:RegisterEspEntity("entity_class", "Entity Name", function(entity, x, y, alpha)
        -- Drawing logic. See cl_plugin.lua for examples.
    end)

If you wish to remove one of the pre-defined entity ESP's, in case you are not using the HL2RP Schema or for any other reason, you can use the `SQUADRON:DeregisterEspEntity(entity_class)` function in `sh_squadron_overrides.lua`.

Finally, if you wish to override any code added by Squadron, you can do that in `sh_squadron_overrides.lua`. Thais way, if you download an update, your changes won't be overridden.
