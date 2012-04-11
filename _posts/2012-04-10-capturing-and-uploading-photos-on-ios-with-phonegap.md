---
layout: post
title: "Capturing and Uploading Photos on iOS with PhoneGap (Cordova)"
description: ""
category: General
tags: [phonegap, ios, iphone, javascript, cordova]
---
{% include JB/setup %}

Lately I've been doing a lot of work with <a href="http://docs.phonegap.com" target="_blank">PhoneGap</a>, now known as Cordova. PhoneGap lets you write "native" iOS, Android, Blackberry, etc... applications using standard web technologies, such as HTML, CSS, and JavaScript. They also give you a JavaScript API to access parts of the device, such as the camera, the accelerometer, the compass, etc... In this article I would like to take a quick look at how to take a new picture, or use an existing library photo, and how to upload it to a webserver somewhere.

### The Code:

{% highlight javascript %}

// use an existing photo from the library:
useExistingPhoto: function(e) {
  this.capture(Camera.PictureSourceType.SAVEDPHOTOALBUM);
};

// take a new photo:
takePhoto: function(e) {
  this.capture(Camera.PictureSourceType.CAMERA);
};

// capture either new or existing photo:
capture: function(sourceType) {
  navigator.camera.getPicture(this.onCaptureSuccess, this.onCaptureFail, {
    destinationType: Camera.DestinationType.FILE_URI,
    sourceType: sourceType,
    correctOrientation: true
  });
};

// if photo is captured successfully, then upload to server:
onCaptureSuccess: function(imageURI) {
  var fail, ft, options, params, win;
  // callback for when the photo has been successfully uploaded:
  success: function(response) {
    alert("Your photo has been uploaded!");
  };
  // callback if the photo fails to upload successfully.
  fail: function(error) {
    alert("An error has occurred: Code = " + error.code);
  };
  options = new FileUploadOptions();
  // parameter name of file:
  options.fileKey = "product[image]";
  // name of the file:
  options.fileName = imageURI.substr(imageURI.lastIndexOf('/') + 1);
  // mime type:
  options.mimeType = "text/plain";
  params = {
    val1: "some value",
    val2: "some other value"
  };
  options.params = params;
  ft = new FileTransfer();
  ft.upload(imageURI, 'http://example.com/path/to/service', success, fail, options);
};

// there was an error capturing the photo:
onCaptureFail: function(message) {
  alert("Failed because: " + message);
};

{% endhighlight %}

On the whole it's not all that difficult a task to accomplish. The two functions that deserve a bit of attention are <code>capture</code> and <code>onCaptureSuccess</code>. Those two functions are where the real heavy lifting is happening.

### capture:

Let's look at the <code>capture</code> function first. The <code>navigator.camera.getPicture</code> function that is provided by PhoneGap takes three arguments. The first argument is a success callback, the second argument is a failure callback, and the third argument is an object containing options. The documentation spells out most of the options you can pass in here, but since the docs don't cover all of the options, specifically the <code>correctOrientation</code> option, let's quickly look at what each one does.

* __destinationType__: It is _incredibly_ important that you set this options to <code>Camera.DestinationType.FILE_URI</code>. This will make sure the <code>onCaptureSuccess</code> gets a path to the image file, and not the image file itself. This is important because as cameras get more powerful on phones, the more memory these images will take up. If you don't set this option correctly your application will quickly throw a out of memory exception and that's it, game over.

* __sourceType__: This option defines where the photo will be coming from. Set to <code>Camera.PictureSourceType.SAVEDPHOTOALBUM</code> for an existing photo or <code>Camera.PictureSourceType.CAMERA</code> to take a new picture.

* __correctOrientation__: This last option is undocumented, but also _incredibly_ important! By default <code>correctOrientation</code> is set to <code>false</code>, because of this the photo that is uploaded won't necessarily have the orientation that the user who took the photo intended. This is because the meta data for such things as orientation is store on the device, and not in the phone. By setting this to <code>true</code>, the photo will be adjusted to the correct orientation when it is passed into the <code>onCaptureSuccess</code> function.

So those are the most important options that need to be set when calling <code>navigator.camera.getPicture</code>.

### onCaptureSuccess:

When a photo is successfully captured, via the <code>capture</code> function, the <code>onCaptureSuccess</code> function will be called. This function will be passed a path, <code>imageURI</code> to the photo on disk.

PhoneGap has an object that is specifically designed for transfers files from the phone to a web service somewhere. This object is called, <code>FileTransfer</code>. This object exposes a function called, <code>upload</code>, that will send an HTTP POST to the web service and properly encode the photo (we can send file we want, for this example it's a photo) for transport.

The <code>upload</code> function takes five arguments. We can see this in action near the bottom of the <code>onCaptureSuccess</code> function.

* The first argument is the path to the file on disk, the <code>imageURI</code> argument that the <code>onCaptureSuccess</code> function received. 

* The second argument is the URL of the web service you wish to post the file to.

* The third argument is a callback that will be executed when the file has been successfully uploaded to the server. This is the <code>success</code> function we defined inside of <code>onCaptureSuccess</code>.

* The fourth argument is a callback that will be executed should the file fail to upload successfully to the server. This is the <code>fail</code> function we defined inside of <code>onCaptureSuccess</code>.

* The fifth argument is an object containing any extra parameters you want to send to the server.