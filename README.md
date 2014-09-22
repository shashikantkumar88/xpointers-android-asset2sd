# Asset2SD plugin for Phonegap - v2.0 #
By Gautam Chaudhary

Phonegap plugin for Android for copying files from app assets to device SD Card.
Tested with Phonegap versions 3.0.9.

## Adding the Plugin to your project ##

1. To install the plugin, 'cordova plugin add https://github.com/gkcgautam/Asset2SD.git'

## Using the plugin ##

### Copy File ###
Use the method `asset2sd.copyFile` with parameters: 

* `asset_file` - The file to be copied from app assets. For example, "www/images/photo.jpg"
* `destination_file` - The destination file to which file has to be copied. If the path doesn't already exist, it gets created automatically. For example, "funnyPhotos/photo.jpg"
* Success callback.
* Error callback

Example usage:

    asset2sd.copyFile({
		asset_file: "www/images/photo.jpg",
		destination_file: "funnyPhotos/photo.jpg",
		function() { alert('success');//open file }, 
		function() { alert('fail'); }
	});       
