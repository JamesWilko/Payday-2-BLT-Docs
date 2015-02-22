
# Automatic Updates

The Payday 2 BLT has a feature that allows some mods to automatically update themselves from within Payday 2 itself.
Any mod that is setup on the [Payday Mods Manager](http://manage.paydaymods.com/) will automatically be checked for updates when the game loads.  

In order for the automatic updates system to work for a mod, it must first have its identifier created in the mod manager.
If you do not have an account for the Mod Manager, [contact one of us](http://paydaymods.com/contact/) and we'll set you up an account and get you started.  

Once an identifier has been created, the mod definition file itself needs to have the identifier data itself put into it, so that the game knows which mods
to check for updates, and to download. _Never put any other identifier other than your own mods in the mod definition file, or your mod will be un-installed
and another mod installed instead during an update._  

There are also some special considerations which should be made when creating your mod if you will want to incorporate automatic updates. Read these carefully,
or you may cause users to lose their save data for your mod, damage your modifications installation, or damage a users Payday installation.  

---

## Mod Definition File
Your mod will require it's mod definition file updating before your automatic updates will work. This is done via adding an `updates` key to your mod definition file.

### Updates Key
The `updates` key is an array of objects with specific keys to tell the mod manager how to handle updating your mod.  
`revision` An integer or float key which contains the number which will be compared to the latest server version for deciding if an update is required or not.  
`identifier` A string key containing the identifier of your mod. This is used to check the correct mods on the PaydayMods API, and to download and update the correct mod when required.  
`install_dir` A string key containing the path of the location to install your mod. This is only required if you need your mod to be installed in a path other than the `mods` folder.
For installing and updating the accompanying mod_overrides of your mod, this value should be set to `assets/mod_overrides/`.  
`install_folder` A string key containing the name of your mod_overrides folder. This folder will be removed, so that the updated version may be installed in its place.  
`display_name` A string key used for the display name of any extra downloads and updates that may be required alongside your mod. If this value is not set, the name of your mod will be used instead.  

	"updates" : [
		{
			"revision" : 12,
			"identifier" : "goonmod",
		},
		{
			"revision" : 10,
			"identifier" : "goonmodwepcust",
			"install_dir" : "assets/mod_overrides/",
			"install_folder" : "GoonModWeaponCustomizer",
			"display_name" : "GoonMod Weapon Customizer"
		}
	]

---

## Updating Your Mod
Once you've added your `updates` key to your mod definition, and setup your mod on the Mod Manager, you can prepare your mod for upload to the server, and to put an update out.  

**Step 1 - Increment your revision**  
You will need to increment your revision numbers of your mod to match the new revision you are about to push to the server.
If you do not update your revision number, then you will either cause everybody to have to update your mod every time they load the game, or your mod will not know that it has to update.

	"revision" : 12,
		to
	"revision" : 13,

Make a note of your new revision since you'll be using this on the Mod Manager. Also remember to do the same for your mod_override updates if you have any defined alongside your main mod.  

**Step 2 - Archive**  
To upload your mod you will need to archive the mod folder, and the mod_overrides folder if necessary, correctly.
This is done by simply creating a zip file of the mod folder from within the mods directory, or of the overrides folder from within the mod_overrides directory.  

!["Archiving a Mod"](http://paydaymods.com/wp-content/uploads/2015/02/archive_mod.png)
_[Archiving mod_overrides works exactly the same...](http://paydaymods.com/wp-content/uploads/2015/02/archive_mod_overrides.png)_

**Step 3 - Mod Manager**  
The next step is done on the Mod Manager, so you'll want to open it up and select the mod you intend to update.
Click on the `New Version` tab if it isn't already open, this is the page you'll use to put out your update.  
First thing, is to put the revision number that you set in Step 1 into the `Revision` field. This will be used to check the server version against the local version of your mod.  
Next, fill in the `Patch Notes` for your mod. These will be displayed to the user when they select that they want to view the patch notes of an update.  
Finally, select your archived mod to be uploaded in the `Release` field. This it the file that will be downloaded and installed by all users of your mod.  

**Step 4 - Publish**  
Once you've filled in your update information, simply click the `Publish New Version` button. Your archive will be uploaded, and once complete will start to automatically update all mod users.  
