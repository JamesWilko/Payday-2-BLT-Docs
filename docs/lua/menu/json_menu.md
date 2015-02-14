
# Json Menus

In-game menus can have their layout created in a json-formatted text file, instead of defining each individual element in a Lua script.  
Json Menus allows you to load a json file which will automatically create, layout, and setup all elements of your in-game menu for you. All you have to do then is implement the callback handlers for your menu, so that you can process any user input.  

---

### Example
A fully working example is available in the Example Mods of the Payday 2 BLT. It is already fully documented in guiding you through the setup of a Json loaded menu.

---

### lua_mod_options_menu 
This is ID of the parent menu for all Lua mods. If you are adding an options menu for your mod, use this ID, as it will automatically added to your Options/Mod Options menu.  
If you want to have your menu appear in a different location, you will have to find the ID of the menu you wish to add it to.  

---

### Base Keys
The set of basic keys that determine where your menu button appears, and how it appears in the menu.  

`menu_id` A unique identifier for your menu, so that the game can find and display your menu when it is clicked.  
`parent_menu_id` The menu ID of the parent menu, this is the menu under which your menu will appear. Under most circumstances should be `lua_mod_options_menu`.  
`title` The key of the name of your menu. This is localized.  
`description` A key for the description of your menu. This is localized.  
`items` An array of Json Objects which will be the menu items which appear in your menu. They will appear in-game in the same order which they are defined. 

	{
		"menu_id" : "json_example_menu",
		"parent_menu_id" : "lua_mod_options_menu",
		"title" : "my_custom_menu",
		"description" : "my_custom_menu_desc",
		"items" : [

		]
	}

### Common Item Keys
These keys are used in all items in the `items` array.  
`type` The type of item to place at this position. The available types are `button`, `divider`, `toggle`, `slider`, `multiple_choice`, and `keybind`.  
`id` A unique ID for this menu item.  
`title` The key for the name of this menu item. This is a localized value.  
`description` The key for the description of this menu item. This is a localized value.  
`callback` The callback function to call on the `MenuCallbackHandler` when this item is modified.  

### Button
Buttons do not need any extra keys in order to function. As long as their callback key is set, they will call the callback function whenever they are pressed.  

	{
		"type" : "button",
		"id" : "json_menu_button",
		"title" : "json_item_button",
		"description" : "json_item_button_desc",
		"callback" : "callback_test_button",
	}


### Divider
Dividers are a special case in that they only need one key in order to appear in the menu.  
`size` The size of the space this divider will create.  

	{
		"type" : "divider",
		"size" : 128,
	}


### Toggle
These keys are only of use on items with the type of `toggle`.  
`value` The key of the value to load from the data table. See the example mod for more information on this.  
`default_value` The default value of the toggle if no data could be loaded from the data table.  

	{
		"type" : "toggle",
		"id" : "json_menu_toggle",
		"title" : "json_item_toggle",
		"description" : "json_item_toggle_desc",
		"callback" : "callback_test_toggle",
		"value" : "toggle_value",
		"default_value" : false,
	}


### Slider
These keys are only of use on items with the type of `slider`.  
`value` The key of the value to load from the data table.  
`default_value` The default value of the slider to use if not data could be loaded from the data table.  
`max` The maximum value this slider can go to, as a number.  
`min` The minimum value this slider can go to, as a number.  
`step` How much this slider will increment when a controller is being used to adjust it.  

	{
		"type" : "slider",
		"id" : "json_menu_slider",
		"title" : "json_item_slider",
		"description" : "json_item_slider_desc",
		"callback" : "callback_test_slider",
		"value" : "slider_value",
		"default_value" : 50,
		"max" : 100,
		"min" : 0,
		"step" : 1,
	}

### Multiple Choice
These keys are only of use on items with the type of `multiple_choice`.  
`items` An array of localized names to use as items for the multiple choice. The value of the multiple choice is saved and loaded as the index of the selected item.  
`value` The key of the value to load from the data table.  
`default_value` The index of the default value to use if no data could be loaded from the data table.  

	{
		"type" : "multiple_choice",
		"id" : "json_menu_mutli",
		"title" : "json_item_multi",
		"description" : "json_item_multi_desc",
		"callback" : "callback_test_multi",
		"items" : [
			"json_multi_item_a",
			"json_multi_item_b",
			"json_multi_item_c",
			"json_multi_item_d",
			"json_multi_item_e"
		],
		"value" : "multi_value",
		"default_value" : 3,
	}

### Keybind
These keybinds are only of use on items with the type of `keybind`.  
`keybind_id` A unique ID for this keybind, it will be used to automatically save and load your customized keybinds.  
`func` The function which should be called when the keybind is pressed.  

	{
		"type" : "keybind",
		"id" : "json_menu_keybind",
		"title" : "json_item_keybind",
		"description" : "json_item_keybind_desc",
		"keybind_id" : "json_menu_example_keybind",
		"func" : "func_test_keybind",
	}
