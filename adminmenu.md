# Snipe Admin Menu

# Permissions
- In Config folder check `permissions.lua`, there are options to set if the particular role for god, admin or mod can access all the panels.

All the roles here can access the admin menu
Only the GOD can set the panels for the other roles
There are unlimited options
1. God -> can access all the commands
2. Others can access panels that the god selects for them

If you have a new role, you can add it here and select to give either it any value you want and it will be available in the settings tab for god roles to select the panels for them.

eg. ["new_role"] = "God",

eg. ["dev"] = "Admin",

```lua
Config.GodRoles = {
    ["god"] = "God", 
    ["admin"] = "Admin",
    ["mod"] = "Moderator",
    -- if you want to add more roles just add them here
}
```

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
- By default, gang related buttons are disabled for ESX since ESX doesnt have default gangs.
- By default, open trunk and open glovebox have been disabled for ox inventory since there are some checks that prevent open trunk and glovebox without being near the car.
- Locales have been moved to locales.lua for ease.

# QBCore and ESX
## Permissions
- Check `permissions.lua` file under config folder.

## Clothing
```lua
Config.Clothing = "qb-clothing" -- qb-clothing || fivem-appearance || esx_skin || other
```
- If you choose other, please check `cl_customise_1.lua` and look for the event `snipe-menu:client:revertClothing` and add your custom event
- If you want to change event to give clothing menu, `check snipe-menu:server:giveClothes` event in sv_customise.lua
# QBCore
## Opening stashes/trunk/glovebox

Add the two following events at the end of the inventory/client/main.lua (do not add it at the beginning please!!)

```lua
RegisterNetEvent('inventory:client:SetCurrentTrunk', function(vehicle)
    CurrentVehicle = vehicle
end)

RegisterNetEvent('inventory:client:SetCurrentGlovebox', function(vehicle)
    CurrentGlovebox = vehicle
end)
```

# ESX

## Config
```lua
Config.Core = "ESX" -- ESX or QBCore
Config.CoreFolderName = "es_extended"  -- es_extended || qb-core

Config.PlayerLoadedEvent = "esx:playerLoaded" -- esx:playerLoaded || QBCore:Client:OnPlayerLoaded
Config.PlayerUnloadEvent = "esx:onPlayerLogout " -- esx:onPlayerLogout || QBCore:Client:OnPlayerUnload           

Config.Target = "qtarget" -- qb-target || ox_target || qtarget (Only these 3 targets are supported. You will have to edit in cl_customise if you want to use any other target other than this. No support is given to other target scripts)
```

- If you have renamed events, you can rename them here. Make sure to choose the right target
## Inventory
```lua
Config.Inventory = "ox" -- qb or qs or ox 
```
- Only supported inventories are qb, ox or quasar. Most of the inventory logic is open in `sv_inventory.lua` and `cl_inventory.lua` if you want to support any other inventory.
## Bans
- Run the `bans.sql` file given in sql folder
- Make the following changes in es_extended/server/main.lua
```lua
AddEventHandler('playerConnecting', function(name, setCallback, deferrals)
	deferrals.defer()
	local playerId = source
	local identifier = ESX.GetIdentifier(playerId)
	Wait(100)
	local isBanned, Reason = exports["snipe-menu"]:IsPlayerBanned(playerId) -- added
	if identifier then
		if ESX.GetPlayerFromIdentifier(identifier) then
			deferrals.done(('There was an error loading your character!\nError code: identifier-active\n\nThis error is caused by a player on this server who has the same identifier as you have. Make sure you are not playing on the same account.\n\nYour identifier: %s'):format(identifier))
		else
			if isBanned then -- added
				deferrals.done(Reason) -- added
			else -- added
				deferrals.done()
			end -- added
		end
	else
		deferrals.done('There was an error loading your character!\nError code: identifier-missing\n\nThe cause of this error is not known, your identifier could not be found. Please come back later or report this problem to the server administration team.')
	end
end)
```

## Weather Sync
- cd easytime is configured by default for weather change. Logic is open in `cl_customise.lua` if you use a different weathersync script.

# Files that are open to edit

-   `'config/config.lua',`
-   `'config/locales.lua',`
-   `'config/permissions.lua',`
-   `'client/cl_customise.lua',`
-   `'client/cl_keybinds.lua',`
-   `'client/cl_noclip.lua',`
-   `'client/cl_names.lua',`
-   `'server/sv_customise.lua',`
-   `'server/sv_webhooks.lua',`
-   `'server/sv_customise_new.lua',`
-   `'client/cl_vehdebug.lua',`
-   `'client/cl_customise_1.lua',`
-   `'client/pedlist.lua',`
-   `'server/sv_utils.lua',`
-   `'client/cl_utils.lua',`
-   `'server/sv_vehicles.lua',`
-   `'client/cl_inventory.lua',`
-   `'server/sv_inventory.lua',`