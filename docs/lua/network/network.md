
# Lua Networking

A collection of helper Lua functions to allow mods to send networked data to other players who have the mod installed.  
All data is sent as string data between clients, so any non-string data, such as numbers or Vector3's, must be converted into a string before transmission.  
  
_All networking functions are contained in the **LuaNetworking** global table. You may access all functions in short by creating an alias variable which can help cut down on lengthy lines of code._  

	local Net = _G.LuaNetworking

---

### Net:IsMultiplayer()
Checks if the game is in a multiplayer state, and has an active multiplayer session.  
`returns` The active multiplayer session, or _nil_.  

	if Net:IsMultiplayer() then
		log("Multiplayer!")
	else
		log("Single-player!")
	end


### Net:IsHost()
Checks if the local player is the host of the multiplayer game session.  
`returns` True if the local player is the host of the game session, or false. Also returns false if not multiplayer session is running.  

	if Net:IsHost() then
		log("I am the host!")
	end


### Net:IsClient()
Checks if the local player is a client of the multiplayer game session.  
`returns` True if the local player is not the host of the game session, or false. Also returns false if not multiplayer session is running.  

	if Net:IsClient() then
		log("I am a client!")
	end


### Net:LocalPeerID()
Returns the peer ID of the local player.  
`returns` The peer ID of the local player in the current multiplayer session. Returns _0_ if no session was found.  

	local peer_id = Net:LocalPeerID()


### Net:GetNameFromPeerID( id )
Returns the name of the player associated with the specified peer ID `id`.  
`id` The peer ID to lookup in the session players and get their name.  
`returns` The name of the player with peer ID `id`. Returns _No Name_ if a name could not be found the specified ID.  

	local my_id = Net:LocalPeerID()
	local my_name = Net:GetNameFromPeerID( my_id )
	log( "My name is: " .. my_name )


### Net:GetPeers()
An accessor for the session peers table.  
`returns` The table of all connected peers in the current multiplayer session.  

	for id, ply in pairs( Net:GetPeers() ) do
		log( id .. " = " .. Net:GetNameFromPeerID( id ) )
	end


### Net:GetNumberOfPeers()
Utility function for quickly and easily getting the number of players in the multiplayer session.  
`returns` The number of connected players in the current session.  

	local num = Net:GetNumberOfPeers()
	log( "There are " .. tostring(num) .. " connected players." )


### Net:SendToPeers( id, data )
Sends networked data `data` with a message id of `id` to all connected players.  
`id` The unique identifier of the data to send to connected players. This value shoud be unique to the data type you are sending, or to the remote function you wish to call on another players game.  
`data` The data to send to all connected players. It should be in string format so that it will be transmitted to other players properly.  

	Net:SendToPeers( "GoonModCustomLaserColour", "1.0000000,0.0000000,1.0000000" )


### Net:SendToPeer( peer, id, data )
Identical to `Net:SendToPeers`, except the first argument is the ID of the peer who should receive the data.  
`peer` The peer ID of the player who should receive the networked data.  
`id` The unique identifier of the data to send to the peer with id `id`.  
`data` The data to send.  

	local message_text = "This is a private message to the player with Peer ID 1."
	Net:SendToPeer( 1, "PrivateMessage", message_text )


### Net:SendToPeersExcept( peer, id, data )
Identical to `Net:SendToPeer`, except the first argument is a peer ID, or table or peer ID's who should be excluded from receiving the networked data.  
`peer` A peer ID, or a table of peer ID's, who should be excluded from receiving this networked data.  
`id` The unique identifier of the data to send to the peer with id `id`.  
`data` The data to send.  

	local message_text = "This message will be send to everybody who does not have a Peer ID of 4."
	Net:SendToPeersExcept( 4, "PrivateMessage", message_text )

	local exclude = { 1, 2 }
	local message_text = "This message will be send to everybody who's peer ID does not appear in the exlude table"
	Net:SendToPeersExcept( exclude, "PrivateMessage", message_text )
