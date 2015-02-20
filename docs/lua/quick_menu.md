
# QuickMenu
An easy and quick way to display small menus to the player. Works extemely similarly to SimpleMenu, and is easy to switch over to using.

---

### QuickMenu:new( title, message, options, show_immediately )
Creates a QuickMenu using the provided `title`, `message`, and `options` and returns it as a class variable.  
`title` The display title of the menu.  
`message` The message to be displayed in the menu. This can be a multiline string.  
`options` An array of options containing data to use for the options of the menu. Specifying a nil value or an empty array will create a default "OK" button.  
`show_immediately` If this QuickMenu should pop-up immediately without requiring the menu to be stored and have `show` expressly called on it.  
`returns` A QuickMenu object.  

`options: text` The text to display on this button.  
`options: callback` The callback to run if this button is pressed by the user.  
`options: is_cancel_button` If this button should do nothing other than close the menu.  

	local menu_title = managers.localization:text("base_mod_updates_show_multiple_update_available")
	local menu_message = managers.localization:text("base_mod_updates_show_multiple_update_available_message")
	local menu_options = {
		[1] = {
			text = managers.localization:text("base_mod_updates_open_update_manager"),
			callback = LuaModUpdates.OpenUpdateManagerNode,
		},
		[2] = {
			text = managers.localization:text("base_mod_updates_update_later"),
			is_cancel_button = true,
		},
	}
	local menu = QuickMenu:new( menu_title, menu_message, menu_options )
	menu:Show()


### QuickMenu:show()
_Can also be called with QuickMenu:Show()_
Displays the specified QuickMenu to the user.  

	local menu = QuickMenu:new( "My Title", "A test message.", {} )
	menu:Show()


### QuickMenu:hide()
_Can also be called with QuickMenu:Hide()_
Hides the specified QuickMenu without removing it, so that it can be shown to the user again.  

	local menu = QuickMenu:new( "My Title", "A test message.", {}, true )
	menu:Hide()
