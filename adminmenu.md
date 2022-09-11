# Snipe Admin Menu

# Permissions
- In Config, there are options to set if the particular role for god, admin or mod can access all the panels.

```lua
Config.GodRoles = {
    ["god"] = true, 
    ["admin"] = false,
    ["mod"] = false,
    -- if you want to add more roles just add them here
}
```
- To give the right roles for a user, make sure to write the right permissions in server.cfg

```cfg
add_principal identifier.fivem:123456 qbcore.god  # gives the god permissions
add_principal identifier.fivem:123456 qbcore.admin # gives the admin permissions
add_principal identifier.fivem:123456 qbcore.mod # gives the mod permissions
```

- According to the config above, only the `god` has the permissions to access each and every panel and each and every button and they can select the panels that will be visible to mods/admins and it will update on real time and go through server restarts.

# Spawning objects
- When spawning objects/job stashes, please look at the 2D text on the screen and use the right keys and everything. Each key is hardcoded and possibly wont be allowed to change.

# Keybinds
- Before starting the script on live server, go through cl_keybinds.lua file and see if you want to change the keybinds. Dont worry if you didnt configure, you can change them through settings. Go to GTA 5 Settings -> Keybinds -> Fivem and look for snipe-menu and change them.
- I would advise using mouse key for delete laser because it will be easier to access multiple keys.
- Keybinds only work if the dev mode is on. It can be turned on using the terminal button above the settings and only accessible to GodRoles.

# Discord Logging
- Change the webhook in sv_webhooks.lua. It logs almost each and every command used and who it was used on. There is not a lot of language options since it will be logged to a discord but you can change some things to your liking in config.

# Give Item
- There are some items which have metadata which needs to be taken care of while giving a item because if you dont, that item wont be useful at all.
- If you have a particular item which has metadata, you need to mention it in the sv_customise.lua -> GetItemMetadataInfo() function. I pass the item spawn name so you can use it to add if condition to add more items to your liking
# Miscellanuous
- There are bunch of client/server scripts which are unencrypted which you can edit it to your liking. 
- I wont be adding supports for other paid scripts but the logic required to edit will be made open if needed.

# Other
- I am open to suggestions about new panels. But dont expect it to get done right away. In next few weeks my availability is going to be a little low so I wont be readily available to add new panels within a day but if the work required is low, I will try to accomplish it.
- To add your suggestions, please create a thread in suggestions channel and post it there.