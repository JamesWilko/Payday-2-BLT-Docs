
### log( str )
Prints a string to the developer console, and saves it in the log file.  
`str` The string to be logged

	log( "Hello World!" )
	log( tostring(managers.player:player_unit():key()) )

### dohttpreq( url, callback(data, id), [progress_callback(id, bytes, total_bytes)] )
Performs a HTTP/S request to the specified URL. If successful, returns any retrieved data to the callback.  
`url` The URL to attempt to retrieve data from.  
`returns` An ID for the current HTTP request.  

`callback(data, id)` A function to run when data is retrieved from the URL.  
`callback: data` The data retrieved from the server, returned as a string.  
`callback: id` The ID of the HTTP request.  

`progress_callback(id, bytes, total_bytes)` A function to run when the HTTP request reports back its progress. It is optional.  
`progress_callback: id` The ID of the HTTP request which is reporting its progress.  
`progress_callback: bytes` The current amount of bytes which have been retrieved.  
`progress_callback: total_bytes` The total amount of bytes which must be downloaded to complete the HTTP request.  

	dohttpreq( "http://google.com/", function(data, id)
		log( "Retrieved server data:\n" .. data )
	end )

	dohttpreq( "http://paydaymods.com/mybigfile.zip",
		function(data, id)
			log( "Retrieved server data:\n" .. data )
		end,
		function(id, bytes, total_bytes)
			log( id .. " downloaded " .. tostring(bytes) .. " / " .. tostring(total_bytes) .. " bytes")
		end
	)

### unzip( zip_file, extract_dir )
Unzips the contents of a specified `zip_file` and places all contents in the directory `extract_dir`. Unzipping archives is slow and is **not** multithreaded, and should only be done during the menu state.  
`zip_file` The zip archive which you wish to extract the contents of.  
`extract_dir` The directory where the contents of ther archive `zip_file` should be extracted to.  

	local zip = "mods/base/downloads/goonmod.zip"
	local mods_folder = "mods/"
	unzip( zip, mods_folder )
