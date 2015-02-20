
### file.GetDirectories( path )
Get all child directories of the specified path, relative to the PAYDAY 2 executable.  
`path` The path to check for child directories.  

	file.GetDirectories( "mods/" )

### file.GetFiles( dir )
Get all files inside the specified directory `dir`.  
`dir` The directory to check for any child files.  

	file.GetFiles( "mods/base/lua/" )

### file.RemoveDirectory( path )  
Removes an empty directory at directory `path`.  
`path` The path to the directory to remove.  
`returns` True if the directory was removed, false if the directory could not be removed.  

	local removed = file.RemoveDirectory( "mods/my_mod/" )

### file.DirectoryExists( path )
Checks if directory at `path` exists or not.  
`path` The path to the directory to check if it exists.  
`returns` True if the directory exists, false is the directory does not.  

	local path = "mods/my_mod/"
	if file.DirectoryExists( path ) then
		file.RemoveDirectory( path )
	end

### io.file_is_readable( file_path )
Checks if the file at `file_path` is able to be opened by the Lua state.   
`file_path` The file to check if the Lua state is able to open or not.  
`returns` True if the file is openable by Lua, false otherwise.  

	local path = "mods/saves/save_data.lua"
	if io.file_is_readable( path ) then
		-- Read file
	end

### io.remove_directory_and_files( path )
Recursively removes all child files and folders from the directory specified at `path`.  
`path` The directory to attempt to remove all child files and folders.  
`returns` True if the directory and all children were removed, false if the remove failed at any point during the remove.  

	local function uninstall_my_mod()
		io.remove_directory_and_files( "mods/my_mod/" )
	end
