
# Delayed Calls

Delayed Calls are function calls which can be delayed by a set amount of time. They are delayed by a time value in seconds, if you want to delay a call until a specific event happens, or another function is ran, you may want to use [`Hooks`](hooks.md) instead.  

---

### DelayedCalls:Add( id, time, func )
Adds a delayed call that will automatically be ran after the time has expired.  
`id` The unique identifier of this delayed call.  
`time` A time value, in seconds, that the function `func` should run after.  
`func` The function that should be ran if `time` passes.  

	DelayedCalls:Add( "DelayedCallsExample", 5, function()
		log("This will be called after 5 seconds.")
	end )

### DelayedCalls:Remove( id )
Removes a delayed call with the identifier that matches `id`. If the delayed call does not exist, or has expired, this function does nothing.  
`id` The unique identifier of the delayed call to attempt to remove.  

	DelayedCalls:Remove( "DelayedCallsExample" )

