
# Mod Definition File

Your mod definition file is what the Payday 2 BLT uses to load your mod. It is a json-formatted text file in your mod directory.  
To setup your definition, simply create a text file `mod.txt` in your mod directory, and setup your required basic details, hooks,
persist-scripts, and keybinds.  

---

### Base Mod Definition

The base definition for your mod. Contains the basic information of your mod.  

`name` The friendly name of your mod.  
`description` A description of your mod, and what it does.  
`author` You, your collaborators, anybody who worked on the mod.  
`contact` Some form of contact details for your users to contact you from.  
`version` A friendly version number that will displayed in the in-game mod manager.  
`priority` An integer, from 0 to 1000, that determines the order in which mods load. This should only be used for mods which act as dependencies for other mods.  

	{
		"name" : "An Example Mod",
		"description" : "My example mod which doesn't actually do anything.",
		"author" : "James Wilkinson",
		"contact" : "jw@jameswilko.com",
		"version" : "1.0",
		"priority" : 10
	}

### Hooks

_Previously Post-Require Scripts in PD2Hook.yml_  
The Payday 2 files to hook and run a specified lua script after. The hooks key is an array of objects.

`hooks` The array of objects containing a `hook_id` and a `script_path`.  
`hook_id` The Payday 2 script file to run the script in `script_path` after.  
`script_path` The path to your Lua script to run. This is relative to your mod folder.  

	"hooks" : [
		{ 	
			"hook_id" : "lib/setups/gamesetup",
			"script_path" : "PostGameSetup.lua"
		},
		{ 	
			"hook_id" : "lib/managers/menu/blackmarketgui",
			"script_path" : "BlackMarketGUIStuff.lua"
		}
	]

### Pre-Hooks

_Previously Pre-Require Scripts in PD2Hook.yml_
Identical to `Hooks`, except that these will run **before** the Payday 2 script defined in `hook_id`.

`pre_hooks` The array of objects containing a `hook_id` and a `script_path`.  
`hook_id` The Payday 2 script file to run the script in `script_path` before.  
`script_path` The path to your Lua script to run. This is relative to your mod folder.  

	"pre_hooks" : [
		{ 	
			"hook_id" : "lib/setups/menusetup",
			"script_path" : "PreSetupMenu.lua"
		}
	]

### Persist Scripts

_Previous Persist-Scripts in PD2Hook.yml_  
A script in `script_path` which is run every frame until the global variable specified in `global` is set to anything other than false or nil.  

`persist_scripts` The array of objects containing a `global` and a `script_path`.  
`global`  The global value to associate with `script_path`.  
`script_path` The script to continuously run until the global variable `global` is set to a value other than false or nil.  

	"persist_scripts" : [
		{
			"global" : "MyGlobalValue",
			"script_path" : "TestPersistScript.lua"
		},
		{
			"global" : "NotPocoHud",
			"script_path" : "not_poco/hud.lua"
		}
	]

### Json-Keybinds

_Previously Keybinds in PD2Hook.yml_  
A script to run when a key is pressed. These keybinds can be customized in-game, instead of being set to a specific hard-coded key.  

`keybinds` An array containing generic keybind information. Each keybind will be saved and loaded automatically for you.   
`keybind_id` A unique ID for your keybind.  
`name` The name of the keybind to display in the keybinds menu.  
`description` A short of description of your keybind.  
`script_path` The path to the script that should be ran when the keybind is pressed.  
`run_in_menu` A boolean of whether this keybind should run when pressed during the menu state.  
`run_in_game` A boolean of whether this keybind should run when pressed during the game state.  
`localized` A boolean of if the menu should attempt to use the name and description as localization keys.
Use `false` if you wish to just type a name and description in.

	"keybinds" : [
		{
			"keybind_id" : "keybind_example_test",
			"name" : "Test Keybind",
			"description" : "An example keybind for demonstration"
			"script_path" : "test.lua",
			"run_in_menu" : true,
			"run_in_game" : true,
			"localized" : false
		}
	]

### Complete Example

	{
		"name" : "An Example Mod",
		"description" : "My example mod which doesn't actually do anything.",
		"author" : "James Wilkinson",
		"contact" : "jw@jameswilko.com",
		"version" : "1.0",
		"hooks" : [
			{ 	
				"hook_id" : "lib/setups/gamesetup",
				"script_path" : "PostGameSetup.lua"
			},
			{ 	
				"hook_id" : "lib/managers/menu/blackmarketgui",
				"script_path" : "BlackMarketGUIStuff.lua"
			}
		],
		"persist_scripts" : [
			{
				"global" : "MyGlobalValue",
				"script_path" : "TestPersistScript.lua"
			}
		],
		"keybinds" : [
			{
				"keybind_id" : "keybind_example_test",
				"name" : "Test Keybind",
				"description" : "An example keybind for demonstration"
				"script_path" : "test.lua",
				"run_in_menu" : true,
				"run_in_game" : true,
			}
		]
	}
