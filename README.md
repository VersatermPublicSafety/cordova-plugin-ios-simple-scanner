# cordova-plugin-ios-simple-scanner [![npm version](https://badge.fury.io/js/cordova-plugin-ios-simple-scanner.svg)](https://badge.fury.io/js/cordova-plugin-ios-simple-scanner)

Simple iOS Barcode Scanner for Cordova.

- **PDF417 Supported!**
- **QR Supported!**
- Flash toggle button
- Cancel scan button
- Optional onscreen guide box (with 'Scanning...' text)

## How To Use

Install the plugin using:

```terminal
cordova plugin add cordova-plugin-ios-simple-scanner

//or

cordova plugin add https://github.com/VersatermPublicSafety/cordova-plugin-ios-simple-scanner
```

Call the `scanBarcode` method with the following parameters:

|Parameter|Type|Description|
|---|---|---|
|orientation|String|The locked orientation to show the scanner in. Can be: "portrait", "landscapeLeft", "landscapeRight", "portraitUpsideDown".|
|show guide|Boolean|If set to true, the guide box and 'Scanning..' label will be shown.|
|success callback|Function|Method to handle successfully scanning a barcode. This method will be passed an object with two string attributes: "format" - Type of the barcode scanned, "data" - all data contained within the barcode (string).|
|error callback|Function|Method to handle all errors / cancelling the scanner. A status message will be passed in.|

Example:

```javascript
var successCallback = function(result) {
    console.log("Format Found: " + result.format + ", Data: " + result.data);
};

var errorCallback = function(error) {
    console.log("Error Reading Barcode: " + error);
};

// Scan as landscapeLeft, showing the box guide, with success and error callbacks
cordova.plugins.ios.simpleScanner.scanBarcode("landscapeLeft", true, successCallback, errorCallback);

// Or you can use promise logic:
cordova.plugins.ios.simpleScanner.scanBarcode("landscapeRight", true)
    .then(result => {
        console.log("Format Found: " + result.format + ", Data: " + result.data);
    })
    .catch(error => {
        console.log("Error Reading Barcode: " + error);
    });
```

## Supported Formats

- PDF417
- QR

## Known Issues

If the scan method is called while the scanner is already running, the scanner will freeze. If you are planning on opening another instance of the scanner, make sure the current one is not scanning.

Since this plugin creates a view to show the user, there will be a warning about time taken to run the plugin that will suggest running in a background thread.

## Images

All icon images were taken and modified from [ionicons](http://ionicons.com/) (100% Free and Open Source - MIT).

## License

MIT License, please look at the LICENSE file.