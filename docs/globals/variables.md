
### RequiredScript
A variable containing the name and path of the Payday lua file that will be run, or was previously run.  

	Hook: lib/setups/gamesetup
	File: my_mod.lua
	RequiredScript: lib/setups/gamesetup

	Pre-Hook: lib/managers/menumanager
	File: my_mod.lua
	RequiredScript: lib/managers/menumanager

### ModPath
A variable containing the path of the mod that is currently being loaded. This value should be cached if it is
intended to be used at some point in the future, such as in a Hook.  

	ModPath: mods/my_example_mod

### PersistScriptPath
A variable containing the path of the mod that is currently being loaded via a persist script. This value should be cached
if it is intended to be used at any point in the future that is not immediate, such as in a Hook.

	ModPath: mods/my_example_mod

### LogsPath
A variable containing the path to the mods logs folder.  

	LogsPath: mods/logs/

### SavePath
A variable containing the path to the save files folder.  

	SavePath: mods/saves/
