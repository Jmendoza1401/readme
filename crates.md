# Crates System

- Make sure to choose the right framework (QBCore or ESX) and if you have renamed cores or foldernames of core, make the necessary changes in Config.
- If you choose any other framework other than one mentioned, the script wont work.
- Script supports cd garage and base qb and base esx garage. If you use another custom garage, make sure to change in sv_customise.lua. (I wont be supporting any other garages)
- All the major code related item giving and removing is present in sv_customise.lua. Make sure to read through it and change it for your other custom scripts. 

# Steps to create new crates

- The script comes with two predefined crate.
- To create new crates, copy the old one and add it under the last crate
- Read the comments near each line properly
- Make sure the probability of all the items in the crates is 100+. IF IT IS NOT GREATER OR EQUAL TO 100, CRATE WONT WORK.
- Also A SMALL TIP - make sure the image sizes (in kb, mb whatever) is as small as possible so that the crates load faster. If you keep the images 1 MB each, it will take atleast 15-20 seconds for the crate to load. Images I am using are all close to 100kb or less.

```
Available Types: 
1. item -> can be given use addinventoryitem or additem (make sure to add name and amount.)
2. car -> car that will be added to the garage (make sure the car is present in vehicles.lua for QBCore and in vehicles table for ESX)
3. boat -> boat that will be added to the garage (differentiating because of the garage types) (make sure the car is present in vehicles.lua for QBCore and in vehicles table for ESX)
4. air -> helis or airplanes that will be added to garage (differentiating because of the garage types) (make sure the car is present in vehicles.lua for QBCore and in vehicles table for ESX)
5. cash -> cash that will be added to their cash balance (amount will be taken for this, you can add the name as anything)
6. other -> if you have a custom requirement, you choose the type to be other and add your own logic in sv_customise.lua. 

If you choose any type other than the 6 mentioned above, the script will break.
```

```lua
["crate1"] = { -- item in items.lua and make sure its useable (this will be the crate used to open the ui)
        items = {
            [1] = {
                name = "weapon_pistol",
                label = "Pistol",
                amount = 1,
                type = "item",
                probability = 10,
                img = "https://cdn.discordapp.com/attachments/909899891705278534/1015602989379092501/ss.jpg",
            },
            [2] = {
                name = "tosti",
                label = "Tosti",
                amount = 1,
                type = "item",
                probability = 45,
                img = "https://cdn.discordapp.com/attachments/909899891705278534/1015602989177778266/istockphoto-1256670482-612x612.jpg"
            },
            [3] = {
                name = "sultan",
                label = "Sultan",
                amount = 1,
                type = "car",
                probability = 1,
                img = "https://cdn.discordapp.com/attachments/909899891705278534/1015602608146219008/sultan-classic.jpg"
            },
            [4] = {
                name = "dinghy",
                label = "Dinghy",
                amount = 1,
                type = "boat",
                probability = 2,
                img = "https://cdn.discordapp.com/attachments/909899891705278534/1015602988963876944/index.jpg"
            },
            [5] = {
                name = "cash",
                label = "Cash Money",
                amount = 1000,
                type = "cash",
                probability = 45,
                img = "https://cdn.discordapp.com/attachments/909899891705278534/1015602989634965555/asd.jpg"
            }
        }
    }, -- Add crates below this line with the same format. DONT FORGET TO ADD COMMA AT END.
```



# QBCore
- Images are present in README folder
```lua
	["crate1"]= {["name"] = "crate1", ["label"] = "Custom Crate 1", 		["weight"] = 2000, 		["type"] = "item", 		["image"] = "crate1.png", ["unique"] = true, 	["useable"] = true, 	["shouldClose"] = true,	   	["combinable"] = nil,   ["description"] = "Custom Crate"},
	["crate2"]= {["name"] = "crate2", ["label"] = "Custom Crate 2", 		["weight"] = 2000, 		["type"] = "item", 		["image"] = "crate2.png", ["unique"] = true, 	["useable"] = true, 	["shouldClose"] = true,	   	["combinable"] = nil,   ["description"] = "Custom Crate"},
```

# ESX
- Images are present in README folder
```sql
INSERT INTO `items` (`name`, `label`, `weight`, `rare`, `can_remove`) VALUES ('crate1', 'Custom Crate 1', 1, 0, 1)
INSERT INTO `items` (`name`, `label`, `weight`, `rare`, `can_remove`) VALUES ('crate2', 'Custom Crate 2', 1, 0, 1)
```

- For ESX, this script has been tested with car, boat and air for cd_garage and car and boat for base esx garage. I am not sure what is the right way to do for air garages in ESX.