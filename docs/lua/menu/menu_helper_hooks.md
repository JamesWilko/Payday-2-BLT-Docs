
# Menu Helper Hooks

These hooks should be used when adding custom menus to the game, as they will be called automatically by the Payday 2 BLT when menus should be added.  

For more information on listening to hooks, see the main [Hooks](../hooks.md) page.  

---

### MenuManagerSetupCustomMenus
Your menu should first be initialized during this hook. This will allow us to add new items to this menu, and to build the menu during the `MenuManagerBuildCustomMenus` hook.  

	local menu_id = "my_custom_menu_example"
	Hooks:Add("MenuManagerSetupCustomMenus", "MenuManagerSetupCustomMenus_Example", function(menu_manager, nodes)
		MenuHelper:NewMenu( menu_id )
	end)


### MenuManagerPopulateCustomMenus
All menu items should be added to your menu during this hook, which will cause them to appear in-game once the menu has been built.  

	Hooks:Add("MenuManagerPopulateCustomMenus", "MenuManagerPopulateCustomMenus_Example", function(menu_manager, nodes)
		-- Add your own menu items here
	end)


### MenuManagerBuildCustomMenus
The final hook to be called, and the hook which your menu should be being built during, and added to the menu.  
In the example below, our custom menu will be added to the options menu.  

	Hooks:Add("MenuManagerBuildCustomMenus", "MenuManagerBuildCustomMenus_Example", function(menu_manager, nodes)
		nodes[menu_id] = MenuHelper:BuildMenu( menu_id )
		MenuHelper:AddMenuItem( nodes.options, menu_id, "my_custom_mod_menu_name", "my_custom_mod_menu_desc" )
	end)
