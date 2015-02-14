
# Lua Networking Hooks

Certain hooks are called when a Lua-network event is received from another player. In order to make use of the data received from other players, your mod should make use of the hooks in order to process the data received and call the appropriate functions required.  

For more information on listening to hooks, see the main [Hooks](../hooks.md) page.

---

### NetworkReceivedData( sender, id, data )
The name of the hook that is called everytime any data is received via LuaNetworking from another player.  
`sender` The peer ID of the player who sent the networked data.  
`id` The unique identifier of the data sent.  
`data` The data sent to us, as a string. It may have to be converted to another data type in order for us to make use of it.  

	local private_message_id = "PrivateMessage"
	Hooks:Add("NetworkReceivedData", "NetworkReceivedData_PMs", function(sender, id, data)

		if id == private_message_id then

			local name = Net:GetNameFromPeerID( sender )
			log( "Received Private Message from: " .. name )
			log( "Message: " .. data )

		end

	end)

As we can see in our example above, once subscribed to our hook we need to check the ID of the data we receive to make sure that the data is relevant to our mod.  
If the data we receive is not relevant, then we should not process or call anything, as another mod is likely handling it instead.  
