
# Lua Networking Extensions

Various extension and helper functions for converting data types that may not normally be convertible into a string, into a string and back into their original type.  

---

### Net:TableToString( tbl )
Converts a table into a string which is able to sent through the Networking functions. It will only perform a shallow conversion, meaning it should not be used with nested tables.  
`tbl` The table to be converted into a string.  
`returns` A string representation of the table passed into the function.  

	local tbl = { 1, 2, 3, 4, "hello world!" }
	local str = Net:TableToString( tbl )
	Net:SendToPeers( "NetworkTableStringTest", str )


### Net:StringToTable( str )
Converts a formatted string into a table. Should be used for turning a networked table sent as a string back into its original table.  
`str` The formatted string to attempt to convert back into a table.  
`returns` A table containing the formatted data from `str`.  

	local str = "key|value,key2|another value,another key|yet another value"
	local tbl = Net:StringToTable( str )


### Net:ColourToString( col )
Converts a colour into a formatted string, which is able to be sent through the Networking functions.  
`col` The colour to be converted into a formatted string.  
`returns` A formatted string containing the colour data from `col`.  

	local color = Color.red
	local col_str = Net:ColourToString( color )
	Net:SendToPeers( "NetworkColourStringTest", col_str )


### Net:StringToColour( str )
Converts a formatted string into a colour. Should be used for turning a networking colour sent as a string back to its original object.  
`str` The formatted string to attempt to convert back into a Color object.  
`returns` A Color object containing the original colour.

	local col_str = "r:1.0000|g:0.2125|b:0.4568|a:1.0000"
	local color = Net:StringToColor( col_str )
