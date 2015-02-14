
# Hooks

Hooked functions which multiple functions can listen to, so that when the original hook is called, all functions
listening to it will be called too.  

---

### Hooks:RegisterHook( hook_id )
_Can also be called as Hooks:Register( hook_id )_  
Registers a hook, so that it may be listened to, and called at a later time.  
`hook_id` The unique identifier of the hooked function to register.

	Hooks:RegisterHook( "OnMyExampleModLoaded" )

### Hooks:AddHook( hook_id, id, func )
_Can also be called as Hooks:Add( hook_id, id, func )_  
Adds a function to the specified hooked function `hook_id` so that the `func` is called when
the parent hook is called.  
`hook_id` The identifier of hook to call this function on.  
`id` A unique identifier for this specific hooked function call, so that we may removed it later.  
`func` A function to be ran when the parent hook `hook_id` is called.  

	Hooks:AddHook( "OnMyExampleModLoaded", "OnMyExampleModLoaded_ExampleMod2", function()
		log("OnMyExampleModLoaded was called!")
	end )

### Hooks:UnregisterHook( hook_id )
_Can also be called as Hooks:Unregister( hook_id )_  
Removes a hook, so that it will no longer call any hooked functions that have been added to it.  
`hook_id` The unique identifier of the hooked function to unregister.  

	Hooks:UnregisterHook( "OnMyExampleModLoaded" )

### Hooks:Call( hook_id, ... )
Calls the hook with `hook_id`, and executes all hooked functions listening to this hook. Any arguments can be passed into the call.  
`hook_id` The unique identifier of the hook to call its hooked functions.  
`...` Any arquements to pass into each of the hooked function calls.  

	Hooks:Call( "OnMyExampleModLoaded", "TestData", 1234, { 5, 6, 7, 8 } )

### Hooks:ReturnCall( hook_id, ... )
Identical to Hooks:Call except will return the first non-nil value returned by a hooked function.
`hook_id` The unique identifier of the hook to call its hooked functions.  
`...` Any arquements to pass into each of the hooked function calls.  

	local r = Hooks:ReturnCall( "OnMyExampleModLoaded", "TestData", 1234, { 5, 6, 7, 8 } )
	do_stuff( r )

### Hooks:PreHook( object, func, id, pre_call )
Automatically hooks a function to be called before the specified function on a specified object.  
`object` The object for the pre-hook to search for the `func` to hook.  
`func` A function name, as a string, on the `object` to be pre-hooked.  
`id` The unique identifier for this pre-hook.  
`pre_call` The function that should be called before `func` is called on `object`.  

	Hooks:PreCall( PlayerManager, "init", "TestPrePlayerManagerInit", function(ply)
		log("PlayerManager Pre-initialized")
	end )

### Hooks:RemovePreHook( id )  
Removes the pre-hook with identifier that matches `id`.  
`id` The unique identifier for the pre-hook to be removed.  

	Hooks:RemovePreHook( "TestPrePlayerManagerInit" )

### Hooks:PostHook( object, func, id, post_call )
Automatically hooks a function to be called after the specified function on a specified object.  
`object` The object for the post-hook to search for the `func` to hook.  
`func` A function name, as a string, on the `object` to be post-hooked.  
`id` The unique identifier for this post-hook.  
`pre_call` The function that should be called after `func` is called on `object`.  

	Hooks:Post( PlayerManager, "init", "TestPostPlayerManagerInit", function(ply)
		log("PlayerManager Post-initialized")
	end )

### Hooks:RemovePostHook( id )  
Removes the post-hook with identifier that matches `id`.  
`id` The unique identifier for the post-hook to be removed.  

	Hooks:RemovePostHook( "TestPostPlayerManagerInit" )
