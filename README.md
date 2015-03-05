# Rb.Forms.Barcode

## What is this?

Rb.Forms.Barcode is a Xamarin.Forms view for scanning barcodes.

While the decoding capabilities are powered by ZXing.Net.Mobile, the plugin is written from the ground up with PCL in mind and full Xamarin.Forms support.

It provides **continues scanning**, aims to give high control to the user  combined with high stability.

[Available via Nuget](https://www.nuget.org/packages/Rb.Forms.Barcode), full of awesomeness and also unicorns.

**Please note** that the library is fairly new and only available as beta as we are missing some features like iOS or WindowsPhone support and more detailed controls.

### Features

* Continues scanning!
* Fully Xamarin.Forms compatible. Add elements on top and adapt it to your needs.
* PCL based as far as possible.
* Bindable properties and events.
* Android support.
* No crashing, hanging or blocking the camera. ;)

## Setup

1. Install the [package via nuget](https://www.nuget.org/packages/Rb.Forms.Barcode) into your PCL and platform specific projects.
2. Add the registration call `BarcodeScannerRenderer.Init();` to your platform specific Main class.  
3. Use the new `BarcodeScanner` class in your c# or xaml code.

Example implementation of the Init call:

```
base.OnCreate(bundle);  
Xamarin.Forms.Forms.Init(this, bundle);  
// this is important so that the compiler picks up the assembly reference
BarcodeScannerRenderer.Init();
```

## Usage

1. Create an instance of the `BarcodeScanner` class. Dont forget to give it a height and width.
2. Register an EventHandler for the `BarcodeScanner.BarcodeFound` event.
3. ???
4. Done

The scanning kicks in as soon as the element is visible on screen and stops when the view is not visible or the page holding the element gets removed from the stack.

You can enable or disable the scanner and preview using the `BarcodeScanner.IsEnabled` property.

### Bindable properties and events

What | Type | Description
---- | ---- | -----------
`BarcodeScanner.BarcodeFound` | EventHandler | The event gets raised when a barcode was found and decoded. Use this to start of your custom logic.
`BarcodeScanner.IsEnabled` | Property | If `true` opens the camera and starts the preview. If `false` stops the preview and releases the camera.
`BarcodeScanner.Barcode` | Property | A bindable property that holds the value of the last found barcode.

### Debugging

Rb.Forms.Barcode provides you with a tremendous amount of debug information, so do not forget to check your application log:

```
[Rb.Forms.Barcode] [BarcodeScannerRenderer] OnElementChanged
[Rb.Forms.Barcode] [BarcodeScannerRenderer] OnElementPropertyChanged
[Rb.Forms.Barcode] [BarcodeScannerRenderer] SurfaceCreated
[Rb.Forms.Barcode] [CameraControl] OpenCamera
[Rb.Forms.Barcode] [CameraControl] AssignPreview
[Rb.Forms.Barcode] [BarcodeScannerRenderer] SurfaceChanged
[Rb.Forms.Barcode] [CameraControl] StartPreview
[Rb.Forms.Barcode] [CameraConfigurator] Focus Mode [continuous-picture]
[Rb.Forms.Barcode] [CameraConfigurator] Scene Mode [auto]
[Rb.Forms.Barcode] [CameraConfigurator] Metering area [True]
[Rb.Forms.Barcode] [CameraConfigurator] Video stabilization [False]
[Rb.Forms.Barcode] [CameraConfigurator] White balance [auto]
[Rb.Forms.Barcode] [BarcodeScannerRenderer] OnVisibilityChanged [Gone]
[Rb.Forms.Barcode] [CameraControl] HaltPreview
[Rb.Forms.Barcode] [BarcodeScannerRenderer] SurfaceDestroyed
[Rb.Forms.Barcode] [CameraControl] ReleaseCamera
[Rb.Forms.Barcode] [BarcodeScannerRenderer] Disposing
```

### A word of warning

The library aims to handle most of the logical usecases automagically. This includes starting/halting the preview and more important opening and releasing the camera.

Given the complexity of apps there are certain scenarios where this is not possible. As example when [sleeping](https://github.com/rebuy-de/rb-forms-barcode/blob/master/Sample/Sample.Pcl/Pages/ScannerPage.cs#L106)/[resuming](https://github.com/rebuy-de/rb-forms-barcode/blob/master/Sample/Sample.Pcl/Pages/ScannerPage.cs#L113) the app or in certain cases when the [page gets disposed](https://github.com/rebuy-de/rb-forms-barcode/blob/master/Sample/Sample.Pcl/Pages/ScannerPage.cs#L135) without notifying the view.

Please ensure that you react on those events and that Rb.Forms.Barcode releases the camera properly, else you might run into issues with the camera not being available for you or other apps on the device because it is already opened!

## Sample

There is a [full working sample](https://github.com/rebuy-de/rb-forms-barcode/tree/master/Sample) in the github repository that should give you a headstart. The relevant code is included in the PCL part of the project. The sample is part of the project solution.

![Android sample](sample.png)

## Whats planed

Take a look at our [planned features issue list](https://github.com/rebuy-de/rb-forms-barcode/labels/planned%20feature) or even better contribute! :)

## Contributing

Don't hesitate to fork and improve the code, as long as you share it with us. ;)