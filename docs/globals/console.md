
# Debug Console
The debug console is available via a simple one-line change to enable it.
This method is used to ensure that the console window is always the first window to appear when it is enabled,
instead of appearing after the game is loaded, due to the base mod loading the console via lua instead of being hard-coded into the DLL itself.

This is only a temporary solution until we come up with a better solution, and we're open to suggestions on the [Payday 2 BLT GitHub](https://github.com/JamesWilko/Payday-2-BLT) page.

### Enabling the Console
Go to your `mods` folder and open the `base` mod.  
Open `base.lua`.  
Change line 3 from `false` to `true` to open the console when the game is opened.  

	-- Create our console
	if true then
		console.CreateConsole()
	end
