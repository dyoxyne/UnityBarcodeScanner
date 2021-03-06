# Unity Barcode Scanner
Small Barcode Scanner library for Unity
 
## Informations
**Author**: Kefniark

**Version**: 0.2

**Main Repository**: https://github.com/kefniark/UnityBarcodeScanner

**Samples**: [Here](https://github.com/kefniark/UnityBarcodeScanner/tree/master/Assets/Samples)

## Usage
Here is a basic example
```csharp
// Create a basic scanner
BarcodeScanner = new Scanner();

// Start playing the camera
BarcodeScanner.Camera.Play();

// When for the camera to be ready
BarcodeScanner.OnReady += (sender, arg) => {
    
    // Bind the Camera texture to any RawImage in your scene
    Image.texture = BarcodeScanner.Camera.Texture;

    // Start Scanning
    BarcodeScanner.Scan((barCodeType, barCodeValue) => {

        // This callback is call when something is scanned
        Debug.Log("Found: " + barCodeType + " / " + barCodeValue);
    });
};

...

void Update()
{
    // The barcode scanner has to be updated manually
	BarcodeScanner.Update();
}
```
Check the samples to have a better example of how to implement it.

## API
** Events **
```csharp
// trigger when the scanner can be used
event EventHandler OnReady;
// trigger when the status of the scanner change
event EventHandler StatusChanged;
```

** Properties **
```csharp
// Status of the scanner (enum with different values: Initialize, Running, Paused)
ScannerStatus Status { get; }
// The current parser used (by default ZXingParser)
IParser Parser { get; }
// The current camera used (by default UnityWebcam)
IWebcam Camera { get; }
```

** Method **
```csharp
// Start to scan (the callback provide the type and the value of any barcode found)
void Scan(Action<string, string> Callback);
// Stop the scan
void Stop();
// NEED to be call in Update or FixedUpdate
void Update();
// NEED to be call before leaving the scene
void Destroy();
```

## Changes

### 0.2 (24/09/2016)
* Implement Basic Samples
* Tested with WebGL & Desktop (pc/mac)
* Add lots of comments
* Fix an issue with releasing the camera when leaving the scene

### 0.1 (22/09/2016)
Just the startup of this small project.
Lots of elements are still missing but should arrive soon.
