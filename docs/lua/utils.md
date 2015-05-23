
### _G.CloneClass( class )
Clones all of a class' variables and functions, so that they may be overwritten, whilest maintaining a reference to the original set of variables and functions.  
`class` The class to the cloned into the `class.orig` table.  

	CloneClass( MenuManager )


### _G.PrintTable( tbl )
Logs all contents of the specified table to the console, and log files.  
`tbl` The table to log all contents of.  

	local test_table = {
		1,
		2,
		"345",
		["hello"] = "test"
	}
	PrintTable( test_table )


### _G.SaveTable( tbl, file )
Saves all contents of the specified table to the file specified. The file will be created if it doesn't exist, and any existing contents will be overwritten.  
`tbl` The table to save to a file.  
`file` The path and name of the file to save the table contents to, relative to PAYDAY 2 directory.  

	SaveTable( MenuManager, "menu_manager.txt" )


### Vector3.ToString( vec ) 
Converts a Vector3 to a formatted string.  
`vec` The Vector3 to convert to a string.  
`returns` A formatted string with the information of the input `vec`.

	local vec = Vector3( 50, 0, 10 )
	vec:ToString()


### string.ToVector3( str )
Converts the formatted string `str` into a usable Vector3.  
`str` The formatted string to convert into a Vector3.  
`returns` A Vector3.  

	local vec_str = "50.000000,25.456841,00.000000"
	vec_str:ToVector3()


### string.is_nil_or_empty( str )
Checks if the specified string `str` contains any data.  
`str` The string to check contains any data.  
`returns` A false if `str` is nil or empty (_""_), true if it contains any data.  

	local s = "hello world!"
	string.is_nil_or_empty( s )

	local s = ""
	s:is_nil_or_empty()


### math.round_with_precision( num, precision )
Rounds a number `num` to the specified number of decimal places in `precision`.  
`num` The number to round.  
`precision` The number of decimal places to round `num` to.  

	local num = 28.15635846315
	num:round_with_precision( 2 )

	local num = 12.54135483153
	math.round_with_precision( num, 4 )


### Utils:GetPlayerAimPos( ply, max_range )
Get the point in the world, as a Vector3, where the player is aiming at.  
`ply` The player to get the aiming position of.  
`max_range` The maximum distance to raycast to check for a point.   
`returns` A Vector3 containing the position that the player was looking at. Returns _false_ if a point could not be found.

	GetPlayerAimPos( managers.player:player_unit(), 10000 )


### Utils:GetCrosshairRay( from, to, slot_mask )
Gets a ray between two points and checks for a collision with the slot_mask along the ray.  
`from` The starting position of the ray, defaults to the player's head.  
`to` The ending position of the ray, defaults to 1m in from of the player's head.  
`slot_mask` The collision group to check against the ray, defaults to all objects the player can shoot.  
`returns` A table containing the ray information.  

	local from = managers.player:player_unit():position()
	local to = managers.player:player_unit():position() + Vector3( 0, 1000, 0 )
	GetCrosshairRay( from, to )

### Utils:ToggleItemToBoolean( item )
Takes a toggle menu item, and returns a boolean based on its current state.  
`item` The toggle menu item.  
`returns` A boolean depending on the state of the toggle item. True if the toggle is on, false if off.  
	
	MenuCallbackHandler.test_toggle_callback = function( self, item )
		local was_enabled = Utils:ToggleItemToBoolean( item )
	end

### Utils:IsInGameState()
Reports if the game is currently in an in-game state, where the player may have direct control over a character at some point, such as the loadout screen, in-heist, victory or loss screens.  
`returns` True if the game is currently in an in-game state, false otherwise.  

### Utils:IsInLoadingState()
Reports if the game is currently loading a new level or menu.  
`returns` True if the game is in a loading state, false otherwise.  

### Utils:IsInHeist()
Reports if the game is in a state where the player is directly controlling a character.  
`returns` True if the game is in a state where the player can directly control a character, false otherwise.  

### Utils:IsInCustody()
Reports if the local player is 'dead' and in police custody in the in-heist state.  
`returns` True if the local player is in police custody, false otherwise.  

### Utils:IsCurrentWeaponPrimary()
Checks if the local player is currently holding their selected primary weapon.  
`returns` True if the local player's equipped weapon is their selected primary.  

### Utils:IsCurrentPrimaryOfCategory( category )
Checks if the local player's primary weapon is of a specific category of firearm.  
Available categories are: `assault_rifle`, `pistol`, `smg`, `shotgun`, `saw`, `lmg`, `snp`, `grenade_launcher`, `akimbo`, `minigun`, `flamethrower`  
`category` A string value containing the category to check that the primary is in.  
`returns` True if the primary weapon is in the category, false otherwise.  

	local is_launcher = Utils:IsCurrentPrimaryOfCategory( "grenade_launcher" )

### Utils:IsCurrentWeaponSecondary()
Checks if the local player is currently holding their selected secondary weapon.  
`returns` True if the local player's equipped weapon is their selected secondary.  

### Utils:IsCurrentSecondaryOfCategory( category )
Checks if the local player's secondary weapon is of a specific category of firearm.  
Available categories are: `assault_rifle`, `pistol`, `smg`, `shotgun`, `saw`, `lmg`, `snp`, `grenade_launcher`, `akimbo`, `minigun`, `flamethrower`  
`category` A string value containing the category to check that the secondary is in.  
`returns` True if the secondary weapon is in the category, false otherwise.  

	local is_smg = Utils:IsCurrentSecondaryOfCategory( "smg" )

### Utils:IsCurrentWeapon( type )
Checks if the local player's equipped weapon is a specific firearm.  
`type` A string value containing the ID of the weapon.  
`returns` True if the current equipped weapon matches `type`, false otherwise.  

	local is_UAR = Utils:IsCurrentWeapon( "aug" )
