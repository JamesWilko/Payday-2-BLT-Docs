
# Localization Functions
A set of functions which are available to the LocalizationManager to add customized localization strings.

---

### LocalizationManager:add_localized_strings( tbl )
Registers a table of keys localized strings.  
`tbl` A table of localized strings, where the key is the localization id, and the value is the localized
string to fetch.  

	-- Directly adding to the localized strings table
	LocalizationManager:add_localized_strings( {
		["loc_example_test_string"] = "This is our localization test string!",
		["loc_example_test_string2"] = "This is another localization test string!",
	} )

	-- Automatically adding localized strings once the LocalizationManager has loaded
	Hooks:Add("LocalizationManagerPostInit", "LocalizationManagerPostInit_LocExample", function(loc)

		loc:add_localized_strings( {
			["loc_example_test_string"] = "This is our localization test string!",
			["loc_example_test_string2"] = "This is another localization test string!",
		} )

	end)

### LocalizationManager:load_localization_file( file_path )
Loads a json formatted file and adds all keys and values to the localization table.  
`file_path` The file to be loaded, and registered in the localization manager.  

	-- loc.txt
	{
		"loc_example_json_file" : "This is a localization string being loaded from JSON",
		"loc_example_json_file2" : "This is another JSON loaded string!"
	}

	-- YourMod.lua
	LocalizationManager:load_localization_file( "loc.txt" )

