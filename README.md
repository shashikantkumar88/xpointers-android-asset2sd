# Asset2SD plugin for Phonegap - v2.0 #
By Gautam Chaudhary

Phonegap plugin for Android for copying files from app assets to device SD Card.
Tested with Phonegap versions 3.0.9.

## Adding the Plugin to your project ##

1. To install the plugin, 'cordova plugin add https://github.com/shashikantkumar88/xpointers-android-asset2sd.git'

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
	
### Folowing are the code for copy file from asset. copyPDF method should be present in controller   - 	
	
	$scope.copyPdf = function() {
                var remoteFile = 'http://ipfdev.stratawiz.com/Topics/ILDIPFUpdateIssue7.pdf';
                var destinationPath;
                var localFileName = remoteFile.substring(remoteFile.lastIndexOf('/') + 1);
                window.requestFileSystem(LocalFileSystem.PERSISTENT, 0, function(fileSystem) {
                    fileSystem.root.getDirectory("IPFDownloads", {create: true}, function(dirEntry) {
                        dirEntry.getFile(localFileName, {create: true, exclusive: false}, function(fileEntry) {
                            var localPath = fileEntry.toURL();
                            if (device.platform === "Android" && localPath.indexOf("file://") === 0) {
                                destinationPath = localPath.substring(7);
                            }
                            var destinationFilePath = destinationPath;
                            asset2sd.copyFile(
                                    {
                                        asset_file: 'www/assets/ILDIPFUpdateIssue7.pdf',
                                        destination_file: destinationFilePath
                                    },
                            function() {
                                alert('success...........');
                            }, function() {
                                alert("File copy error.");
                            });
                        }, function(error) {
                            alert("Get file error");
                        });
                    }, function(error) {
                        alert("Get dir error");
                    });
                }, function(error) {
                    alert("Get System error");
                });
            };

After success, it will create IPFDownload folder and inside that it will copy file from asset.
