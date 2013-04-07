# ZXing QR code scanner

### Challenge

Create a new project in Xamarin Studio and add the ZXing framework from the Component Store. Use the ZXing framework to create a barcode scanner that displays the text value of scanned QR codes in a label.

### Walkthrough (iOS version)

* In Xamarin Studio, Create a new single-view iOS project called `ZXingScanner`

* Using Xamarin Studio's built-in Component Store, add the free ZXing component to your project

* Double-click the MainStoryboard file in the Xamarin Studio solution pane to open the application's main layout in Xcode's integrated design tool

* Drag a `UIButton` control from the Xcode object library into the application view. In the property editor, change its label to say "Scan"

* Drag a `UILabel` control onto the view and place it near the top. Resize it horizontally so that it stretches across the entire top of the view.

* Activate Xcode’s assistant editor view to expose the generated Objective-C code

* Create an outlet for the button and name it `buttonScan`

* Create an outlet for the label and name it `labelOutput`

* Save the storyboard file and return focus to Xamarin Studio

* Add the following lines to the view controller source file, right under the existing `using` statements at the top of the file:

```
using ZXing;
```

* Add the following code to the `ViewDidLoad` method to make the application launch the ZXing scanner when the Scan button is pressed and display the captured value in the label when a QR code is scanned:

```
buttonScan.TouchUpInside += (sender, e) => {
  var scanner = new ZXing.Mobile.MobileBarcodeScanner();
  scanner.Scan().ContinueWith(t => {
    if (t.Result != null)
      InvokeOnMainThread(() => labelOutput.Text = t.Result.Text);
  });
};
```
* Run your application on a device! You can use [this QR code](https://github.com/xamarin/mini-hacks/blob/master/QRScanner/qrcode.png) to make sure that it works.

### Walkthrough (Android Version)

* In Xamarin Studio, Create a new Android Application project called `ZXingScanner`

* Using Xamarin Studio's built-in Component Store, add the free ZXing component to your project

* Double-click the main.axml file in the Xamarin Studio solution pane under Resources/layout to open the application's main layout

* Using the default button, in the property editor, change its Text to say `Scan`

* Change the button's id to `@+id/buttonScan`

* Drag a `TextView` control onto the view and place it underneath the button. 

* Change the TextView's id to `labelOutput`

* Save the main.axml layout file and return to the 'MainActivity.cs'

* Add the following lines to the MainActivity.cs source file, right under the existing `using` statements at the top of the file:

```
using ZXing;
```

* Add the following code to the `button.Click += delegate` method to make the application launch the ZXing scanner when the Scan button is pressed and display the captured value in the label when a QR code is scanned:

```
button.Click += delegate
{
	var scanner = new ZXing.Mobile.MobileBarcodeScanner();
	scanner.Scan().ContinueWith(t => {   
		if (t.Result != null)
			RunOnUiThread(()=> labelOutput.Text = t.Result.Text);
	});
};
```

* Add the following line to the AndroidManifest.xml
```
<uses-permission android:name="android.permission.CAMERA" />
````

* Run your application on a device! You can use [this QR code](https://github.com/xamarin/mini-hacks/blob/master/QRScanner/qrcode.png) to make sure that it works.