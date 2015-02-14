
# Menu Helper

The MenuHelper class is a set of functions which are used in conjunction with a set of [specialized hooks](menu_helper_hooks.md) in order to add custom menus to the game.  
Adding menus via MenuHelper is best left for menus that require more advanced setup, as [Json Menus](json_menu.md) can be used in most other circumstances to add menus to your mods.  

---

### MenuHelper:NewMenu( menu_id )
Registers a new menu that can have items added to it.  
`menu_id` The unique ID to use for this menu.  

	local menu_id = "my_custom_menu"
	MenuHelper:NewMenu( menu_id )


### MenuHelper:GetMenu( menu_id )
Returns the registered menu with id of `menu_id`.  
`menu_id` The unique ID of the menu to get.  
`returns` The menu with the specified `menu_id`. Logs an error, and returns nil, if no menu with the specified ID could be found.  

	local menu = MenuHelper:GetMenu( "my_custom_menu" )


### MenuHelper:BuildMenu( menu_id, data )
Sets up, and returns, the menu with ID `menu_id` so that it can be added to the in-game menus.  
`menu_id` The ID of the menu which should be built.  
`data` A table containing extra data which this menu should be built with.  
`data: back_callback` The function to be called on `MenuCallbackHandler` when the menu is left.  
`data: area_bg` The area the background covers when this menu is opened whilest in-heist. Available values are `full`, `half`, and `none`.  

	Hooks:Add("MenuManagerBuildCustomMenus", "MenuManagerBuildCustomMenus_Example", function( menu_manager, nodes )
		local menu_data = {
			area_bg = "half"
		}
		nodes["my_custom_menu"] = MenuHelper:BuildMenu( "my_custom_menu", menu_data )		
	end)


### MenuHelper:AddMenuItem( parent_menu, child_menu, name, desc, menu_position, subposition )
Adds a button to an already existing parent menu.  
`parent_menu` The menu which the menu item will be added to.  
`child_menu` The ID of the menu which this menu item should open when clicked.  
`name` The key of the display name of this button. This is a localized value.  
`desc` The key of the description to display when highlighting this button. This is a localized value.  
`[menu_position]` A value of where this menu item should be inserted into the parent menu. Using a number will insert it at a guaranteed position. Using a string as the name of another child item will insert it at a specified `subposition` relative to the child item. Optional.  
`[subposition]` The position to place this object at if we are using a child object's name. This can either be `before` or `after` and will place it above or below the object in the menu accordingly.  

	Hooks:Add("MenuManagerBuildCustomMenus", "MenuManagerBuildCustomMenus_Example", function( menu_manager, nodes )
		MenuHelper:AddMenuItem( nodes.options, lua_mod_options_menu_id, "base_options_menu_lua_mod_options", "base_options_menu_lua_mod_options_desc", "video", "before" )
	end)


### MenuHelper:LoadFromJsonFile( file_path, parent_class, data_table )
Loads a json-formatted text file and automatically parses and converts into a usable menu. Check the [JsonMenu documentation](json_menu.md) and the JsonMenuExample in the Example Mods.  
`file_path` The json-formatted file to load and convert into a menu.  
`parent_class` The class of which all keybind functions and data will be loaded and saved to.  
`data_table` A table containing the data keys which various menu items can load their `value` from.  

	local MyMod = {}
	MyMod._data = {}
	MenuHelper:LoadFromJsonFile( "path/to/example_file.txt", MyMod, MyMod._data )


### MenuHelper:AddButton( button_data )
Adds a button to the menu specified in the table `button_data`, as well as the data specified.  
`button_data` A table containing data on the button to be added to the menu.  
`button_data: id` A unique identifier for this button.  
`button_data: title` A key for the display name of this button. This is a localized value.  
`button_data: desc` A key for the display description of this button. This is a localized value.  
`button_data: callback` The function to be called on `MenuCallbackHandler` when the button is clicked.  
`button_data: menu_id` The ID of the menu which this button should be created on.  
`[button_data: disabled_color]` The display color of this button when it is disabled. Optional.  
`[button_data: next_node]` The ID of the menu which should be opened when this button is clicked. Optional, leaving it as nil will not open a menu when clicked.
`[button_data: priority]` The position to display this button in the menu, higher values display higher in the menu. Optional.  

	MenuHelper:AddButton({
		id = "example_button",
		title = "example_mod_test_button",
		desc = "example_mod_test_button_desc",
		callback = "test_button_callback",
		menu_id = "my_custom_menu",
		priority = 10,
	})


### MenuHelper:AddDivider( divider_data )
Adds a divider to the menu specified in the table `divider_data`.  
`divider_data` A table containing data on the divider to be added to the menu.  
`divider_data: id` The unique identifier for this divider.  
`divider_data: size` The height of the divider to be added to the menu.  
`divider_data: menu_id` The ID of the menu which this divider should be created on.  
`[divider_data: priority]` The position to display this divider in the menu, higher values display higher in the menu. Optional.  

	MenuHelper:AddDivider({
		id = "example_divider_1",
		size = 16,
		menu_id = "my_custom_menu",
		priority = 9,
	})


### MenuHelper:AddToggle( toggle_data )
Adds a toggle button to the menu specified in the table `toggle_data`, as well as the data specified.  
`toggle_data` A table containing data on the toggle to be added to the menu.  
`toggle_data: id` The unique identifier for this toggle button.  
`toggle_data: title` A key for the display name of this button. This is a localized value.  
`toggle_data: desc` A key for the display description of this button. This is a localized value.  
`[toggle_data: value]` The default value to be shown when this toggle is displayed. Optional, defaults to false/off.  
`toggle_data: callback` The function to be called on `MenuCallbackHandler` when this toggle button is toggled.  
`toggle_data: menu_id` The ID of the menu which this toggle should be created on.  
`[toggle_data: disabled_color]` The display color of this toggle when it is disabled. Optional.  
`[toggle_data: icon_by_text]` Places the icon up against the name text of the toggle if true. Optional, defaults to false.  
`[toggle_data: priority]` The position to display this divider in the menu, higher values display higher in the menu. Optional.  


	MenuHelper:AddToggle({
		id = "example_toggle",
		title = "example_mod_test_toggle",
		desc = "example_mod_test_toggle_desc",
		callback = "test_toggle_callback",
		value = true,
		menu_id = "my_custom_menu",
		priority = 8,
	})


### MenuHelper:AddSlider( slider_data )
Adds a slider to the menu specified in the table `slider_data`, as well as the data specified.  
`slider_data` A table containing data on the slider to be added to the menu.  
`slider_data: id` The unique identifier for this slider.  
`slider_data: title` A key for the display name of this slider. This is a localized value.  
`slider_data: desc` A key for the display description of this slider. This is a localized value.  
`slider_data: value` The default value to be shown when this slider is displayed.  
`slider_data: min` The minimum value for this slider to go down to.  
`slider_data: max` The maximum value for this slider to go up to.  
`slider_data: step` The value which this slider should be adjusted when using a controller to change the value.  
`slider_data: callback` The function to be called on `MenuCallbackHandler` when this slider button is adjusted.  
`slider_data: menu_id` The ID of the menu which this slider should be created on.  
`[slider_data: show_value]` Displays the value of the slider. Optional, defaults to true.   
`[slider_data: disabled_color]` The display color of this slider when it is disabled. Optional.  

	MenuHelper:AddSlider({
		id = "example_slider",
		title = "example_mod_test_slider",
		desc = "example_mod_test_slider_desc",
		callback = "test_slider_callback",
		value = 128,
		min = 0,
		max = 256,
		step = 1,
		show_value = true,
		menu_id = "my_custom_menu",
		priority = 7
	})

### MenuHelper:AddMultipleChoice( multi_data )
Adds a multiple choice item to the menu specified in the table `multi_data`, as well as the data specified.  
`multi_data` A table containing data on the multiple choice to be added to the menu.  
`multi_data: id` The unique identifier for this multiple choice.  
`multi_data: title` A key for the display name of this multiple choice. This is a localized value.  
`multi_data: desc` A key for the display description of this multiple choice. This is a localized value.  
`multi_data: callback` The function to be called on `MenuCallbackHandler` when this multiple choice is switched.  
`multi_data: menu_id` The ID of the menu which this multiple choice should be created on.  
`[multi_data: value]` The default value to be shown when this multiple choice is displayed. Optional, defaults to the first available item.  
`[multi_data: priority]` The position to display this divider in the menu, higher values display higher in the menu. Optional.  

	local items = {
		"First Item",
		"Second Item",
		"Third Item"
	}

	MenuHelper:AddMultipleChoice({
		id = "example_multiple_choice",
		title = "example_mod_test_multichoice",
		desc = "example_mod_test_multichoice_desc",
		callback = "test_multi_callback",
		items = items,
		value = 1,
		menu_id = "my_custom_menu",
		priority = 6,
	})


### MenuHelper:AddKeybinding( bind_data )
Adds a customizable keybinding to the menu specified. Keybinds will automatically saved and loaded by the Lua hook.  
`bind_data` A table containing data on the keybind to be added to the menu.  
`bind_data: id` The unique identifier for this keybind item.  
`bind_data: title` A key for the display name of this keybind. This is a localized value.  
`bind_data: connection_name` A unique name to save this keybind as. This value will be used to save and load the keybind, and to check if the keybind is being pressed.  
`bind_data: callback` The function to be called on `MenuCallbackHandler` when this keybind is assigned.  
`bind_data: menu_id` The ID of the menu which this keybind should be created on.  
`[bind_data: binding]` The default key for which this keybind is assigned. Optional, defaults to unbound.  
`[bind_data: button]` The default key for which this keybind is assigned. Optional, defaults to unbound.  
`[bind_data: priority]` The position to display this keybind in the menu, higher values display higher in the menu. Optional.  

	local default_key = "K"
	MenuHelper:AddKeybinding({
		id = "example_keybind",
		title = "example_mod_test_keybind",
		callback = "test_multi_callback",
		connection_name = "example_keybind_connection",
		binding = default_key,
		button = default_key,
		menu_id = "my_custom_menu",
		priority = 5,
	})


### MenuHelper:ResetItemsToDefaultValue( item, items_table, value )
Resets all items passed into the `items_table` to the value specified in `value`.  
`item` A menu item for which the helper function can retreive any items specified in `items_table`.  
`items_table` A table of items, where the item name is the key, which should be reset to the value.  
`value` The value which all items specified should be reset to.  

	MenuCallbackHandler.test_button_callback = function(self, item)

		local items_to_reset = {
			["example_slider"] = true,
		}
		local default_value = 128
		MenuHelper:ResetItemsToDefaultValue( item, items_to_reset, default_value )

	end
