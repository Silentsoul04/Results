The MIT License (MIT)

Copyright (c) 2012 - 2015 Bartosz Firyn and Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
# Webcam Capture API

This library allows you to use your build-in or external webcam directly from Java. It's designed to abstract commonly used camera features and support various capturing frameworks.

[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.github.sarxos/webcam-capture/badge.svg)](http://search.maven.org/#artifactdetails|com.github.sarxos|webcam-capture|0.3.10|bundle)
[![Build Status](https://img.shields.io/travis/sarxos/webcam-capture.svg?branch=master)](http://travis-ci.org/sarxos/webcam-capture)
[![Coverage Status](https://img.shields.io/coveralls/sarxos/webcam-capture.svg?branch=master)](https://coveralls.io/r/sarxos/webcam-capture?branch=master)

## Rationale

Assume situation when your code depends on some capturing framework, but suddenly you have to drop it and use different, maybe newer one (e.g. replace archaic JMF with newest GStreamer). By doing this you will have to rewrite significant piece of your code because these frameworks are completely different and not compatible at all. This is where Webcam Capture API comes to save the world - it was created to remove the burden of such situations so you do not have to rewrite your code never again, but instead you can simply switch the driver class to different one.

## Features

* Simple, thread-safe and non-blocking API,
* No additional software required,
* Supports multiple platforms (Windows, Linux, Mac OS, etc) and various architectures (32-bit, 64-bit, ARM),
* Get images from build-in or USB-connected PC webcams, 
* Get images from IP / network cameras (as MJPEG or JPEG),
* Offers ready to use motion detector,
* All required JARs Available in Maven Central,
* Offers possibility to expose images as MJPEG stream,
* It is available as Maven dependency or standalone ZIP binary (with all dependencies included),
* Swing component to display video feed from camera,
* Swing component to choose camera (drop down),
* Multiple capturing frameworks are supported:
  * [OpenIMAJ][];
  * [LTI CIVIL][LTI-CIVIL];
  * [Java Media Framework (JMF)][JMF];
  * [Freedom for Media in Java (FMJ)][FMJ];
  * [OpenCV][] via [JavaCV][];
  * [VLC][] via [vlcj][];
  * [V4L][] via [v4l4j][V4L4j];
  * [GStreamer][] (0.10.x only) via [gstreamer-java][gstreamerj];
  * [FFmpeg][];
  * MJPEG IP Cameras;
  

The latest stable version is: **```0.3.12```**

The latest development version is: **```0.3.13-SNAPSHOT```**

## Raspberry PI

_(and other ARM devices)_

The lates version (0.3.10) does not work on ARM just out of the box. To make it working you need to replace version 0.6.2 of BridJ JAR by the [0.6.3-SNAPSHOT](https://oss.sonatype.org/service/local/artifact/maven/redirect?r=snapshots&g=com.nativelibs4java&a=bridj&v=0.6.3-SNAPSHOT) or newer [bridj-0.7-20140918](http://maven.ecs.soton.ac.uk/content/groups/maven.openimaj.org/com/nativelibs4java/bridj/0.7-20140918/bridj-0.7-20140918.jar). Moreover, lately Jonathon Hare from OpenIMAJ team, found a problem described in [bridj #525](https://github.com/ochafik/nativelibs4java/issues/525) which causes problems on armhf architecture.

## Maven

The latest stable version is [available](http://search.maven.org/#artifactdetails|com.github.sarxos|webcam-capture|0.3.12|bundle) in Maven Central:

```xml
<dependency>
  <groupId>com.github.sarxos</groupId>
  <artifactId>webcam-capture</artifactId>
  <version>0.3.12</version>
</dependency>
```

Snapshot version:

```xml
<repository>
	<id>Sonatype OSS Snapshot Repository</id>
	<url>http://oss.sonatype.org/content/repositories/snapshots</url>
</repository>
```
```xml
<dependency>
	<groupId>com.github.sarxos</groupId>
	<artifactId>webcam-capture</artifactId>
	<version>0.3.13-SNAPSHOT</version>
</dependency>
```

## Download

The newest stable version can be downloaded as separated ZIP binary. This ZIP file contains Webcam Capture API itself and all required dependencies (in ```libs``` directory). Click on the below link to download it:

 [webcam-capture-0.3.12-dist.zip](https://github.com/sarxos/webcam-capture/releases/download/webcam-capture-parent-0.3.12/webcam-capture-0.3.12-dist.zip)

The latest development version JAR (aka SNAPSHOT) can be downloaded [here](https://oss.sonatype.org/service/local/artifact/maven/redirect?r=snapshots&g=com.github.sarxos&a=webcam-capture&v=0.3.13-SNAPSHOT).

## Contribution

If you have strong will, spare time, knowledge or even some small amount of money you would like to spent for good purpose you can help developing this awesome Webcam Capture API and make it even better! Several kinds of contributions are very welcome:

##### Star Project

If you think this project is great, you would like to help, but you don't know how - you can become project's stargazer. By starring you're making project more popular. Visit [this](https://github.com/blog/1204-notifications-stars) link if you would like to learn more about how notifications and stars works on Github.

##### Report Bug or Feature

If you've found a bug or you've came-up with some fantastic feature which can make Webcam Capture a better API to use, don't hesitate to [create new issue](https://github.com/sarxos/webcam-capture/issues/new) where you can describe in details what the problem is, or what would you like to improve.

##### Perform Tests

Since Webcam Capture use some part of native code, it's very hard to cover all supported operating systems. I'm always testing it on 64-bit Ubuntu Linux, Windows XP and Vista (both 32-bit), but I have no possibility to test on Raspberry Pi, Mac OS and 32-bit Linux. Please help and test on those systems if you have such possibility. 

##### Write Code

If you know Java or C++ you can help developing Webcam Capture by forking repository and sending pull requests. Please visit [this](http://stackoverflow.com/questions/4384776/how-do-i-contribute-to-others-code-in-github) link if you don't know how to contribute to other's code at Github. 

##### Donate

People have expressed a wish to donate a little money. Donating won't get you anything special, other than a warm feeling inside, and possibly urge me to produce more freely available material for Webcam Capture project. You can donate via [PayPal](https://www.paypal.com), just click [donate](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=UYMENK76CSYZU) button available below - it will redirect you to the secured PayPal page where you can provide donation amount (there is no minimal value).

[![Donate via PayPal](https://www.paypalobjects.com/en_US/GB/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=UYMENK76CSYZU)

## Hello World

Code below will capture image from your default webcam and save it in ```hello-world.png``` file:

```java
Webcam webcam = Webcam.getDefault();
webcam.open();
ImageIO.write(webcam.getImage(), "PNG", new File("hello-world.png"));
```

## More Examples!

Below are the very pretty basic examples demonstrating of how Webcam Capture API can be used in the Java code. All can be found in the project source code. Please note that some of those examples may use the newest API which has not yet been released to maven Central. In such a case please make sure you are using the newest Webcam Capture API SNAPSHOT.

* [How to detect webcam](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/DetectWebcamExample.java)
* [How to take picture and save to file](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/TakePictureExample.java)
* [How to display image from webcam in Swing panel (basic)](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/WebcamPanelExample.java)
* [How to display image from webcam in Swing panel (more advanced)](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/WebcamViewerExample.java)
* [How to listen on camera connection / disconnection events](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/WebcamDiscoveryListenerExample.java)
* [How to configure capture resolution](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/TakePictureDifferentSizeExample.java)
* [How to configure non-standard capture resolution (e.g. HD720)](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/CustomResolutionExample.java)
* [How to save captured image in PNG / JPG / GIF / BMP etc](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/DifferentFileFormatsExample.java)
* [How to capture with many parallel threads](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/ConcurrentThreadsExample.java)
* [How to detect motion (text mode only)](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/DetectMotionExample.java)
* [How to detect motion with Do-Not-Engage zone](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/DetectMotionDoNotEngageZoneExample.java)
* [How to perform multipoint motion detection](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/MultipointMotionDetectionExample.java)
* [How to display images from multiple IP cameras exposing pictures in JPG format](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-drivers/driver-ipcam/src/examples/java/JpegDasdingStudioExample.java)
* [How to display image from IP camera exposing MJPEG stream](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-drivers/driver-ipcam/src/examples/java/MjpegLignanoBeachExample.java)
* [How to use composite driver to display both, build-in and IP camera images](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-drivers/driver-ipcam/src/examples/java/DualNativeAndMjpegWebcamExample.java)
* [How to work with Raspberry Pi (camera module or UVC device)](https://github.com/sarxos/webcam-capture/wiki/How-To-Configure-Raspberry-Pi)
* [How to flip (mirror) image displayed in ```WebcamPanel```](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/WebcamPanelFlippingExample.java)
* [How to rotate image displayed in ```WebcamPanel```](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/WebcamPanelRotationExample.java)
* [How to rotate image from camera with ```WebcamImageTransformer```](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/ImageTransformerRotationExample.java)
* [How to use AdaptiveSizeWriter to compress images](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/AdaptiveSizeWriterExample.java)
* [How to use Webcam Capture with DroidCam application (smartphone working as IP camera)](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-drivers/driver-ipcam/src/examples/java/DroidCamExample.java)

And here are some more advanced examples, few with quite fancy GUI.

* [How to detect and mark human faces](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-detect-face)
* [How to use ```WebcamMotionDetector``` with the ```JFrame``` window](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-examples/webcam-capture-motiondetector)
* [How to use webcam capture in Java Applet](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-applet)
* [How to use ```WebcamPanel.Painter``` interface to draw effects on ```WebcamPanel``` component](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-painter)
* [How to read QR / DataMatrix and Bar codes (2 examples)](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-qrcode)
* [How to record video from webcam](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-examples/webcam-capture-video-recording/src/main/java/com/github/sarxos/webcam/Encoder.java)
* [How to transcode webcam images into live h264 stream](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-live-streaming)
* [How to use Webcam Capture API in JavaFX](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-javafx)
* [How to use Webcam Capture API in JavaFX and FXML](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-javafx-fxml)
* [How to use Webcam Capture API as JavaFX Service and View](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-javafx-service)
* [How to use Webcam Capture API in SWT](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-swt-awt)
* [How to use ```WebcamImageTransformer``` to draw effects directly on image from camera](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-transformer)
* [How to use Webcam Capture API and WebSockets to transport images from server to web client](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-websockets)
* [How to use Webcam Capture API from Akka](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-examples/webcam-capture-akka/src/main/java/Application.java)


## YouTube Tutorials

Video series by [Genuine Coder](https://www.youtube.com/GenuineCoder) for Webcam Capture beginners:
* [Java Webcam Capture #1: Introduction and Capturing with 3 lines of code](https://www.youtube.com/watch?v=2BHyL_XK8YQ)
* [Java Webcam Capture #2: Take Images with Different Resolutions](https://www.youtube.com/watch?v=dL4MVWJjVVY)
* [Java Webcam Capture #3: Video Feed from Webcam using Thread](https://www.youtube.com/watch?v=RkzfFGP60fw)
* [Java Webcam Capture #4: Video Feed from Webcam (Easy Way)](https://www.youtube.com/watch?v=amMaYzl45Pw)


## Capture Drivers

Webcam Capture API defines ```WebcamDriver``` interface which has been already implemented in several _capturing drivers_ build on top of well-known frameworks used to work with multimedia and cameras. Complete list can be found below.

By default (if other driver is not specified) library uses **default driver** which consists of small, refined part of awesome [OpenIMAJ](http://sourceforge.net/p/openimaj/home/OpenIMAJ/) framework wrapped in thread-safe container. However, there are more ready-to-use drivers which can be used as a replacement or addition to the default one. By utilizing those drivers Webcam Capture can be extended with various new features (e.g. IP camera support). 

List of additional capture drivers includes:

| Driver Name     | Stable | Central | Description                             |
|-----------------|--------|---------|-----------------------------------------|
| [ipcam][]       | yes    | yes     | Driver for IP / network camera          |
| [fswebcam][]    | yes    | yes     | Driver for [FSWebcam][] [CLI][] tool    |
| [gstreamer][]   | yes    | yes     | Driver for [GStreamer][] framework      |
| [openimaj][]    | yes    | yes     | Driver for [OpenIMAJ][] framework       |
| [v4l4j][]       | yes    | no      | Driver for [V4L4j][] library            |
| [jmf][]         | yes    | yes     | Driver for [JMF][] / [FMJ][] frameworks |
| [lti-civil][]   | yes    | yes     | Driver for [LTI-CIVIL][] library        |
| [vlcj][]        | yes    | yes     | Driver for [vlcj][] library             |
| [javacv][]      | yes    | yes     | Driver for [JavaCV][] library           |
| [ffmpeg-cli][]  | poc    | no      | Driver for [FFmpeg][] [CLI][] tool      |

* Central = available in Maven Central Repository
* _poc_ = Proof of Concept

[FSWebcam]:   http://www.firestorm.cx/fswebcam/
[GStreamer]:  http://gstreamer.freedesktop.org/
[gstreamerj]: https://github.com/gstreamer-java
[OpenIMAJ]:   http://www.openimaj.org/
[V4L4j]:      http://code.google.com/p/v4l4j/
[JMF]:        http://www.oracle.com/technetwork/java/javase/download-142937.html
[FMJ]:        http://fmj-sf.net/
[LTI-CIVIL]:  http://lti-civil.org/
[JavaCV]:     https://github.com/bytedeco/javacv/
[VLC]:        http://www.videolan.org/vlc/
[VLCj]:       https://github.com/caprica/vlcj
[V4L]:        https://en.wikipedia.org/wiki/Video4Linux
[FFmpeg]:     http://www.ffmpeg.org/
[OpenCV]:     http://opencv.org/
[CLI]:        http://en.wikipedia.org/wiki/Command-line_interface/

[fswebcam]:   https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-fswebcam
[ipcam]:      https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-ipcam
[gstreamer]:  https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-gstreamer
[openimaj]:   https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-openimaj
[v4l4j]:      https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-v4l4j
[jmf]:        https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-jmf
[lti-civil]:  https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-lti-civil
[javacv]:     https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-javacv
[vlcj]:       https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-vlcj
[ffmpeg-cli]: https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-ffmpeg-cli

### Default Driver

If no other driver is specified, the default driver will be used. It consists of small, refined part of awesome [OpenIMAJ][] framework wrapped in thread-safe container.

### IP Camera Driver

This capture driver gives possibility to access IP camera devices and handle images in form of JPEG pictures or MJPEG streams.

Maven dependency:

```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-ipcam</artifactId>
    <version>{webcam-capture-version-here}</version>
</dependency>
```

How to use:

```java
Webcam.setDriver(new IpCamDriver());
```

More details and binaries download can be found on dedicated [webcam-capture-driver-ipcam](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-ipcam) page.

### Fswebcam Driver

This capture driver gives possibility to use CLI tool called ```fswebcam``` (written by Philip Heron) to access UVC devices connected to the computer. It works only on *nix and requires tool to be installed on the environment where driver is used.

Maven dependency:

```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-fswebcam</artifactId>
    <version>{webcam-capture-version-here}</version>
</dependency>
```

How to use:

```java
Webcam.setDriver(new FsWebcamDriver());
```

More details on how to use, how to install ```fswebcam``` and where binaries can be downloaed, can be found on dedicated [webcam-capture-driver-fswebcam](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-fswebcam) page.

### GStreamer Driver

This capture driver gives possibility to use 
[GStreamer][] to access UVC camera devices connected to computer. It works on Windows and Linux only.

Maven dependency:

```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-gstreamer</artifactId>
    <version>{webcam-capture-version-here}</version>
</dependency>
```

How to use:

```java
Webcam.setDriver(new GStreamerDriver());
```

More details on how to use, how to install GStreamer and where binaries can be downloaded, can be found on dedicated [webcam-capture-driver-gstreamer](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-gstreamer) page.

### OpenIMAJ Driver

This capture driver gives possibility to use [OpenIMAJ][] to access UVC camera devices connected to the computer.

Maven dependency:

```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-openimaj</artifactId>
    <version>{webcam-capture-version-here}</version>
</dependency>
```

How to use:

```java
Webcam.setDriver(new OpenImajDriver());
```

More details on how to use it and where binaries can be downloaded, can be found on dedicated [webcam-capture-driver-openimaj](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-openimaj) page.

### V4L4j Driver

This is capture driver which uses [V4L4j][] project to access UVC camera devices. It works on Linux only and it seems like it is most suitable for use on Raspberry Pi.

Maven dependency:

```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-v4l4j</artifactId>
    <version>{webcam-capture-version-here}</version>
</dependency>
```

How to use:

```java
Webcam.setDriver(new V4l4jDriver());
```

More details on how to use it and where necessary binaries can be downloaded, can be found on dedicated [webcam-capture-driver-v4l4j](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-v4l4j) page.

### JMF Driver

This is capture driver which uses [JMF][] (Java Media Framework) to access UVC webcam devices. The JMF needs to be installed and configured on the PC before this driver can be used. It can also be used alternatively with the [FMJ][] project.

Maven dependency:

```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-jmf</artifactId>
    <version>{webcam-capture-version-here}</version>
</dependency>
```

How to use:

```java
Webcam.setDriver(new JmfDriver());
```

More details on how to use it, install, and where necessary binaries can be downloaded, can be found on dedicated [webcam-capture-driver-jmf](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-jmf) page.

### LTI-CIVIL Driver

This is capture driver designed to leverage capabilities of [LTI-CIVIL](http://sourceforge.net/projects/lti-civil/) project (by Larson Technologies Inc.) and use it to access wide range of UVC devices. It works on 32-bit architectures only.

Maven dependency:

```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-lti-civil</artifactId>
    <version>{webcam-capture-version-here}</version>
</dependency>
```

How to use it:

```java
Webcam.setDriver(new LtiCivilDriver());
```

More details on how to use it, and where necessary binaries can be downloaded, can be found on dedicated [webcam-capture-driver-lti-civil](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-lti-civil) page.

### VLCj Driver

This is capture driver which uses [VLCj][] library from [Caprica Software Limited](http://www.capricasoftware.co.uk/) to gain access to the UVC camera device.

Maven dependency:

```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-vlcj</artifactId>
    <version>{webcam-capture-version-here}</version>
</dependency>
```

How to use it:

```java
Webcam.setDriver(new VlcjDriver());
```

More details on how to use it, how to install, and where necessary binaries can be downloaded, can be found on dedicated [webcam-capture-driver-vlcj](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-vlcj) page.

### JavaCV Driver

This is capture driver which uses [JavaCV][] binding for [OpenCV](https://opencv.org/) to gain access to the UVC camera device.

Maven dependency:

```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-opencv</artifactId>
    <version>{webcam-capture-version-here}</version>
</dependency>
```

or if you are using webcam-capture < 0.3.12:

```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-javacv</artifactId>
    <version>{webcam-capture-version-here}</version>
</dependency>
```

How to use it:

```java
Webcam.setDriver(new JavaCvDriver());
```

More details on how to use it, how to install, and where necessary binaries can be downloaded, can be found on dedicated [webcam-capture-driver-javacv](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-javacv) page.

### FFmpeg CLI Driver

This is capture driver which uses ```ffmpeg``` [CLI][] tool from [FFmpeg][] to access UVC camera device.

Maven dependency:

```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-ffmpeg-cli</artifactId>
    <version>{webcam-capture-version-here}</version>
</dependency>
```

How to use it:

```java
Webcam.setDriver(new FFmpegCliDriver());
```

More details on how to use it, how to install, and where necessary binaries can be downloaded, can be found on dedicated [webcam-capture-driver-ffmpeg-cli](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-ffmpeg-cli) page.


## History

I initially started working on Webcam Capture as a simple proof-of-concept after I read [Andrew Davison](http://fivedots.coe.psu.ac.th/~ad/)'s fantastic book entitled [Killer Game Programming](http://www.amazon.com/Killer-Game-Programming-Andrew-Davison/dp/0596007302/ref=sr_1_1?s=books&ie=UTF8&qid=1360352393&sr=1-1&keywords=killer+game+programming) (which is also available [online](http://fivedots.coe.psu.ac.th/~ad/jg/)). Thank you Andrew! Later I found that there is a complete mess in Java APIs allowing you to capture images from webcams. Once you choose specific API you cannot change it without modifying large parts of the code. I decided to change this situation and write general purpose wrapper for various different APIs (like JMF, OpenCV, OpenIMAJ, LTI-CIVIL, VLC). In such a way, Webcam Capture as we know it today, was brought to life. Today you can change underlying frameworks just by replacing webcam driver (one line code change). If there is no driver for particular framework, it's very easy to write it yourself.

## License

Copyright (C) 2012 - 2017 Bartosz Firyn (https://github.com/sarxos) and contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

![sarxos](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture/src/etc/resources/sarxos.png "sarxos")
Copyright (c) 2010-2012, Olivier Chafik
All rights reserved.
Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

  * Redistributions of source code must retain the above copyright notice, this list of conditions and the following disclaimer.
  * Redistributions in binary form must reproduce the above copyright notice, this list of conditions and the following disclaimer in the documentation and/or other materials provided with the distribution.
  * Neither the name of Olivier Chafik nor the names of its contributors may be used to endorse or promote products derived from this software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE REGENTS AND CONTRIBUTORS ``AS IS'' AND ANY
EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE REGENTS AND CONTRIBUTORS BE LIABLE FOR ANY
DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND
ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
Copyright (c) 2011, The University of Southampton and the individual contributors.
All rights reserved.

Redistribution and use in source and binary forms, with or without modification,
are permitted provided that the following conditions are met:

  * 	Redistributions of source code must retain the above copyright notice, 
	this list of conditions and the following disclaimer.

  *	Redistributions in binary form must reproduce the above copyright notice,
	this list of conditions and the following disclaimer in the documentation
	and/or other materials provided with the distribution.

  *	Neither the name of the University of Southampton nor the names of its
	contributors may be used to endorse or promote products derived from this
	software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR
ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON
ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.   Copyright (c) 2005-2008, The Android Open Source Project

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.


                                 Apache License
                           Version 2.0, January 2004
                        http://www.apache.org/licenses/

   TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

   1. Definitions.

      "License" shall mean the terms and conditions for use, reproduction,
      and distribution as defined by Sections 1 through 9 of this document.

      "Licensor" shall mean the copyright owner or entity authorized by
      the copyright owner that is granting the License.

      "Legal Entity" shall mean the union of the acting entity and all
      other entities that control, are controlled by, or are under common
      control with that entity. For the purposes of this definition,
      "control" means (i) the power, direct or indirect, to cause the
      direction or management of such entity, whether by contract or
      otherwise, or (ii) ownership of fifty percent (50%) or more of the
      outstanding shares, or (iii) beneficial ownership of such entity.

      "You" (or "Your") shall mean an individual or Legal Entity
      exercising permissions granted by this License.

      "Source" form shall mean the preferred form for making modifications,
      including but not limited to software source code, documentation
      source, and configuration files.

      "Object" form shall mean any form resulting from mechanical
      transformation or translation of a Source form, including but
      not limited to compiled object code, generated documentation,
      and conversions to other media types.

      "Work" shall mean the work of authorship, whether in Source or
      Object form, made available under the License, as indicated by a
      copyright notice that is included in or attached to the work
      (an example is provided in the Appendix below).

      "Derivative Works" shall mean any work, whether in Source or Object
      form, that is based on (or derived from) the Work and for which the
      editorial revisions, annotations, elaborations, or other modifications
      represent, as a whole, an original work of authorship. For the purposes
      of this License, Derivative Works shall not include works that remain
      separable from, or merely link (or bind by name) to the interfaces of,
      the Work and Derivative Works thereof.

      "Contribution" shall mean any work of authorship, including
      the original version of the Work and any modifications or additions
      to that Work or Derivative Works thereof, that is intentionally
      submitted to Licensor for inclusion in the Work by the copyright owner
      or by an individual or Legal Entity authorized to submit on behalf of
      the copyright owner. For the purposes of this definition, "submitted"
      means any form of electronic, verbal, or written communication sent
      to the Licensor or its representatives, including but not limited to
      communication on electronic mailing lists, source code control systems,
      and issue tracking systems that are managed by, or on behalf of, the
      Licensor for the purpose of discussing and improving the Work, but
      excluding communication that is conspicuously marked or otherwise
      designated in writing by the copyright owner as "Not a Contribution."

      "Contributor" shall mean Licensor and any individual or Legal Entity
      on behalf of whom a Contribution has been received by Licensor and
      subsequently incorporated within the Work.

   2. Grant of Copyright License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      copyright license to reproduce, prepare Derivative Works of,
      publicly display, publicly perform, sublicense, and distribute the
      Work and such Derivative Works in Source or Object form.

   3. Grant of Patent License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      (except as stated in this section) patent license to make, have made,
      use, offer to sell, sell, import, and otherwise transfer the Work,
      where such license applies only to those patent claims licensable
      by such Contributor that are necessarily infringed by their
      Contribution(s) alone or by combination of their Contribution(s)
      with the Work to which such Contribution(s) was submitted. If You
      institute patent litigation against any entity (including a
      cross-claim or counterclaim in a lawsuit) alleging that the Work
      or a Contribution incorporated within the Work constitutes direct
      or contributory patent infringement, then any patent licenses
      granted to You under this License for that Work shall terminate
      as of the date such litigation is filed.

   4. Redistribution. You may reproduce and distribute copies of the
      Work or Derivative Works thereof in any medium, with or without
      modifications, and in Source or Object form, provided that You
      meet the following conditions:

      (a) You must give any other recipients of the Work or
          Derivative Works a copy of this License; and

      (b) You must cause any modified files to carry prominent notices
          stating that You changed the files; and

      (c) You must retain, in the Source form of any Derivative Works
          that You distribute, all copyright, patent, trademark, and
          attribution notices from the Source form of the Work,
          excluding those notices that do not pertain to any part of
          the Derivative Works; and

      (d) If the Work includes a "NOTICE" text file as part of its
          distribution, then any Derivative Works that You distribute must
          include a readable copy of the attribution notices contained
          within such NOTICE file, excluding those notices that do not
          pertain to any part of the Derivative Works, in at least one
          of the following places: within a NOTICE text file distributed
          as part of the Derivative Works; within the Source form or
          documentation, if provided along with the Derivative Works; or,
          within a display generated by the Derivative Works, if and
          wherever such third-party notices normally appear. The contents
          of the NOTICE file are for informational purposes only and
          do not modify the License. You may add Your own attribution
          notices within Derivative Works that You distribute, alongside
          or as an addendum to the NOTICE text from the Work, provided
          that such additional attribution notices cannot be construed
          as modifying the License.

      You may add Your own copyright statement to Your modifications and
      may provide additional or different license terms and conditions
      for use, reproduction, or distribution of Your modifications, or
      for any such Derivative Works as a whole, provided Your use,
      reproduction, and distribution of the Work otherwise complies with
      the conditions stated in this License.

   5. Submission of Contributions. Unless You explicitly state otherwise,
      any Contribution intentionally submitted for inclusion in the Work
      by You to the Licensor shall be under the terms and conditions of
      this License, without any additional terms or conditions.
      Notwithstanding the above, nothing herein shall supersede or modify
      the terms of any separate license agreement you may have executed
      with Licensor regarding such Contributions.

   6. Trademarks. This License does not grant permission to use the trade
      names, trademarks, service marks, or product names of the Licensor,
      except as required for reasonable and customary use in describing the
      origin of the Work and reproducing the content of the NOTICE file.

   7. Disclaimer of Warranty. Unless required by applicable law or
      agreed to in writing, Licensor provides the Work (and each
      Contributor provides its Contributions) on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
      implied, including, without limitation, any warranties or conditions
      of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A
      PARTICULAR PURPOSE. You are solely responsible for determining the
      appropriateness of using or redistributing the Work and assume any
      risks associated with Your exercise of permissions under this License.

   8. Limitation of Liability. In no event and under no legal theory,
      whether in tort (including negligence), contract, or otherwise,
      unless required by applicable law (such as deliberate and grossly
      negligent acts) or agreed to in writing, shall any Contributor be
      liable to You for damages, including any direct, indirect, special,
      incidental, or consequential damages of any character arising as a
      result of this License or out of the use or inability to use the
      Work (including but not limited to damages for loss of goodwill,
      work stoppage, computer failure or malfunction, or any and all
      other commercial damages or losses), even if such Contributor
      has been advised of the possibility of such damages.

   9. Accepting Warranty or Additional Liability. While redistributing
      the Work or Derivative Works thereof, You may choose to offer,
      and charge a fee for, acceptance of support, warranty, indemnity,
      or other liability obligations and/or rights consistent with this
      License. However, in accepting such obligations, You may act only
      on Your own behalf and on Your sole responsibility, not on behalf
      of any other Contributor, and only if You agree to indemnify,
      defend, and hold each Contributor harmless for any liability
      incurred by, or claims asserted against, such Contributor by reason
      of your accepting any such warranty or additional liability.

   END OF TERMS AND CONDITIONS
Apache License

Version 2.0, January 2004

http://www.apache.org/licenses/

TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

1. Definitions.

"License" shall mean the terms and conditions for use, reproduction, and distribution as defined by Sections 1 through 9 of this document.

"Licensor" shall mean the copyright owner or entity authorized by the copyright owner that is granting the License.

"Legal Entity" shall mean the union of the acting entity and all other entities that control, are controlled by, or are under common control with that entity. For the purposes of this definition, "control" means (i) the power, direct or indirect, to cause the direction or management of such entity, whether by contract or otherwise, or (ii) ownership of fifty percent (50%) or more of the outstanding shares, or (iii) beneficial ownership of such entity.

"You" (or "Your") shall mean an individual or Legal Entity exercising permissions granted by this License.

"Source" form shall mean the preferred form for making modifications, including but not limited to software source code, documentation source, and configuration files.

"Object" form shall mean any form resulting from mechanical transformation or translation of a Source form, including but not limited to compiled object code, generated documentation, and conversions to other media types.

"Work" shall mean the work of authorship, whether in Source or Object form, made available under the License, as indicated by a copyright notice that is included in or attached to the work (an example is provided in the Appendix below).

"Derivative Works" shall mean any work, whether in Source or Object form, that is based on (or derived from) the Work and for which the editorial revisions, annotations, elaborations, or other modifications represent, as a whole, an original work of authorship. For the purposes of this License, Derivative Works shall not include works that remain separable from, or merely link (or bind by name) to the interfaces of, the Work and Derivative Works thereof.

"Contribution" shall mean any work of authorship, including the original version of the Work and any modifications or additions to that Work or Derivative Works thereof, that is intentionally submitted to Licensor for inclusion in the Work by the copyright owner or by an individual or Legal Entity authorized to submit on behalf of the copyright owner. For the purposes of this definition, "submitted" means any form of electronic, verbal, or written communication sent to the Licensor or its representatives, including but not limited to communication on electronic mailing lists, source code control systems, and issue tracking systems that are managed by, or on behalf of, the Licensor for the purpose of discussing and improving the Work, but excluding communication that is conspicuously marked or otherwise designated in writing by the copyright owner as "Not a Contribution."

"Contributor" shall mean Licensor and any individual or Legal Entity on behalf of whom a Contribution has been received by Licensor and subsequently incorporated within the Work.

2. Grant of Copyright License. Subject to the terms and conditions of this License, each Contributor hereby grants to You a perpetual, worldwide, non-exclusive, no-charge, royalty-free, irrevocable copyright license to reproduce, prepare Derivative Works of, publicly display, publicly perform, sublicense, and distribute the Work and such Derivative Works in Source or Object form.

3. Grant of Patent License. Subject to the terms and conditions of this License, each Contributor hereby grants to You a perpetual, worldwide, non-exclusive, no-charge, royalty-free, irrevocable (except as stated in this section) patent license to make, have made, use, offer to sell, sell, import, and otherwise transfer the Work, where such license applies only to those patent claims licensable by such Contributor that are necessarily infringed by their Contribution(s) alone or by combination of their Contribution(s) with the Work to which such Contribution(s) was submitted. If You institute patent litigation against any entity (including a cross-claim or counterclaim in a lawsuit) alleging that the Work or a Contribution incorporated within the Work constitutes direct or contributory patent infringement, then any patent licenses granted to You under this License for that Work shall terminate as of the date such litigation is filed.

4. Redistribution. You may reproduce and distribute copies of the Work or Derivative Works thereof in any medium, with or without modifications, and in Source or Object form, provided that You meet the following conditions:

    You must give any other recipients of the Work or Derivative Works a copy of this License; and

    You must cause any modified files to carry prominent notices stating that You changed the files; and

    You must retain, in the Source form of any Derivative Works that You distribute, all copyright, patent, trademark, and attribution notices from the Source form of the Work, excluding those notices that do not pertain to any part of the Derivative Works; and

    If the Work includes a "NOTICE" text file as part of its distribution, then any Derivative Works that You distribute must include a readable copy of the attribution notices contained within such NOTICE file, excluding those notices that do not pertain to any part of the Derivative Works, in at least one of the following places: within a NOTICE text file distributed as part of the Derivative Works; within the Source form or documentation, if provided along with the Derivative Works; or, within a display generated by the Derivative Works, if and wherever such third-party notices normally appear. The contents of the NOTICE file are for informational purposes only and do not modify the License. You may add Your own attribution notices within Derivative Works that You distribute, alongside or as an addendum to the NOTICE text from the Work, provided that such additional attribution notices cannot be construed as modifying the License. You may add Your own copyright statement to Your modifications and may provide additional or different license terms and conditions for use, reproduction, or distribution of Your modifications, or for any such Derivative Works as a whole, provided Your use, reproduction, and distribution of the Work otherwise complies with the conditions stated in this License.

5. Submission of Contributions. Unless You explicitly state otherwise, any Contribution intentionally submitted for inclusion in the Work by You to the Licensor shall be under the terms and conditions of this License, without any additional terms or conditions. Notwithstanding the above, nothing herein shall supersede or modify the terms of any separate license agreement you may have executed with Licensor regarding such Contributions.

6. Trademarks. This License does not grant permission to use the trade names, trademarks, service marks, or product names of the Licensor, except as required for reasonable and customary use in describing the origin of the Work and reproducing the content of the NOTICE file.

7. Disclaimer of Warranty. Unless required by applicable law or agreed to in writing, Licensor provides the Work (and each Contributor provides its Contributions) on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied, including, without limitation, any warranties or conditions of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A PARTICULAR PURPOSE. You are solely responsible for determining the appropriateness of using or redistributing the Work and assume any risks associated with Your exercise of permissions under this License.

8. Limitation of Liability. In no event and under no legal theory, whether in tort (including negligence), contract, or otherwise, unless required by applicable law (such as deliberate and grossly negligent acts) or agreed to in writing, shall any Contributor be liable to You for damages, including any direct, indirect, special, incidental, or consequential damages of any character arising as a result of this License or out of the use or inability to use the Work (including but not limited to damages for loss of goodwill, work stoppage, computer failure or malfunction, or any and all other commercial damages or losses), even if such Contributor has been advised of the possibility of such damages.

9. Accepting Warranty or Additional Liability. While redistributing the Work or Derivative Works thereof, You may choose to offer, and charge a fee for, acceptance of support, warranty, indemnity, or other liability obligations and/or rights consistent with this License. However, in accepting such obligations, You may act only on Your own behalf and on Your sole responsibility, not on behalf of any other Contributor, and only if You agree to indemnify, defend, and hold each Contributor harmless for any liability incurred by, or claims asserted against, such Contributor by reason of your accepting any such warranty or additional liability.

END OF TERMS AND CONDITIONSCopyright (c) 2004-2011 QOS.ch
All rights reserved.
 
Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
Apache License

Version 2.0, January 2004

http://www.apache.org/licenses/

TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

1. Definitions.

"License" shall mean the terms and conditions for use, reproduction, and distribution as defined by Sections 1 through 9 of this document.

"Licensor" shall mean the copyright owner or entity authorized by the copyright owner that is granting the License.

"Legal Entity" shall mean the union of the acting entity and all other entities that control, are controlled by, or are under common control with that entity. For the purposes of this definition, "control" means (i) the power, direct or indirect, to cause the direction or management of such entity, whether by contract or otherwise, or (ii) ownership of fifty percent (50%) or more of the outstanding shares, or (iii) beneficial ownership of such entity.

"You" (or "Your") shall mean an individual or Legal Entity exercising permissions granted by this License.

"Source" form shall mean the preferred form for making modifications, including but not limited to software source code, documentation source, and configuration files.

"Object" form shall mean any form resulting from mechanical transformation or translation of a Source form, including but not limited to compiled object code, generated documentation, and conversions to other media types.

"Work" shall mean the work of authorship, whether in Source or Object form, made available under the License, as indicated by a copyright notice that is included in or attached to the work (an example is provided in the Appendix below).

"Derivative Works" shall mean any work, whether in Source or Object form, that is based on (or derived from) the Work and for which the editorial revisions, annotations, elaborations, or other modifications represent, as a whole, an original work of authorship. For the purposes of this License, Derivative Works shall not include works that remain separable from, or merely link (or bind by name) to the interfaces of, the Work and Derivative Works thereof.

"Contribution" shall mean any work of authorship, including the original version of the Work and any modifications or additions to that Work or Derivative Works thereof, that is intentionally submitted to Licensor for inclusion in the Work by the copyright owner or by an individual or Legal Entity authorized to submit on behalf of the copyright owner. For the purposes of this definition, "submitted" means any form of electronic, verbal, or written communication sent to the Licensor or its representatives, including but not limited to communication on electronic mailing lists, source code control systems, and issue tracking systems that are managed by, or on behalf of, the Licensor for the purpose of discussing and improving the Work, but excluding communication that is conspicuously marked or otherwise designated in writing by the copyright owner as "Not a Contribution."

"Contributor" shall mean Licensor and any individual or Legal Entity on behalf of whom a Contribution has been received by Licensor and subsequently incorporated within the Work.

2. Grant of Copyright License. Subject to the terms and conditions of this License, each Contributor hereby grants to You a perpetual, worldwide, non-exclusive, no-charge, royalty-free, irrevocable copyright license to reproduce, prepare Derivative Works of, publicly display, publicly perform, sublicense, and distribute the Work and such Derivative Works in Source or Object form.

3. Grant of Patent License. Subject to the terms and conditions of this License, each Contributor hereby grants to You a perpetual, worldwide, non-exclusive, no-charge, royalty-free, irrevocable (except as stated in this section) patent license to make, have made, use, offer to sell, sell, import, and otherwise transfer the Work, where such license applies only to those patent claims licensable by such Contributor that are necessarily infringed by their Contribution(s) alone or by combination of their Contribution(s) with the Work to which such Contribution(s) was submitted. If You institute patent litigation against any entity (including a cross-claim or counterclaim in a lawsuit) alleging that the Work or a Contribution incorporated within the Work constitutes direct or contributory patent infringement, then any patent licenses granted to You under this License for that Work shall terminate as of the date such litigation is filed.

4. Redistribution. You may reproduce and distribute copies of the Work or Derivative Works thereof in any medium, with or without modifications, and in Source or Object form, provided that You meet the following conditions:

    You must give any other recipients of the Work or Derivative Works a copy of this License; and

    You must cause any modified files to carry prominent notices stating that You changed the files; and

    You must retain, in the Source form of any Derivative Works that You distribute, all copyright, patent, trademark, and attribution notices from the Source form of the Work, excluding those notices that do not pertain to any part of the Derivative Works; and

    If the Work includes a "NOTICE" text file as part of its distribution, then any Derivative Works that You distribute must include a readable copy of the attribution notices contained within such NOTICE file, excluding those notices that do not pertain to any part of the Derivative Works, in at least one of the following places: within a NOTICE text file distributed as part of the Derivative Works; within the Source form or documentation, if provided along with the Derivative Works; or, within a display generated by the Derivative Works, if and wherever such third-party notices normally appear. The contents of the NOTICE file are for informational purposes only and do not modify the License. You may add Your own attribution notices within Derivative Works that You distribute, alongside or as an addendum to the NOTICE text from the Work, provided that such additional attribution notices cannot be construed as modifying the License. You may add Your own copyright statement to Your modifications and may provide additional or different license terms and conditions for use, reproduction, or distribution of Your modifications, or for any such Derivative Works as a whole, provided Your use, reproduction, and distribution of the Work otherwise complies with the conditions stated in this License.

5. Submission of Contributions. Unless You explicitly state otherwise, any Contribution intentionally submitted for inclusion in the Work by You to the Licensor shall be under the terms and conditions of this License, without any additional terms or conditions. Notwithstanding the above, nothing herein shall supersede or modify the terms of any separate license agreement you may have executed with Licensor regarding such Contributions.

6. Trademarks. This License does not grant permission to use the trade names, trademarks, service marks, or product names of the Licensor, except as required for reasonable and customary use in describing the origin of the Work and reproducing the content of the NOTICE file.

7. Disclaimer of Warranty. Unless required by applicable law or agreed to in writing, Licensor provides the Work (and each Contributor provides its Contributions) on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied, including, without limitation, any warranties or conditions of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A PARTICULAR PURPOSE. You are solely responsible for determining the appropriateness of using or redistributing the Work and assume any risks associated with Your exercise of permissions under this License.

8. Limitation of Liability. In no event and under no legal theory, whether in tort (including negligence), contract, or otherwise, unless required by applicable law (such as deliberate and grossly negligent acts) or agreed to in writing, shall any Contributor be liable to You for damages, including any direct, indirect, special, incidental, or consequential damages of any character arising as a result of this License or out of the use or inability to use the Work (including but not limited to damages for loss of goodwill, work stoppage, computer failure or malfunction, or any and all other commercial damages or losses), even if such Contributor has been advised of the possibility of such damages.

9. Accepting Warranty or Additional Liability. While redistributing the Work or Derivative Works thereof, You may choose to offer, and charge a fee for, acceptance of support, warranty, indemnity, or other liability obligations and/or rights consistent with this License. However, in accepting such obligations, You may act only on Your own behalf and on Your sole responsibility, not on behalf of any other Contributor, and only if You agree to indemnify, defend, and hold each Contributor harmless for any liability incurred by, or claims asserted against, such Contributor by reason of your accepting any such warranty or additional liability.

END OF TERMS AND CONDITIONSCopyright (c) 2011, The University of Southampton and the individual contributors.
All rights reserved.

Redistribution and use in source and binary forms, with or without modification,
are permitted provided that the following conditions are met:

  * 	Redistributions of source code must retain the above copyright notice, 
	this list of conditions and the following disclaimer.

  *	Redistributions in binary form must reproduce the above copyright notice,
	this list of conditions and the following disclaimer in the documentation
	and/or other materials provided with the distribution.

  *	Neither the name of the University of Southampton nor the names of its
	contributors may be used to endorse or promote products derived from this
	software without specific prior written permission.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS" AND
ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED
WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE
DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR CONTRIBUTORS BE LIABLE FOR
ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON
ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
(INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
# webcam-capture-addon-spycam

Java/PHP set to setup spy camera.

Work in progress. STAY TUNED!

## License

Copyright (C) 2012 Bartosz Firyn

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

This directory will store pictures from spy camera.# FFmpeg CLI Capture Driver

This is a proof-of-concept, experimental capture driver. It uses FFmpeg to 
stream video from webcam device through process standard output.

This driver has been tested on:

* Fedora 26 (FFmpeg 3.1.11 and Oracle JDK 8),
* Ubuntu 14.04 (FFmpeg 3.3.3 and Oracle JDK 8) ,
* Raspbian GNU/Linux 9.3 (stretch) (FFmpeg 3.2.10 and OpenJDK 1.8.0_151),
* Windows 7 64bits (FFmpeg 3.4.1 and Oracle JDK 9).

It has some problems because
it starts own sub-process to stream data from `ffmpeg` and this process needs to be killed,
but in general works well.

## How To Use

Set new driver before you start using Webcam class:

```java
public class TakePictureExample {

	// set capture driver for ffmpeg tool
	static {
		Webcam.setDriver(new FFmpegCliDriver());
	}

	public static void main(String[] args) throws IOException {

		// get default webcam and open it
		Webcam webcam = Webcam.getDefault();
		webcam.open();

		// get image from webcam device
		BufferedImage image = webcam.getImage();

		// save image to PNG file
		ImageIO.write(image, "JPG", new File("test.jpg"));

		// close webcam
		webcam.close();
	}
}
```

## License

This particular driver code is released under Public Domain license.

---

I, the copyright holder of this work, hereby release it into the
public domain. This applies worldwide.

In case this is not legally possible, I grant any entity the right
to use this work for any purpose, without any conditions, unless 
such conditions are required by law.

# webcam-capture-driver-fswebcam

This capture driver is designed to allow developers to use console program called _fswebcam_ written by Philip Heron as the source of images for Webcam Capture API. This capture driver works on **only** on *nix and requires [fswebcam](https://github.com/fsphil/fswebcam) command line too to be installed on the environment where Webcam Capture API is used.

To install fswebcam:

```plain
$ sudo apt-get install fswebcam
```

## Download

The latest **development** version JAR (aka SNAPSHOT) can be downloaded [here](https://oss.sonatype.org/service/local/artifact/maven/redirect?r=snapshots&g=com.github.sarxos&a=webcam-capture-driver-fswebcam&v=0.3.13-SNAPSHOT).

The latest **stable** ZIP bundle can be downloaded [here](http://repo.sarxos.pl/maven2/com/github/sarxos/webcam-capture-driver-fswebcam/0.3.12/webcam-capture-driver-fswebcam-0.3.12-dist.zip).

## Maven

Stable:

```xml
<dependency>
	<groupId>com.github.sarxos</groupId>
	<artifactId>webcam-capture-driver-fswebcam</artifactId>
	<version>0.3.12</version>
</dependency>
```

Snapshot:

```xml
<repository>
    <id>Sonatype OSS Snapshot Repository</id>
    <url>http://oss.sonatype.org/content/repositories/snapshots</url>
</repository>
```
```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-fswebcam</artifactId>
    <version>0.3.13-SNAPSHOT</version>
</dependency>
```

## How To Use

Set capture driver before you start using Webcam class:

```java
public class TakePictureExample {

	// set capture driver for fswebcam tool
	static {
		Webcam.setDriver(new FsWebcamDriver());
	}

	public static void main(String[] args) throws IOException {

		// get default webcam and open it
		Webcam webcam = Webcam.getDefault();
		webcam.open();

		// get image from webcam device
		BufferedImage image = webcam.getImage();

		// save image to PNG file
		ImageIO.write(image, "JPG", new File("test.jpg"));

		// close webcam
		webcam.close();
	}
}
```

## Issues

There are several known issues. If you have an idea of how those can be fixed, please send the pull request with the code change and I will be happy to merge it into the master branch.

1. Single call to getImage() causes webcam to be re-open again,
2. Because of 1, webcam diode is blinking,
3. Because of 1, FPS is pretty slow (0.2 FPS on my Ubuntu laptop),
4. In some cases when the main Java process is killed, the fswebcam subprocess keeps running because no one is reading from the pipe.


## License

Copyright (C) 2012 - 2017 Bartosz Firyn

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
# webcam-capture-driver-gstreamer

This is capture driver which gives Webcam Capture API possibility to use
[GStreamer 0.10+](http://gstreamer.freedesktop.org/documentation/gstreamer010.html)
as a middleware accessing webcam devices (build-in or USB enabled).

**NOTE**: This capture driver is **only** for GStreamer 0.10+. With GStramer 1.0+ you have to use
[webcam-capture-driver-gst1](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-gst1)
instead!

It has been designed to work with Windows and Linux **only**. To make use of it user have to 
[download](http://code.google.com/p/ossbuild/) GStreamer application installer 
on Windows or use _apt-get_, _yum_ or other packages manager to install it on Linux.

Currently supported GStreamer version is 0.10.x, so make sure you are installing
the correct one! It is **not** compatible with GStreamer 1.0 and above!

## Supported Platforms

* Windows
* Linux

## Download

The latest **development** version JAR (aka SNAPSHOT) can be downloaded [here](https://oss.sonatype.org/service/local/artifact/maven/redirect?r=snapshots&g=com.github.sarxos&a=webcam-capture-driver-gstreamer&v=0.3.13-SNAPSHOT).

The latest **stable** version ZIP bundle can be downloaded [here](http://repo.sarxos.pl/maven2/com/github/sarxos/webcam-capture-driver-gstreamer/0.3.12/webcam-capture-driver-gstreamer-0.3.12-dist.zip).

## Maven

Stable:

```xml
<dependency>
	<groupId>com.github.sarxos</groupId>
	<artifactId>webcam-capture-driver-gstreamer</artifactId>
	<version>0.3.12</version>
</dependency>
```

Snapshot:

```xml
<repository>
    <id>Sonatype OSS Snapshot Repository</id>
    <url>http://oss.sonatype.org/content/repositories/snapshots</url>
</repository>
```
```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-gstreamer</artifactId>
    <version>0.3.13-SNAPSHOT</version>
</dependency>
```

## Example

```java
static {
	Webcam.setDriver(new GStreamerDriver());
}

public static void main(String[] args) {
	JFrame frame = new JFrame("GStreamer Webcam Capture Driver Demo");
	frame.add(new WebcamPanel(Webcam.getDefault()));
	frame.pack();
	frame.setVisible(true);
	frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
}
```

## License

Copyright (C) 2012 - 2017 Bartosz Firyn

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

AppleJavaExtensions

 

This is a pluggable jar of stub classes representing the new Apple eAWT and eIO APIs for Java on Mac OS X.  The purpose of these stubs is to allow for compilation of eAWT- or eIO-referencing code on platforms other than Mac OS X.  The jar file is enclosed in a zip archive for easy expansion on other platforms.  

 

These stubs are not intended for the runtime classpath on non-Mac platforms.  Please see the OSXAdapter sample for how to write cross-platform code that uses eAWT.

 

Disclaimer: IMPORTANT:  This Apple software is supplied to you by Apple

Computer, Inc. ("Apple") in consideration of your agreement to the

following terms, and your use, installation, modification or

redistribution of this Apple software constitutes acceptance of these

terms.  If you do not agree with these terms, please do not use,

install, modify or redistribute this Apple software.

 

In consideration of your agreement to abide by the following terms, and

subject to these terms, Apple grants you a personal, non-exclusive

license, under Apple's copyrights in this original Apple software (the

"Apple Software"), to use, reproduce, modify and redistribute the Apple

Software, with or without modifications, in source and/or binary forms;

provided that if you redistribute the Apple Software in its entirety and

without modifications, you must retain this notice and the following

text and disclaimers in all such redistributions of the Apple Software. 

Neither the name, trademarks, service marks or logos of Apple Computer,

Inc. may be used to endorse or promote products derived from the Apple

Software without specific prior written permission from Apple.  Except

as expressly stated in this notice, no other rights or licenses, express

or implied, are granted by Apple herein, including but not limited to

any patent rights that may be infringed by your derivative works or by

other works in which the Apple Software may be incorporated.

 

The Apple Software is provided by Apple on an "AS IS" basis.  APPLE

MAKES NO WARRANTIES, EXPRESS OR IMPLIED, INCLUDING WITHOUT LIMITATION

THE IMPLIED WARRANTIES OF NON-INFRINGEMENT, MERCHANTABILITY AND FITNESS

FOR A PARTICULAR PURPOSE, REGARDING THE APPLE SOFTWARE OR ITS USE AND

OPERATION ALONE OR IN COMBINATION WITH YOUR PRODUCTS.

 

IN NO EVENT SHALL APPLE BE LIABLE FOR ANY SPECIAL, INDIRECT, INCIDENTAL

OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF

SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS

INTERRUPTION) ARISING IN ANY WAY OUT OF THE USE, REPRODUCTION,

MODIFICATION AND/OR DISTRIBUTION OF THE APPLE SOFTWARE, HOWEVER CAUSED

AND WHETHER UNDER THEORY OF CONTRACT, TORT (INCLUDING NEGLIGENCE),

STRICT LIABILITY OR OTHERWISE, EVEN IF APPLE HAS BEEN ADVISED OF THE

POSSIBILITY OF SUCH DAMAGE.

 

Copyright © 2003-2010 Apple Inc., All Rights Reserved		  GNU LESSER GENERAL PUBLIC LICENSE
		       Version 2.1, February 1999

 Copyright (C) 1991, 1999 Free Software Foundation, Inc.
 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301  USA
 Everyone is permitted to copy and distribute verbatim copies
 of this license document, but changing it is not allowed.

[This is the first released version of the Lesser GPL.  It also counts
 as the successor of the GNU Library Public License, version 2, hence
 the version number 2.1.]

			    Preamble

  The licenses for most software are designed to take away your
freedom to share and change it.  By contrast, the GNU General Public
Licenses are intended to guarantee your freedom to share and change
free software--to make sure the software is free for all its users.

  This license, the Lesser General Public License, applies to some
specially designated software packages--typically libraries--of the
Free Software Foundation and other authors who decide to use it.  You
can use it too, but we suggest you first think carefully about whether
this license or the ordinary General Public License is the better
strategy to use in any particular case, based on the explanations below.

  When we speak of free software, we are referring to freedom of use,
not price.  Our General Public Licenses are designed to make sure that
you have the freedom to distribute copies of free software (and charge
for this service if you wish); that you receive source code or can get
it if you want it; that you can change the software and use pieces of
it in new free programs; and that you are informed that you can do
these things.

  To protect your rights, we need to make restrictions that forbid
distributors to deny you these rights or to ask you to surrender these
rights.  These restrictions translate to certain responsibilities for
you if you distribute copies of the library or if you modify it.

  For example, if you distribute copies of the library, whether gratis
or for a fee, you must give the recipients all the rights that we gave
you.  You must make sure that they, too, receive or can get the source
code.  If you link other code with the library, you must provide
complete object files to the recipients, so that they can relink them
with the library after making changes to the library and recompiling
it.  And you must show them these terms so they know their rights.

  We protect your rights with a two-step method: (1) we copyright the
library, and (2) we offer you this license, which gives you legal
permission to copy, distribute and/or modify the library.

  To protect each distributor, we want to make it very clear that
there is no warranty for the free library.  Also, if the library is
modified by someone else and passed on, the recipients should know
that what they have is not the original version, so that the original
author's reputation will not be affected by problems that might be
introduced by others.

  Finally, software patents pose a constant threat to the existence of
any free program.  We wish to make sure that a company cannot
effectively restrict the users of a free program by obtaining a
restrictive license from a patent holder.  Therefore, we insist that
any patent license obtained for a version of the library must be
consistent with the full freedom of use specified in this license.

  Most GNU software, including some libraries, is covered by the
ordinary GNU General Public License.  This license, the GNU Lesser
General Public License, applies to certain designated libraries, and
is quite different from the ordinary General Public License.  We use
this license for certain libraries in order to permit linking those
libraries into non-free programs.

  When a program is linked with a library, whether statically or using
a shared library, the combination of the two is legally speaking a
combined work, a derivative of the original library.  The ordinary
General Public License therefore permits such linking only if the
entire combination fits its criteria of freedom.  The Lesser General
Public License permits more lax criteria for linking other code with
the library.

  We call this license the "Lesser" General Public License because it
does Less to protect the user's freedom than the ordinary General
Public License.  It also provides other free software developers Less
of an advantage over competing non-free programs.  These disadvantages
are the reason we use the ordinary General Public License for many
libraries.  However, the Lesser license provides advantages in certain
special circumstances.

  For example, on rare occasions, there may be a special need to
encourage the widest possible use of a certain library, so that it becomes
a de-facto standard.  To achieve this, non-free programs must be
allowed to use the library.  A more frequent case is that a free
library does the same job as widely used non-free libraries.  In this
case, there is little to gain by limiting the free library to free
software only, so we use the Lesser General Public License.

  In other cases, permission to use a particular library in non-free
programs enables a greater number of people to use a large body of
free software.  For example, permission to use the GNU C Library in
non-free programs enables many more people to use the whole GNU
operating system, as well as its variant, the GNU/Linux operating
system.

  Although the Lesser General Public License is Less protective of the
users' freedom, it does ensure that the user of a program that is
linked with the Library has the freedom and the wherewithal to run
that program using a modified version of the Library.

  The precise terms and conditions for copying, distribution and
modification follow.  Pay close attention to the difference between a
"work based on the library" and a "work that uses the library".  The
former contains code derived from the library, whereas the latter must
be combined with the library in order to run.

		  GNU LESSER GENERAL PUBLIC LICENSE
   TERMS AND CONDITIONS FOR COPYING, DISTRIBUTION AND MODIFICATION

  0. This License Agreement applies to any software library or other
program which contains a notice placed by the copyright holder or
other authorized party saying it may be distributed under the terms of
this Lesser General Public License (also called "this License").
Each licensee is addressed as "you".

  A "library" means a collection of software functions and/or data
prepared so as to be conveniently linked with application programs
(which use some of those functions and data) to form executables.

  The "Library", below, refers to any such software library or work
which has been distributed under these terms.  A "work based on the
Library" means either the Library or any derivative work under
copyright law: that is to say, a work containing the Library or a
portion of it, either verbatim or with modifications and/or translated
straightforwardly into another language.  (Hereinafter, translation is
included without limitation in the term "modification".)

  "Source code" for a work means the preferred form of the work for
making modifications to it.  For a library, complete source code means
all the source code for all modules it contains, plus any associated
interface definition files, plus the scripts used to control compilation
and installation of the library.

  Activities other than copying, distribution and modification are not
covered by this License; they are outside its scope.  The act of
running a program using the Library is not restricted, and output from
such a program is covered only if its contents constitute a work based
on the Library (independent of the use of the Library in a tool for
writing it).  Whether that is true depends on what the Library does
and what the program that uses the Library does.
  
  1. You may copy and distribute verbatim copies of the Library's
complete source code as you receive it, in any medium, provided that
you conspicuously and appropriately publish on each copy an
appropriate copyright notice and disclaimer of warranty; keep intact
all the notices that refer to this License and to the absence of any
warranty; and distribute a copy of this License along with the
Library.

  You may charge a fee for the physical act of transferring a copy,
and you may at your option offer warranty protection in exchange for a
fee.

  2. You may modify your copy or copies of the Library or any portion
of it, thus forming a work based on the Library, and copy and
distribute such modifications or work under the terms of Section 1
above, provided that you also meet all of these conditions:

    a) The modified work must itself be a software library.

    b) You must cause the files modified to carry prominent notices
    stating that you changed the files and the date of any change.

    c) You must cause the whole of the work to be licensed at no
    charge to all third parties under the terms of this License.

    d) If a facility in the modified Library refers to a function or a
    table of data to be supplied by an application program that uses
    the facility, other than as an argument passed when the facility
    is invoked, then you must make a good faith effort to ensure that,
    in the event an application does not supply such function or
    table, the facility still operates, and performs whatever part of
    its purpose remains meaningful.

    (For example, a function in a library to compute square roots has
    a purpose that is entirely well-defined independent of the
    application.  Therefore, Subsection 2d requires that any
    application-supplied function or table used by this function must
    be optional: if the application does not supply it, the square
    root function must still compute square roots.)

These requirements apply to the modified work as a whole.  If
identifiable sections of that work are not derived from the Library,
and can be reasonably considered independent and separate works in
themselves, then this License, and its terms, do not apply to those
sections when you distribute them as separate works.  But when you
distribute the same sections as part of a whole which is a work based
on the Library, the distribution of the whole must be on the terms of
this License, whose permissions for other licensees extend to the
entire whole, and thus to each and every part regardless of who wrote
it.

Thus, it is not the intent of this section to claim rights or contest
your rights to work written entirely by you; rather, the intent is to
exercise the right to control the distribution of derivative or
collective works based on the Library.

In addition, mere aggregation of another work not based on the Library
with the Library (or with a work based on the Library) on a volume of
a storage or distribution medium does not bring the other work under
the scope of this License.

  3. You may opt to apply the terms of the ordinary GNU General Public
License instead of this License to a given copy of the Library.  To do
this, you must alter all the notices that refer to this License, so
that they refer to the ordinary GNU General Public License, version 2,
instead of to this License.  (If a newer version than version 2 of the
ordinary GNU General Public License has appeared, then you can specify
that version instead if you wish.)  Do not make any other change in
these notices.

  Once this change is made in a given copy, it is irreversible for
that copy, so the ordinary GNU General Public License applies to all
subsequent copies and derivative works made from that copy.

  This option is useful when you wish to copy part of the code of
the Library into a program that is not a library.

  4. You may copy and distribute the Library (or a portion or
derivative of it, under Section 2) in object code or executable form
under the terms of Sections 1 and 2 above provided that you accompany
it with the complete corresponding machine-readable source code, which
must be distributed under the terms of Sections 1 and 2 above on a
medium customarily used for software interchange.

  If distribution of object code is made by offering access to copy
from a designated place, then offering equivalent access to copy the
source code from the same place satisfies the requirement to
distribute the source code, even though third parties are not
compelled to copy the source along with the object code.

  5. A program that contains no derivative of any portion of the
Library, but is designed to work with the Library by being compiled or
linked with it, is called a "work that uses the Library".  Such a
work, in isolation, is not a derivative work of the Library, and
therefore falls outside the scope of this License.

  However, linking a "work that uses the Library" with the Library
creates an executable that is a derivative of the Library (because it
contains portions of the Library), rather than a "work that uses the
library".  The executable is therefore covered by this License.
Section 6 states terms for distribution of such executables.

  When a "work that uses the Library" uses material from a header file
that is part of the Library, the object code for the work may be a
derivative work of the Library even though the source code is not.
Whether this is true is especially significant if the work can be
linked without the Library, or if the work is itself a library.  The
threshold for this to be true is not precisely defined by law.

  If such an object file uses only numerical parameters, data
structure layouts and accessors, and small macros and small inline
functions (ten lines or less in length), then the use of the object
file is unrestricted, regardless of whether it is legally a derivative
work.  (Executables containing this object code plus portions of the
Library will still fall under Section 6.)

  Otherwise, if the work is a derivative of the Library, you may
distribute the object code for the work under the terms of Section 6.
Any executables containing that work also fall under Section 6,
whether or not they are linked directly with the Library itself.

  6. As an exception to the Sections above, you may also combine or
link a "work that uses the Library" with the Library to produce a
work containing portions of the Library, and distribute that work
under terms of your choice, provided that the terms permit
modification of the work for the customer's own use and reverse
engineering for debugging such modifications.

  You must give prominent notice with each copy of the work that the
Library is used in it and that the Library and its use are covered by
this License.  You must supply a copy of this License.  If the work
during execution displays copyright notices, you must include the
copyright notice for the Library among them, as well as a reference
directing the user to the copy of this License.  Also, you must do one
of these things:

    a) Accompany the work with the complete corresponding
    machine-readable source code for the Library including whatever
    changes were used in the work (which must be distributed under
    Sections 1 and 2 above); and, if the work is an executable linked
    with the Library, with the complete machine-readable "work that
    uses the Library", as object code and/or source code, so that the
    user can modify the Library and then relink to produce a modified
    executable containing the modified Library.  (It is understood
    that the user who changes the contents of definitions files in the
    Library will not necessarily be able to recompile the application
    to use the modified definitions.)

    b) Use a suitable shared library mechanism for linking with the
    Library.  A suitable mechanism is one that (1) uses at run time a
    copy of the library already present on the user's computer system,
    rather than copying library functions into the executable, and (2)
    will operate properly with a modified version of the library, if
    the user installs one, as long as the modified version is
    interface-compatible with the version that the work was made with.

    c) Accompany the work with a written offer, valid for at
    least three years, to give the same user the materials
    specified in Subsection 6a, above, for a charge no more
    than the cost of performing this distribution.

    d) If distribution of the work is made by offering access to copy
    from a designated place, offer equivalent access to copy the above
    specified materials from the same place.

    e) Verify that the user has already received a copy of these
    materials or that you have already sent this user a copy.

  For an executable, the required form of the "work that uses the
Library" must include any data and utility programs needed for
reproducing the executable from it.  However, as a special exception,
the materials to be distributed need not include anything that is
normally distributed (in either source or binary form) with the major
components (compiler, kernel, and so on) of the operating system on
which the executable runs, unless that component itself accompanies
the executable.

  It may happen that this requirement contradicts the license
restrictions of other proprietary libraries that do not normally
accompany the operating system.  Such a contradiction means you cannot
use both them and the Library together in an executable that you
distribute.

  7. You may place library facilities that are a work based on the
Library side-by-side in a single library together with other library
facilities not covered by this License, and distribute such a combined
library, provided that the separate distribution of the work based on
the Library and of the other library facilities is otherwise
permitted, and provided that you do these two things:

    a) Accompany the combined library with a copy of the same work
    based on the Library, uncombined with any other library
    facilities.  This must be distributed under the terms of the
    Sections above.

    b) Give prominent notice with the combined library of the fact
    that part of it is a work based on the Library, and explaining
    where to find the accompanying uncombined form of the same work.

  8. You may not copy, modify, sublicense, link with, or distribute
the Library except as expressly provided under this License.  Any
attempt otherwise to copy, modify, sublicense, link with, or
distribute the Library is void, and will automatically terminate your
rights under this License.  However, parties who have received copies,
or rights, from you under this License will not have their licenses
terminated so long as such parties remain in full compliance.

  9. You are not required to accept this License, since you have not
signed it.  However, nothing else grants you permission to modify or
distribute the Library or its derivative works.  These actions are
prohibited by law if you do not accept this License.  Therefore, by
modifying or distributing the Library (or any work based on the
Library), you indicate your acceptance of this License to do so, and
all its terms and conditions for copying, distributing or modifying
the Library or works based on it.

  10. Each time you redistribute the Library (or any work based on the
Library), the recipient automatically receives a license from the
original licensor to copy, distribute, link with or modify the Library
subject to these terms and conditions.  You may not impose any further
restrictions on the recipients' exercise of the rights granted herein.
You are not responsible for enforcing compliance by third parties with
this License.

  11. If, as a consequence of a court judgment or allegation of patent
infringement or for any other reason (not limited to patent issues),
conditions are imposed on you (whether by court order, agreement or
otherwise) that contradict the conditions of this License, they do not
excuse you from the conditions of this License.  If you cannot
distribute so as to satisfy simultaneously your obligations under this
License and any other pertinent obligations, then as a consequence you
may not distribute the Library at all.  For example, if a patent
license would not permit royalty-free redistribution of the Library by
all those who receive copies directly or indirectly through you, then
the only way you could satisfy both it and this License would be to
refrain entirely from distribution of the Library.

If any portion of this section is held invalid or unenforceable under any
particular circumstance, the balance of the section is intended to apply,
and the section as a whole is intended to apply in other circumstances.

It is not the purpose of this section to induce you to infringe any
patents or other property right claims or to contest validity of any
such claims; this section has the sole purpose of protecting the
integrity of the free software distribution system which is
implemented by public license practices.  Many people have made
generous contributions to the wide range of software distributed
through that system in reliance on consistent application of that
system; it is up to the author/donor to decide if he or she is willing
to distribute software through any other system and a licensee cannot
impose that choice.

This section is intended to make thoroughly clear what is believed to
be a consequence of the rest of this License.

  12. If the distribution and/or use of the Library is restricted in
certain countries either by patents or by copyrighted interfaces, the
original copyright holder who places the Library under this License may add
an explicit geographical distribution limitation excluding those countries,
so that distribution is permitted only in or among countries not thus
excluded.  In such case, this License incorporates the limitation as if
written in the body of this License.

  13. The Free Software Foundation may publish revised and/or new
versions of the Lesser General Public License from time to time.
Such new versions will be similar in spirit to the present version,
but may differ in detail to address new problems or concerns.

Each version is given a distinguishing version number.  If the Library
specifies a version number of this License which applies to it and
"any later version", you have the option of following the terms and
conditions either of that version or of any later version published by
the Free Software Foundation.  If the Library does not specify a
license version number, you may choose any version ever published by
the Free Software Foundation.

  14. If you wish to incorporate parts of the Library into other free
programs whose distribution conditions are incompatible with these,
write to the author to ask for permission.  For software which is
copyrighted by the Free Software Foundation, write to the Free
Software Foundation; we sometimes make exceptions for this.  Our
decision will be guided by the two goals of preserving the free status
of all derivatives of our free software and of promoting the sharing
and reuse of software generally.

			    NO WARRANTY

  15. BECAUSE THE LIBRARY IS LICENSED FREE OF CHARGE, THERE IS NO
WARRANTY FOR THE LIBRARY, TO THE EXTENT PERMITTED BY APPLICABLE LAW.
EXCEPT WHEN OTHERWISE STATED IN WRITING THE COPYRIGHT HOLDERS AND/OR
OTHER PARTIES PROVIDE THE LIBRARY "AS IS" WITHOUT WARRANTY OF ANY
KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
PURPOSE.  THE ENTIRE RISK AS TO THE QUALITY AND PERFORMANCE OF THE
LIBRARY IS WITH YOU.  SHOULD THE LIBRARY PROVE DEFECTIVE, YOU ASSUME
THE COST OF ALL NECESSARY SERVICING, REPAIR OR CORRECTION.

  16. IN NO EVENT UNLESS REQUIRED BY APPLICABLE LAW OR AGREED TO IN
WRITING WILL ANY COPYRIGHT HOLDER, OR ANY OTHER PARTY WHO MAY MODIFY
AND/OR REDISTRIBUTE THE LIBRARY AS PERMITTED ABOVE, BE LIABLE TO YOU
FOR DAMAGES, INCLUDING ANY GENERAL, SPECIAL, INCIDENTAL OR
CONSEQUENTIAL DAMAGES ARISING OUT OF THE USE OR INABILITY TO USE THE
LIBRARY (INCLUDING BUT NOT LIMITED TO LOSS OF DATA OR DATA BEING
RENDERED INACCURATE OR LOSSES SUSTAINED BY YOU OR THIRD PARTIES OR A
FAILURE OF THE LIBRARY TO OPERATE WITH ANY OTHER SOFTWARE), EVEN IF
SUCH HOLDER OR OTHER PARTY HAS BEEN ADVISED OF THE POSSIBILITY OF SUCH
DAMAGES.

		     END OF TERMS AND CONDITIONS

           How to Apply These Terms to Your New Libraries

  If you develop a new library, and you want it to be of the greatest
possible use to the public, we recommend making it free software that
everyone can redistribute and change.  You can do so by permitting
redistribution under these terms (or, alternatively, under the terms of the
ordinary General Public License).

  To apply these terms, attach the following notices to the library.  It is
safest to attach them to the start of each source file to most effectively
convey the exclusion of warranty; and each file should have at least the
"copyright" line and a pointer to where the full notice is found.

    <one line to give the library's name and a brief idea of what it does.>
    Copyright (C) <year>  <name of author>

    This library is free software; you can redistribute it and/or
    modify it under the terms of the GNU Lesser General Public
    License as published by the Free Software Foundation; either
    version 2.1 of the License, or (at your option) any later version.

    This library is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
    Lesser General Public License for more details.

    You should have received a copy of the GNU Lesser General Public
    License along with this library; if not, write to the Free Software
    Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301  USA

Also add information on how to contact you by electronic and paper mail.

You should also get your employer (if you work as a programmer) or your
school, if any, to sign a "copyright disclaimer" for the library, if
necessary.  Here is a sample; alter the names:

  Yoyodyne, Inc., hereby disclaims all copyright interest in the
  library `Frob' (a library for tweaking knobs) written by James Random Hacker.

  <signature of Ty Coon>, 1 April 1990
  Ty Coon, President of Vice

That's all there is to it!


		  GNU LESSER GENERAL PUBLIC LICENSE
		       Version 2.1, February 1999

 Copyright (C) 1991, 1999 Free Software Foundation, Inc.
 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301  USA
 Everyone is permitted to copy and distribute verbatim copies
 of this license document, but changing it is not allowed.

[This is the first released version of the Lesser GPL.  It also counts
 as the successor of the GNU Library Public License, version 2, hence
 the version number 2.1.]

			    Preamble

  The licenses for most software are designed to take away your
freedom to share and change it.  By contrast, the GNU General Public
Licenses are intended to guarantee your freedom to share and change
free software--to make sure the software is free for all its users.

  This license, the Lesser General Public License, applies to some
specially designated software packages--typically libraries--of the
Free Software Foundation and other authors who decide to use it.  You
can use it too, but we suggest you first think carefully about whether
this license or the ordinary General Public License is the better
strategy to use in any particular case, based on the explanations below.

  When we speak of free software, we are referring to freedom of use,
not price.  Our General Public Licenses are designed to make sure that
you have the freedom to distribute copies of free software (and charge
for this service if you wish); that you receive source code or can get
it if you want it; that you can change the software and use pieces of
it in new free programs; and that you are informed that you can do
these things.

  To protect your rights, we need to make restrictions that forbid
distributors to deny you these rights or to ask you to surrender these
rights.  These restrictions translate to certain responsibilities for
you if you distribute copies of the library or if you modify it.

  For example, if you distribute copies of the library, whether gratis
or for a fee, you must give the recipients all the rights that we gave
you.  You must make sure that they, too, receive or can get the source
code.  If you link other code with the library, you must provide
complete object files to the recipients, so that they can relink them
with the library after making changes to the library and recompiling
it.  And you must show them these terms so they know their rights.

  We protect your rights with a two-step method: (1) we copyright the
library, and (2) we offer you this license, which gives you legal
permission to copy, distribute and/or modify the library.

  To protect each distributor, we want to make it very clear that
there is no warranty for the free library.  Also, if the library is
modified by someone else and passed on, the recipients should know
that what they have is not the original version, so that the original
author's reputation will not be affected by problems that might be
introduced by others.

  Finally, software patents pose a constant threat to the existence of
any free program.  We wish to make sure that a company cannot
effectively restrict the users of a free program by obtaining a
restrictive license from a patent holder.  Therefore, we insist that
any patent license obtained for a version of the library must be
consistent with the full freedom of use specified in this license.

  Most GNU software, including some libraries, is covered by the
ordinary GNU General Public License.  This license, the GNU Lesser
General Public License, applies to certain designated libraries, and
is quite different from the ordinary General Public License.  We use
this license for certain libraries in order to permit linking those
libraries into non-free programs.

  When a program is linked with a library, whether statically or using
a shared library, the combination of the two is legally speaking a
combined work, a derivative of the original library.  The ordinary
General Public License therefore permits such linking only if the
entire combination fits its criteria of freedom.  The Lesser General
Public License permits more lax criteria for linking other code with
the library.

  We call this license the "Lesser" General Public License because it
does Less to protect the user's freedom than the ordinary General
Public License.  It also provides other free software developers Less
of an advantage over competing non-free programs.  These disadvantages
are the reason we use the ordinary General Public License for many
libraries.  However, the Lesser license provides advantages in certain
special circumstances.

  For example, on rare occasions, there may be a special need to
encourage the widest possible use of a certain library, so that it becomes
a de-facto standard.  To achieve this, non-free programs must be
allowed to use the library.  A more frequent case is that a free
library does the same job as widely used non-free libraries.  In this
case, there is little to gain by limiting the free library to free
software only, so we use the Lesser General Public License.

  In other cases, permission to use a particular library in non-free
programs enables a greater number of people to use a large body of
free software.  For example, permission to use the GNU C Library in
non-free programs enables many more people to use the whole GNU
operating system, as well as its variant, the GNU/Linux operating
system.

  Although the Lesser General Public License is Less protective of the
users' freedom, it does ensure that the user of a program that is
linked with the Library has the freedom and the wherewithal to run
that program using a modified version of the Library.

  The precise terms and conditions for copying, distribution and
modification follow.  Pay close attention to the difference between a
"work based on the library" and a "work that uses the library".  The
former contains code derived from the library, whereas the latter must
be combined with the library in order to run.

		  GNU LESSER GENERAL PUBLIC LICENSE
   TERMS AND CONDITIONS FOR COPYING, DISTRIBUTION AND MODIFICATION

  0. This License Agreement applies to any software library or other
program which contains a notice placed by the copyright holder or
other authorized party saying it may be distributed under the terms of
this Lesser General Public License (also called "this License").
Each licensee is addressed as "you".

  A "library" means a collection of software functions and/or data
prepared so as to be conveniently linked with application programs
(which use some of those functions and data) to form executables.

  The "Library", below, refers to any such software library or work
which has been distributed under these terms.  A "work based on the
Library" means either the Library or any derivative work under
copyright law: that is to say, a work containing the Library or a
portion of it, either verbatim or with modifications and/or translated
straightforwardly into another language.  (Hereinafter, translation is
included without limitation in the term "modification".)

  "Source code" for a work means the preferred form of the work for
making modifications to it.  For a library, complete source code means
all the source code for all modules it contains, plus any associated
interface definition files, plus the scripts used to control compilation
and installation of the library.

  Activities other than copying, distribution and modification are not
covered by this License; they are outside its scope.  The act of
running a program using the Library is not restricted, and output from
such a program is covered only if its contents constitute a work based
on the Library (independent of the use of the Library in a tool for
writing it).  Whether that is true depends on what the Library does
and what the program that uses the Library does.
  
  1. You may copy and distribute verbatim copies of the Library's
complete source code as you receive it, in any medium, provided that
you conspicuously and appropriately publish on each copy an
appropriate copyright notice and disclaimer of warranty; keep intact
all the notices that refer to this License and to the absence of any
warranty; and distribute a copy of this License along with the
Library.

  You may charge a fee for the physical act of transferring a copy,
and you may at your option offer warranty protection in exchange for a
fee.

  2. You may modify your copy or copies of the Library or any portion
of it, thus forming a work based on the Library, and copy and
distribute such modifications or work under the terms of Section 1
above, provided that you also meet all of these conditions:

    a) The modified work must itself be a software library.

    b) You must cause the files modified to carry prominent notices
    stating that you changed the files and the date of any change.

    c) You must cause the whole of the work to be licensed at no
    charge to all third parties under the terms of this License.

    d) If a facility in the modified Library refers to a function or a
    table of data to be supplied by an application program that uses
    the facility, other than as an argument passed when the facility
    is invoked, then you must make a good faith effort to ensure that,
    in the event an application does not supply such function or
    table, the facility still operates, and performs whatever part of
    its purpose remains meaningful.

    (For example, a function in a library to compute square roots has
    a purpose that is entirely well-defined independent of the
    application.  Therefore, Subsection 2d requires that any
    application-supplied function or table used by this function must
    be optional: if the application does not supply it, the square
    root function must still compute square roots.)

These requirements apply to the modified work as a whole.  If
identifiable sections of that work are not derived from the Library,
and can be reasonably considered independent and separate works in
themselves, then this License, and its terms, do not apply to those
sections when you distribute them as separate works.  But when you
distribute the same sections as part of a whole which is a work based
on the Library, the distribution of the whole must be on the terms of
this License, whose permissions for other licensees extend to the
entire whole, and thus to each and every part regardless of who wrote
it.

Thus, it is not the intent of this section to claim rights or contest
your rights to work written entirely by you; rather, the intent is to
exercise the right to control the distribution of derivative or
collective works based on the Library.

In addition, mere aggregation of another work not based on the Library
with the Library (or with a work based on the Library) on a volume of
a storage or distribution medium does not bring the other work under
the scope of this License.

  3. You may opt to apply the terms of the ordinary GNU General Public
License instead of this License to a given copy of the Library.  To do
this, you must alter all the notices that refer to this License, so
that they refer to the ordinary GNU General Public License, version 2,
instead of to this License.  (If a newer version than version 2 of the
ordinary GNU General Public License has appeared, then you can specify
that version instead if you wish.)  Do not make any other change in
these notices.

  Once this change is made in a given copy, it is irreversible for
that copy, so the ordinary GNU General Public License applies to all
subsequent copies and derivative works made from that copy.

  This option is useful when you wish to copy part of the code of
the Library into a program that is not a library.

  4. You may copy and distribute the Library (or a portion or
derivative of it, under Section 2) in object code or executable form
under the terms of Sections 1 and 2 above provided that you accompany
it with the complete corresponding machine-readable source code, which
must be distributed under the terms of Sections 1 and 2 above on a
medium customarily used for software interchange.

  If distribution of object code is made by offering access to copy
from a designated place, then offering equivalent access to copy the
source code from the same place satisfies the requirement to
distribute the source code, even though third parties are not
compelled to copy the source along with the object code.

  5. A program that contains no derivative of any portion of the
Library, but is designed to work with the Library by being compiled or
linked with it, is called a "work that uses the Library".  Such a
work, in isolation, is not a derivative work of the Library, and
therefore falls outside the scope of this License.

  However, linking a "work that uses the Library" with the Library
creates an executable that is a derivative of the Library (because it
contains portions of the Library), rather than a "work that uses the
library".  The executable is therefore covered by this License.
Section 6 states terms for distribution of such executables.

  When a "work that uses the Library" uses material from a header file
that is part of the Library, the object code for the work may be a
derivative work of the Library even though the source code is not.
Whether this is true is especially significant if the work can be
linked without the Library, or if the work is itself a library.  The
threshold for this to be true is not precisely defined by law.

  If such an object file uses only numerical parameters, data
structure layouts and accessors, and small macros and small inline
functions (ten lines or less in length), then the use of the object
file is unrestricted, regardless of whether it is legally a derivative
work.  (Executables containing this object code plus portions of the
Library will still fall under Section 6.)

  Otherwise, if the work is a derivative of the Library, you may
distribute the object code for the work under the terms of Section 6.
Any executables containing that work also fall under Section 6,
whether or not they are linked directly with the Library itself.

  6. As an exception to the Sections above, you may also combine or
link a "work that uses the Library" with the Library to produce a
work containing portions of the Library, and distribute that work
under terms of your choice, provided that the terms permit
modification of the work for the customer's own use and reverse
engineering for debugging such modifications.

  You must give prominent notice with each copy of the work that the
Library is used in it and that the Library and its use are covered by
this License.  You must supply a copy of this License.  If the work
during execution displays copyright notices, you must include the
copyright notice for the Library among them, as well as a reference
directing the user to the copy of this License.  Also, you must do one
of these things:

    a) Accompany the work with the complete corresponding
    machine-readable source code for the Library including whatever
    changes were used in the work (which must be distributed under
    Sections 1 and 2 above); and, if the work is an executable linked
    with the Library, with the complete machine-readable "work that
    uses the Library", as object code and/or source code, so that the
    user can modify the Library and then relink to produce a modified
    executable containing the modified Library.  (It is understood
    that the user who changes the contents of definitions files in the
    Library will not necessarily be able to recompile the application
    to use the modified definitions.)

    b) Use a suitable shared library mechanism for linking with the
    Library.  A suitable mechanism is one that (1) uses at run time a
    copy of the library already present on the user's computer system,
    rather than copying library functions into the executable, and (2)
    will operate properly with a modified version of the library, if
    the user installs one, as long as the modified version is
    interface-compatible with the version that the work was made with.

    c) Accompany the work with a written offer, valid for at
    least three years, to give the same user the materials
    specified in Subsection 6a, above, for a charge no more
    than the cost of performing this distribution.

    d) If distribution of the work is made by offering access to copy
    from a designated place, offer equivalent access to copy the above
    specified materials from the same place.

    e) Verify that the user has already received a copy of these
    materials or that you have already sent this user a copy.

  For an executable, the required form of the "work that uses the
Library" must include any data and utility programs needed for
reproducing the executable from it.  However, as a special exception,
the materials to be distributed need not include anything that is
normally distributed (in either source or binary form) with the major
components (compiler, kernel, and so on) of the operating system on
which the executable runs, unless that component itself accompanies
the executable.

  It may happen that this requirement contradicts the license
restrictions of other proprietary libraries that do not normally
accompany the operating system.  Such a contradiction means you cannot
use both them and the Library together in an executable that you
distribute.

  7. You may place library facilities that are a work based on the
Library side-by-side in a single library together with other library
facilities not covered by this License, and distribute such a combined
library, provided that the separate distribution of the work based on
the Library and of the other library facilities is otherwise
permitted, and provided that you do these two things:

    a) Accompany the combined library with a copy of the same work
    based on the Library, uncombined with any other library
    facilities.  This must be distributed under the terms of the
    Sections above.

    b) Give prominent notice with the combined library of the fact
    that part of it is a work based on the Library, and explaining
    where to find the accompanying uncombined form of the same work.

  8. You may not copy, modify, sublicense, link with, or distribute
the Library except as expressly provided under this License.  Any
attempt otherwise to copy, modify, sublicense, link with, or
distribute the Library is void, and will automatically terminate your
rights under this License.  However, parties who have received copies,
or rights, from you under this License will not have their licenses
terminated so long as such parties remain in full compliance.

  9. You are not required to accept this License, since you have not
signed it.  However, nothing else grants you permission to modify or
distribute the Library or its derivative works.  These actions are
prohibited by law if you do not accept this License.  Therefore, by
modifying or distributing the Library (or any work based on the
Library), you indicate your acceptance of this License to do so, and
all its terms and conditions for copying, distributing or modifying
the Library or works based on it.

  10. Each time you redistribute the Library (or any work based on the
Library), the recipient automatically receives a license from the
original licensor to copy, distribute, link with or modify the Library
subject to these terms and conditions.  You may not impose any further
restrictions on the recipients' exercise of the rights granted herein.
You are not responsible for enforcing compliance by third parties with
this License.

  11. If, as a consequence of a court judgment or allegation of patent
infringement or for any other reason (not limited to patent issues),
conditions are imposed on you (whether by court order, agreement or
otherwise) that contradict the conditions of this License, they do not
excuse you from the conditions of this License.  If you cannot
distribute so as to satisfy simultaneously your obligations under this
License and any other pertinent obligations, then as a consequence you
may not distribute the Library at all.  For example, if a patent
license would not permit royalty-free redistribution of the Library by
all those who receive copies directly or indirectly through you, then
the only way you could satisfy both it and this License would be to
refrain entirely from distribution of the Library.

If any portion of this section is held invalid or unenforceable under any
particular circumstance, the balance of the section is intended to apply,
and the section as a whole is intended to apply in other circumstances.

It is not the purpose of this section to induce you to infringe any
patents or other property right claims or to contest validity of any
such claims; this section has the sole purpose of protecting the
integrity of the free software distribution system which is
implemented by public license practices.  Many people have made
generous contributions to the wide range of software distributed
through that system in reliance on consistent application of that
system; it is up to the author/donor to decide if he or she is willing
to distribute software through any other system and a licensee cannot
impose that choice.

This section is intended to make thoroughly clear what is believed to
be a consequence of the rest of this License.

  12. If the distribution and/or use of the Library is restricted in
certain countries either by patents or by copyrighted interfaces, the
original copyright holder who places the Library under this License may add
an explicit geographical distribution limitation excluding those countries,
so that distribution is permitted only in or among countries not thus
excluded.  In such case, this License incorporates the limitation as if
written in the body of this License.

  13. The Free Software Foundation may publish revised and/or new
versions of the Lesser General Public License from time to time.
Such new versions will be similar in spirit to the present version,
but may differ in detail to address new problems or concerns.

Each version is given a distinguishing version number.  If the Library
specifies a version number of this License which applies to it and
"any later version", you have the option of following the terms and
conditions either of that version or of any later version published by
the Free Software Foundation.  If the Library does not specify a
license version number, you may choose any version ever published by
the Free Software Foundation.

  14. If you wish to incorporate parts of the Library into other free
programs whose distribution conditions are incompatible with these,
write to the author to ask for permission.  For software which is
copyrighted by the Free Software Foundation, write to the Free
Software Foundation; we sometimes make exceptions for this.  Our
decision will be guided by the two goals of preserving the free status
of all derivatives of our free software and of promoting the sharing
and reuse of software generally.

			    NO WARRANTY

  15. BECAUSE THE LIBRARY IS LICENSED FREE OF CHARGE, THERE IS NO
WARRANTY FOR THE LIBRARY, TO THE EXTENT PERMITTED BY APPLICABLE LAW.
EXCEPT WHEN OTHERWISE STATED IN WRITING THE COPYRIGHT HOLDERS AND/OR
OTHER PARTIES PROVIDE THE LIBRARY "AS IS" WITHOUT WARRANTY OF ANY
KIND, EITHER EXPRESSED OR IMPLIED, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR
PURPOSE.  THE ENTIRE RISK AS TO THE QUALITY AND PERFORMANCE OF THE
LIBRARY IS WITH YOU.  SHOULD THE LIBRARY PROVE DEFECTIVE, YOU ASSUME
THE COST OF ALL NECESSARY SERVICING, REPAIR OR CORRECTION.

  16. IN NO EVENT UNLESS REQUIRED BY APPLICABLE LAW OR AGREED TO IN
WRITING WILL ANY COPYRIGHT HOLDER, OR ANY OTHER PARTY WHO MAY MODIFY
AND/OR REDISTRIBUTE THE LIBRARY AS PERMITTED ABOVE, BE LIABLE TO YOU
FOR DAMAGES, INCLUDING ANY GENERAL, SPECIAL, INCIDENTAL OR
CONSEQUENTIAL DAMAGES ARISING OUT OF THE USE OR INABILITY TO USE THE
LIBRARY (INCLUDING BUT NOT LIMITED TO LOSS OF DATA OR DATA BEING
RENDERED INACCURATE OR LOSSES SUSTAINED BY YOU OR THIRD PARTIES OR A
FAILURE OF THE LIBRARY TO OPERATE WITH ANY OTHER SOFTWARE), EVEN IF
SUCH HOLDER OR OTHER PARTY HAS BEEN ADVISED OF THE POSSIBILITY OF SUCH
DAMAGES.

		     END OF TERMS AND CONDITIONS

           How to Apply These Terms to Your New Libraries

  If you develop a new library, and you want it to be of the greatest
possible use to the public, we recommend making it free software that
everyone can redistribute and change.  You can do so by permitting
redistribution under these terms (or, alternatively, under the terms of the
ordinary General Public License).

  To apply these terms, attach the following notices to the library.  It is
safest to attach them to the start of each source file to most effectively
convey the exclusion of warranty; and each file should have at least the
"copyright" line and a pointer to where the full notice is found.

    <one line to give the library's name and a brief idea of what it does.>
    Copyright (C) <year>  <name of author>

    This library is free software; you can redistribute it and/or
    modify it under the terms of the GNU Lesser General Public
    License as published by the Free Software Foundation; either
    version 2.1 of the License, or (at your option) any later version.

    This library is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU
    Lesser General Public License for more details.

    You should have received a copy of the GNU Lesser General Public
    License along with this library; if not, write to the Free Software
    Foundation, Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02110-1301  USA

Also add information on how to contact you by electronic and paper mail.

You should also get your employer (if you work as a programmer) or your
school, if any, to sign a "copyright disclaimer" for the library, if
necessary.  Here is a sample; alter the names:

  Yoyodyne, Inc., hereby disclaims all copyright interest in the
  library `Frob' (a library for tweaking knobs) written by James Random Hacker.

  <signature of Ty Coon>, 1 April 1990
  Ty Coon, President of Vice

That's all there is to it!



Eclipse Public License - v 1.0

THE ACCOMPANYING PROGRAM IS PROVIDED UNDER THE TERMS OF THIS ECLIPSE PUBLIC LICENSE ("AGREEMENT"). ANY USE, REPRODUCTION OR DISTRIBUTION OF THE PROGRAM CONSTITUTES RECIPIENT'S ACCEPTANCE OF THIS AGREEMENT.

1. DEFINITIONS

"Contribution" means:

a) in the case of the initial Contributor, the initial code and documentation distributed under this Agreement, and

b) in the case of each subsequent Contributor:

i) changes to the Program, and

ii) additions to the Program;

where such changes and/or additions to the Program originate from and are distributed by that particular Contributor. A Contribution 'originates' from a Contributor if it was added to the Program by such Contributor itself or anyone acting on such Contributor's behalf. Contributions do not include additions to the Program which: (i) are separate modules of software distributed in conjunction with the Program under their own license agreement, and (ii) are not derivative works of the Program.

"Contributor" means any person or entity that distributes the Program.

"Licensed Patents" mean patent claims licensable by a Contributor which are necessarily infringed by the use or sale of its Contribution alone or when combined with the Program.

"Program" means the Contributions distributed in accordance with this Agreement.

"Recipient" means anyone who receives the Program under this Agreement, including all Contributors.

2. GRANT OF RIGHTS

a) Subject to the terms of this Agreement, each Contributor hereby grants Recipient a non-exclusive, worldwide, royalty-free copyright license to reproduce, prepare derivative works of, publicly display, publicly perform, distribute and sublicense the Contribution of such Contributor, if any, and such derivative works, in source code and object code form.

b) Subject to the terms of this Agreement, each Contributor hereby grants Recipient a non-exclusive, worldwide, royalty-free patent license under Licensed Patents to make, use, sell, offer to sell, import and otherwise transfer the Contribution of such Contributor, if any, in source code and object code form. This patent license shall apply to the combination of the Contribution and the Program if, at the time the Contribution is added by the Contributor, such addition of the Contribution causes such combination to be covered by the Licensed Patents. The patent license shall not apply to any other combinations which include the Contribution. No hardware per se is licensed hereunder.

c) Recipient understands that although each Contributor grants the licenses to its Contributions set forth herein, no assurances are provided by any Contributor that the Program does not infringe the patent or other intellectual property rights of any other entity. Each Contributor disclaims any liability to Recipient for claims brought by any other entity based on infringement of intellectual property rights or otherwise. As a condition to exercising the rights and licenses granted hereunder, each Recipient hereby assumes sole responsibility to secure any other intellectual property rights needed, if any. For example, if a third party patent license is required to allow Recipient to distribute the Program, it is Recipient's responsibility to acquire that license before distributing the Program.

d) Each Contributor represents that to its knowledge it has sufficient copyright rights in its Contribution, if any, to grant the copyright license set forth in this Agreement.

3. REQUIREMENTS

A Contributor may choose to distribute the Program in object code form under its own license agreement, provided that:

a) it complies with the terms and conditions of this Agreement; and

b) its license agreement:

i) effectively disclaims on behalf of all Contributors all warranties and conditions, express and implied, including warranties or conditions of title and non-infringement, and implied warranties or conditions of merchantability and fitness for a particular purpose;

ii) effectively excludes on behalf of all Contributors all liability for damages, including direct, indirect, special, incidental and consequential damages, such as lost profits;

iii) states that any provisions which differ from this Agreement are offered by that Contributor alone and not by any other party; and

iv) states that source code for the Program is available from such Contributor, and informs licensees how to obtain it in a reasonable manner on or through a medium customarily used for software exchange.

When the Program is made available in source code form:

a) it must be made available under this Agreement; and

b) a copy of this Agreement must be included with each copy of the Program.

Contributors may not remove or alter any copyright notices contained within the Program.

Each Contributor must identify itself as the originator of its Contribution, if any, in a manner that reasonably allows subsequent Recipients to identify the originator of the Contribution.

4. COMMERCIAL DISTRIBUTION

Commercial distributors of software may accept certain responsibilities with respect to end users, business partners and the like. While this license is intended to facilitate the commercial use of the Program, the Contributor who includes the Program in a commercial product offering should do so in a manner which does not create potential liability for other Contributors. Therefore, if a Contributor includes the Program in a commercial product offering, such Contributor ("Commercial Contributor") hereby agrees to defend and indemnify every other Contributor ("Indemnified Contributor") against any losses, damages and costs (collectively "Losses") arising from claims, lawsuits and other legal actions brought by a third party against the Indemnified Contributor to the extent caused by the acts or omissions of such Commercial Contributor in connection with its distribution of the Program in a commercial product offering. The obligations in this section do not apply to any claims or Losses relating to any actual or alleged intellectual property infringement. In order to qualify, an Indemnified Contributor must: a) promptly notify the Commercial Contributor in writing of such claim, and b) allow the Commercial Contributor to control, and cooperate with the Commercial Contributor in, the defense and any related settlement negotiations. The Indemnified Contributor may participate in any such claim at its own expense.

For example, a Contributor might include the Program in a commercial product offering, Product X. That Contributor is then a Commercial Contributor. If that Commercial Contributor then makes performance claims, or offers warranties related to Product X, those performance claims and warranties are such Commercial Contributor's responsibility alone. Under this section, the Commercial Contributor would have to defend claims against the other Contributors related to those performance claims and warranties, and if a court requires any other Contributor to pay any damages as a result, the Commercial Contributor must pay those damages.

5. NO WARRANTY

EXCEPT AS EXPRESSLY SET FORTH IN THIS AGREEMENT, THE PROGRAM IS PROVIDED ON AN "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, EITHER EXPRESS OR IMPLIED INCLUDING, WITHOUT LIMITATION, ANY WARRANTIES OR CONDITIONS OF TITLE, NON-INFRINGEMENT, MERCHANTABILITY OR FITNESS FOR A PARTICULAR PURPOSE. Each Recipient is solely responsible for determining the appropriateness of using and distributing the Program and assumes all risks associated with its exercise of rights under this Agreement , including but not limited to the risks and costs of program errors, compliance with applicable laws, damage to or loss of data, programs or equipment, and unavailability or interruption of operations.

6. DISCLAIMER OF LIABILITY

EXCEPT AS EXPRESSLY SET FORTH IN THIS AGREEMENT, NEITHER RECIPIENT NOR ANY CONTRIBUTORS SHALL HAVE ANY LIABILITY FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING WITHOUT LIMITATION LOST PROFITS), HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OR DISTRIBUTION OF THE PROGRAM OR THE EXERCISE OF ANY RIGHTS GRANTED HEREUNDER, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGES.

7. GENERAL

If any provision of this Agreement is invalid or unenforceable under applicable law, it shall not affect the validity or enforceability of the remainder of the terms of this Agreement, and without further action by the parties hereto, such provision shall be reformed to the minimum extent necessary to make such provision valid and enforceable.

If Recipient institutes patent litigation against any entity (including a cross-claim or counterclaim in a lawsuit) alleging that the Program itself (excluding combinations of the Program with other software or hardware) infringes such Recipient's patent(s), then such Recipient's rights granted under Section 2(b) shall terminate as of the date such litigation is filed.

All Recipient's rights under this Agreement shall terminate if it fails to comply with any of the material terms or conditions of this Agreement and does not cure such failure in a reasonable period of time after becoming aware of such noncompliance. If all Recipient's rights under this Agreement terminate, Recipient agrees to cease use and distribution of the Program as soon as reasonably practicable. However, Recipient's obligations under this Agreement and any licenses granted by Recipient relating to the Program shall continue and survive.

Everyone is permitted to copy and distribute copies of this Agreement, but in order to avoid inconsistency the Agreement is copyrighted and may only be modified in the following manner. The Agreement Steward reserves the right to publish new versions (including revisions) of this Agreement from time to time. No one other than the Agreement Steward has the right to modify this Agreement. The Eclipse Foundation is the initial Agreement Steward. The Eclipse Foundation may assign the responsibility to serve as the Agreement Steward to a suitable separate entity. Each new version of the Agreement will be given a distinguishing version number. The Program (including Contributions) may always be distributed subject to the version of the Agreement under which it was received. In addition, after a new version of the Agreement is published, Contributor may elect to distribute the Program (including its Contributions) under the new version. Except as expressly stated in Sections 2(a) and 2(b) above, Recipient receives no rights or licenses to the intellectual property of any Contributor under this Agreement, whether expressly, by implication, estoppel or otherwise. All rights in the Program not expressly granted under this Agreement are reserved.

This Agreement is governed by the laws of the State of New York and the intellectual property laws of the United States of America. No party to this Agreement will bring a legal action under this Agreement more than one year after the cause of action arose. Each party waives its rights to a jury trial in any resulting litigation.
# webcam-capture-driver-ipcam

This is capture driver which gives Webcam Capture API possibility to
access IP camera devices. It allows it to
handle pictures from IP cameras supporting JPEG and MJPEG (Motion JPEG) compression
and can work in two modes - ```PULL``` for JPEG and ```PUSH``` for MJPEG.

What are the differences between these two modes:

* ```PULL``` - will request new JPEG image each time when it is required,
* ```PUSH``` - stream Motion JPEG in real time and serve newest image on-demand.

Support for few IP cameras is build-in, that list includes:

* [IP Robocam 641](http://www.marmitek.com/en/product-details/home-automation-security/ip-cameras/ip-robocam-641.php) by [Marmitek](http://www.marmitek.com/) (MJPEG)
* [Speed Dome X104S](http://www.ipcctv.com/product.php?xProd=10&xSec=26) by [Xvision](http://www.ipcctv.com/) (MJPEG)
* [B7210](http://www.zavio.com/product.php?id=45) by [Zavio](http://www.zavio.com/) (JPEG)
* [F3201](http://www.zavio.com/product.php?id=28) by [Zavio](http://www.zavio.com/) (JPEG)

If you would like to have more IP cameras supported, please create new issue, describe the camera
model, provide demo URL and API if available. You can also create your own IP camera class. In such 
a case please use provided models as a reference. In case of any issues don't hesitate to ask for
help :) Later, when your class is ready, I will be happy to merge it with official distribution.


## Download

The latest **development** version JAR (aka SNAPSHOT) can be downloaded [here](https://oss.sonatype.org/service/local/artifact/maven/redirect?r=snapshots&g=com.github.sarxos&a=webcam-capture-driver-ipcam&v=0.3.13-SNAPSHOT).

The latest **stable** version ZIP bundle can be downloaded [here](http://repo.sarxos.pl/maven2/com/github/sarxos/webcam-capture-driver-ipcam/0.3.12/webcam-capture-driver-ipcam-0.3.12-dist.zip).

## Maven

Stable:

```xml
<dependency>
	<groupId>com.github.sarxos</groupId>
	<artifactId>webcam-capture-driver-ipcam</artifactId>
	<version>0.3.12</version>
</dependency>
```

Snapshot:

```xml
<repository>
    <id>Sonatype OSS Snapshot Repository</id>
    <url>http://oss.sonatype.org/content/repositories/snapshots</url>
</repository>
```
```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-ipcam</artifactId>
    <version>0.3.13-SNAPSHOT</version>
</dependency>
```

## Examples

Few real live examples of how to use Webcam Capture together with IP camera driver.
Please note that some URLs can be out-of-date when you test this code, however you
can find some usable IP camera demos googling _"ip camera demo"_ or accessing 
[this page](http://www.axis.com/solutions/video/gallery.htm).

### Example 1

Example of how to display image from IP camera device which expose pictures 
as MJPEG stream (this is refered as PUSH mode, because camera push new images 
to the client as soon as new one is available).

```java
static {
	Webcam.setDriver(new IpCamDriver());
}

public static void main(String[] args) throws MalformedURLException {
	IpCamDeviceRegistry.register(new IpCamDevice("Lignano", "http://88.37.116.138/mjpg/video.mjpg", IpCamMode.PUSH));
	JFrame f = new JFrame("Live Views From Lignano Beach");
	f.add(new WebcamPanel(Webcam.getDefault()));
	f.pack();
	f.setVisible(true);
	f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
}
```

![Lignano Beach](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-drivers/webcam-capture-driver-ipcam/src/etc/resources/lignano-beach.png "Lignano Beach")

### Example 2

Example of how to display image from multiple IP camera devices which expose 
it as JPG pictures. In this example we are using IP camera storage feature which
use XML file to define all available cameras.

```java
/**
 * Here we are additionally using cameras storage which is based on simple
 * XML file where all cameras which will be used are listed. By using
 * cameras storage you do not have to register devices neither thru the
 * registry nor driver instance. It's the simplest to deal with multiple
 * cameras when you do not have to add/remove cameras in runtime.
 */
static {
	Webcam.setDriver(new IpCamDriver(new IpCamStorage("src/examples/resources/cameras.xml")));
}

public static void main(String[] args) throws MalformedURLException {

	JFrame f = new JFrame("Dasding Studio Live IP Cameras Demo");
	f.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
	f.setLayout(new GridLayout(0, 3, 1, 1));

	List<WebcamPanel> panels = new ArrayList<WebcamPanel>();

	for (Webcam webcam : Webcam.getWebcams()) {

		WebcamPanel panel = new WebcamPanel(webcam, new Dimension(256, 144), false);
		panel.setFillArea(true);
		panel.setFPSLimited(true);
		panel.setFPS(0.2); // 0.1 FPS = 1 frame per 10 seconds
		panel.setBorder(BorderFactory.createEmptyBorder());

		f.add(panel);
		panels.add(panel);
	}

	f.pack();
	f.setVisible(true);

	for (WebcamPanel panel : panels) {
		panel.start();
	}
}
```

And here is the cameras.xml file used in the above example:

```xml
<?xml version="1.0" encoding="UTF-8" ?> 
<storage>
	<ipcam name="Dasding 01" url="http://www.dasding.de/ext/webcam/webcam770.php?cam=1" />
	<ipcam name="Dasding 02" url="http://www.dasding.de/ext/webcam/webcam770.php?cam=2" />
	<ipcam name="Dasding 04" url="http://www.dasding.de/ext/webcam/webcam770.php?cam=4" />
	<ipcam name="Dasding 06" url="http://www.dasding.de/ext/webcam/webcam770.php?cam=6" />
	<ipcam name="Dasding 07" url="http://www.dasding.de/ext/webcam/webcam770.php?cam=7" />
	<ipcam name="Dasding 10" url="http://www.dasding.de/ext/webcam/webcam770.php?cam=10" />
</storage>
```

![Dasding Studio Live IP Camera](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-drivers/webcam-capture-driver-ipcam/src/etc/resources/dasding-live.png "Dasding Studio Live IP Camera")

## License

Copyright (C) 2012 - 2014 Bartosz Firyn

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

                                 Apache License
                           Version 2.0, January 2004
                        http://www.apache.org/licenses/

   TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

   1. Definitions.

      "License" shall mean the terms and conditions for use, reproduction,
      and distribution as defined by Sections 1 through 9 of this document.

      "Licensor" shall mean the copyright owner or entity authorized by
      the copyright owner that is granting the License.

      "Legal Entity" shall mean the union of the acting entity and all
      other entities that control, are controlled by, or are under common
      control with that entity. For the purposes of this definition,
      "control" means (i) the power, direct or indirect, to cause the
      direction or management of such entity, whether by contract or
      otherwise, or (ii) ownership of fifty percent (50%) or more of the
      outstanding shares, or (iii) beneficial ownership of such entity.

      "You" (or "Your") shall mean an individual or Legal Entity
      exercising permissions granted by this License.

      "Source" form shall mean the preferred form for making modifications,
      including but not limited to software source code, documentation
      source, and configuration files.

      "Object" form shall mean any form resulting from mechanical
      transformation or translation of a Source form, including but
      not limited to compiled object code, generated documentation,
      and conversions to other media types.

      "Work" shall mean the work of authorship, whether in Source or
      Object form, made available under the License, as indicated by a
      copyright notice that is included in or attached to the work
      (an example is provided in the Appendix below).

      "Derivative Works" shall mean any work, whether in Source or Object
      form, that is based on (or derived from) the Work and for which the
      editorial revisions, annotations, elaborations, or other modifications
      represent, as a whole, an original work of authorship. For the purposes
      of this License, Derivative Works shall not include works that remain
      separable from, or merely link (or bind by name) to the interfaces of,
      the Work and Derivative Works thereof.

      "Contribution" shall mean any work of authorship, including
      the original version of the Work and any modifications or additions
      to that Work or Derivative Works thereof, that is intentionally
      submitted to Licensor for inclusion in the Work by the copyright owner
      or by an individual or Legal Entity authorized to submit on behalf of
      the copyright owner. For the purposes of this definition, "submitted"
      means any form of electronic, verbal, or written communication sent
      to the Licensor or its representatives, including but not limited to
      communication on electronic mailing lists, source code control systems,
      and issue tracking systems that are managed by, or on behalf of, the
      Licensor for the purpose of discussing and improving the Work, but
      excluding communication that is conspicuously marked or otherwise
      designated in writing by the copyright owner as "Not a Contribution."

      "Contributor" shall mean Licensor and any individual or Legal Entity
      on behalf of whom a Contribution has been received by Licensor and
      subsequently incorporated within the Work.

   2. Grant of Copyright License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      copyright license to reproduce, prepare Derivative Works of,
      publicly display, publicly perform, sublicense, and distribute the
      Work and such Derivative Works in Source or Object form.

   3. Grant of Patent License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      (except as stated in this section) patent license to make, have made,
      use, offer to sell, sell, import, and otherwise transfer the Work,
      where such license applies only to those patent claims licensable
      by such Contributor that are necessarily infringed by their
      Contribution(s) alone or by combination of their Contribution(s)
      with the Work to which such Contribution(s) was submitted. If You
      institute patent litigation against any entity (including a
      cross-claim or counterclaim in a lawsuit) alleging that the Work
      or a Contribution incorporated within the Work constitutes direct
      or contributory patent infringement, then any patent licenses
      granted to You under this License for that Work shall terminate
      as of the date such litigation is filed.

   4. Redistribution. You may reproduce and distribute copies of the
      Work or Derivative Works thereof in any medium, with or without
      modifications, and in Source or Object form, provided that You
      meet the following conditions:

      (a) You must give any other recipients of the Work or
          Derivative Works a copy of this License; and

      (b) You must cause any modified files to carry prominent notices
          stating that You changed the files; and

      (c) You must retain, in the Source form of any Derivative Works
          that You distribute, all copyright, patent, trademark, and
          attribution notices from the Source form of the Work,
          excluding those notices that do not pertain to any part of
          the Derivative Works; and

      (d) If the Work includes a "NOTICE" text file as part of its
          distribution, then any Derivative Works that You distribute must
          include a readable copy of the attribution notices contained
          within such NOTICE file, excluding those notices that do not
          pertain to any part of the Derivative Works, in at least one
          of the following places: within a NOTICE text file distributed
          as part of the Derivative Works; within the Source form or
          documentation, if provided along with the Derivative Works; or,
          within a display generated by the Derivative Works, if and
          wherever such third-party notices normally appear. The contents
          of the NOTICE file are for informational purposes only and
          do not modify the License. You may add Your own attribution
          notices within Derivative Works that You distribute, alongside
          or as an addendum to the NOTICE text from the Work, provided
          that such additional attribution notices cannot be construed
          as modifying the License.

      You may add Your own copyright statement to Your modifications and
      may provide additional or different license terms and conditions
      for use, reproduction, or distribution of Your modifications, or
      for any such Derivative Works as a whole, provided Your use,
      reproduction, and distribution of the Work otherwise complies with
      the conditions stated in this License.

   5. Submission of Contributions. Unless You explicitly state otherwise,
      any Contribution intentionally submitted for inclusion in the Work
      by You to the Licensor shall be under the terms and conditions of
      this License, without any additional terms or conditions.
      Notwithstanding the above, nothing herein shall supersede or modify
      the terms of any separate license agreement you may have executed
      with Licensor regarding such Contributions.

   6. Trademarks. This License does not grant permission to use the trade
      names, trademarks, service marks, or product names of the Licensor,
      except as required for reasonable and customary use in describing the
      origin of the Work and reproducing the content of the NOTICE file.

   7. Disclaimer of Warranty. Unless required by applicable law or
      agreed to in writing, Licensor provides the Work (and each
      Contributor provides its Contributions) on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
      implied, including, without limitation, any warranties or conditions
      of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A
      PARTICULAR PURPOSE. You are solely responsible for determining the
      appropriateness of using or redistributing the Work and assume any
      risks associated with Your exercise of permissions under this License.

   8. Limitation of Liability. In no event and under no legal theory,
      whether in tort (including negligence), contract, or otherwise,
      unless required by applicable law (such as deliberate and grossly
      negligent acts) or agreed to in writing, shall any Contributor be
      liable to You for damages, including any direct, indirect, special,
      incidental, or consequential damages of any character arising as a
      result of this License or out of the use or inability to use the
      Work (including but not limited to damages for loss of goodwill,
      work stoppage, computer failure or malfunction, or any and all
      other commercial damages or losses), even if such Contributor
      has been advised of the possibility of such damages.

   9. Accepting Warranty or Additional Liability. While redistributing
      the Work or Derivative Works thereof, You may choose to offer,
      and charge a fee for, acceptance of support, warranty, indemnity,
      or other liability obligations and/or rights consistent with this
      License. However, in accepting such obligations, You may act only
      on Your own behalf and on Your sole responsibility, not on behalf
      of any other Contributor, and only if You agree to indemnify,
      defend, and hold each Contributor harmless for any liability
      incurred by, or claims asserted against, such Contributor by reason
      of your accepting any such warranty or additional liability.

   END OF TERMS AND CONDITIONS
                                 Apache License
                           Version 2.0, January 2004
                        http://www.apache.org/licenses/

   TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

   1. Definitions.

      "License" shall mean the terms and conditions for use, reproduction,
      and distribution as defined by Sections 1 through 9 of this document.

      "Licensor" shall mean the copyright owner or entity authorized by
      the copyright owner that is granting the License.

      "Legal Entity" shall mean the union of the acting entity and all
      other entities that control, are controlled by, or are under common
      control with that entity. For the purposes of this definition,
      "control" means (i) the power, direct or indirect, to cause the
      direction or management of such entity, whether by contract or
      otherwise, or (ii) ownership of fifty percent (50%) or more of the
      outstanding shares, or (iii) beneficial ownership of such entity.

      "You" (or "Your") shall mean an individual or Legal Entity
      exercising permissions granted by this License.

      "Source" form shall mean the preferred form for making modifications,
      including but not limited to software source code, documentation
      source, and configuration files.

      "Object" form shall mean any form resulting from mechanical
      transformation or translation of a Source form, including but
      not limited to compiled object code, generated documentation,
      and conversions to other media types.

      "Work" shall mean the work of authorship, whether in Source or
      Object form, made available under the License, as indicated by a
      copyright notice that is included in or attached to the work
      (an example is provided in the Appendix below).

      "Derivative Works" shall mean any work, whether in Source or Object
      form, that is based on (or derived from) the Work and for which the
      editorial revisions, annotations, elaborations, or other modifications
      represent, as a whole, an original work of authorship. For the purposes
      of this License, Derivative Works shall not include works that remain
      separable from, or merely link (or bind by name) to the interfaces of,
      the Work and Derivative Works thereof.

      "Contribution" shall mean any work of authorship, including
      the original version of the Work and any modifications or additions
      to that Work or Derivative Works thereof, that is intentionally
      submitted to Licensor for inclusion in the Work by the copyright owner
      or by an individual or Legal Entity authorized to submit on behalf of
      the copyright owner. For the purposes of this definition, "submitted"
      means any form of electronic, verbal, or written communication sent
      to the Licensor or its representatives, including but not limited to
      communication on electronic mailing lists, source code control systems,
      and issue tracking systems that are managed by, or on behalf of, the
      Licensor for the purpose of discussing and improving the Work, but
      excluding communication that is conspicuously marked or otherwise
      designated in writing by the copyright owner as "Not a Contribution."

      "Contributor" shall mean Licensor and any individual or Legal Entity
      on behalf of whom a Contribution has been received by Licensor and
      subsequently incorporated within the Work.

   2. Grant of Copyright License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      copyright license to reproduce, prepare Derivative Works of,
      publicly display, publicly perform, sublicense, and distribute the
      Work and such Derivative Works in Source or Object form.

   3. Grant of Patent License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      (except as stated in this section) patent license to make, have made,
      use, offer to sell, sell, import, and otherwise transfer the Work,
      where such license applies only to those patent claims licensable
      by such Contributor that are necessarily infringed by their
      Contribution(s) alone or by combination of their Contribution(s)
      with the Work to which such Contribution(s) was submitted. If You
      institute patent litigation against any entity (including a
      cross-claim or counterclaim in a lawsuit) alleging that the Work
      or a Contribution incorporated within the Work constitutes direct
      or contributory patent infringement, then any patent licenses
      granted to You under this License for that Work shall terminate
      as of the date such litigation is filed.

   4. Redistribution. You may reproduce and distribute copies of the
      Work or Derivative Works thereof in any medium, with or without
      modifications, and in Source or Object form, provided that You
      meet the following conditions:

      (a) You must give any other recipients of the Work or
          Derivative Works a copy of this License; and

      (b) You must cause any modified files to carry prominent notices
          stating that You changed the files; and

      (c) You must retain, in the Source form of any Derivative Works
          that You distribute, all copyright, patent, trademark, and
          attribution notices from the Source form of the Work,
          excluding those notices that do not pertain to any part of
          the Derivative Works; and

      (d) If the Work includes a "NOTICE" text file as part of its
          distribution, then any Derivative Works that You distribute must
          include a readable copy of the attribution notices contained
          within such NOTICE file, excluding those notices that do not
          pertain to any part of the Derivative Works, in at least one
          of the following places: within a NOTICE text file distributed
          as part of the Derivative Works; within the Source form or
          documentation, if provided along with the Derivative Works; or,
          within a display generated by the Derivative Works, if and
          wherever such third-party notices normally appear. The contents
          of the NOTICE file are for informational purposes only and
          do not modify the License. You may add Your own attribution
          notices within Derivative Works that You distribute, alongside
          or as an addendum to the NOTICE text from the Work, provided
          that such additional attribution notices cannot be construed
          as modifying the License.

      You may add Your own copyright statement to Your modifications and
      may provide additional or different license terms and conditions
      for use, reproduction, or distribution of Your modifications, or
      for any such Derivative Works as a whole, provided Your use,
      reproduction, and distribution of the Work otherwise complies with
      the conditions stated in this License.

   5. Submission of Contributions. Unless You explicitly state otherwise,
      any Contribution intentionally submitted for inclusion in the Work
      by You to the Licensor shall be under the terms and conditions of
      this License, without any additional terms or conditions.
      Notwithstanding the above, nothing herein shall supersede or modify
      the terms of any separate license agreement you may have executed
      with Licensor regarding such Contributions.

   6. Trademarks. This License does not grant permission to use the trade
      names, trademarks, service marks, or product names of the Licensor,
      except as required for reasonable and customary use in describing the
      origin of the Work and reproducing the content of the NOTICE file.

   7. Disclaimer of Warranty. Unless required by applicable law or
      agreed to in writing, Licensor provides the Work (and each
      Contributor provides its Contributions) on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
      implied, including, without limitation, any warranties or conditions
      of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A
      PARTICULAR PURPOSE. You are solely responsible for determining the
      appropriateness of using or redistributing the Work and assume any
      risks associated with Your exercise of permissions under this License.

   8. Limitation of Liability. In no event and under no legal theory,
      whether in tort (including negligence), contract, or otherwise,
      unless required by applicable law (such as deliberate and grossly
      negligent acts) or agreed to in writing, shall any Contributor be
      liable to You for damages, including any direct, indirect, special,
      incidental, or consequential damages of any character arising as a
      result of this License or out of the use or inability to use the
      Work (including but not limited to damages for loss of goodwill,
      work stoppage, computer failure or malfunction, or any and all
      other commercial damages or losses), even if such Contributor
      has been advised of the possibility of such damages.

   9. Accepting Warranty or Additional Liability. While redistributing
      the Work or Derivative Works thereof, You may choose to offer,
      and charge a fee for, acceptance of support, warranty, indemnity,
      or other liability obligations and/or rights consistent with this
      License. However, in accepting such obligations, You may act only
      on Your own behalf and on Your sole responsibility, not on behalf
      of any other Contributor, and only if You agree to indemnify,
      defend, and hold each Contributor harmless for any liability
      incurred by, or claims asserted against, such Contributor by reason
      of your accepting any such warranty or additional liability.

   END OF TERMS AND CONDITIONS
                                 Apache License
                           Version 2.0, January 2004
                        http://www.apache.org/licenses/

   TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

   1. Definitions.

      "License" shall mean the terms and conditions for use, reproduction,
      and distribution as defined by Sections 1 through 9 of this document.

      "Licensor" shall mean the copyright owner or entity authorized by
      the copyright owner that is granting the License.

      "Legal Entity" shall mean the union of the acting entity and all
      other entities that control, are controlled by, or are under common
      control with that entity. For the purposes of this definition,
      "control" means (i) the power, direct or indirect, to cause the
      direction or management of such entity, whether by contract or
      otherwise, or (ii) ownership of fifty percent (50%) or more of the
      outstanding shares, or (iii) beneficial ownership of such entity.

      "You" (or "Your") shall mean an individual or Legal Entity
      exercising permissions granted by this License.

      "Source" form shall mean the preferred form for making modifications,
      including but not limited to software source code, documentation
      source, and configuration files.

      "Object" form shall mean any form resulting from mechanical
      transformation or translation of a Source form, including but
      not limited to compiled object code, generated documentation,
      and conversions to other media types.

      "Work" shall mean the work of authorship, whether in Source or
      Object form, made available under the License, as indicated by a
      copyright notice that is included in or attached to the work
      (an example is provided in the Appendix below).

      "Derivative Works" shall mean any work, whether in Source or Object
      form, that is based on (or derived from) the Work and for which the
      editorial revisions, annotations, elaborations, or other modifications
      represent, as a whole, an original work of authorship. For the purposes
      of this License, Derivative Works shall not include works that remain
      separable from, or merely link (or bind by name) to the interfaces of,
      the Work and Derivative Works thereof.

      "Contribution" shall mean any work of authorship, including
      the original version of the Work and any modifications or additions
      to that Work or Derivative Works thereof, that is intentionally
      submitted to Licensor for inclusion in the Work by the copyright owner
      or by an individual or Legal Entity authorized to submit on behalf of
      the copyright owner. For the purposes of this definition, "submitted"
      means any form of electronic, verbal, or written communication sent
      to the Licensor or its representatives, including but not limited to
      communication on electronic mailing lists, source code control systems,
      and issue tracking systems that are managed by, or on behalf of, the
      Licensor for the purpose of discussing and improving the Work, but
      excluding communication that is conspicuously marked or otherwise
      designated in writing by the copyright owner as "Not a Contribution."

      "Contributor" shall mean Licensor and any individual or Legal Entity
      on behalf of whom a Contribution has been received by Licensor and
      subsequently incorporated within the Work.

   2. Grant of Copyright License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      copyright license to reproduce, prepare Derivative Works of,
      publicly display, publicly perform, sublicense, and distribute the
      Work and such Derivative Works in Source or Object form.

   3. Grant of Patent License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      (except as stated in this section) patent license to make, have made,
      use, offer to sell, sell, import, and otherwise transfer the Work,
      where such license applies only to those patent claims licensable
      by such Contributor that are necessarily infringed by their
      Contribution(s) alone or by combination of their Contribution(s)
      with the Work to which such Contribution(s) was submitted. If You
      institute patent litigation against any entity (including a
      cross-claim or counterclaim in a lawsuit) alleging that the Work
      or a Contribution incorporated within the Work constitutes direct
      or contributory patent infringement, then any patent licenses
      granted to You under this License for that Work shall terminate
      as of the date such litigation is filed.

   4. Redistribution. You may reproduce and distribute copies of the
      Work or Derivative Works thereof in any medium, with or without
      modifications, and in Source or Object form, provided that You
      meet the following conditions:

      (a) You must give any other recipients of the Work or
          Derivative Works a copy of this License; and

      (b) You must cause any modified files to carry prominent notices
          stating that You changed the files; and

      (c) You must retain, in the Source form of any Derivative Works
          that You distribute, all copyright, patent, trademark, and
          attribution notices from the Source form of the Work,
          excluding those notices that do not pertain to any part of
          the Derivative Works; and

      (d) If the Work includes a "NOTICE" text file as part of its
          distribution, then any Derivative Works that You distribute must
          include a readable copy of the attribution notices contained
          within such NOTICE file, excluding those notices that do not
          pertain to any part of the Derivative Works, in at least one
          of the following places: within a NOTICE text file distributed
          as part of the Derivative Works; within the Source form or
          documentation, if provided along with the Derivative Works; or,
          within a display generated by the Derivative Works, if and
          wherever such third-party notices normally appear. The contents
          of the NOTICE file are for informational purposes only and
          do not modify the License. You may add Your own attribution
          notices within Derivative Works that You distribute, alongside
          or as an addendum to the NOTICE text from the Work, provided
          that such additional attribution notices cannot be construed
          as modifying the License.

      You may add Your own copyright statement to Your modifications and
      may provide additional or different license terms and conditions
      for use, reproduction, or distribution of Your modifications, or
      for any such Derivative Works as a whole, provided Your use,
      reproduction, and distribution of the Work otherwise complies with
      the conditions stated in this License.

   5. Submission of Contributions. Unless You explicitly state otherwise,
      any Contribution intentionally submitted for inclusion in the Work
      by You to the Licensor shall be under the terms and conditions of
      this License, without any additional terms or conditions.
      Notwithstanding the above, nothing herein shall supersede or modify
      the terms of any separate license agreement you may have executed
      with Licensor regarding such Contributions.

   6. Trademarks. This License does not grant permission to use the trade
      names, trademarks, service marks, or product names of the Licensor,
      except as required for reasonable and customary use in describing the
      origin of the Work and reproducing the content of the NOTICE file.

   7. Disclaimer of Warranty. Unless required by applicable law or
      agreed to in writing, Licensor provides the Work (and each
      Contributor provides its Contributions) on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
      implied, including, without limitation, any warranties or conditions
      of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A
      PARTICULAR PURPOSE. You are solely responsible for determining the
      appropriateness of using or redistributing the Work and assume any
      risks associated with Your exercise of permissions under this License.

   8. Limitation of Liability. In no event and under no legal theory,
      whether in tort (including negligence), contract, or otherwise,
      unless required by applicable law (such as deliberate and grossly
      negligent acts) or agreed to in writing, shall any Contributor be
      liable to You for damages, including any direct, indirect, special,
      incidental, or consequential damages of any character arising as a
      result of this License or out of the use or inability to use the
      Work (including but not limited to damages for loss of goodwill,
      work stoppage, computer failure or malfunction, or any and all
      other commercial damages or losses), even if such Contributor
      has been advised of the possibility of such damages.

   9. Accepting Warranty or Additional Liability. While redistributing
      the Work or Derivative Works thereof, You may choose to offer,
      and charge a fee for, acceptance of support, warranty, indemnity,
      or other liability obligations and/or rights consistent with this
      License. However, in accepting such obligations, You may act only
      on Your own behalf and on Your sole responsibility, not on behalf
      of any other Contributor, and only if You agree to indemnify,
      defend, and hold each Contributor harmless for any liability
      incurred by, or claims asserted against, such Contributor by reason
      of your accepting any such warranty or additional liability.

   END OF TERMS AND CONDITIONS
                                 Apache License
                           Version 2.0, January 2004
                        http://www.apache.org/licenses/

   TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

   1. Definitions.

      "License" shall mean the terms and conditions for use, reproduction,
      and distribution as defined by Sections 1 through 9 of this document.

      "Licensor" shall mean the copyright owner or entity authorized by
      the copyright owner that is granting the License.

      "Legal Entity" shall mean the union of the acting entity and all
      other entities that control, are controlled by, or are under common
      control with that entity. For the purposes of this definition,
      "control" means (i) the power, direct or indirect, to cause the
      direction or management of such entity, whether by contract or
      otherwise, or (ii) ownership of fifty percent (50%) or more of the
      outstanding shares, or (iii) beneficial ownership of such entity.

      "You" (or "Your") shall mean an individual or Legal Entity
      exercising permissions granted by this License.

      "Source" form shall mean the preferred form for making modifications,
      including but not limited to software source code, documentation
      source, and configuration files.

      "Object" form shall mean any form resulting from mechanical
      transformation or translation of a Source form, including but
      not limited to compiled object code, generated documentation,
      and conversions to other media types.

      "Work" shall mean the work of authorship, whether in Source or
      Object form, made available under the License, as indicated by a
      copyright notice that is included in or attached to the work
      (an example is provided in the Appendix below).

      "Derivative Works" shall mean any work, whether in Source or Object
      form, that is based on (or derived from) the Work and for which the
      editorial revisions, annotations, elaborations, or other modifications
      represent, as a whole, an original work of authorship. For the purposes
      of this License, Derivative Works shall not include works that remain
      separable from, or merely link (or bind by name) to the interfaces of,
      the Work and Derivative Works thereof.

      "Contribution" shall mean any work of authorship, including
      the original version of the Work and any modifications or additions
      to that Work or Derivative Works thereof, that is intentionally
      submitted to Licensor for inclusion in the Work by the copyright owner
      or by an individual or Legal Entity authorized to submit on behalf of
      the copyright owner. For the purposes of this definition, "submitted"
      means any form of electronic, verbal, or written communication sent
      to the Licensor or its representatives, including but not limited to
      communication on electronic mailing lists, source code control systems,
      and issue tracking systems that are managed by, or on behalf of, the
      Licensor for the purpose of discussing and improving the Work, but
      excluding communication that is conspicuously marked or otherwise
      designated in writing by the copyright owner as "Not a Contribution."

      "Contributor" shall mean Licensor and any individual or Legal Entity
      on behalf of whom a Contribution has been received by Licensor and
      subsequently incorporated within the Work.

   2. Grant of Copyright License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      copyright license to reproduce, prepare Derivative Works of,
      publicly display, publicly perform, sublicense, and distribute the
      Work and such Derivative Works in Source or Object form.

   3. Grant of Patent License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      (except as stated in this section) patent license to make, have made,
      use, offer to sell, sell, import, and otherwise transfer the Work,
      where such license applies only to those patent claims licensable
      by such Contributor that are necessarily infringed by their
      Contribution(s) alone or by combination of their Contribution(s)
      with the Work to which such Contribution(s) was submitted. If You
      institute patent litigation against any entity (including a
      cross-claim or counterclaim in a lawsuit) alleging that the Work
      or a Contribution incorporated within the Work constitutes direct
      or contributory patent infringement, then any patent licenses
      granted to You under this License for that Work shall terminate
      as of the date such litigation is filed.

   4. Redistribution. You may reproduce and distribute copies of the
      Work or Derivative Works thereof in any medium, with or without
      modifications, and in Source or Object form, provided that You
      meet the following conditions:

      (a) You must give any other recipients of the Work or
          Derivative Works a copy of this License; and

      (b) You must cause any modified files to carry prominent notices
          stating that You changed the files; and

      (c) You must retain, in the Source form of any Derivative Works
          that You distribute, all copyright, patent, trademark, and
          attribution notices from the Source form of the Work,
          excluding those notices that do not pertain to any part of
          the Derivative Works; and

      (d) If the Work includes a "NOTICE" text file as part of its
          distribution, then any Derivative Works that You distribute must
          include a readable copy of the attribution notices contained
          within such NOTICE file, excluding those notices that do not
          pertain to any part of the Derivative Works, in at least one
          of the following places: within a NOTICE text file distributed
          as part of the Derivative Works; within the Source form or
          documentation, if provided along with the Derivative Works; or,
          within a display generated by the Derivative Works, if and
          wherever such third-party notices normally appear. The contents
          of the NOTICE file are for informational purposes only and
          do not modify the License. You may add Your own attribution
          notices within Derivative Works that You distribute, alongside
          or as an addendum to the NOTICE text from the Work, provided
          that such additional attribution notices cannot be construed
          as modifying the License.

      You may add Your own copyright statement to Your modifications and
      may provide additional or different license terms and conditions
      for use, reproduction, or distribution of Your modifications, or
      for any such Derivative Works as a whole, provided Your use,
      reproduction, and distribution of the Work otherwise complies with
      the conditions stated in this License.

   5. Submission of Contributions. Unless You explicitly state otherwise,
      any Contribution intentionally submitted for inclusion in the Work
      by You to the Licensor shall be under the terms and conditions of
      this License, without any additional terms or conditions.
      Notwithstanding the above, nothing herein shall supersede or modify
      the terms of any separate license agreement you may have executed
      with Licensor regarding such Contributions.

   6. Trademarks. This License does not grant permission to use the trade
      names, trademarks, service marks, or product names of the Licensor,
      except as required for reasonable and customary use in describing the
      origin of the Work and reproducing the content of the NOTICE file.

   7. Disclaimer of Warranty. Unless required by applicable law or
      agreed to in writing, Licensor provides the Work (and each
      Contributor provides its Contributions) on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
      implied, including, without limitation, any warranties or conditions
      of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A
      PARTICULAR PURPOSE. You are solely responsible for determining the
      appropriateness of using or redistributing the Work and assume any
      risks associated with Your exercise of permissions under this License.

   8. Limitation of Liability. In no event and under no legal theory,
      whether in tort (including negligence), contract, or otherwise,
      unless required by applicable law (such as deliberate and grossly
      negligent acts) or agreed to in writing, shall any Contributor be
      liable to You for damages, including any direct, indirect, special,
      incidental, or consequential damages of any character arising as a
      result of this License or out of the use or inability to use the
      Work (including but not limited to damages for loss of goodwill,
      work stoppage, computer failure or malfunction, or any and all
      other commercial damages or losses), even if such Contributor
      has been advised of the possibility of such damages.

   9. Accepting Warranty or Additional Liability. While redistributing
      the Work or Derivative Works thereof, You may choose to offer,
      and charge a fee for, acceptance of support, warranty, indemnity,
      or other liability obligations and/or rights consistent with this
      License. However, in accepting such obligations, You may act only
      on Your own behalf and on Your sole responsibility, not on behalf
      of any other Contributor, and only if You agree to indemnify,
      defend, and hold each Contributor harmless for any liability
      incurred by, or claims asserted against, such Contributor by reason
      of your accepting any such warranty or additional liability.

   END OF TERMS AND CONDITIONS
                                 Apache License
                           Version 2.0, January 2004
                        http://www.apache.org/licenses/

   TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

   1. Definitions.

      "License" shall mean the terms and conditions for use, reproduction,
      and distribution as defined by Sections 1 through 9 of this document.

      "Licensor" shall mean the copyright owner or entity authorized by
      the copyright owner that is granting the License.

      "Legal Entity" shall mean the union of the acting entity and all
      other entities that control, are controlled by, or are under common
      control with that entity. For the purposes of this definition,
      "control" means (i) the power, direct or indirect, to cause the
      direction or management of such entity, whether by contract or
      otherwise, or (ii) ownership of fifty percent (50%) or more of the
      outstanding shares, or (iii) beneficial ownership of such entity.

      "You" (or "Your") shall mean an individual or Legal Entity
      exercising permissions granted by this License.

      "Source" form shall mean the preferred form for making modifications,
      including but not limited to software source code, documentation
      source, and configuration files.

      "Object" form shall mean any form resulting from mechanical
      transformation or translation of a Source form, including but
      not limited to compiled object code, generated documentation,
      and conversions to other media types.

      "Work" shall mean the work of authorship, whether in Source or
      Object form, made available under the License, as indicated by a
      copyright notice that is included in or attached to the work
      (an example is provided in the Appendix below).

      "Derivative Works" shall mean any work, whether in Source or Object
      form, that is based on (or derived from) the Work and for which the
      editorial revisions, annotations, elaborations, or other modifications
      represent, as a whole, an original work of authorship. For the purposes
      of this License, Derivative Works shall not include works that remain
      separable from, or merely link (or bind by name) to the interfaces of,
      the Work and Derivative Works thereof.

      "Contribution" shall mean any work of authorship, including
      the original version of the Work and any modifications or additions
      to that Work or Derivative Works thereof, that is intentionally
      submitted to Licensor for inclusion in the Work by the copyright owner
      or by an individual or Legal Entity authorized to submit on behalf of
      the copyright owner. For the purposes of this definition, "submitted"
      means any form of electronic, verbal, or written communication sent
      to the Licensor or its representatives, including but not limited to
      communication on electronic mailing lists, source code control systems,
      and issue tracking systems that are managed by, or on behalf of, the
      Licensor for the purpose of discussing and improving the Work, but
      excluding communication that is conspicuously marked or otherwise
      designated in writing by the copyright owner as "Not a Contribution."

      "Contributor" shall mean Licensor and any individual or Legal Entity
      on behalf of whom a Contribution has been received by Licensor and
      subsequently incorporated within the Work.

   2. Grant of Copyright License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      copyright license to reproduce, prepare Derivative Works of,
      publicly display, publicly perform, sublicense, and distribute the
      Work and such Derivative Works in Source or Object form.

   3. Grant of Patent License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      (except as stated in this section) patent license to make, have made,
      use, offer to sell, sell, import, and otherwise transfer the Work,
      where such license applies only to those patent claims licensable
      by such Contributor that are necessarily infringed by their
      Contribution(s) alone or by combination of their Contribution(s)
      with the Work to which such Contribution(s) was submitted. If You
      institute patent litigation against any entity (including a
      cross-claim or counterclaim in a lawsuit) alleging that the Work
      or a Contribution incorporated within the Work constitutes direct
      or contributory patent infringement, then any patent licenses
      granted to You under this License for that Work shall terminate
      as of the date such litigation is filed.

   4. Redistribution. You may reproduce and distribute copies of the
      Work or Derivative Works thereof in any medium, with or without
      modifications, and in Source or Object form, provided that You
      meet the following conditions:

      (a) You must give any other recipients of the Work or
          Derivative Works a copy of this License; and

      (b) You must cause any modified files to carry prominent notices
          stating that You changed the files; and

      (c) You must retain, in the Source form of any Derivative Works
          that You distribute, all copyright, patent, trademark, and
          attribution notices from the Source form of the Work,
          excluding those notices that do not pertain to any part of
          the Derivative Works; and

      (d) If the Work includes a "NOTICE" text file as part of its
          distribution, then any Derivative Works that You distribute must
          include a readable copy of the attribution notices contained
          within such NOTICE file, excluding those notices that do not
          pertain to any part of the Derivative Works, in at least one
          of the following places: within a NOTICE text file distributed
          as part of the Derivative Works; within the Source form or
          documentation, if provided along with the Derivative Works; or,
          within a display generated by the Derivative Works, if and
          wherever such third-party notices normally appear. The contents
          of the NOTICE file are for informational purposes only and
          do not modify the License. You may add Your own attribution
          notices within Derivative Works that You distribute, alongside
          or as an addendum to the NOTICE text from the Work, provided
          that such additional attribution notices cannot be construed
          as modifying the License.

      You may add Your own copyright statement to Your modifications and
      may provide additional or different license terms and conditions
      for use, reproduction, or distribution of Your modifications, or
      for any such Derivative Works as a whole, provided Your use,
      reproduction, and distribution of the Work otherwise complies with
      the conditions stated in this License.

   5. Submission of Contributions. Unless You explicitly state otherwise,
      any Contribution intentionally submitted for inclusion in the Work
      by You to the Licensor shall be under the terms and conditions of
      this License, without any additional terms or conditions.
      Notwithstanding the above, nothing herein shall supersede or modify
      the terms of any separate license agreement you may have executed
      with Licensor regarding such Contributions.

   6. Trademarks. This License does not grant permission to use the trade
      names, trademarks, service marks, or product names of the Licensor,
      except as required for reasonable and customary use in describing the
      origin of the Work and reproducing the content of the NOTICE file.

   7. Disclaimer of Warranty. Unless required by applicable law or
      agreed to in writing, Licensor provides the Work (and each
      Contributor provides its Contributions) on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
      implied, including, without limitation, any warranties or conditions
      of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A
      PARTICULAR PURPOSE. You are solely responsible for determining the
      appropriateness of using or redistributing the Work and assume any
      risks associated with Your exercise of permissions under this License.

   8. Limitation of Liability. In no event and under no legal theory,
      whether in tort (including negligence), contract, or otherwise,
      unless required by applicable law (such as deliberate and grossly
      negligent acts) or agreed to in writing, shall any Contributor be
      liable to You for damages, including any direct, indirect, special,
      incidental, or consequential damages of any character arising as a
      result of this License or out of the use or inability to use the
      Work (including but not limited to damages for loss of goodwill,
      work stoppage, computer failure or malfunction, or any and all
      other commercial damages or losses), even if such Contributor
      has been advised of the possibility of such damages.

   9. Accepting Warranty or Additional Liability. While redistributing
      the Work or Derivative Works thereof, You may choose to offer,
      and charge a fee for, acceptance of support, warranty, indemnity,
      or other liability obligations and/or rights consistent with this
      License. However, in accepting such obligations, You may act only
      on Your own behalf and on Your sole responsibility, not on behalf
      of any other Contributor, and only if You agree to indemnify,
      defend, and hold each Contributor harmless for any liability
      incurred by, or claims asserted against, such Contributor by reason
      of your accepting any such warranty or additional liability.

   END OF TERMS AND CONDITIONS
# webcam-capture-driver-jmf

This is capture driver which gives Webcam Capture API
possibility to use [JMF](http://www.oracle.com/technetwork/java/javase/download-142937.html)
(Java Media Framework) as a middleware accessing webcam devices 
(those build-in and USB enabled). The JMF needs to be installed 
and configured on the PC before this driver can be used.

It can also be used with the alternative [FMJ](http://fmj-sf.net/).

## Download

The latest **development** version JAR (aka SNAPSHOT) can be downloaded [here](https://oss.sonatype.org/service/local/artifact/maven/redirect?r=snapshots&g=com.github.sarxos&a=webcam-capture-driver-jmf&v=0.3.13-SNAPSHOT).

The latest **stable** version ZIP bundle can be downloaded [here](http://repo.sarxos.pl/maven2/com/github/sarxos/webcam-capture-driver-jmf/0.3.12/webcam-capture-driver-jmf-0.3.12-dist.zip).


## Maven

Release:

```xml
<dependency>
	<groupId>com.github.sarxos</groupId>
	<artifactId>webcam-capture-driver-jmf</artifactId>
	<version>0.3.12</version>
</dependency>
```

Stable:

```xml
<repository>
	<id>SarXos Repository</id>
	<url>http://www.sarxos.pl/repo/maven2</url>
</repository>
```
```xml
<dependency>
	<groupId>com.github.sarxos</groupId>
	<artifactId>webcam-capture-driver-jmf</artifactId>
	<version>0.3.13-SNAPSHOT</version>
</dependency>
```

Snapshot:

```xml
<repository>
    <id>Sonatype OSS Snapshot Repository</id>
    <url>http://oss.sonatype.org/content/repositories/snapshots</url>
</repository>
```
```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-jmf</artifactId>
    <version>0.3.10-SNAPSHOT</version>
</dependency>
```

## Example

```java
static {
	Webcam.setDriver(new JmfDriver());
}

public static void main(String[] args) {
	JFrame frame = new JFrame("JMF Webcam Capture Driver Demo");
	frame.add(new WebcamPanel(Webcam.getDefault()));
	frame.pack();
	frame.setVisible(true);
	frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
}
```

## License

Copyright (C) 2012 - 2017 Bartosz Firyn

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

Oracle Binary Code License Agreement for Java SE and JavaFX Technologies

 

ORACLE  AMERICA, INC. ("ORACLE"), FOR AND ON BEHALF OF ITSELF AND ITS SUBSIDIARIES AND AFFILIATES UNDER COMMON CONTROL, IS WILLING TO  LICENSE  THE SOFTWARE  TO YOU ONLY UPON THE CONDITION THAT YOU ACCEPT ALL OF THE TERMS CONTAINED IN THIS BINARY CODE LICENSE AGREEMENT AND SUPPLEMENTAL  LICENSE TERMS (COLLECTIVELY "AGREEMENT").  PLEASE READ THE AGREEMENT CAREFULLY.  BY SELECTING THE "ACCEPT LICENSE AGREEMENT" (OR THE EQUIVALENT) BUTTON AND/OR BY USING THE SOFTWARE YOU ACKNOWLEDGE THAT YOU HAVE READ THE TERMS AND AGREE TO THEM.  IF YOU ARE AGREEING TO THESE TERMS ON BEHALF OF A COMPANY OR OTHER LEGAL ENTITY, YOU REPRESENT THAT YOU HAVE THE LEGAL AUTHORITY TO BIND THE LEGAL ENTITY TO THESE TERMS.  IF YOU DO NOT HAVE SUCH AUTHORITY, OR IF YOU DO NOT WISH TO BE BOUND BY THE TERMS, THEN SELECT THE "DECLINE LICENSE AGREEMENT" (OR THE EQUIVALENT) BUTTON AND YOU MUST NOT USE THE SOFTWARE ON THIS SITE OR ANY OTHER MEDIA ON WHICH THE SOFTWARE IS CONTAINED.

 

1.  DEFINITIONS.  "Software" means the software identified above in binary form that you selected for download, install or use (in the version You selected for download, install or use) from Oracle or its authorized licensees, any other machine readable materials (including, but not limited to,  libraries,  source  files,  header  files, and data  files), any updates or error corrections provided by Oracle, and any user manuals, programming guides and other documentation provided to you by Oracle under this Agreement.  "General Purpose Desktop Computers and Servers" means computers, including desktop and laptop computers, or servers, used for general computing functions under end user control (such as but not specifically limited to email, general purpose Internet browsing, and office suite productivity tools).  The use of Software in systems and solutions that provide dedicated functionality (other than as mentioned above) or designed for use in embedded or function-specific software applications, for example but not limited to: Software embedded in or bundled with industrial control systems, wireless mobile telephones, wireless handheld devices, netbooks, kiosks, TV/STB, Blu-ray Disc devices, telematics and network control switching equipment, printers and storage management systems, and other related systems are excluded from this definition and not licensed under this Agreement.  "Programs" means: (a) Java technology applets and applications intended to run on the Java Platform, Standard Edition platform on Java-enabled General Purpose Desktop Computers and Servers, and (b) JavaFX technology applications intended to run on the JavaFX Runtime on JavaFX-enabled General Purpose Desktop Computers and Servers.    “README File” means the README file for the Software set forth in the Software or otherwise available from Oracle at or through the following URL: http://www.oracle.com/technetwork/java/javase/documentation/index.html

 

2.  LICENSE TO USE.  Subject to the terms and conditions of this Agreement including, but not limited to, the Java Technology Restrictions of the Supplemental License Terms, Oracle grants you a non-exclusive, non-transferable, limited license without license fees to reproduce and use internally the Software complete and unmodified for the sole purpose of running Programs.

 

3.  RESTRICTIONS.  Software is copyrighted.  Title to Software and all associated intellectual property rights is retained by Oracle and/or its licensors.  Unless enforcement is prohibited by applicable law, you may not modify, decompile, or reverse engineer Software.  You acknowledge that the Software is developed for general use in a variety of information management applications; it is not developed or intended for use in any inherently dangerous applications, including applications that may create a risk of personal injury. If you use the Software in dangerous applications, then you shall be responsible to take all appropriate fail-safe, backup, redundancy, and other measures to ensure its safe use.  Oracle disclaims any express or implied warranty of fitness for such uses.  No right, title or interest in or to any trademark, service mark, logo or trade name of Oracle or its licensors is granted under this Agreement.  Additional restrictions for developers and/or publishers licenses are set forth in the Supplemental License Terms.

 

4.  DISCLAIMER OF WARRANTY.  THE SOFTWARE IS PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND.  ORACLE FURTHER DISCLAIMS ALL WARRANTIES, EXPRESS AND IMPLIED, INCLUDING WITHOUT LIMITATION, ANY IMPLIED WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE OR NONINFRINGEMENT.

 

5.  LIMITATION OF LIABILITY.  IN NO EVENT SHALL ORACLE BE LIABLE FOR ANY INDIRECT, INCIDENTAL, SPECIAL, PUNITIVE OR CONSEQUENTIAL DAMAGES, OR DAMAGES FOR LOSS OF PROFITS, REVENUE, DATA OR DATA USE, INCURRED BY YOU OR ANY THIRD PARTY, WHETHER IN AN ACTION IN CONTRACT OR TORT, EVEN IF ORACLE HAS BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGES. ORACLE'S ENTIRE LIABILITY FOR DAMAGES HEREUNDER SHALL IN NO EVENT EXCEED ONE THOUSAND DOLLARS (U.S. $1,000).

 

6.  TERMINATION.  This Agreement is effective until terminated.  You may terminate this Agreement at any time by destroying all copies of Software.  This Agreement will terminate immediately without notice from Oracle if you fail to comply with any provision of this Agreement.  Either party may terminate this Agreement immediately should any Software become, or in either party's opinion be likely to become, the subject of a claim of infringement of any intellectual property right.  Upon termination, you must destroy all copies of Software.

 

7.  EXPORT REGULATIONS.  You agree that U.S. export control laws and other applicable export and import laws govern your use of the Software, including technical data; additional information can be found on Oracle's Global Trade Compliance web site (http://www.oracle.com/products/export). You agree that neither the Software nor any direct product thereof will be exported, directly, or indirectly, in violation of these laws, or will be used for any purpose prohibited by these laws including, without limitation, nuclear, chemical, or biological weapons proliferation. 

 

8.  TRADEMARKS AND LOGOS.  You acknowledge and agree as between you and Oracle that Oracle owns the ORACLE and JAVA trademarks and all ORACLE- and JAVA-related trademarks, service marks, logos and other brand designations ("Oracle Marks"), and you agree to comply with the Third Party Usage Guidelines for Oracle Trademarks currently located at http://www.oracle.com/us/legal/third-party-trademarks/index.html.  Any use you make of the Oracle Marks inures to Oracle's benefit.

 

9.  U.S. GOVERNMENT LICENSE RIGHTS.  If Software is being acquired by or on behalf of the U.S. Government or by a U.S. Government prime contractor or subcontractor (at any tier), then the Government's rights in Software and accompanying documentation shall be only those set forth in this Agreement. 

 

10.  GOVERNING LAW.  This agreement is governed by the substantive and procedural laws of California. You and Oracle agree to submit to the exclusive jurisdiction of, and venue in, the courts of San Francisco, or Santa Clara counties in California in any dispute arising out of or relating to this agreement. 

 

11.  SEVERABILITY.  If any provision of this Agreement is held to be unenforceable, this Agreement will remain in effect with the provision omitted, unless omission would frustrate the intent of the parties, in which case this Agreement will immediately terminate.

 

12.  INTEGRATION.  This Agreement is the entire agreement between you and Oracle relating to its subject matter.  It supersedes all prior or contemporaneous oral or written communications, proposals, representations and warranties and prevails over any conflicting or additional terms of any quote, order, acknowledgment, or other communication between the parties relating to its subject matter during the term of this Agreement.  No modification of this Agreement will be binding, unless in writing and signed by an authorized representative of each party.

 

SUPPLEMENTAL LICENSE TERMS

 

These Supplemental License Terms add to or modify the terms of the Binary Code License Agreement.  Capitalized terms not defined in these Supplemental Terms shall have the same meanings ascribed to them in the Binary Code License Agreement.  These Supplemental Terms shall supersede any inconsistent or conflicting terms in the Binary Code License Agreement, or in any license contained within the Software.

 

A.  SOFTWARE INTERNAL USE FOR DEVELOPMENT LICENSE GRANT.  Subject to the terms and conditions of this Agreement and restrictions and exceptions set forth in the README File incorporated herein by reference, including, but not limited to the Java Technology Restrictions of these Supplemental Terms, Oracle grants you a non-exclusive, non-transferable, limited license without fees to reproduce internally and use internally the Software complete and unmodified for the purpose of designing, developing, and testing your Programs.

 

B.  LICENSE TO DISTRIBUTE SOFTWARE.  Subject to the terms and conditions of this Agreement and restrictions and exceptions set forth in the README File, including, but not limited to the Java Technology Restrictions of these Supplemental Terms, Oracle grants you a non-exclusive, non-transferable, limited license without fees to reproduce and distribute the Software, provided that (i) you distribute the Software complete and  unmodified and only bundled as part of, and for the sole purpose of running, your Programs, (ii) the Programs add significant and primary functionality  to the Software, (iii) you do not distribute additional  software intended to replace any component(s) of the Software, (iv) you do not remove or alter any proprietary legends or notices contained in the Software, (v) you only distribute the Software subject to a license agreement that protects Oracle's  interests consistent with the terms contained in this Agreement, and (vi) you agree to defend and indemnify Oracle and its licensors from and against any damages, costs, liabilities, settlement amounts and/or expenses (including  attorneys' fees)  incurred in connection  with any claim, lawsuit or action by any third party that arises or results from the use or distribution of any and all Programs and/or Software.   The license set forth in this Section B does not extend to the Software identified in Section D.

 

C.  LICENSE TO DISTRIBUTE REDISTRIBUTABLES.  Subject to the terms and conditions of this Agreement and restrictions and exceptions set forth in the README  File, including but not limited to the Java Technology Restrictions of these Supplemental Terms, Oracle grants you a non-exclusive,  non-transferable, limited license without fees to reproduce and distribute  those files specifically identified as redistributable in the README File ("Redistributables") provided that: (i) you distribute the Redistributables complete and unmodified, and only bundled as part of Programs, (ii) the Programs add significant and primary functionality to the  Redistributables, (iii) you do not distribute additional software intended to supersede any component(s) of the Redistributables (unless otherwise specified in the applicable README File), (iv) you do not remove or alter any proprietary legends or notices contained in or on the Redistributables, (v)  you only distribute the Redistributables pursuant to a license agreement  that protects Oracle's interests consistent with the terms contained in the Agreement, (vi) you agree to defend and indemnify Oracle and its licensors from and against any damages,  costs, liabilities, settlement amounts and/or expenses (including  attorneys'  fees) incurred in connection with any claim, lawsuit or action by any third  party that arises or results from the use or distribution of any and all Programs and/or Software.  The license set forth in this Section C does not extend to the Software identified in Section D.

 

D.  JAVA TECHNOLOGY RESTRICTIONS.  You may not create, modify, or change the behavior of, or authorize your licensees to create, modify, or change the behavior of, classes, interfaces, or subpackages that are in any way  identified  as  "java", "javax", "javafx", "sun", “oracle” or similar convention as   specified by Oracle in any naming convention designation. You shall not redistribute the Software listed on Schedule 1.

 

E.  SOURCE CODE.  Software may contain source code that, unless expressly licensed for other purposes, is provided solely for reference purposes pursuant to the terms of this Agreement.  Source code may not be redistributed unless expressly provided for in this Agreement.

 

F.  THIRD PARTY CODE.  Additional copyright notices and license terms applicable to portions of the Software are set forth in the THIRDPARTYLICENSEREADME file set forth in the Software or otherwise available from Oracle at or through the following URL: http://www.oracle.com/technetwork/java/javase/documentation/index.html.  In addition to any terms and conditions of any third party opensource/freeware license identified in the THIRDPARTYLICENSEREADME file, the disclaimer of warranty and limitation of liability provisions in paragraphs 4 and 5 of the Binary Code License Agreement shall apply to all Software in this distribution.

 

G.  TERMINATION FOR INFRINGEMENT.  Either party may terminate this Agreement immediately should any Software become, or in either party's opinion be likely to become, the subject of a claim of infringement of any intellectual property right.

 

H.  INSTALLATION AND AUTO-UPDATE.  The Software's installation and auto-update processes transmit a limited amount of data to Oracle (or its service provider) about those specific processes to help Oracle understand and optimize them.  Oracle does not associate the data with personally identifiable information.  You can find more information about the data Oracle collects as a result of your Software download at http://www.oracle.com/technetwork/java/javase/documentation/index.html.

 

For inquiries please contact:  Oracle America, Inc., 500 Oracle Parkway,

Redwood Shores, California 94065, USA.

 

License for Archived Java SE Technologies; Last updated 13 March 2012

Schedule 1 to Supplemental Terms

Non-redistributable Java Technologies

 

JavaFX Runtime

 

JavaFX Development Kit

 

JavaFX Production Suite

 

Java Naming and Directory Interface(TM)

Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files

jvmstat# webcam-capture-driver-lti-civil

This is webcam capture driver designed to leverage capabilities of
[LTI-CIVIL](http://sourceforge.net/projects/lti-civil/) project by Larson Technologies Inc. 
and use it to access wide range of UVC devices which can be build-in or connected
with the USB cable.

Although, the LTI-CIVIL works with Mac OS as well as with Linux or Windows, this driver 
has been designed for Linux and Windows only (32- and 64-bit). This is because I
do not have Mac OS machine to perform tests.

## NOTES

* LTI-CIVIL does not work on Ubuntu 12.04 on x86_64!

## Download

The latest **development** version JAR (aka SNAPSHOT) can be downloaded [here](https://oss.sonatype.org/service/local/artifact/maven/redirect?r=snapshots&g=com.github.sarxos&a=webcam-capture-driver-lti-civil&v=0.3.13-SNAPSHOT).

The latest **stable** version ZIP bundle can be downloaded [here](http://repo.sarxos.pl/maven2/com/github/sarxos/webcam-capture-driver-lti-civil/0.3.12/webcam-capture-driver-lti-civil-0.3.12-dist.zip).

## Maven

Stable:

```xml
<dependency>
	<groupId>com.github.sarxos</groupId>
	<artifactId>webcam-capture-driver-lti-civil</artifactId>
	<version>0.3.12</version>
</dependency>
```

Snapshot:

```xml
<repository>
    <id>Sonatype OSS Snapshot Repository</id>
    <url>http://oss.sonatype.org/content/repositories/snapshots</url>
</repository>
```
```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-lti-civil</artifactId>
    <version>0.3.13-SNAPSHOT</version>
</dependency>
```

## How To Use It

```java
static {
	Webcam.setDriver(new LtiCivilDriver());
}

public static void main(String[] args) {

	WebcamPanel panel = new WebcamPanel(Webcam.getWebcams().get(0));
	panel.setFPSDisplayed(true);

	JFrame frame = new JFrame("LTI-CIVIL Webcam Capture Driver Demo");
	frame.add(panel);
	frame.pack();
	frame.setVisible(true);
	frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
}
```

## Webcam Capture Driver License

Copyright (C) 2012 - 2017 Bartosz Firyn and contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## LTI-CIVIL Binaries License

[GNU Lesser General Public License, version 3.0](http://lti-civil.cvs.sourceforge.net/viewvc/lti-civil/lti-civil/LICENSE?revision=1.1&view=markup)
		   GNU LESSER GENERAL PUBLIC LICENSE
                       Version 3, 29 June 2007

 Copyright (C) 2007 Free Software Foundation, Inc. <http://fsf.org/>
 Everyone is permitted to copy and distribute verbatim copies
 of this license document, but changing it is not allowed.


  This version of the GNU Lesser General Public License incorporates
the terms and conditions of version 3 of the GNU General Public
License, supplemented by the additional permissions listed below.

  0. Additional Definitions. 

  As used herein, "this License" refers to version 3 of the GNU Lesser
General Public License, and the "GNU GPL" refers to version 3 of the GNU
General Public License.

  "The Library" refers to a covered work governed by this License,
other than an Application or a Combined Work as defined below.

  An "Application" is any work that makes use of an interface provided
by the Library, but which is not otherwise based on the Library.
Defining a subclass of a class defined by the Library is deemed a mode
of using an interface provided by the Library.

  A "Combined Work" is a work produced by combining or linking an
Application with the Library.  The particular version of the Library
with which the Combined Work was made is also called the "Linked
Version".

  The "Minimal Corresponding Source" for a Combined Work means the
Corresponding Source for the Combined Work, excluding any source code
for portions of the Combined Work that, considered in isolation, are
based on the Application, and not on the Linked Version.

  The "Corresponding Application Code" for a Combined Work means the
object code and/or source code for the Application, including any data
and utility programs needed for reproducing the Combined Work from the
Application, but excluding the System Libraries of the Combined Work.

  1. Exception to Section 3 of the GNU GPL.

  You may convey a covered work under sections 3 and 4 of this License
without being bound by section 3 of the GNU GPL.

  2. Conveying Modified Versions.

  If you modify a copy of the Library, and, in your modifications, a
facility refers to a function or data to be supplied by an Application
that uses the facility (other than as an argument passed when the
facility is invoked), then you may convey a copy of the modified
version:

   a) under this License, provided that you make a good faith effort to
   ensure that, in the event an Application does not supply the
   function or data, the facility still operates, and performs
   whatever part of its purpose remains meaningful, or

   b) under the GNU GPL, with none of the additional permissions of
   this License applicable to that copy.

  3. Object Code Incorporating Material from Library Header Files.

  The object code form of an Application may incorporate material from
a header file that is part of the Library.  You may convey such object
code under terms of your choice, provided that, if the incorporated
material is not limited to numerical parameters, data structure
layouts and accessors, or small macros, inline functions and templates
(ten or fewer lines in length), you do both of the following:

   a) Give prominent notice with each copy of the object code that the
   Library is used in it and that the Library and its use are
   covered by this License.

   b) Accompany the object code with a copy of the GNU GPL and this license
   document.

  4. Combined Works.

  You may convey a Combined Work under terms of your choice that,
taken together, effectively do not restrict modification of the
portions of the Library contained in the Combined Work and reverse
engineering for debugging such modifications, if you also do each of
the following:

   a) Give prominent notice with each copy of the Combined Work that
   the Library is used in it and that the Library and its use are
   covered by this License.

   b) Accompany the Combined Work with a copy of the GNU GPL and this license
   document.

   c) For a Combined Work that displays copyright notices during
   execution, include the copyright notice for the Library among
   these notices, as well as a reference directing the user to the
   copies of the GNU GPL and this license document.

   d) Do one of the following:

       0) Convey the Minimal Corresponding Source under the terms of this
       License, and the Corresponding Application Code in a form
       suitable for, and under terms that permit, the user to
       recombine or relink the Application with a modified version of
       the Linked Version to produce a modified Combined Work, in the
       manner specified by section 6 of the GNU GPL for conveying
       Corresponding Source.

       1) Use a suitable shared library mechanism for linking with the
       Library.  A suitable mechanism is one that (a) uses at run time
       a copy of the Library already present on the user's computer
       system, and (b) will operate properly with a modified version
       of the Library that is interface-compatible with the Linked
       Version. 

   e) Provide Installation Information, but only if you would otherwise
   be required to provide such information under section 6 of the
   GNU GPL, and only to the extent that such information is
   necessary to install and execute a modified version of the
   Combined Work produced by recombining or relinking the
   Application with a modified version of the Linked Version. (If
   you use option 4d0, the Installation Information must accompany
   the Minimal Corresponding Source and Corresponding Application
   Code. If you use option 4d1, you must provide the Installation
   Information in the manner specified by section 6 of the GNU GPL
   for conveying Corresponding Source.)

  5. Combined Libraries.

  You may place library facilities that are a work based on the
Library side by side in a single library together with other library
facilities that are not Applications and are not covered by this
License, and convey such a combined library under terms of your
choice, if you do both of the following:

   a) Accompany the combined library with a copy of the same work based
   on the Library, uncombined with any other library facilities,
   conveyed under the terms of this License.

   b) Give prominent notice with the combined library that part of it
   is a work based on the Library, and explaining where to find the
   accompanying uncombined form of the same work.

  6. Revised Versions of the GNU Lesser General Public License.

  The Free Software Foundation may publish revised and/or new versions
of the GNU Lesser General Public License from time to time. Such new
versions will be similar in spirit to the present version, but may
differ in detail to address new problems or concerns.

  Each version is given a distinguishing version number. If the
Library as you received it specifies that a certain numbered version
of the GNU Lesser General Public License "or any later version"
applies to it, you have the option of following the terms and
conditions either of that published version or of any later version
published by the Free Software Foundation. If the Library as you
received it does not specify a version number of the GNU Lesser
General Public License, you may choose any version of the GNU Lesser
General Public License ever published by the Free Software Foundation.

  If the Library as you received it specifies that a proxy can decide
whether future versions of the GNU Lesser General Public License shall
apply, that proxy's public statement of acceptance of any version is
permanent authorization for you to choose that version for the
Library.		   GNU LESSER GENERAL PUBLIC LICENSE
                       Version 3, 29 June 2007

 Copyright (C) 2007 Free Software Foundation, Inc. <http://fsf.org/>
 Everyone is permitted to copy and distribute verbatim copies
 of this license document, but changing it is not allowed.


  This version of the GNU Lesser General Public License incorporates
the terms and conditions of version 3 of the GNU General Public
License, supplemented by the additional permissions listed below.

  0. Additional Definitions. 

  As used herein, "this License" refers to version 3 of the GNU Lesser
General Public License, and the "GNU GPL" refers to version 3 of the GNU
General Public License.

  "The Library" refers to a covered work governed by this License,
other than an Application or a Combined Work as defined below.

  An "Application" is any work that makes use of an interface provided
by the Library, but which is not otherwise based on the Library.
Defining a subclass of a class defined by the Library is deemed a mode
of using an interface provided by the Library.

  A "Combined Work" is a work produced by combining or linking an
Application with the Library.  The particular version of the Library
with which the Combined Work was made is also called the "Linked
Version".

  The "Minimal Corresponding Source" for a Combined Work means the
Corresponding Source for the Combined Work, excluding any source code
for portions of the Combined Work that, considered in isolation, are
based on the Application, and not on the Linked Version.

  The "Corresponding Application Code" for a Combined Work means the
object code and/or source code for the Application, including any data
and utility programs needed for reproducing the Combined Work from the
Application, but excluding the System Libraries of the Combined Work.

  1. Exception to Section 3 of the GNU GPL.

  You may convey a covered work under sections 3 and 4 of this License
without being bound by section 3 of the GNU GPL.

  2. Conveying Modified Versions.

  If you modify a copy of the Library, and, in your modifications, a
facility refers to a function or data to be supplied by an Application
that uses the facility (other than as an argument passed when the
facility is invoked), then you may convey a copy of the modified
version:

   a) under this License, provided that you make a good faith effort to
   ensure that, in the event an Application does not supply the
   function or data, the facility still operates, and performs
   whatever part of its purpose remains meaningful, or

   b) under the GNU GPL, with none of the additional permissions of
   this License applicable to that copy.

  3. Object Code Incorporating Material from Library Header Files.

  The object code form of an Application may incorporate material from
a header file that is part of the Library.  You may convey such object
code under terms of your choice, provided that, if the incorporated
material is not limited to numerical parameters, data structure
layouts and accessors, or small macros, inline functions and templates
(ten or fewer lines in length), you do both of the following:

   a) Give prominent notice with each copy of the object code that the
   Library is used in it and that the Library and its use are
   covered by this License.

   b) Accompany the object code with a copy of the GNU GPL and this license
   document.

  4. Combined Works.

  You may convey a Combined Work under terms of your choice that,
taken together, effectively do not restrict modification of the
portions of the Library contained in the Combined Work and reverse
engineering for debugging such modifications, if you also do each of
the following:

   a) Give prominent notice with each copy of the Combined Work that
   the Library is used in it and that the Library and its use are
   covered by this License.

   b) Accompany the Combined Work with a copy of the GNU GPL and this license
   document.

   c) For a Combined Work that displays copyright notices during
   execution, include the copyright notice for the Library among
   these notices, as well as a reference directing the user to the
   copies of the GNU GPL and this license document.

   d) Do one of the following:

       0) Convey the Minimal Corresponding Source under the terms of this
       License, and the Corresponding Application Code in a form
       suitable for, and under terms that permit, the user to
       recombine or relink the Application with a modified version of
       the Linked Version to produce a modified Combined Work, in the
       manner specified by section 6 of the GNU GPL for conveying
       Corresponding Source.

       1) Use a suitable shared library mechanism for linking with the
       Library.  A suitable mechanism is one that (a) uses at run time
       a copy of the Library already present on the user's computer
       system, and (b) will operate properly with a modified version
       of the Library that is interface-compatible with the Linked
       Version. 

   e) Provide Installation Information, but only if you would otherwise
   be required to provide such information under section 6 of the
   GNU GPL, and only to the extent that such information is
   necessary to install and execute a modified version of the
   Combined Work produced by recombining or relinking the
   Application with a modified version of the Linked Version. (If
   you use option 4d0, the Installation Information must accompany
   the Minimal Corresponding Source and Corresponding Application
   Code. If you use option 4d1, you must provide the Installation
   Information in the manner specified by section 6 of the GNU GPL
   for conveying Corresponding Source.)

  5. Combined Libraries.

  You may place library facilities that are a work based on the
Library side by side in a single library together with other library
facilities that are not Applications and are not covered by this
License, and convey such a combined library under terms of your
choice, if you do both of the following:

   a) Accompany the combined library with a copy of the same work based
   on the Library, uncombined with any other library facilities,
   conveyed under the terms of this License.

   b) Give prominent notice with the combined library that part of it
   is a work based on the Library, and explaining where to find the
   accompanying uncombined form of the same work.

  6. Revised Versions of the GNU Lesser General Public License.

  The Free Software Foundation may publish revised and/or new versions
of the GNU Lesser General Public License from time to time. Such new
versions will be similar in spirit to the present version, but may
differ in detail to address new problems or concerns.

  Each version is given a distinguishing version number. If the
Library as you received it specifies that a certain numbered version
of the GNU Lesser General Public License "or any later version"
applies to it, you have the option of following the terms and
conditions either of that published version or of any later version
published by the Free Software Foundation. If the Library as you
received it does not specify a version number of the GNU Lesser
General Public License, you may choose any version of the GNU Lesser
General Public License ever published by the Free Software Foundation.

  If the Library as you received it specifies that a proxy can decide
whether future versions of the GNU Lesser General Public License shall
apply, that proxy's public statement of acceptance of any version is
permanent authorization for you to choose that version for the
Library.Native libraries for LTI-CIVIL has been taken from [this LTI-CIVIL patch](http://sourceforge.net/p/lti-civil/patches/4/)
submitted by [George Rhoten](http://sourceforge.net/u/blackdiamond/profile/) at 2012-04-23.

All can be found in the following ZIP files:

* [lti-civil-bin32.zip](http://sourceforge.net/p/lti-civil/patches/_discuss/thread/cb267e8d/6b31/attachment/lti-civil-bin32.zip)
* [lti-civil-bin64-linux.zip](http://sourceforge.net/p/lti-civil/patches/_discuss/thread/cb267e8d/6c3d/attachment/lti-civil-bin64-linux.zip)
* [lti-civil-bin64-windows.zip](http://sourceforge.net/p/lti-civil/patches/_discuss/thread/cb267e8d/9579/attachment/lti-civil-bin64-windows.zip)



# webcam-capture-driver-mjpeg

This is capture driver which is able to capture video feed from MJPEG stream. But how to create MJPEG stream? This can be done with GStreamer, FFMpeg or other tool. Streaming can be done by TCP, UDP, or even named pipe (FIFO).

### Streaming With GStreamer

Here is example of how GStreamer 1.x can be used to stream video feed as MJPEG on Raspberry Pi
or any other Linux system with gStreamer 1.x installed. This command should be executed on the
host computer (i.e. the server with connected webcam and from where we want to stream video feed).

```plain
$ gst-launch-1.0 -v v4l2src device=/dev/video0 \
  ! capsfilter caps="video/x-raw, width=640, height=480" \
  ! decodebin name=dec ! videoconvert ! jpegenc \
  ! multipartmux ! tcpserversink host=0.0.0.0 port=5000
``` 

The above will `/dev/video0` device (default webcam) to get video from and convert
individual frames to JPEG and then perform MIME multipart encoding to make it finally available
over TCP on port `5000`.

Expected command output is something like this:

```plain
$ gst-launch-1.0 -v v4l2src device=/dev/video0 ! decodebin name=dec ! videoconvert ! jpegenc ! multipartmux ! tcpserversink host=0.0.0.0 port=5000
Setting pipeline to PAUSED ...
/GstPipeline:pipeline0/GstTCPServerSink:tcpserversink0: current-port = 5000
Pipeline is live and does not need PREROLL ...
Setting pipeline to PLAYING ...
New clock: GstSystemClock
/GstPipeline:pipeline0/GstV4l2Src:v4l2src0.GstPad:src: caps = video/x-raw, format=(string)YUY2, width=(int)1280, height=(int)720, pixel-aspect-ratio=(fraction)1/1, interlace-mode=(string)progressive, framerate=(fraction)10/1
/GstPipeline:pipeline0/GstDecodeBin:dec.GstGhostPad:sink.GstProxyPad:proxypad0: caps = video/x-raw, format=(string)YUY2, width=(int)1280, height=(int)720, pixel-aspect-ratio=(fraction)1/1, interlace-mode=(string)progressive, framerate=(fraction)10/1
/GstPipeline:pipeline0/GstDecodeBin:dec/GstTypeFindElement:typefind.GstPad:src: caps = video/x-raw, format=(string)YUY2, width=(int)1280, height=(int)720, pixel-aspect-ratio=(fraction)1/1, interlace-mode=(string)progressive, framerate=(fraction)10/1
/GstPipeline:pipeline0/GstDecodeBin:dec/GstTypeFindElement:typefind.GstPad:sink: caps = video/x-raw, format=(string)YUY2, width=(int)1280, height=(int)720, pixel-aspect-ratio=(fraction)1/1, interlace-mode=(string)progressive, framerate=(fraction)10/1
/GstPipeline:pipeline0/GstDecodeBin:dec.GstGhostPad:sink: caps = video/x-raw, format=(string)YUY2, width=(int)1280, height=(int)720, pixel-aspect-ratio=(fraction)1/1, interlace-mode=(string)progressive, framerate=(fraction)10/1
/GstPipeline:pipeline0/GstVideoConvert:videoconvert0.GstPad:src: caps = video/x-raw, format=(string)YUY2, width=(int)1280, height=(int)720, pixel-aspect-ratio=(fraction)1/1, interlace-mode=(string)progressive, framerate=(fraction)10/1
/GstPipeline:pipeline0/GstJpegEnc:jpegenc0.GstPad:sink: caps = video/x-raw, format=(string)YUY2, width=(int)1280, height=(int)720, pixel-aspect-ratio=(fraction)1/1, interlace-mode=(string)progressive, framerate=(fraction)10/1
/GstPipeline:pipeline0/GstVideoConvert:videoconvert0.GstPad:sink: caps = video/x-raw, format=(string)YUY2, width=(int)1280, height=(int)720, pixel-aspect-ratio=(fraction)1/1, interlace-mode=(string)progressive, framerate=(fraction)10/1
/GstPipeline:pipeline0/GstDecodeBin:dec.GstDecodePad:src_0.GstProxyPad:proxypad1: caps = video/x-raw, format=(string)YUY2, width=(int)1280, height=(int)720, pixel-aspect-ratio=(fraction)1/1, interlace-mode=(string)progressive, framerate=(fraction)10/1
/GstPipeline:pipeline0/GstJpegEnc:jpegenc0.GstPad:src: caps = image/jpeg, sof-marker=(int)0, width=(int)1280, height=(int)720, pixel-aspect-ratio=(fraction)1/1, framerate=(fraction)10/1
/GstPipeline:pipeline0/GstMultipartMux:multipartmux0.GstPad:sink_0: caps = image/jpeg, sof-marker=(int)0, width=(int)1280, height=(int)720, pixel-aspect-ratio=(fraction)1/1, framerate=(fraction)10/1
/GstPipeline:pipeline0/GstMultipartMux:multipartmux0.GstPad:src: caps = multipart/x-mixed-replace, boundary=(string)ThisRandomString
/GstPipeline:pipeline0/GstTCPServerSink:tcpserversink0.GstPad:sink: caps = multipart/x-mixed-replace, boundary=(string)ThisRandomString
```

You can break streaming by pressing `Ctrl + C` or by closing your terminal. The best way to leave streaming open after terminal is closed is to use `nohup`, for example:

```plain
$ nohup gst-launch-1.0 -v v4l2src device=/dev/video0 ! \
  decodebin name=dec ! videoconvert ! \
  jpegenc ! multipartmux ! \
  tcpserversink host=0.0.0.0 port=5000 &
``` 

## Maven

<!--
Stable:

```xml
<dependency>
	<groupId>com.github.sarxos</groupId>
	<artifactId>webcam-capture-driver-mjpeg</artifactId>
	<version>0.3.12</version>
</dependency>
```
-->

Snapshot:

```xml
<repository>
    <id>Sonatype OSS Snapshot Repository</id>
    <url>http://oss.sonatype.org/content/repositories/snapshots</url>
</repository>
```
```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-mjpeg</artifactId>
    <version>0.3.13-SNAPSHOT</version>
</dependency>
```

## How To Use

Set capture driver before you start using Webcam class:

```java
import javax.swing.JFrame;

import com.github.sarxos.webcam.Webcam;
import com.github.sarxos.webcam.WebcamPanel;
import com.github.sarxos.webcam.ds.mjpeg.MjpegCaptureDriver;


public class WebcamPanelExample {

	static {
		Webcam.setDriver(new MjpegCaptureDriver()
			.withUri("tcp://127.0.0.1:5000") // this is your local host
			.withUri("tcp://192.168.1.12:5000")); // this is some remote host
	}

	public static void main(String[] args) throws InterruptedException {

		// run this from your terminal (as a single line, and remove dollar sign):

		// $ gst-launch-1.0 -v v4l2src device=/dev/video0 ! capsfilter caps="video/x-raw, width=320,
		// height=240" ! decodebin name=dec ! videoconvert ! jpegenc ! multipartmux ! tcpserversink
		// host=0.0.0.0 port=5000

		final Webcam webcam = Webcam.getDefault();

		final WebcamPanel panel = new WebcamPanel(webcam);
		panel.setFPSDisplayed(true);
		panel.setImageSizeDisplayed(true);
		panel.setMirrored(true);

		final JFrame window = new JFrame("MJPEG Streaming From TCP Socket");
		window.add(panel);
		window.setResizable(true);
		window.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		window.pack();
		window.setVisible(true);
	}
}
```

## Capture Driver License

Copyright (C) 2012 - 2018 Bartosz Firyn <https://github.com/sarxos> and contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

# webcam-capture-driver-opencv

This is capture driver which uses [JavaCV](https://github.com/bytedeco/javacv) 
interface to [OpenCV](http://opencv.org/) to access camera devices.

## Maven

Stable:

```xml
<dependency>
	<groupId>com.github.sarxos</groupId>
	<artifactId>webcam-capture-driver-javacv</artifactId>
	<version>0.3.12</version>
</dependency>
```

Snapshot:

```xml
<repository>
    <id>Sonatype OSS Snapshot Repository</id>
    <url>http://oss.sonatype.org/content/repositories/snapshots</url>
</repository>
```
```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-javacv</artifactId>
    <version>0.3.13-SNAPSHOT</version>
</dependency>
```

## Example

```java
static {
	Webcam.setDriver(new JavaCvDriver());
}

public static void main(String[] args) {
	JFrame frame = new JFrame("JavaCv Capture Driver Demo");
	frame.add(new WebcamPanel(Webcam.getDefault()));
	frame.pack();
	frame.setVisible(true);
	frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
}
```

## License

Copyright (C) 2012 - 2017 Bartosz Firyn

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

You may use this work under the terms of either the Apache License,
Version 2.0, or the GNU General Public License (GPL), either version 2,
or any later version, with "Classpath" exception (details below).

You don't have to do anything special to choose one license or the other
and you don't have to notify anyone which license you are using. You are
free to use this work in any project (even commercial projects) as long
as the copyright header is left intact.

===============================================================================

                                 Apache License
                           Version 2.0, January 2004
                        http://www.apache.org/licenses/

   TERMS AND CONDITIONS FOR USE, REPRODUCTION, AND DISTRIBUTION

   1. Definitions.

      "License" shall mean the terms and conditions for use, reproduction,
      and distribution as defined by Sections 1 through 9 of this document.

      "Licensor" shall mean the copyright owner or entity authorized by
      the copyright owner that is granting the License.

      "Legal Entity" shall mean the union of the acting entity and all
      other entities that control, are controlled by, or are under common
      control with that entity. For the purposes of this definition,
      "control" means (i) the power, direct or indirect, to cause the
      direction or management of such entity, whether by contract or
      otherwise, or (ii) ownership of fifty percent (50%) or more of the
      outstanding shares, or (iii) beneficial ownership of such entity.

      "You" (or "Your") shall mean an individual or Legal Entity
      exercising permissions granted by this License.

      "Source" form shall mean the preferred form for making modifications,
      including but not limited to software source code, documentation
      source, and configuration files.

      "Object" form shall mean any form resulting from mechanical
      transformation or translation of a Source form, including but
      not limited to compiled object code, generated documentation,
      and conversions to other media types.

      "Work" shall mean the work of authorship, whether in Source or
      Object form, made available under the License, as indicated by a
      copyright notice that is included in or attached to the work
      (an example is provided in the Appendix below).

      "Derivative Works" shall mean any work, whether in Source or Object
      form, that is based on (or derived from) the Work and for which the
      editorial revisions, annotations, elaborations, or other modifications
      represent, as a whole, an original work of authorship. For the purposes
      of this License, Derivative Works shall not include works that remain
      separable from, or merely link (or bind by name) to the interfaces of,
      the Work and Derivative Works thereof.

      "Contribution" shall mean any work of authorship, including
      the original version of the Work and any modifications or additions
      to that Work or Derivative Works thereof, that is intentionally
      submitted to Licensor for inclusion in the Work by the copyright owner
      or by an individual or Legal Entity authorized to submit on behalf of
      the copyright owner. For the purposes of this definition, "submitted"
      means any form of electronic, verbal, or written communication sent
      to the Licensor or its representatives, including but not limited to
      communication on electronic mailing lists, source code control systems,
      and issue tracking systems that are managed by, or on behalf of, the
      Licensor for the purpose of discussing and improving the Work, but
      excluding communication that is conspicuously marked or otherwise
      designated in writing by the copyright owner as "Not a Contribution."

      "Contributor" shall mean Licensor and any individual or Legal Entity
      on behalf of whom a Contribution has been received by Licensor and
      subsequently incorporated within the Work.

   2. Grant of Copyright License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      copyright license to reproduce, prepare Derivative Works of,
      publicly display, publicly perform, sublicense, and distribute the
      Work and such Derivative Works in Source or Object form.

   3. Grant of Patent License. Subject to the terms and conditions of
      this License, each Contributor hereby grants to You a perpetual,
      worldwide, non-exclusive, no-charge, royalty-free, irrevocable
      (except as stated in this section) patent license to make, have made,
      use, offer to sell, sell, import, and otherwise transfer the Work,
      where such license applies only to those patent claims licensable
      by such Contributor that are necessarily infringed by their
      Contribution(s) alone or by combination of their Contribution(s)
      with the Work to which such Contribution(s) was submitted. If You
      institute patent litigation against any entity (including a
      cross-claim or counterclaim in a lawsuit) alleging that the Work
      or a Contribution incorporated within the Work constitutes direct
      or contributory patent infringement, then any patent licenses
      granted to You under this License for that Work shall terminate
      as of the date such litigation is filed.

   4. Redistribution. You may reproduce and distribute copies of the
      Work or Derivative Works thereof in any medium, with or without
      modifications, and in Source or Object form, provided that You
      meet the following conditions:

      (a) You must give any other recipients of the Work or
          Derivative Works a copy of this License; and

      (b) You must cause any modified files to carry prominent notices
          stating that You changed the files; and

      (c) You must retain, in the Source form of any Derivative Works
          that You distribute, all copyright, patent, trademark, and
          attribution notices from the Source form of the Work,
          excluding those notices that do not pertain to any part of
          the Derivative Works; and

      (d) If the Work includes a "NOTICE" text file as part of its
          distribution, then any Derivative Works that You distribute must
          include a readable copy of the attribution notices contained
          within such NOTICE file, excluding those notices that do not
          pertain to any part of the Derivative Works, in at least one
          of the following places: within a NOTICE text file distributed
          as part of the Derivative Works; within the Source form or
          documentation, if provided along with the Derivative Works; or,
          within a display generated by the Derivative Works, if and
          wherever such third-party notices normally appear. The contents
          of the NOTICE file are for informational purposes only and
          do not modify the License. You may add Your own attribution
          notices within Derivative Works that You distribute, alongside
          or as an addendum to the NOTICE text from the Work, provided
          that such additional attribution notices cannot be construed
          as modifying the License.

      You may add Your own copyright statement to Your modifications and
      may provide additional or different license terms and conditions
      for use, reproduction, or distribution of Your modifications, or
      for any such Derivative Works as a whole, provided Your use,
      reproduction, and distribution of the Work otherwise complies with
      the conditions stated in this License.

   5. Submission of Contributions. Unless You explicitly state otherwise,
      any Contribution intentionally submitted for inclusion in the Work
      by You to the Licensor shall be under the terms and conditions of
      this License, without any additional terms or conditions.
      Notwithstanding the above, nothing herein shall supersede or modify
      the terms of any separate license agreement you may have executed
      with Licensor regarding such Contributions.

   6. Trademarks. This License does not grant permission to use the trade
      names, trademarks, service marks, or product names of the Licensor,
      except as required for reasonable and customary use in describing the
      origin of the Work and reproducing the content of the NOTICE file.

   7. Disclaimer of Warranty. Unless required by applicable law or
      agreed to in writing, Licensor provides the Work (and each
      Contributor provides its Contributions) on an "AS IS" BASIS,
      WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
      implied, including, without limitation, any warranties or conditions
      of TITLE, NON-INFRINGEMENT, MERCHANTABILITY, or FITNESS FOR A
      PARTICULAR PURPOSE. You are solely responsible for determining the
      appropriateness of using or redistributing the Work and assume any
      risks associated with Your exercise of permissions under this License.

   8. Limitation of Liability. In no event and under no legal theory,
      whether in tort (including negligence), contract, or otherwise,
      unless required by applicable law (such as deliberate and grossly
      negligent acts) or agreed to in writing, shall any Contributor be
      liable to You for damages, including any direct, indirect, special,
      incidental, or consequential damages of any character arising as a
      result of this License or out of the use or inability to use the
      Work (including but not limited to damages for loss of goodwill,
      work stoppage, computer failure or malfunction, or any and all
      other commercial damages or losses), even if such Contributor
      has been advised of the possibility of such damages.

   9. Accepting Warranty or Additional Liability. While redistributing
      the Work or Derivative Works thereof, You may choose to offer,
      and charge a fee for, acceptance of support, warranty, indemnity,
      or other liability obligations and/or rights consistent with this
      License. However, in accepting such obligations, You may act only
      on Your own behalf and on Your sole responsibility, not on behalf
      of any other Contributor, and only if You agree to indemnify,
      defend, and hold each Contributor harmless for any liability
      incurred by, or claims asserted against, such Contributor by reason
      of your accepting any such warranty or additional liability.

   END OF TERMS AND CONDITIONS

   APPENDIX: How to apply the Apache License to your work.

      To apply the Apache License to your work, attach the following
      boilerplate notice, with the fields enclosed by brackets "[]"
      replaced with your own identifying information. (Don't include
      the brackets!)  The text should be enclosed in the appropriate
      comment syntax for the file format. We also recommend that a
      file or class name and description of purpose be included on the
      same "printed page" as the copyright notice for easier
      identification within third-party archives.

   Copyright [yyyy] [name of copyright owner]

   Licensed under the Apache License, Version 2.0 (the "License");
   you may not use this file except in compliance with the License.
   You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

   Unless required by applicable law or agreed to in writing, software
   distributed under the License is distributed on an "AS IS" BASIS,
   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
   See the License for the specific language governing permissions and
   limitations under the License.

===============================================================================

		    GNU GENERAL PUBLIC LICENSE
		       Version 2, June 1991

 Copyright (C) 1989, 1991 Free Software Foundation, Inc.,
 51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA
 Everyone is permitted to copy and distribute verbatim copies
 of this license document, but changing it is not allowed.

			    Preamble

  The licenses for most software are designed to take away your
freedom to share and change it.  By contrast, the GNU General Public
License is intended to guarantee your freedom to share and change free
software--to make sure the software is free for all its users.  This
General Public License applies to most of the Free Software
Foundation's software and to any other program whose authors commit to
using it.  (Some other Free Software Foundation software is covered by
the GNU Lesser General Public License instead.)  You can apply it to
your programs, too.

  When we speak of free software, we are referring to freedom, not
price.  Our General Public Licenses are designed to make sure that you
have the freedom to distribute copies of free software (and charge for
this service if you wish), that you receive source code or can get it
if you want it, that you can change the software or use pieces of it
in new free programs; and that you know you can do these things.

  To protect your rights, we need to make restrictions that forbid
anyone to deny you these rights or to ask you to surrender the rights.
These restrictions translate to certain responsibilities for you if you
distribute copies of the software, or if you modify it.

  For example, if you distribute copies of such a program, whether
gratis or for a fee, you must give the recipients all the rights that
you have.  You must make sure that they, too, receive or can get the
source code.  And you must show them these terms so they know their
rights.

  We protect your rights with two steps: (1) copyright the software, and
(2) offer you this license which gives you legal permission to copy,
distribute and/or modify the software.

  Also, for each author's protection and ours, we want to make certain
that everyone understands that there is no warranty for this free
software.  If the software is modified by someone else and passed on, we
want its recipients to know that what they have is not the original, so
that any problems introduced by others will not reflect on the original
authors' reputations.

  Finally, any free program is threatened constantly by software
patents.  We wish to avoid the danger that redistributors of a free
program will individually obtain patent licenses, in effect making the
program proprietary.  To prevent this, we have made it clear that any
patent must be licensed for everyone's free use or not licensed at all.

  The precise terms and conditions for copying, distribution and
modification follow.

		    GNU GENERAL PUBLIC LICENSE
   TERMS AND CONDITIONS FOR COPYING, DISTRIBUTION AND MODIFICATION

  0. This License applies to any program or other work which contains
a notice placed by the copyright holder saying it may be distributed
under the terms of this General Public License.  The "Program", below,
refers to any such program or work, and a "work based on the Program"
means either the Program or any derivative work under copyright law:
that is to say, a work containing the Program or a portion of it,
either verbatim or with modifications and/or translated into another
language.  (Hereinafter, translation is included without limitation in
the term "modification".)  Each licensee is addressed as "you".

Activities other than copying, distribution and modification are not
covered by this License; they are outside its scope.  The act of
running the Program is not restricted, and the output from the Program
is covered only if its contents constitute a work based on the
Program (independent of having been made by running the Program).
Whether that is true depends on what the Program does.

  1. You may copy and distribute verbatim copies of the Program's
source code as you receive it, in any medium, provided that you
conspicuously and appropriately publish on each copy an appropriate
copyright notice and disclaimer of warranty; keep intact all the
notices that refer to this License and to the absence of any warranty;
and give any other recipients of the Program a copy of this License
along with the Program.

You may charge a fee for the physical act of transferring a copy, and
you may at your option offer warranty protection in exchange for a fee.

  2. You may modify your copy or copies of the Program or any portion
of it, thus forming a work based on the Program, and copy and
distribute such modifications or work under the terms of Section 1
above, provided that you also meet all of these conditions:

    a) You must cause the modified files to carry prominent notices
    stating that you changed the files and the date of any change.

    b) You must cause any work that you distribute or publish, that in
    whole or in part contains or is derived from the Program or any
    part thereof, to be licensed as a whole at no charge to all third
    parties under the terms of this License.

    c) If the modified program normally reads commands interactively
    when run, you must cause it, when started running for such
    interactive use in the most ordinary way, to print or display an
    announcement including an appropriate copyright notice and a
    notice that there is no warranty (or else, saying that you provide
    a warranty) and that users may redistribute the program under
    these conditions, and telling the user how to view a copy of this
    License.  (Exception: if the Program itself is interactive but
    does not normally print such an announcement, your work based on
    the Program is not required to print an announcement.)

These requirements apply to the modified work as a whole.  If
identifiable sections of that work are not derived from the Program,
and can be reasonably considered independent and separate works in
themselves, then this License, and its terms, do not apply to those
sections when you distribute them as separate works.  But when you
distribute the same sections as part of a whole which is a work based
on the Program, the distribution of the whole must be on the terms of
this License, whose permissions for other licensees extend to the
entire whole, and thus to each and every part regardless of who wrote it.

Thus, it is not the intent of this section to claim rights or contest
your rights to work written entirely by you; rather, the intent is to
exercise the right to control the distribution of derivative or
collective works based on the Program.

In addition, mere aggregation of another work not based on the Program
with the Program (or with a work based on the Program) on a volume of
a storage or distribution medium does not bring the other work under
the scope of this License.

  3. You may copy and distribute the Program (or a work based on it,
under Section 2) in object code or executable form under the terms of
Sections 1 and 2 above provided that you also do one of the following:

    a) Accompany it with the complete corresponding machine-readable
    source code, which must be distributed under the terms of Sections
    1 and 2 above on a medium customarily used for software interchange; or,

    b) Accompany it with a written offer, valid for at least three
    years, to give any third party, for a charge no more than your
    cost of physically performing source distribution, a complete
    machine-readable copy of the corresponding source code, to be
    distributed under the terms of Sections 1 and 2 above on a medium
    customarily used for software interchange; or,

    c) Accompany it with the information you received as to the offer
    to distribute corresponding source code.  (This alternative is
    allowed only for noncommercial distribution and only if you
    received the program in object code or executable form with such
    an offer, in accord with Subsection b above.)

The source code for a work means the preferred form of the work for
making modifications to it.  For an executable work, complete source
code means all the source code for all modules it contains, plus any
associated interface definition files, plus the scripts used to
control compilation and installation of the executable.  However, as a
special exception, the source code distributed need not include
anything that is normally distributed (in either source or binary
form) with the major components (compiler, kernel, and so on) of the
operating system on which the executable runs, unless that component
itself accompanies the executable.

If distribution of executable or object code is made by offering
access to copy from a designated place, then offering equivalent
access to copy the source code from the same place counts as
distribution of the source code, even though third parties are not
compelled to copy the source along with the object code.

  4. You may not copy, modify, sublicense, or distribute the Program
except as expressly provided under this License.  Any attempt
otherwise to copy, modify, sublicense or distribute the Program is
void, and will automatically terminate your rights under this License.
However, parties who have received copies, or rights, from you under
this License will not have their licenses terminated so long as such
parties remain in full compliance.

  5. You are not required to accept this License, since you have not
signed it.  However, nothing else grants you permission to modify or
distribute the Program or its derivative works.  These actions are
prohibited by law if you do not accept this License.  Therefore, by
modifying or distributing the Program (or any work based on the
Program), you indicate your acceptance of this License to do so, and
all its terms and conditions for copying, distributing or modifying
the Program or works based on it.

  6. Each time you redistribute the Program (or any work based on the
Program), the recipient automatically receives a license from the
original licensor to copy, distribute or modify the Program subject to
these terms and conditions.  You may not impose any further
restrictions on the recipients' exercise of the rights granted herein.
You are not responsible for enforcing compliance by third parties to
this License.

  7. If, as a consequence of a court judgment or allegation of patent
infringement or for any other reason (not limited to patent issues),
conditions are imposed on you (whether by court order, agreement or
otherwise) that contradict the conditions of this License, they do not
excuse you from the conditions of this License.  If you cannot
distribute so as to satisfy simultaneously your obligations under this
License and any other pertinent obligations, then as a consequence you
may not distribute the Program at all.  For example, if a patent
license would not permit royalty-free redistribution of the Program by
all those who receive copies directly or indirectly through you, then
the only way you could satisfy both it and this License would be to
refrain entirely from distribution of the Program.

If any portion of this section is held invalid or unenforceable under
any particular circumstance, the balance of the section is intended to
apply and the section as a whole is intended to apply in other
circumstances.

It is not the purpose of this section to induce you to infringe any
patents or other property right claims or to contest validity of any
such claims; this section has the sole purpose of protecting the
integrity of the free software distribution system, which is
implemented by public license practices.  Many people have made
generous contributions to the wide range of software distributed
through that system in reliance on consistent application of that
system; it is up to the author/donor to decide if he or she is willing
to distribute software through any other system and a licensee cannot
impose that choice.

This section is intended to make thoroughly clear what is believed to
be a consequence of the rest of this License.

  8. If the distribution and/or use of the Program is restricted in
certain countries either by patents or by copyrighted interfaces, the
original copyright holder who places the Program under this License
may add an explicit geographical distribution limitation excluding
those countries, so that distribution is permitted only in or among
countries not thus excluded.  In such case, this License incorporates
the limitation as if written in the body of this License.

  9. The Free Software Foundation may publish revised and/or new versions
of the General Public License from time to time.  Such new versions will
be similar in spirit to the present version, but may differ in detail to
address new problems or concerns.

Each version is given a distinguishing version number.  If the Program
specifies a version number of this License which applies to it and "any
later version", you have the option of following the terms and conditions
either of that version or of any later version published by the Free
Software Foundation.  If the Program does not specify a version number of
this License, you may choose any version ever published by the Free Software
Foundation.

  10. If you wish to incorporate parts of the Program into other free
programs whose distribution conditions are different, write to the author
to ask for permission.  For software which is copyrighted by the Free
Software Foundation, write to the Free Software Foundation; we sometimes
make exceptions for this.  Our decision will be guided by the two goals
of preserving the free status of all derivatives of our free software and
of promoting the sharing and reuse of software generally.

			    NO WARRANTY

  11. BECAUSE THE PROGRAM IS LICENSED FREE OF CHARGE, THERE IS NO WARRANTY
FOR THE PROGRAM, TO THE EXTENT PERMITTED BY APPLICABLE LAW.  EXCEPT WHEN
OTHERWISE STATED IN WRITING THE COPYRIGHT HOLDERS AND/OR OTHER PARTIES
PROVIDE THE PROGRAM "AS IS" WITHOUT WARRANTY OF ANY KIND, EITHER EXPRESSED
OR IMPLIED, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE.  THE ENTIRE RISK AS
TO THE QUALITY AND PERFORMANCE OF THE PROGRAM IS WITH YOU.  SHOULD THE
PROGRAM PROVE DEFECTIVE, YOU ASSUME THE COST OF ALL NECESSARY SERVICING,
REPAIR OR CORRECTION.

  12. IN NO EVENT UNLESS REQUIRED BY APPLICABLE LAW OR AGREED TO IN WRITING
WILL ANY COPYRIGHT HOLDER, OR ANY OTHER PARTY WHO MAY MODIFY AND/OR
REDISTRIBUTE THE PROGRAM AS PERMITTED ABOVE, BE LIABLE TO YOU FOR DAMAGES,
INCLUDING ANY GENERAL, SPECIAL, INCIDENTAL OR CONSEQUENTIAL DAMAGES ARISING
OUT OF THE USE OR INABILITY TO USE THE PROGRAM (INCLUDING BUT NOT LIMITED
TO LOSS OF DATA OR DATA BEING RENDERED INACCURATE OR LOSSES SUSTAINED BY
YOU OR THIRD PARTIES OR A FAILURE OF THE PROGRAM TO OPERATE WITH ANY OTHER
PROGRAMS), EVEN IF SUCH HOLDER OR OTHER PARTY HAS BEEN ADVISED OF THE
POSSIBILITY OF SUCH DAMAGES.

		     END OF TERMS AND CONDITIONS

	    How to Apply These Terms to Your New Programs

  If you develop a new program, and you want it to be of the greatest
possible use to the public, the best way to achieve this is to make it
free software which everyone can redistribute and change under these terms.

  To do so, attach the following notices to the program.  It is safest
to attach them to the start of each source file to most effectively
convey the exclusion of warranty; and each file should have at least
the "copyright" line and a pointer to where the full notice is found.

    <one line to give the program's name and a brief idea of what it does.>
    Copyright (C) <year>  <name of author>

    This program is free software; you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation; either version 2 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License along
    with this program; if not, write to the Free Software Foundation, Inc.,
    51 Franklin Street, Fifth Floor, Boston, MA 02110-1301 USA.

Also add information on how to contact you by electronic and paper mail.

If the program is interactive, make it output a short notice like this
when it starts in an interactive mode:

    Gnomovision version 69, Copyright (C) year name of author
    Gnomovision comes with ABSOLUTELY NO WARRANTY; for details type `show w'.
    This is free software, and you are welcome to redistribute it
    under certain conditions; type `show c' for details.

The hypothetical commands `show w' and `show c' should show the appropriate
parts of the General Public License.  Of course, the commands you use may
be called something other than `show w' and `show c'; they could even be
mouse-clicks or menu items--whatever suits your program.

You should also get your employer (if you work as a programmer) or your
school, if any, to sign a "copyright disclaimer" for the program, if
necessary.  Here is a sample; alter the names:

  Yoyodyne, Inc., hereby disclaims all copyright interest in the program
  `Gnomovision' (which makes passes at compilers) written by James Hacker.

  <signature of Ty Coon>, 1 April 1989
  Ty Coon, President of Vice

This General Public License does not permit incorporating your program into
proprietary programs.  If your program is a subroutine library, you may
consider it more useful to permit linking proprietary applications with the
library.  If this is what you want to do, use the GNU Lesser General
Public License instead of this License.


"CLASSPATH" EXCEPTION TO THE GPL

    Linking this library statically or dynamically with other modules is making
    a combined work based on this library.  Thus, the terms and conditions of
    the GNU General Public License cover the whole combination.

    As a special exception, the copyright holders of this library give you
    permission to link this library with independent modules to produce an
    executable, regardless of the license terms of these independent modules,
    and to copy and distribute the resulting executable under terms of your
    choice, provided that you also meet, for each linked independent module,
    the terms and conditions of the license of that module.  An independent
    module is a module which is not derived from or based on this library.  If
    you modify this library, you may extend this exception to your version of
    the library, but you are not obligated to do so.  If you do not wish to do
    so, delete this exception statement from your version.
# webcam-capture-driver-openimaj

This is capture driver which uses [OpenIMAJ](http://openimaj.org) to access camera devices.

## Maven

Stable:

```xml
<dependency>
	<groupId>com.github.sarxos</groupId>
	<artifactId>webcam-capture-driver-openimaj</artifactId>
	<version>0.3.12</version>
</dependency>
```

Snapshot:

```xml
<repository>
    <id>Sonatype OSS Snapshot Repository</id>
    <url>http://oss.sonatype.org/content/repositories/snapshots</url>
</repository>
```
```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-openimaj</artifactId>
    <version>0.3.13-SNAPSHOT</version>
</dependency>
```

## Example

```java
static {
	Webcam.setDriver(new OpenImajDriver());
}

public static void main(String[] args) {
	JFrame frame = new JFrame("OpenIMAJDriver Capture Driver Demo");
	frame.add(new WebcamPanel(Webcam.getDefault()));
	frame.pack();
	frame.setVisible(true);
	frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
}
```

## License

Copyright (C) 2012 - 2017 Bartosz Firyn

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

# webcam-capture-driver-raspberrypi

This capture driver is designed special for raspberrypi. __raspistill，raspiyuv, ...__ are the command line tools on raspberrypi for capturing photographs or vedios with the camera module. The most important is that command line tools have feature grabbing image repeatly(mock FPS) from camera and print to file or console. They are:

1.  -o, --output : Output filename <filename> (to **write to stdout, use '-o -**'). If not specified, no file is saved
2.  -tl, --timelapse : Timelapse mode. Takes a picture every <t>ms
3.  -n, --nopreview : Do not display a preview window

So it is possible to use java `Runtime.execute()` to launch raspixxx process and intercept its console output, makes them as
webcam driver. this is one simple and straightforward approach without native JNI or JNA call, no file system exchange. You
will not struggle with performance issue and native code compiling. Because raspberrypi camera is connected to GPU directly,
the only CPU usage of drivers is converting rgb24 data to java BufferedImage, the system average CPU loading is 30% when
driver and Swing panel running.

This dirver has been contributed by Alex Mao (alexmao86, https://github.com/alexmao86). Thank you Alex!

## Install Required Binaries

sudo apt-get update
sudo apt-get install raspistill raspivid raspiyuv raspividyuv

## Maven

```xml
<!--If you want to access snapshot repo, please add this to your pom -->
<repository>
    <id>Sonatype OSS Snapshot Repository</id>
    <url>http://oss.sonatype.org/content/repositories/snapshots</url>
</repository>
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-raspberrypi</artifactId>
    <version>${your version}</version>
</dependency>
```

## How To Use

Set capture driver before you start using Webcam class. this is one basic demo, check test source for demo with option panel.

```java
import java.awt.Dimension;
import java.awt.FlowLayout;

import javax.swing.JFrame;

import com.github.sarxos.webcam.Webcam;
import com.github.sarxos.webcam.WebcamPanel;
import com.github.sarxos.webcam.WebcamPanel.DrawMode;
import com.github.sarxos.webcam.WebcamResolution;
import com.github.sarxos.webcam.ds.raspberrypi.*;


public class WebcamPanelExample {

	static {
		//Webcam.setDriver(new RaspistillDriver());
		Webcam.setDriver(new RaspiYUVDriver());
		//Webcam.setDriver(new RaspividDriver());
		//Webcam.setDriver(new RaspividYUVDriver());
	}

	public static void main(String[] args) throws InterruptedException {

		final JFrame window = new JFrame("Raspberrypi Capture Example");
		window.setResizable(true);
		window.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		window.getContentPane().setLayout(new FlowLayout());

		final Dimension resolution = WebcamResolution.QVGA.getSize();

		for (final Webcam webcam : Webcam.getWebcams()) {

			webcam.setCustomViewSizes(resolution);
			webcam.setViewSize(resolution);
			webcam.open();

			final WebcamPanel panel = new WebcamPanel(webcam);
			panel.setFPSDisplayed(true);
			panel.setDrawMode(DrawMode.FIT);
			panel.setImageSizeDisplayed(true);
			panel.setPreferredSize(resolution);

			window.getContentPane().add(panel);
		}

		window.pack();
		window.setVisible(true);
	}
}
```

Please check WebcamPanelExample.java in src/test/java for detail.

## Known Problems

Because is its based on pure Java image processing, the performance of `RaspistillDriver` and `RaspiYUVDriver` is not very good. The actuall FPS is low. According to test, about 500ms for PNG decoder to decode 640x480 image from raspistill stream. But the advantage of `RaspividDriver` and `RaspividYUVDriver` is the fact that Java code is comsuming RAW RGB24 data in _almost_ realtime by following native process STDOUT.

## Driver Parameters

This driver makes above arguments configurable, when driver instance created, it will load arguments step by step as follows:

1. Load built-in parameters
2. Search system properties which starts with "raspi.", then merge to properties
3. You can set all command line arguments from device instance's setParameters

## Capture Driver License

Copyright (C) 2012 - 2019 Webcam Capture API Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


raspistill Camera App v1.3.11

Runs camera for specific time, and take JPG capture at end if requested

usage: raspistill [options]

Image parameter commands

-?, --help	: This help information
-w, --width	: Set image width <size>
-h, --height	: Set image height <size>
-q, --quality	: Set jpeg quality <0 to 100>
-r, --raw	: Add raw bayer data to jpeg metadata
-o, --output	: Output filename <filename> (to write to stdout, use '-o -'). If not specified, no file is saved
-l, --latest	: Link latest complete image to filename <filename>
-v, --verbose	: Output verbose information during run
-t, --timeout	: Time (in ms) before takes picture and shuts down (if not specified, set to 5s)
-th, --thumb	: Set thumbnail parameters (x:y:quality) or none
-d, --demo	: Run a demo mode (cycle through range of camera options, no capture)
-e, --encoding	: Encoding to use for output file (jpg, bmp, gif, png)
-x, --exif	: EXIF tag to apply to captures (format as 'key=value') or none
-tl, --timelapse	: Timelapse mode. Takes a picture every <t>ms. %d == frame number (Try: -o img_%04d.jpg)
-fp, --fullpreview	: Run the preview using the still capture resolution (may reduce preview fps)
-k, --keypress	: Wait between captures for a ENTER, X then ENTER to exit
-s, --signal	: Wait between captures for a SIGUSR1 or SIGUSR2 from another process
-g, --gl	: Draw preview to texture instead of using video render component
-gc, --glcapture	: Capture the GL frame-buffer instead of the camera image
-set, --settings	: Retrieve camera settings and write to stdout
-cs, --camselect	: Select camera <number>. Default 0
-bm, --burst	: Enable 'burst capture mode'
-md, --mode	: Force sensor mode. 0=auto. See docs for other modes available
-dt, --datetime	: Replace output pattern (%d) with DateTime (MonthDayHourMinSec)
-ts, --timestamp	: Replace output pattern (%d) with unix timestamp (seconds since 1970)
-fs, --framestart	: Starting frame number in output pattern(%d)
-rs, --restart	: JPEG Restart interval (default of 0 for none)

Preview parameter commands

-p, --preview	: Preview window settings <'x,y,w,h'>
-f, --fullscreen	: Fullscreen preview mode
-op, --opacity	: Preview window opacity (0-255)
-n, --nopreview	: Do not display a preview window

Image parameter commands

-sh, --sharpness	: Set image sharpness (-100 to 100)
-co, --contrast	: Set image contrast (-100 to 100)
-br, --brightness	: Set image brightness (0 to 100)
-sa, --saturation	: Set image saturation (-100 to 100)
-ISO, --ISO	: Set capture ISO
-vs, --vstab	: Turn on video stabilisation
-ev, --ev	: Set EV compensation - steps of 1/6 stop
-ex, --exposure	: Set exposure mode (see Notes)
-fli, --flicker	: Set flicker avoid mode (see Notes)
-awb, --awb	: Set AWB mode (see Notes)
-ifx, --imxfx	: Set image effect (see Notes)
-cfx, --colfx	: Set colour effect (U:V)
-mm, --metering	: Set metering mode (see Notes)
-rot, --rotation	: Set image rotation (0-359)
-hf, --hflip	: Set horizontal flip
-vf, --vflip	: Set vertical flip
-roi, --roi	: Set region of interest (x,y,w,d as normalised coordinates [0.0-1.0])
-ss, --shutter	: Set shutter speed in microseconds
-awbg, --awbgains	: Set AWB gains - AWB mode must be off
-drc, --drc	: Set DRC Level (see Notes)
-st, --stats	: Force recomputation of statistics on stills capture pass
-a, --annotate	: Enable/Set annotate flags or text
-3d, --stereo	: Select stereoscopic mode
-dec, --decimate	: Half width/height of stereo image
-3dswap, --3dswap	: Swap camera order for stereoscopic
-ae, --annotateex	: Set extra annotation parameters (text size, text colour(hex YUV), bg colour(hex YUV))
-ag, --analoggain	: Set the analog gain (floating point)
-dg, --digitalgain	: Set the digital gain (floating point)


Notes

Exposure mode options :
off,auto,night,nightpreview,backlight,spotlight,sports,snow,beach,verylong,fixedfps,antishake,fireworks

Flicker avoid mode options :
off,auto,50hz,60hz

AWB mode options :
off,auto,sun,cloud,shade,tungsten,fluorescent,incandescent,flash,horizon

Image Effect mode options :
none,negative,solarise,sketch,denoise,emboss,oilpaint,hatch,gpen,pastel,watercolour,film,blur,saturation,colourswap,washedout,posterise,colourpoint,colourbalance,cartoon

Metering Mode options :
average,spot,backlit,matrix

Dynamic Range Compression (DRC) options :
off,low,med,high

Preview parameter commands

-gs, --glscene	: GL scene square,teapot,mirror,yuv,sobel,vcsm_square
-gw, --glwin	: GL window settings <'x,y,w,h'>


raspivid Camera App v1.3.12

Display camera output to display, and optionally saves an H264 capture at requested bitrate


usage: raspivid [options]

Image parameter commands

-?, --help	: This help information
-w, --width	: Set image width <size>. Default 1920
-h, --height	: Set image height <size>. Default 1080
-b, --bitrate	: Set bitrate. Use bits per second (e.g. 10MBits/s would be -b 10000000)
-o, --output	: Output filename <filename> (to write to stdout, use '-o -').
		  Connect to a remote IPv4 host (e.g. tcp://192.168.1.2:1234, udp://192.168.1.2:1234)
		  To listen on a TCP port (IPv4) and wait for an incoming connection use -l
		  (e.g. raspivid -l -o tcp://0.0.0.0:3333 -> bind to all network interfaces, raspivid -l -o tcp://192.168.1.1:3333 -> bind to a certain local IPv4)
-v, --verbose	: Output verbose information during run
-t, --timeout	: Time (in ms) to capture for. If not specified, set to 5s. Zero to disable
-d, --demo	: Run a demo mode (cycle through range of camera options, no capture)
-fps, --framerate	: Specify the frames per second to record
-e, --penc	: Display preview image *after* encoding (shows compression artifacts)
-g, --intra	: Specify the intra refresh period (key frame rate/GoP size). Zero to produce an initial I-frame and then just P-frames.
-pf, --profile	: Specify H264 profile to use for encoding
-td, --timed	: Cycle between capture and pause. -cycle on,off where on is record time and off is pause time in ms
-s, --signal	: Cycle between capture and pause on Signal
-k, --keypress	: Cycle between capture and pause on ENTER
-i, --initial	: Initial state. Use 'record' or 'pause'. Default 'record'
-qp, --qp	: Quantisation parameter. Use approximately 10-40. Default 0 (off)
-ih, --inline	: Insert inline headers (SPS, PPS) to stream
-sg, --segment	: Segment output file in to multiple files at specified interval <ms>
-wr, --wrap	: In segment mode, wrap any numbered filename back to 1 when reach number
-sn, --start	: In segment mode, start with specified segment number
-sp, --split	: In wait mode, create new output file for each start event
-c, --circular	: Run encoded data through circular buffer until triggered then save
-x, --vectors	: Output filename <filename> for inline motion vectors
-cs, --camselect	: Select camera <number>. Default 0
-set, --settings	: Retrieve camera settings and write to stdout
-md, --mode	: Force sensor mode. 0=auto. See docs for other modes available
-if, --irefresh	: Set intra refresh type
-fl, --flush	: Flush buffers in order to decrease latency
-pts, --save-pts	: Save Timestamps to file for mkvmerge
-cd, --codec	: Specify the codec to use - H264 (default) or MJPEG
-lev, --level	: Specify H264 level to use for encoding
-r, --raw	: Output filename <filename> for raw video
-rf, --raw-format	: Specify output format for raw video. Default is yuv
-l, --listen	: Listen on a TCP socket


H264 Profile options :
baseline,main,high

H264 Level options :
4,4.1,4.2

H264 Intra refresh options :
cyclic,adaptive,both,cyclicrows

Raw output format options :
yuv,rgb,gray

Preview parameter commands

-p, --preview	: Preview window settings <'x,y,w,h'>
-f, --fullscreen	: Fullscreen preview mode
-op, --opacity	: Preview window opacity (0-255)
-n, --nopreview	: Do not display a preview window

Image parameter commands

-sh, --sharpness	: Set image sharpness (-100 to 100)
-co, --contrast	: Set image contrast (-100 to 100)
-br, --brightness	: Set image brightness (0 to 100)
-sa, --saturation	: Set image saturation (-100 to 100)
-ISO, --ISO	: Set capture ISO
-vs, --vstab	: Turn on video stabilisation
-ev, --ev	: Set EV compensation - steps of 1/6 stop
-ex, --exposure	: Set exposure mode (see Notes)
-fli, --flicker	: Set flicker avoid mode (see Notes)
-awb, --awb	: Set AWB mode (see Notes)
-ifx, --imxfx	: Set image effect (see Notes)
-cfx, --colfx	: Set colour effect (U:V)
-mm, --metering	: Set metering mode (see Notes)
-rot, --rotation	: Set image rotation (0-359)
-hf, --hflip	: Set horizontal flip
-vf, --vflip	: Set vertical flip
-roi, --roi	: Set region of interest (x,y,w,d as normalised coordinates [0.0-1.0])
-ss, --shutter	: Set shutter speed in microseconds
-awbg, --awbgains	: Set AWB gains - AWB mode must be off
-drc, --drc	: Set DRC Level (see Notes)
-st, --stats	: Force recomputation of statistics on stills capture pass
-a, --annotate	: Enable/Set annotate flags or text
-3d, --stereo	: Select stereoscopic mode
-dec, --decimate	: Half width/height of stereo image
-3dswap, --3dswap	: Swap camera order for stereoscopic
-ae, --annotateex	: Set extra annotation parameters (text size, text colour(hex YUV), bg colour(hex YUV))
-ag, --analoggain	: Set the analog gain (floating point)
-dg, --digitalgain	: Set the digital gain (floating point)


Notes

Exposure mode options :
off,auto,night,nightpreview,backlight,spotlight,sports,snow,beach,verylong,fixedfps,antishake,fireworks

Flicker avoid mode options :
off,auto,50hz,60hz

AWB mode options :
off,auto,sun,cloud,shade,tungsten,fluorescent,incandescent,flash,horizon

Image Effect mode options :
none,negative,solarise,sketch,denoise,emboss,oilpaint,hatch,gpen,pastel,watercolour,film,blur,saturation,colourswap,washedout,posterise,colourpoint,colourbalance,cartoon

Metering Mode options :
average,spot,backlit,matrix

Dynamic Range Compression (DRC) options :
off,low,med,high


raspividyuv Camera App v1.3.15

Display camera output to display, and optionally saves an uncompressed YUV420 file 

NOTE: High resolutions and/or frame rates may exceed the bandwidth of the system due
to the large amounts of data being moved to the SD card. This will result in undefined
results in the subsequent file.
The raw file produced contains all the files. Each image in the files will be of size
width*height*1.5, unless width and/or height are not divisible by 16. Use the image size
displayed during the run (in verbose mode) for an accurate value
The Linux split command can be used to split up the file to individual frames

usage: raspividyuv [options]

Image parameter commands

-?, --help	: This help information
-w, --width	: Set image width <size>. Default 1920
-h, --height	: Set image height <size>. Default 1080
-o, --output	: Output filename <filename> (to write to stdout, use '-o -')
-v, --verbose	: Output verbose information during run
-t, --timeout	: Time (in ms) to capture for. If not specified, set to 5s. Zero to disable
-d, --demo	: Run a demo mode (cycle through range of camera options, no capture)
-fps, --framerate	: Specify the frames per second to record
-td, --timed	: Cycle between capture and pause. -cycle on,off where on is record time and off is pause time in ms
-s, --signal	: Cycle between capture and pause on Signal
-k, --keypress	: Cycle between capture and pause on ENTER
-i, --initial	: Initial state. Use 'record' or 'pause'. Default 'record'
-cs, --camselect	: Select camera <number>. Default 0
-set, --settings	: Retrieve camera settings and write to stdout
-md, --mode	: Force sensor mode. 0=auto. See docs for other modes available
-y, --luma	: Only output the luma / Y of the YUV data'
-rgb, --rgb	: Save as RGB data rather than YUV
-pts, --save-pts	: Save Timestamps to file
-l, --listen	: Listen on a TCP socket


Preview parameter commands

-p, --preview	: Preview window settings <'x,y,w,h'>
-f, --fullscreen	: Fullscreen preview mode
-op, --opacity	: Preview window opacity (0-255)
-n, --nopreview	: Do not display a preview window

Image parameter commands

-sh, --sharpness	: Set image sharpness (-100 to 100)
-co, --contrast	: Set image contrast (-100 to 100)
-br, --brightness	: Set image brightness (0 to 100)
-sa, --saturation	: Set image saturation (-100 to 100)
-ISO, --ISO	: Set capture ISO
-vs, --vstab	: Turn on video stabilisation
-ev, --ev	: Set EV compensation - steps of 1/6 stop
-ex, --exposure	: Set exposure mode (see Notes)
-fli, --flicker	: Set flicker avoid mode (see Notes)
-awb, --awb	: Set AWB mode (see Notes)
-ifx, --imxfx	: Set image effect (see Notes)
-cfx, --colfx	: Set colour effect (U:V)
-mm, --metering	: Set metering mode (see Notes)
-rot, --rotation	: Set image rotation (0-359)
-hf, --hflip	: Set horizontal flip
-vf, --vflip	: Set vertical flip
-roi, --roi	: Set region of interest (x,y,w,d as normalised coordinates [0.0-1.0])
-ss, --shutter	: Set shutter speed in microseconds
-awbg, --awbgains	: Set AWB gains - AWB mode must be off
-drc, --drc	: Set DRC Level (see Notes)
-st, --stats	: Force recomputation of statistics on stills capture pass
-a, --annotate	: Enable/Set annotate flags or text
-3d, --stereo	: Select stereoscopic mode
-dec, --decimate	: Half width/height of stereo image
-3dswap, --3dswap	: Swap camera order for stereoscopic
-ae, --annotateex	: Set extra annotation parameters (text size, text colour(hex YUV), bg colour(hex YUV))
-ag, --analoggain	: Set the analog gain (floating point)
-dg, --digitalgain	: Set the digital gain (floating point)


Notes

Exposure mode options :
off,auto,night,nightpreview,backlight,spotlight,sports,snow,beach,verylong,fixedfps,antishake,fireworks

Flicker avoid mode options :
off,auto,50hz,60hz

AWB mode options :
off,auto,sun,cloud,shade,tungsten,fluorescent,incandescent,flash,horizon

Image Effect mode options :
none,negative,solarise,sketch,denoise,emboss,oilpaint,hatch,gpen,pastel,watercolour,film,blur,saturation,colourswap,washedout,posterise,colourpoint,colourbalance,cartoon

Metering Mode options :
average,spot,backlit,matrix

Dynamic Range Compression (DRC) options :
off,low,med,high


raspiyuv Camera App v1.3.7

Runs camera for specific time, and take uncompressed YUV capture at end if requested

usage: raspiyuv [options]

Image parameter commands

-?, --help	: This help information
-w, --width	: Set image width <size>
-h, --height	: Set image height <size>
-o, --output	: Output filename <filename>. If not specifed, no image is saved
-v, --verbose	: Output verbose information during run
-t, --timeout	: Time (in ms) before takes picture and shuts down. If not specified set to 5s
-tl, --timelapse	: Timelapse mode. Takes a picture every <t>ms
-rgb, --rgb	: Save as RGB data rather than YUV
-cs, --camselect	: Select camera <number>. Default 0
-fp, --fullpreview	: Run the preview using the still capture resolution (may reduce preview fps)
-l, --latest	: Link latest complete image to filename <filename>
-k, --keypress	: Wait between captures for a ENTER, X then ENTER to exit
-s, --signal	: Wait between captures for a SIGUSR1 from another process
-set, --settings	: Retrieve camera settings and write to stdout

-bm, --burst	: Enable 'burst capture mode'
-y, --luma	: Only output the luma / Y of the YUV data'

Preview parameter commands

-p, --preview	: Preview window settings <'x,y,w,h'>
-f, --fullscreen	: Fullscreen preview mode
-op, --opacity	: Preview window opacity (0-255)
-n, --nopreview	: Do not display a preview window

Image parameter commands

-sh, --sharpness	: Set image sharpness (-100 to 100)
-co, --contrast	: Set image contrast (-100 to 100)
-br, --brightness	: Set image brightness (0 to 100)
-sa, --saturation	: Set image saturation (-100 to 100)
-ISO, --ISO	: Set capture ISO
-vs, --vstab	: Turn on video stabilisation
-ev, --ev	: Set EV compensation - steps of 1/6 stop
-ex, --exposure	: Set exposure mode (see Notes)
-fli, --flicker	: Set flicker avoid mode (see Notes)
-awb, --awb	: Set AWB mode (see Notes)
-ifx, --imxfx	: Set image effect (see Notes)
-cfx, --colfx	: Set colour effect (U:V)
-mm, --metering	: Set metering mode (see Notes)
-rot, --rotation	: Set image rotation (0-359)
-hf, --hflip	: Set horizontal flip
-vf, --vflip	: Set vertical flip
-roi, --roi	: Set region of interest (x,y,w,d as normalised coordinates [0.0-1.0])
-ss, --shutter	: Set shutter speed in microseconds
-awbg, --awbgains	: Set AWB gains - AWB mode must be off
-drc, --drc	: Set DRC Level (see Notes)
-st, --stats	: Force recomputation of statistics on stills capture pass
-a, --annotate	: Enable/Set annotate flags or text
-3d, --stereo	: Select stereoscopic mode
-dec, --decimate	: Half width/height of stereo image
-3dswap, --3dswap	: Swap camera order for stereoscopic
-ae, --annotateex	: Set extra annotation parameters (text size, text colour(hex YUV), bg colour(hex YUV))
-ag, --analoggain	: Set the analog gain (floating point)
-dg, --digitalgain	: Set the digital gain (floating point)


Notes

Exposure mode options :
off,auto,night,nightpreview,backlight,spotlight,sports,snow,beach,verylong,fixedfps,antishake,fireworks

Flicker avoid mode options :
off,auto,50hz,60hz

AWB mode options :
off,auto,sun,cloud,shade,tungsten,fluorescent,incandescent,flash,horizon

Image Effect mode options :
none,negative,solarise,sketch,denoise,emboss,oilpaint,hatch,gpen,pastel,watercolour,film,blur,saturation,colourswap,washedout,posterise,colourpoint,colourbalance,cartoon

Metering Mode options :
average,spot,backlit,matrix

Dynamic Range Compression (DRC) options :
off,low,med,high

# webcam-capture-driver-screencapture

This is capture driver which is able to capture video feed from your screen devices. It uses AWT Robot under
the hood. Every screen device connected to your computer will be abstracted as a separate webcam device.

## Maven

Stable:

```xml
<dependency>
	<groupId>com.github.sarxos</groupId>
	<artifactId>webcam-capture-driver-screencapture</artifactId>
	<version>0.3.12</version>
</dependency>
```

Snapshot:

```xml
<repository>
    <id>Sonatype OSS Snapshot Repository</id>
    <url>http://oss.sonatype.org/content/repositories/snapshots</url>
</repository>
```
```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-screencapture</artifactId>
    <version>0.3.13-SNAPSHOT</version>
</dependency>
```

## How To Use

Set capture driver before you start using Webcam class.

```java
import java.awt.Dimension;
import java.awt.FlowLayout;

import javax.swing.JFrame;

import com.github.sarxos.webcam.Webcam;
import com.github.sarxos.webcam.WebcamPanel;
import com.github.sarxos.webcam.WebcamPanel.DrawMode;
import com.github.sarxos.webcam.WebcamResolution;
import com.github.sarxos.webcam.ds.gstreamer.ScreenCaptureDriver;


public class WebcamPanelExample {

	static {
		Webcam.setDriver(new ScreenCaptureDriver());
	}

	public static void main(String[] args) throws InterruptedException {

		final JFrame window = new JFrame("Screen Capture Example");
		window.setResizable(true);
		window.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		window.getContentPane().setLayout(new FlowLayout());

		final Dimension resolution = WebcamResolution.QVGA.getSize();

		for (final Webcam webcam : Webcam.getWebcams()) {

			webcam.setCustomViewSizes(resolution);
			webcam.setViewSize(resolution);
			webcam.open();

			final WebcamPanel panel = new WebcamPanel(webcam);
			panel.setFPSDisplayed(true);
			panel.setDrawMode(DrawMode.FIT);
			panel.setImageSizeDisplayed(true);
			panel.setPreferredSize(resolution);

			window.getContentPane().add(panel);
		}

		window.pack();
		window.setVisible(true);
	}
}
```
The picture below is an effect of the above code running. All my three screens are captured in real time.

![](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-drivers/driver-screencapture/src/etc/resources/screen-1.jpg?raw=true)

## More Examples

Please check [this](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-screencapture/src/example/java) directory to see more examples.

![](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-drivers/driver-screencapture/src/etc/resources/screen-2.jpg)

## Known Problems

1. I noticed this on my Ubuntu Linux - black regions appear in place where other application (e.g. Cairo Dock)
   render OpenGL content. I don't know about any workaround or solution for this problem other than disabling
   these applications. Not verified on Mac and Windows. Please report
   [new issue](https://github.com/sarxos/webcam-capture/issues/new) if you know how to fix this. 

## Capture Driver License

Copyright (C) 2012 - 2018 Bartosz Firyn <https://github.com/sarxos> and contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

# webcam-capture-driver-v4l4j

This is capture driver which uses [V4L4J](http://code.google.com/p/v4l4j) project to access camera devices. It uses V4L4J customized fork available [here](https://github.com/sarxos/v4l4j).

Currently this is the most stable capture driver to be used with the Raspberry Pi boards.

**NOTE!** This driver supports only UVC devices and therefore it will not work with the Raspberry Pi dedicated camera module.

## Maven

Stable:

```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-v4l4j</artifactId>
    <version>0.3.12</version>
</dependency>
```

Snapshot:

```xml
<repository>
    <id>Sonatype OSS Snapshot Repository</id>
    <url>http://oss.sonatype.org/content/repositories/snapshots</url>
</repository>
```
```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-v4l4j</artifactId>
    <version>0.3.13-SNAPSHOT</version>
</dependency>
```

## Example

```java
static {
	Webcam.setDriver(new V4l4jDriver());
}

public static void main(String[] args) {
	JFrame frame = new JFrame("V4L4J Webcam Capture Driver Demo");
	frame.add(new WebcamPanel(Webcam.getDefault()));
	frame.pack();
	frame.setVisible(true);
	frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
}
```

## License

This specific driver is distributed under the terms of [GNU GPL v3](http://www.gnu.org/copyleft/gpl.html) license.
# webcam-capture-driver-vlcj

This is capture driver which uses [vlcj](http://www.capricasoftware.co.uk/projects/vlcj/index.html) library from [Caprica Software Limited](http://www.capricasoftware.co.uk/) to gain access to the camera device.

**NOTE!** On Windows one needs to provide list of webcam devices manually because ```vlclib``` does not implement video devices discovery on this platform (please see [this example](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-drivers/driver-vlcj/src/example/java/WebcamPanelForWindows.java) to find out how this should be done).

The vlcj library is distributed according to the terms of the [GPL](http://www.gnu.org/licenses/gpl.html) license.

## Maven

Stable:

```xml
<dependency>
	<groupId>com.github.sarxos</groupId>
	<artifactId>webcam-capture-driver-vlcj</artifactId>
	<version>0.3.12</version>
</dependency>
```

Snapshot:

```xml
<repository>
    <id>Sonatype OSS Snapshot Repository</id>
    <url>http://oss.sonatype.org/content/repositories/snapshots</url>
</repository>
```
```xml
<dependency>
    <groupId>com.github.sarxos</groupId>
    <artifactId>webcam-capture-driver-vlcj</artifactId>
    <version>0.3.13-SNAPSHOT</version>
</dependency>
```

## How To Use

Set capture driver before you start using Webcam class:

```java
public class TakePictureExample {

	// set capture driver for fswebcam tool
	static {
		Webcam.setDriver(new VlcjDriver());
	}

	public static void main(String[] args) throws IOException {

		// get default webcam and open it
		Webcam webcam = Webcam.getDefault();
		webcam.open();

		// get image from webcam device
		BufferedImage image = webcam.getImage();

		// save image to PNG file
		ImageIO.write(image, "JPG", new File("test.jpg"));

		// close webcam
		webcam.close();
	}
}
```

## Capture Driver License

Copyright (C) 2012 - 2017 Bartosz Firyn <https://github.com/sarxos>

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

JNA is dual-licensed under 2 alternative Open Source/Free
licenses: LGPL 2.1 and Apache License 2.0. (starting with
JNA version 4.0.0).

What this means is that one can choose either one of these
licenses (for purposes of re-distributing JNA; usually by
including it as one of jars another application or
library uses) by downloading corresponding jar file,
using it, and living happily everafter.

You may obtain a copy of the LGPL License at:

http://www.gnu.org/licenses/licenses.html

A copy is also included in the downloadable source code package
containing JNA, in file "LGPL2.1", under the same directory
as this file.

You may obtain a copy of the ASL License at:

http://www.apache.org/licenses/

A copy is also included in the downloadable source code package
containing JNA, in file "ASL2.0", under the same directory
as this file.
		   GNU LESSER GENERAL PUBLIC LICENSE
                       Version 3, 29 June 2007

 Copyright (C) 2007 Free Software Foundation, Inc. <http://fsf.org/>
 Everyone is permitted to copy and distribute verbatim copies
 of this license document, but changing it is not allowed.


  This version of the GNU Lesser General Public License incorporates
the terms and conditions of version 3 of the GNU General Public
License, supplemented by the additional permissions listed below.

  0. Additional Definitions.

  As used herein, "this License" refers to version 3 of the GNU Lesser
General Public License, and the "GNU GPL" refers to version 3 of the GNU
General Public License.

  "The Library" refers to a covered work governed by this License,
other than an Application or a Combined Work as defined below.

  An "Application" is any work that makes use of an interface provided
by the Library, but which is not otherwise based on the Library.
Defining a subclass of a class defined by the Library is deemed a mode
of using an interface provided by the Library.

  A "Combined Work" is a work produced by combining or linking an
Application with the Library.  The particular version of the Library
with which the Combined Work was made is also called the "Linked
Version".

  The "Minimal Corresponding Source" for a Combined Work means the
Corresponding Source for the Combined Work, excluding any source code
for portions of the Combined Work that, considered in isolation, are
based on the Application, and not on the Linked Version.

  The "Corresponding Application Code" for a Combined Work means the
object code and/or source code for the Application, including any data
and utility programs needed for reproducing the Combined Work from the
Application, but excluding the System Libraries of the Combined Work.

  1. Exception to Section 3 of the GNU GPL.

  You may convey a covered work under sections 3 and 4 of this License
without being bound by section 3 of the GNU GPL.

  2. Conveying Modified Versions.

  If you modify a copy of the Library, and, in your modifications, a
facility refers to a function or data to be supplied by an Application
that uses the facility (other than as an argument passed when the
facility is invoked), then you may convey a copy of the modified
version:

   a) under this License, provided that you make a good faith effort to
   ensure that, in the event an Application does not supply the
   function or data, the facility still operates, and performs
   whatever part of its purpose remains meaningful, or

   b) under the GNU GPL, with none of the additional permissions of
   this License applicable to that copy.

  3. Object Code Incorporating Material from Library Header Files.

  The object code form of an Application may incorporate material from
a header file that is part of the Library.  You may convey such object
code under terms of your choice, provided that, if the incorporated
material is not limited to numerical parameters, data structure
layouts and accessors, or small macros, inline functions and templates
(ten or fewer lines in length), you do both of the following:

   a) Give prominent notice with each copy of the object code that the
   Library is used in it and that the Library and its use are
   covered by this License.

   b) Accompany the object code with a copy of the GNU GPL and this license
   document.

  4. Combined Works.

  You may convey a Combined Work under terms of your choice that,
taken together, effectively do not restrict modification of the
portions of the Library contained in the Combined Work and reverse
engineering for debugging such modifications, if you also do each of
the following:

   a) Give prominent notice with each copy of the Combined Work that
   the Library is used in it and that the Library and its use are
   covered by this License.

   b) Accompany the Combined Work with a copy of the GNU GPL and this license
   document.

   c) For a Combined Work that displays copyright notices during
   execution, include the copyright notice for the Library among
   these notices, as well as a reference directing the user to the
   copies of the GNU GPL and this license document.

   d) Do one of the following:

       0) Convey the Minimal Corresponding Source under the terms of this
       License, and the Corresponding Application Code in a form
       suitable for, and under terms that permit, the user to
       recombine or relink the Application with a modified version of
       the Linked Version to produce a modified Combined Work, in the
       manner specified by section 6 of the GNU GPL for conveying
       Corresponding Source.

       1) Use a suitable shared library mechanism for linking with the
       Library.  A suitable mechanism is one that (a) uses at run time
       a copy of the Library already present on the user's computer
       system, and (b) will operate properly with a modified version
       of the Library that is interface-compatible with the Linked
       Version.

   e) Provide Installation Information, but only if you would otherwise
   be required to provide such information under section 6 of the
   GNU GPL, and only to the extent that such information is
   necessary to install and execute a modified version of the
   Combined Work produced by recombining or relinking the
   Application with a modified version of the Linked Version. (If
   you use option 4d0, the Installation Information must accompany
   the Minimal Corresponding Source and Corresponding Application
   Code. If you use option 4d1, you must provide the Installation
   Information in the manner specified by section 6 of the GNU GPL
   for conveying Corresponding Source.)

  5. Combined Libraries.

  You may place library facilities that are a work based on the
Library side by side in a single library together with other library
facilities that are not Applications and are not covered by this
License, and convey such a combined library under terms of your
choice, if you do both of the following:

   a) Accompany the combined library with a copy of the same work based
   on the Library, uncombined with any other library facilities,
   conveyed under the terms of this License.

   b) Give prominent notice with the combined library that part of it
   is a work based on the Library, and explaining where to find the
   accompanying uncombined form of the same work.

  6. Revised Versions of the GNU Lesser General Public License.

  The Free Software Foundation may publish revised and/or new versions
of the GNU Lesser General Public License from time to time. Such new
versions will be similar in spirit to the present version, but may
differ in detail to address new problems or concerns.

  Each version is given a distinguishing version number. If the
Library as you received it specifies that a certain numbered version
of the GNU Lesser General Public License "or any later version"
applies to it, you have the option of following the terms and
conditions either of that published version or of any later version
published by the Free Software Foundation. If the Library as you
received it does not specify a version number of the GNU Lesser
General Public License, you may choose any version of the GNU Lesser
General Public License ever published by the Free Software Foundation.

  If the Library as you received it specifies that a proxy can decide
whether future versions of the GNU Lesser General Public License shall
apply, that proxy's public statement of acceptance of any version is
permanent authorization for you to choose that version for the
Library.
In this directory you can find some more or less complicated examples
of how Webcam Capture can be used with additional 3'rd party frameworks.

Enjoy!
# Webcam Capture Example Applet

This example presents how to create Java Applet using Webcam Capture project.

You can check working example [here](http://webcam-capture.sarxos.pl/examples/applet).

## Generate Java Keystore

Since our Applet will be using users hardware, we have to either sign it, or 
specify appropriate permissions. Without doing this user will get ```SecurityPermissionException```
when trying to use Applet. This is because Java restrict access to various system elements 
(filesystem, hardware, etc). But when you sign application, Java assume it is safe (since 
you signed it with your personal certificate), and grant access to the system hardware after
user confirm security dialog. 

Therefore, before you start build you have to generate Java keystore which will be used
later by Maven to sign Applet JAR. To do that you have to use ```keytool``` program 
available within JDK ```bin``` directory.

```
$ keytool -genkey -alias example -keyalg RSA -keystore keystore.jks -keysize 2048
```

After executing this command, ```keytool``` will ask you to provide all required information,
such as:

* Keystore password,
* First and last name,
* Your organizational unit name,
* Your organization name,
* City or Locality,
* State or Province name,
* Two-letter country code for this unit,
* Key password for alias (in this case alias is _example_).

In this example, in root directory, I included predefined keystore with alias
_example_ with password _test1234_.

## How To Build

Like in all my other projects you have to have Maven 3.0 or later available in ```PATH```. 
You can download Maven binaries from **[here](http://maventest.apache.org/download.html)**.

When you have Maven on your PC, it's enough to run this command to build project:

```
$ mvn clean install
```

This will cause ```target``` directory to be created, where will find output JAR together 
with ```index.html``` file which both should be deployed to the server.

## Where Are All Required JARs Gone?

None is required in this example. That's because I used _maven-shade-plugin_ to merge all JARs together, so 
you will get only one JAR with all required classes inside (this is known as shaded JAR).

For more details I suggest to check ```pom.xml``` or [google](https://www.google.pl/search?q=shaded+jar+maven&ie=utf-8&oe=utf-8&aq=t&rls=org.mozilla:en-US:official&client=firefox-a).

## How To Sign JAR?

You don't have to. Maven will do that for you. This has been done by using _maven-jarsigner-plugin_
which is using ```keystore.jks``` file to get self-signed certificate and use it to sign the JAR.

## How To Upload Applet To Server?

Use FTP client of your choice and upload these files to the remote site:

* ```webcam-capture-example-applet-[version].jar```
* ```index.html```

You can also modify ```pom.xml``` and add [maven-upload-plugin](http://docs.atlassian.com/maven-upload-plugin/1.1/usage.html)
to automatically upload specific files to the server when running ```mvn deploy```.

## How To Run

Simply access remote site URL. Follow the security confirmation dialog and enjoy 
using this example.

![Security Dialog](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-applet/src/etc/resources/security.png "Security Dialog")

Et voilà! My son's picture is visible in Applet window.

![Running Applet](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-applet/src/etc/resources/applet.png "Running Applet")

## License

Copyright (C) 2012 Bartosz Firyn

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


# Webcam Capture Detect Face Example

This simple example show how to use painter interface and default painter 
to mark located face, which has been found using awesome [OpenIMAJ](http://www.openimaj.org/)
framework.
 
## What Is This

This example presents how to use custom painter with conjunction of default one to alter
image displayed in `WebcamPanel` component.

In this example I used Haar Cascade from [OpenIMAJ](http://www.openimaj.org/) to detect faces.


### Screenshoots:

The Trolls:

![The Trolls](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-detect-face/src/etc/resources/faces.jpg "The Trolls")


## License

Copyright (C) 2013 Bartosz Firyn

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
Icon from http://www.iconarchive.com/show/vista-hardware-devices-icons-by-icons-land/Security-Camera-icon.html

Artist: Icons-Land (Available for custom work)
Iconset: Vista Hardware Devices Icons (28 icons)
License: Free for non-commercial use.
Commercial usage: Not allowed
# JavaFX Example With Webcam Capture API

This simple example, generously provided by Rakesh Bhatt ([rakeshbhatt10](https://github.com/rakeshbhatt10)),
demonstrates how to use Webcam Capture API inside JavaFX application. 
FXML is not used at all and complete scene structure is composed directly 
in the Java code. For the FXML demonstration check another example available [here](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-javafx-fxml). 

Original project can be found [here](https://github.com/rakeshbhatt10/WebCamJavaFXSampleSarcoxAPI).

Thank you Rakesh!


## How To Build

By using Maven:


```plain
$ cd webcam-capture-examples/webcam-capture-javafx
$ mvn clean package
```

The executable JAR, together with all required dependencies (inside ```lib``` folder), 
will be placed in ```target/jfx/app``` directory.


## Screenshoots

![javafx1.png](https://raw.githubusercontent.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-javafx/src/etc/resources/javafx1.png)
![javafx2.png](https://raw.githubusercontent.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-javafx/src/etc/resources/javafx2.png)


## License

Copyright (C) 2014 Rakesh Bhatt (https://github.com/rakeshbhatt10)
# JavaFX Example With Webcam Capture API

This simple example, generously provided by Rakesh Bhatt ([rakeshbhatt10](https://github.com/rakeshbhatt10)),
demonstrates how to use Webcam Capture API inside JavaFX application with 
scene constructed with FXML and simple FXML controller.

Original project can be found [here](https://github.com/rakeshbhatt10/WebCamJavaFXFXMLSample).

Thank you Rakesh!


## How To Build

By using Maven:


```plain
cd webcam-capture-examples/webcam-capture-javafx-fxml
mvn clean package
```

The executable JAR, together with all required dependencies (inside ```lib``` folder), 
will be placed in ```target/jfx/app``` directory.


## Screenshoots

![javafx-fxml.png](https://raw.githubusercontent.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-javafx-fxml/src/etc/resources/javafx-fxml.png)


## License

Copyright (C) 2014 Rakesh Bhatt (https://github.com/rakeshbhatt10)
## Webcam Capture Live Streaming Example

This example has been created by [james-d](https://github.com/james-d) in response to [this question](http://stackoverflow.com/questions/42816859/run-javafx-and-swing-application-at-the-same-time) on Stack Overflow and put in [this gist](https://gist.github.com/james-d/f826c9f38d53628114124a56fb7c4557).

James found that, in general, the FX application thread is prone to hanging if you interact with the webcam much at all on that thread. E.g. ```webcam.close()``` or ```Webcam.getWebcams()``` seem to cause deadlock (on Mac OS X Sierra on a Macbook Pro with built-in camera) and created a couple of wrapper classes that wrap the Webcam as a JavaFX service and a corresponding view.

### How To Use

1. Simply run [FXCamTest](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-examples/webcam-capture-javafx-service/src/main/java/FXCamTest.java).

#### Notes

1. Not a production quiality code.
2. Java 8 is required to build it.

## Webcam Capture Live Streaming Example

This example demonstrate how to encode set of buffered images obtained 
from ```Webcam``` instance, transcode into h.264 stream and send to remote peer
where it is decoded and rendered in panel.

Example provided by [hepin1989](https://github.com/hepin1989). Thank you! This is wonderful piece of the good code :)

### How To Use

1. Run [StreamServer](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-examples/webcam-capture-live-streaming/src/main/java/us/sosia/video/stream/agent/StreamServer.java) - this will open the webcam device and start listening for incoming streaming requests.
2. Run [StreamClient](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-examples/webcam-capture-live-streaming/src/main/java/us/sosia/video/stream/agent/StreamClient.java) - this will connect to the StreamServer and start displaying image from the remote camera.

The server / client address is ```localhost``` by default to run client and server on the same machine, but if you want to stream over the network, you need to change it to reflect your _real_ IP address (server must bind to ```eth0``` instead of ```lo``` interface to be visible from the NAT).

#### Notes

1. The code supports sunny-day scenario only, just to demonstrate the idea, so there are is no complex error checking statements and the code may behave in unexpected manner when launched in _real_ network.
2. It uses [Xuggler](https://github.com/artclarke/xuggle-xuggler) which seems to be discontinued.
3. Remember, this example is to present an idea, so if you need enhancement or bug fix, please implement it and send pull request to share it with community. Be creative :)
4. To perform streaming over the network you need to change address in server from ```localhost``` to your real IP address (e.g. such as ```192.168.1.10``` or ```0.0.0.0``` in general). I'm not sure how it works with the IPv6 support - feel free to test it.
# Webcam Capture Many Cameras Example

This example proves that displaying image from multiple web cameras at once is
practically possible. This example will work with only one camera too, but in
general, it will use all cameras you have connected to your PC. To perform this
test I had to connect [Microsoft LifeCam VX-1000](https://www.google.com/search?q=Microsoft+LifeCam+VX-1000&tbm=isch)
camera to my laptop USB port. 

Just a not:

This is very interesting. I found that build-in camera initialization in my 
case (HP HD webcam) requires about 8 seconds for camera to be ready, and USB 
is ready in less than 1 second.

Camera used to perform tests:

![Camera](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-manycams/src/etc/resources/camera.jpg "Camera")

### Screenshoots:

Not yet running:

![Not Running](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-manycams/src/etc/resources/not-running.jpg "Not Running")

Running:

![Webcam Capture Many Cameras](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-manycams/src/etc/resources/two-cams.jpg "Webcam Capture Many Cameras")

## License

Copyright (C) 2012 Bartosz Firyn

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
# Webcam Capture Motion Detector Example

This is simple application illustrating of how to use build-in motion detector.
 
## Detect Motion

Detector use data from webcam and perform numeric analysis to decide if there 
is a motion, or there is none.

This sample application uses ```while / isMotion()``` approach (the second way
to use motion detector is listener approach). It display Me Gusta Guy when motion
has been detected and Forever Alone Guy when no motion has been detected. In this
example motion inertia is 1000 milliseconds. 

### Some screenshoots:

When motion has ben detected (my son's teddy bear was in move):

![Movement](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-motiondetector/src/etc/resources/movement.png "Movement")

When there was no motion at all:

![No motion](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-motiondetector/src/etc/resources/nothing.png "No motion")

## License

Copyright (C) 2012 Bartosz Firyn

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
# Webcam Capture Custom Painter Example

This simple example show how to create custom painter for `WebcamCapture` Swing 
component used to draw images from `Webcam` instance.
 
## What Is This

This example presents how to use custom painters to alter image displayed in 
`WebcamPanel` component. Usually, if user won't change it, `DefaultPainter` is
being used. This painter implements `Painter` interface which consists of two methods:

* `paintPanel(WebcamPanel wp, Graphics2D g2)` which paints panel when image from camera
is not disdplayed, and second one,
* `paintImage(WebcamPanel wp, BufferedImage img, Graphics2D g2)` which pains image from
camera when camera is turned on.

In this example I used filters from awesome image processing library by
_[Jerry Huxtable Labs](http://www.jhlabs.com/)_
which descriptions be found **[here](http://www.jhlabs.com/ip/filters/)** and which can be
[downloaded](http://search.maven.org/#artifactdetails|com.jhlabs|filters|2.0.235|jar) from Maven Central.

[Look and Feel](http://docs.oracle.com/javase/tutorial/uiswing/lookandfeel/plaf.html) 
used in all examples can be found in [Insubstantial](https://github.com/Insubstantial/insubstantial) project.
The one I used in this example is `SubstanceTwilightLookAndFeel`. Thank you 
_[Kirill](http://www.linkedin.com/in/kirillcool)_ for this awesome Look and Feel stuff! 

### Screenshoots:

Capturing is disabled:

![Capturing Disabled](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-painter/src/etc/resources/not-displayed.png "Capturing Disabled")

Possible filters (only few from whole JS Labs filters set):

![Filters](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-painter/src/etc/resources/filters.png "Filters")

Crystallize filter:

![Crystallize](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-painter/src/etc/resources/crystallize.png "Crystallize")

Dither filter:

![Dither](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-painter/src/etc/resources/dither.png "Dither")

Invert filter:

![Invert](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-painter/src/etc/resources/invert.png "Invert")

Kaleidoscope filter:

![Kaleidoscope](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-painter/src/etc/resources/kaleidoscope.png "Kaleidoscope")

Noise filter:

![Noise](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-painter/src/etc/resources/noise.png "Noise")

Sphere filter:

![Sphere](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-painter/src/etc/resources/sphere.png "Sphere")

Threshold filter:

![Threshold](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-painter/src/etc/resources/threshold.png "Threshold")

## License

Copyright (C) 2012 Bartosz Firyn

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
# Webcam Capture QR Code Reader Example

This example show how to read QR and bar codes with Webcam Capture.
 
## What Is This

This example show how to process QR and bar codes with your webcam using 
[Webcam Capture](https://github.com/sarxos/webcam-capture) 
project together with awesome [ZXing](https://github.com/zxing/zxing) library.

Youtube video demonstrating how it is working is [available here](http://youtu.be/JLUJWgveEco). 

### Screenshoots:

First I took a picture of some sample QR code I found on Google 
([link](http://www.google.pl/imgres?um=1&hl=pl&client=firefox-a&sa=N&tbo=d&rls=org.mozilla:en-US:official&biw=1366&bih=552&tbm=isch&tbnid=ZnVvKF0A2BGNTM:&imgrefurl=http://www.qrstuff.com/&docid=1A-zeI71ulZS1M&imgurl=http://www.qrstuff.com/images/sample.png&w=3000&h=3000&ei=yLSwUNTdCIOC4gS1xIGIBQ&zoom=1&iact=hc&vpx=154&vpy=141&dur=1160&hovh=225&hovw=225&tx=124&ty=78&sig=117284320547613276213&page=1&tbnh=149&tbnw=159&start=0&ndsp=24&ved=1t:429,r:1,s:0,i:87))
and then put it opposite to my build-in PC web camera.

In the application window webcam image is displayed on the left side, and on the right
side there is a text area containing QR code data. In this case this is just a link
to the web page from where I took my QR code example.

![QR Code Example Application](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-qrcode/src/etc/resources/qrcode-zxing.png "QR Code Example Application")

Some bar codes:

![Bar Code 1](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-qrcode/src/etc/resources/bar1.jpg "Bar Code 1")
![Bar Code 2](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-qrcode/src/etc/resources/bar2.jpg "Bar Code 2")
![Bar Code 3](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-qrcode/src/etc/resources/bar3.jpg "Bar Code 3")

Some QR codes:

![QR Code 2](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-qrcode/src/etc/resources/qrcode2.jpg "QR Code 2")
![QR Code 3](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-qrcode/src/etc/resources/qrcode3.jpg "QR Code 3")
![QR Code 4](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-qrcode/src/etc/resources/qrcode4.jpg "QR Code 4")
![QR Code 5](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-qrcode/src/etc/resources/qrcode5.jpg "QR Code 5")
![QR Code 6](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-qrcode/src/etc/resources/qrcode6.jpg "QR Code 6")

## License

Copyright (C) 2012 Bartosz Firyn

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
# WebcamPanel in SWT Application Example

This example show one of the methods of how ```WebcamPanel``` can be used 
in SWT-based appliaction.


# Webcam Capture Image Transformer Example

This simple example show how to use webcam image transformer feature.
 
## What Is This

This example presents how to use transformation feature to paint a frame on
the image. The goal of this simple application is to draw transparent frame
at the image from the camera video feed. The frame is created from the normal
PNG file with alpha channel. The inner part of the image is completely transparent.

The frame image has been found on [pixabay.com](http://pixabay.com/) and can
be downloaded from [here](http://pixabay.com/pl/rozk%C5%82ad-jazdy-ramki-potw%C3%B3r-183669).
It's redistributed under Creative Commons Deed CC0 license.

### Screenshoots:

The frame only:

![Frame](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-transformer/src/main/resources/frame.png "Frame")

And how the application actually works:

![Screenshoot](https://raw.github.com/sarxos/webcam-capture/master/webcam-capture-examples/webcam-capture-transformer/src/etc/resources/screen.png "Screenshoot")

## Frame Image License

[Creative Commons Deed CC0](http://creativecommons.org/publicdomain/zero/1.0/)

## Code License

Copyright (C) 2014 Bartosz Firyn

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
# Webcam WebSockets Example

This example demonstrates how images feed can be transported over the WebSocket. 
 
## What Is This

This example has been prepared to demonstrate very primitive way to transport images from server to frontend using HTML5 WebSockets.

After the ```WebcamWebSocketsExample``` is started, the server starts on port 8123. Front end can subscribe to new images by accessing ```ws://127.0.0.1:8123/```.

The example is composed of server and frontend parts:

* [Server - Java files](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-websockets/src/main/java)
* [Frontend - HTML, JavaScript and CSS](https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-websockets/src/main/html)

## Screenshoots

![web page](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-examples/webcam-capture-websockets/src/etc/resources/screen.png?raw=true "web page")

![initializing](https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-examples/webcam-capture-websockets/src/etc/resources/screen2.png?raw=true "initializing")


## License

Copyright (C) 2015 Bartosz Firyn

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
# Webcam Capture Pages

This project is to generate the website.

### Update Site From README.md

To regenerate HTML from ```README.md``` file the following must be done:

```plain
$ cd webcam-capture-pages
$ mvn clean process-sources
```

After the Maven completed all its tasks, the newest website code is available in ```src/main/resources/html```.

### Upload File via FTP/SCP

Just use your tool of choice to deploy the site to the server.

<!doctype html>
<html>
  <head>
    <meta charset="utf-8">
    <meta http-equiv="X-UA-Compatible" content="chrome=1">
    <title>Webcam Capture in Java</title>
    <link rel="stylesheet" href="stylesheets/styles.css">
    <link rel="stylesheet" href="stylesheets/pygment_trac.css">
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js"></script>
    <script src="javascripts/main.js"></script>
    <script src="examples/google-code-prettify/prettify.js"></script>
    <link rel="stylesheet" href="examples/google-code-prettify/sons-of-obsidian-2.css">
    <!--[if lt IE 9]>
      <script src="//html5shiv.googlecode.com/svn/trunk/html5.js"></script>
    <![endif]-->
    <meta name="viewport" content="width=device-width, initial-scale=1, user-scalable=no">
  </head>
  <body>
  
      <a href="https://github.com/sarxos/webcam-capture"><img style="position: absolute; top: 0; right: 0; border: 0; z-index: 100;" src="https://s3.amazonaws.com/github/ribbons/forkme_right_red_aa0000.png"></a>

      <header>
        <h1>Webcam Capture</h1>
        <p>Generic Webcam Java API</p>
      </header>

      <div id="banner">
        <span id="logo"></span>

        <a href="https://github.com/sarxos/webcam-capture" class="button fork"><strong>GitHub</strong></a>
        <div class="downloads">
          <span>Download:</span>
          <ul>
            <li><a href="https://github.com/sarxos/webcam-capture/releases/download/webcam-capture-parent-0.3.10/webcam-capture-0.3.10-dist.zip" class="button">ZIP</a></li>
          </ul>
        </div>
      </div><!-- end banner -->

    <div class="wrapper">
      <nav>
        <ul></ul>
      </nav>
      <section>

      <!-- markdown header end -->
<h1>Webcam Capture API</h1><p>This library allows you to use your build-in or external webcam directly from Java. It's designed to abstract commonly used camera features and support various capturing farmeworks.</p><p><a href="http://search.maven.org/#artifactdetails|com.github.sarxos|webcam-capture|0.3.10|bundle"><img src="https://maven-badges.herokuapp.com/maven-central/com.github.sarxos/webcam-capture/badge.svg"  alt="Maven Central"/></a><br/><a href="http://travis-ci.org/sarxos/webcam-capture"><img src="https://img.shields.io/travis/sarxos/webcam-capture.svg?branch=master"  alt="Build Status"/></a><br/><a href="https://coveralls.io/r/sarxos/webcam-capture?branch=master"><img src="https://img.shields.io/coveralls/sarxos/webcam-capture.svg?branch=master"  alt="Coverage Status"/></a></p><h2>Rationale</h2><p>Assume situation when your code depends on some capturing framework, but suddenly you have to drop it and use different, maybe newer one (e.g. replace archaic JMF with newest GStreamer). By doing this you will have to rewrite significant piece of your code because these frameworks are completely different and not compatible at all. This is where Webcam Capture API comes to save the world - it was created to remove the burden of such situations so you do not have to rewrite your code never again, but instead you can simply switch the driver class to different one.</p><h2>Features</h2>
<ul>
  <li>Simple, thread-safe and non-blocking API,</li>
  <li>No additional software required,</li>
  <li>Supports multiple platforms (Windows, Linux, Mac OS, etc) and various architectures (32-bit, 64-bit, ARM),</li>
  <li>Get images from build-in or USB-connected PC webcams,</li>
  <li>Get images from IP / network cameras (as MJPEG or JPEG),</li>
  <li>Offers ready to use motion detector,</li>
  <li>All required JARs Available in Maven Central,</li>
  <li>Offers possibility to expose images as MJPEG stream,</li>
  <li>It is available as Maven dependency or standalone ZIP binary (with all dependencies included),</li>
  <li>Swing component to display video feed from camera,</li>
  <li>Swing component to choose camera (drop down),</li>
  <li>Multiple capturing frameworks are supported:</li>
  <li><a href="http://www.openimaj.org/">OpenIMAJ</a>,</li>
  <li><a href="http://sourceforge.net/projects/lti-civil/">LTI CIVIL</a>,</li>
  <li><a href="http://www.oracle.com/technetwork/java/javase/tech/index-jsp-140239.html">Java Media Framework (JMF)</a>,</li>
  <li><a href="http://fmj-sf.net/">Freedom for Media in Java (FMJ)</a>,</li>
  <li><a href="http://opencv.org/">OpenCV</a> via <a href="https://github.com/bytedeco/javacv">JavaCV</a>,</li>
  <li><a href="http://www.videolan.org/vlc/">VLC</a> via <a href="http://www.capricasoftware.co.uk/projects/vlcj/index.html">vlcj</a>,</li>
  <li><a href="http://gstreamer.freedesktop.org/">GStreamer</a> (0.10.x only) via <a href="https://code.google.com/p/gstreamer-java/">gstreamer-java</a></li>
  <li>MJPEG IP Cameras,</li>
</ul><p>The latest stable version is: <strong><code>0.3.11</code></strong></p><p>The latest development version is: <strong><code>0.3.12-SNAPSHOT</code></strong></p><h2>Raspberry PI</h2><p><em>(and other ARM devices)</em></p><p>The lates version (0.3.10) does not work on ARM just out of the box. To make it working you need to replace version 0.6.2 of BridJ JAR by the <a href="https://oss.sonatype.org/service/local/artifact/maven/redirect?r=snapshots&g=com.nativelibs4java&a=bridj&v=0.6.3-SNAPSHOT">0.6.3-SNAPHOST</a> or newer <a href="http://maven.ecs.soton.ac.uk/content/groups/maven.openimaj.org/com/nativelibs4java/bridj/0.7-20140918/bridj-0.7-20140918.jar">bridj-0.7-20140918</a>. Moreover, lately Jonathon Hare from OpenIMAJ team, found a problem described in <a href="https://github.com/ochafik/nativelibs4java/issues/525">bridj #525</a> which causes problems on armhf architecture.</p><h2>Maven</h2><p>The latest stable version is <a href="http://search.maven.org/#artifactdetails|com.github.sarxos|webcam-capture|0.3.11|bundle">available</a> in Maven Central:</p>
<pre><code class="xml">&lt;dependency&gt;
  &lt;groupId&gt;com.github.sarxos&lt;/groupId&gt;
  &lt;artifactId&gt;webcam-capture&lt;/artifactId&gt;
  &lt;version&gt;0.3.11&lt;/version&gt;
&lt;/dependency&gt;
</code></pre><p>Snapshot version:</p>
<pre><code class="xml">&lt;repository&gt;
	&lt;id&gt;Sonatype OSS Snapshot Repository&lt;/id&gt;
	&lt;url&gt;http://oss.sonatype.org/content/repositories/snapshots&lt;/url&gt;
&lt;/repository&gt;
</code></pre>
<pre><code class="xml">&lt;dependency&gt;
	&lt;groupId&gt;com.github.sarxos&lt;/groupId&gt;
	&lt;artifactId&gt;webcam-capture&lt;/artifactId&gt;
	&lt;version&gt;0.3.12-SNAPSHOT&lt;/version&gt;
&lt;/dependency&gt;
</code></pre><h2>Download</h2><p>The newest stable version can be downloaded as separated ZIP binary. This ZIP file contains Webcam Capture API itself and all required dependencies (in <code>libs</code> directory). Click on the below link to download it:</p><p><a href="https://github.com/sarxos/webcam-capture/releases/download/webcam-capture-parent-0.3.11/webcam-capture-0.3.11-dist.zip">webcam-capture-0.3.11-dist.zip</a></p><p>The latest development version JAR (aka SNAPSHOT) can be downloaded <a href="https://oss.sonatype.org/service/local/artifact/maven/redirect?r=snapshots&g=com.github.sarxos&a=webcam-capture&v=0.3.12-SNAPSHOT">here</a>.</p><h2>Contribution</h2><p>If you have strong will, spare time, knowledge or even some small amount of money you would like to spent for good purpose you can help developing this awesome Webcam Capture API and make it even better! Several kinds of contributions are very welcome:</p><h5>Star Project</h5><p>If you think this project is great, you would like to help, but you don't know how - you can become project's stargazer. By starring you're making project more popular. Visit <a href="https://github.com/blog/1204-notifications-stars">this</a> link if you would like to learn more about how notifications and stars works on Github.</p><h5>Report Bug or Feature</h5><p>If you've found a bug or you've came-up with some fantastic feature which can make Webcam Capture a better API to use, don't hesitate to <a href="https://github.com/sarxos/webcam-capture/issues/new">create new issue</a> where you can describe in details what the problem is, or what would you like to improve.</p><h5>Perform Tests</h5><p>Since Webcam Capture use some part of native code, it's very hard to cover all supported operating systems. I'm always testing it on 64-bit Ubuntu Linux, Windows XP and Vista (both 32-bit), but I have no possibility to test on Raspberry Pi, Mac OS and 32-bit Linux. Please help and test on those systems if you have such possibility. </p><h5>Write Code</h5><p>If you know Java or C++ you can help developing Webcam Capture by forking repository and sending pull requests. Please visit <a href="http://stackoverflow.com/questions/4384776/how-do-i-contribute-to-others-code-in-github">this</a> link if you don't know how to contribute to other's code at Github. </p><h5>Donate</h5><p>People have expressed a wish to donate a little money. Donating won't get you anything special, other than a warm feeling inside, and possibly urge me to produce more freely available material for Webcam Capture project. You can donate via <a href="https://www.paypal.com">PayPal</a>, just click <a href="https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=UYMENK76CSYZU">donate</a> button available below - it will redirect you to the secured PayPal page where you can provide donation amount (there is no minimal value).</p><p><a href="https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=UYMENK76CSYZU"><img src="https://www.paypalobjects.com/en_US/GB/i/btn/btn_donateCC_LG.gif"  alt="Donate via PayPal"/></a></p><h2>Hello World</h2><p>Code below will capture image from your default webcam and save it in <code>hello-world.png</code> file:</p>
<pre><code class="java">Webcam webcam = Webcam.getDefault();
webcam.open();
ImageIO.write(webcam.getImage(), &quot;PNG&quot;, new File(&quot;hello-world.png&quot;));
</code></pre><h2>More Examples!</h2><p>Below are the very pretty basic examples demonstrating of how Webcam Capture API can be used in the Java code. All can be found in the project source code. Please note that some of those examples may use the newest API which has not yet been released to maven Central. In such a case please make sure you are using the newest Webcam Capture API SNAPSHOT.</p>
<ul>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/DetectWebcamExample.java">How to detect webcam</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/TakePictureExample.java">How to take picture and save to file</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/WebcamPanelExample.java">How to display image from webcam in Swing panel (basic)</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/WebcamViewerExample.java">How to display image from webcam in Swing panel (more advanced)</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/WebcamDiscoveryListenerExample.java">How to listen on camera connection / disconnection events</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/TakePictureDifferentSizeExample.java">How to configure capture resolution</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/CustomResolutionExample.java">How to configure non-standard capture resolution (e.g. HD720)</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/DifferentFileFormatsExample.java">How to save captured image in PNG / JPG / GIF / BMP etc</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/ConcurrentThreadsExample.java">How to capture with many parallel threads</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/DetectMotionExample.java">How to detect motion (text mode only)</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/DetectMotionDoNotEngageZoneExample.java">How to detect motion with Do-Not-Engage zone</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/MultipointMotionDetectionExample.java">How to perform multipoint motion detection</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-drivers/driver-ipcam/src/examples/java/JpegDasdingStudioExample.java">How to display images from multiple IP cameras exposing pictures in JPG format</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-drivers/driver-ipcam/src/examples/java/MjpegLignanoBeachExample.java">How to display image from IP camera exposing MJPEG stream</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-drivers/driver-ipcam/src/examples/java/DualNativeAndMjpegWebcamExample.java">How to use composite driver to display both, build-in and IP camera images</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/wiki/How-To-Configure-Raspberry-Pi">How to work with Raspberry Pi (camera module or UVC device)</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/WebcamPanelFlippingExample.java">How to flip (mirror) image displayed in <code>WebcamPanel</code></a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/WebcamPanelRotationExample.java">How to rotate image displayed in <code>WebcamPanel</code></a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/ImageTransformerRotationExample.java">How to rotate image from camera with <code>WebcamImageTransformer</code></a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture/src/example/java/AdaptiveSizeWriterExample.java">How to use AdaptiveSizeWriter to compress images</a></li>
</ul><p>And here are some more advanced examples, few with quite fancy GUI.</p>
<ul>
  <li><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-detect-face">How to detect and mark human faces</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-examples/webcam-capture-motiondetector">How to use <code>WebcamMotionDetector</code> with the <code>JFrame</code> window</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-applet">How to use webcam capture in Java Applet</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-painter">How to use <code>WebcamPanel.Painter</code> interface to draw effects on <code>WebcamPanel</code> component</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-qrcode">How to read QR / DataMatrix and Bar codes (2 examples)</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-examples/webcam-capture-video-recording/src/main/java/com/github/sarxos/webcam/Encoder.java">How to record video from webcam</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-live-streaming">How to transcode webcam images into live h264 stream</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-javafx">How to use Webcam Capture API in JavaFX</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-javafx-fxml">How to use Webcam Capture API in JavaFX and FXML</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-javafx-service">How to use Webcam Capture API as JavaFX Service and View</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-swt-awt">How to use Webcam Capture API in SWT</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-transformer">How to use <code>WebcamImageTransformer</code> to draw effects directly on image from camera</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-examples/webcam-capture-websockets">How to use Webcam Capture API and WebSockets to transport images from server to web client</a></li>
  <li><a href="https://github.com/sarxos/webcam-capture/blob/master/webcam-capture-examples/webcam-capture-akka/src/main/java/Application.java">How to use Webcam Capture API from Akka</a></li>
</ul><h2>YouTube Tutorials</h2><p>Video series by <a href="https://www.youtube.com/GenuineCoder">Genuine Coder</a> for Webcam Capture beginners:<br/>* <a href="https://www.youtube.com/watch?v=2BHyL_XK8YQ">Java Webcam Capture #1: Introduction and Capturing with 3 lines of code</a><br/>* <a href="https://www.youtube.com/watch?v=dL4MVWJjVVY">Java Webcam Capture #2: Take Images with Different Resolutions</a><br/>* <a href="https://www.youtube.com/watch?v=RkzfFGP60fw">Java Webcam Capture #3: Video Feed from Webcam using Thread</a><br/>* <a href="https://www.youtube.com/watch?v=amMaYzl45Pw">Java Webcam Capture #4: Video Feed from Webcam (Easy Way)</a></p><h2>Capture Drivers</h2><p>Webcam Capture API defines <code>WebcamDriver</code> interface which has been already implemented in several <em>capturing drivers</em> build on top of well-known frameworks used to work with multimedia and cameras. Complete list can be found below.</p><p>By default (if other driver is not specified) library uses <strong>default driver</strong> which consists of small, refined part of awesome <a href="http://sourceforge.net/p/openimaj/home/OpenIMAJ/">OpenIMAJ</a> framework wrapped in thread-safe container. However, there are more ready-to-use drivers which can be used as a replacement or addition to the default one. By utilizing those drivers Webcam Capture can be extended with various new features (e.g. IP camera support). </p><p>List of additional capture drivers includes:</p>
<table>
  <thead>
    <tr>
      <th>Driver Name </th>
      <th>Stable </th>
      <th>Central </th>
      <th>Description </th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-ipcam">ipcam</a> </td>
      <td>yes </td>
      <td>yes </td>
      <td>Driver for IP / network camera </td>
    </tr>
    <tr>
      <td><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-fswebcam">fswebcam</a> </td>
      <td>yes </td>
      <td>yes </td>
      <td>Driver for <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-fswebcam">FSWebcam</a> <a href="http://en.wikipedia.org/wiki/Command-line_interface">CLI</a> tool </td>
    </tr>
    <tr>
      <td><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-gstreamer">gstreamer</a> </td>
      <td>yes </td>
      <td>yes </td>
      <td>Driver for <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-gstreamer">GStreamer</a> framework </td>
    </tr>
    <tr>
      <td><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-openimaj">openimaj</a> </td>
      <td>yes </td>
      <td>yes </td>
      <td>Driver for <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-openimaj">OpenIMAJ</a> framework </td>
    </tr>
    <tr>
      <td><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-v4l4j">v4l4j</a> </td>
      <td>yes </td>
      <td>no </td>
      <td>Driver for <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-v4l4j">V4L4j</a> library </td>
    </tr>
    <tr>
      <td><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-jmf">jmf</a> </td>
      <td>yes </td>
      <td>yes </td>
      <td>Driver for <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-jmf">JMF</a> / <a href="http://fmj-sf.net/">FMJ</a> frameworks </td>
    </tr>
    <tr>
      <td><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-lti-civil">lti-civil</a> </td>
      <td>yes </td>
      <td>yes </td>
      <td>Driver for <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-lti-civil">LTI-CIVIL</a> library </td>
    </tr>
    <tr>
      <td><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-vlcj">vlcj</a> </td>
      <td>yes </td>
      <td>yes </td>
      <td>Driver for <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-vlcj">vlcj</a> library </td>
    </tr>
    <tr>
      <td><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-javacv">javacv</a> </td>
      <td>yes </td>
      <td>yes </td>
      <td>Driver for <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-javacv">JavaCV</a> library </td>
    </tr>
    <tr>
      <td><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-ffmpeg-cli">ffmpeg-cli</a> </td>
      <td>poc </td>
      <td>no </td>
      <td>Driver for <a href="http://www.ffmpeg.org/">FFmpeg</a> <a href="http://en.wikipedia.org/wiki/Command-line_interface">CLI</a> tool </td>
    </tr>
  </tbody>
</table>
<ul>
  <li>Central = available in Maven Central Repository</li>
  <li><em>poc</em> = Proof of Concept</li>
</ul><h3>Default Driver</h3><p>If no other driver is specified, the default driver will be used. It consists of small, refined part of awesome <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-openimaj">OpenIMAJ</a> framework wrapped in thread-safe container.</p><h3>IP Camera Driver</h3><p>This capture driver gives possibility to access IP camera devices and handle images in form of JPEG pictures or MJPEG streams.</p><p>Maven dependency:</p>
<pre><code class="xml">&lt;dependency&gt;
    &lt;groupId&gt;com.github.sarxos&lt;/groupId&gt;
    &lt;artifactId&gt;webcam-capture-driver-ipcam&lt;/artifactId&gt;
    &lt;version&gt;{webcam-capture-version-here}&lt;/version&gt;
&lt;/dependency&gt;
</code></pre><p>How to use:</p>
<pre><code class="java">Webcam.setDriver(new IpCamDriver());
</code></pre><p>More details and binaries download can be found on dedicated <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-ipcam">webcam-capture-driver-ipcam</a> page.</p><h3>Fswebcam Driver</h3><p>This capture driver gives possibility to use CLI tool called <code>fswebcam</code> (written by Philip Heron) to access UVC devices connected to the computer. It works only on *nix and requires tool to be installed on the environment where driver is used.</p><p>Maven dependency:</p>
<pre><code class="xml">&lt;dependency&gt;
    &lt;groupId&gt;com.github.sarxos&lt;/groupId&gt;
    &lt;artifactId&gt;webcam-capture-driver-fswebcam&lt;/artifactId&gt;
    &lt;version&gt;{webcam-capture-version-here}&lt;/version&gt;
&lt;/dependency&gt;
</code></pre><p>How to use:</p>
<pre><code class="java">Webcam.setDriver(new FsWebcamDriver());
</code></pre><p>More details on how to use, how to install <code>fswebcam</code> and where binaries can be downloaed, can be found on dedicated <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-fswebcam">webcam-capture-driver-fswebcam</a> page.</p><h3>GStreamer Driver</h3><p>This capture driver gives possibility to use<br/><a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-gstreamer">GStreamer</a> to access UVC camera devices connected to computer. It works on Windows and Linux only.</p><p>Maven dependency:</p>
<pre><code class="xml">&lt;dependency&gt;
    &lt;groupId&gt;com.github.sarxos&lt;/groupId&gt;
    &lt;artifactId&gt;webcam-capture-driver-gstreamer&lt;/artifactId&gt;
    &lt;version&gt;{webcam-capture-version-here}&lt;/version&gt;
&lt;/dependency&gt;
</code></pre><p>How to use:</p>
<pre><code class="java">Webcam.setDriver(new GStreamerDriver());
</code></pre><p>More details on how to use, how to install GStreamer and where binaries can be downloaded, can be found on dedicated <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-gstreamer">webcam-capture-driver-gstreamer</a> page.</p><h3>OpenIMAJ Driver</h3><p>This capture driver gives possibility to use <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-openimaj">OpenIMAJ</a> to access UVC camera devices connected to the computer.</p><p>Maven dependency:</p>
<pre><code class="xml">&lt;dependency&gt;
    &lt;groupId&gt;com.github.sarxos&lt;/groupId&gt;
    &lt;artifactId&gt;webcam-capture-driver-openimaj&lt;/artifactId&gt;
    &lt;version&gt;{webcam-capture-version-here}&lt;/version&gt;
&lt;/dependency&gt;
</code></pre><p>How to use:</p>
<pre><code class="java">Webcam.setDriver(new OpenImajDriver());
</code></pre><p>More details on how to use it and where binaries can be downloaded, can be found on dedicated <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-openimaj">webcam-capture-driver-openimaj</a> page.</p><h3>V4L4j Driver</h3><p>This is capture driver which uses <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-v4l4j">V4L4j</a> project to access UVC camera devices. It works on Linux only and it seems like it is most suitable for use on Raspberry Pi.</p><p>Maven dependency:</p>
<pre><code class="xml">&lt;dependency&gt;
    &lt;groupId&gt;com.github.sarxos&lt;/groupId&gt;
    &lt;artifactId&gt;webcam-capture-driver-v4l4j&lt;/artifactId&gt;
    &lt;version&gt;{webcam-capture-version-here}&lt;/version&gt;
&lt;/dependency&gt;
</code></pre><p>How to use:</p>
<pre><code class="java">Webcam.setDriver(new V4l4jDriver());
</code></pre><p>More details on how to use it and where necessary binaries can be downloaded, can be found on dedicated <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-v4l4j">webcam-capture-driver-v4l4j</a> page.</p><h3>JMF Driver</h3><p>This is capture driver which uses <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-jmf">JMF</a> (Java Media Framework) to access UVC webcam devices. The JMF needs to be installed and configured on the PC before this driver can be used. It can also be used alternatively with the <a href="http://fmj-sf.net/">FMJ</a> project.</p><p>Maven dependency:</p>
<pre><code class="xml">&lt;dependency&gt;
    &lt;groupId&gt;com.github.sarxos&lt;/groupId&gt;
    &lt;artifactId&gt;webcam-capture-driver-jmf&lt;/artifactId&gt;
    &lt;version&gt;{webcam-capture-version-here}&lt;/version&gt;
&lt;/dependency&gt;
</code></pre><p>How to use:</p>
<pre><code class="java">Webcam.setDriver(new JmfDriver());
</code></pre><p>More details on how to use it, install, and where necessary binaries can be downloaded, can be found on dedicated <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-jmf">webcam-capture-driver-jmf</a> page.</p><h3>LTI-CIVIL Driver</h3><p>This is capture driver designed to leverage capabilities of <a href="http://sourceforge.net/projects/lti-civil/">LTI-CIVIL</a> project (by Larson Technologies Inc.) and use it to access wide range of UVC devices. It works on 32-bit architectures only.</p><p>Maven dependency:</p>
<pre><code class="xml">&lt;dependency&gt;
    &lt;groupId&gt;com.github.sarxos&lt;/groupId&gt;
    &lt;artifactId&gt;webcam-capture-driver-lti-civil&lt;/artifactId&gt;
    &lt;version&gt;{webcam-capture-version-here}&lt;/version&gt;
&lt;/dependency&gt;
</code></pre><p>How to use it:</p>
<pre><code class="java">Webcam.setDriver(new LtiCivilDriver());
</code></pre><p>More details on how to use it, and where necessary binaries can be downloaded, can be found on dedicated <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-lti-civil">webcam-capture-driver-lti-civil</a> page.</p><h3>VLCj Driver</h3><p>This is capture driver which uses <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-vlcj">VLCj</a> library from <a href="http://www.capricasoftware.co.uk/">Caprica Software Limited</a> to gain access to the UVC camera device.</p><p>Maven dependency:</p>
<pre><code class="xml">&lt;dependency&gt;
    &lt;groupId&gt;com.github.sarxos&lt;/groupId&gt;
    &lt;artifactId&gt;webcam-capture-driver-vlcj&lt;/artifactId&gt;
    &lt;version&gt;{webcam-capture-version-here}&lt;/version&gt;
&lt;/dependency&gt;
</code></pre><p>How to use it:</p>
<pre><code class="java">Webcam.setDriver(new VlcjDriver());
</code></pre><p>More details on how to use it, how to install, and where necessary binaries can be downloaded, can be found on dedicated <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-vlcj">webcam-capture-driver-vlcj</a> page.</p><h3>JavaCV Driver</h3><p>This is capture driver which uses <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-javacv">JavaCV</a> binding for [OpenCV][] to gain access to the UVC camera device.</p><p>Maven dependency:</p>
<pre><code class="xml">&lt;dependency&gt;
    &lt;groupId&gt;com.github.sarxos&lt;/groupId&gt;
    &lt;artifactId&gt;webcam-capture-driver-javacv&lt;/artifactId&gt;
    &lt;version&gt;{webcam-capture-version-here}&lt;/version&gt;
&lt;/dependency&gt;
</code></pre><p>How to use it:</p>
<pre><code class="java">Webcam.setDriver(new JavaCvDriver());
</code></pre><p>More details on how to use it, how to install, and where necessary binaries can be downloaded, can be found on dedicated <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-javacv">webcam-capture-driver-javacv</a> page.</p><h3>FFmpeg CLI Driver</h3><p>This is capture driver which uses <code>ffmpeg</code> <a href="http://en.wikipedia.org/wiki/Command-line_interface">CLI</a> tool from <a href="http://www.ffmpeg.org/">FFmpeg</a> to access UVC camera device. It works on Linux only.</p><p>Maven dependency:</p>
<pre><code class="xml">&lt;dependency&gt;
    &lt;groupId&gt;com.github.sarxos&lt;/groupId&gt;
    &lt;artifactId&gt;webcam-capture-driver-ffmpeg-cli&lt;/artifactId&gt;
    &lt;version&gt;{webcam-capture-version-here}&lt;/version&gt;
&lt;/dependency&gt;
</code></pre><p>How to use it:</p>
<pre><code class="java">Webcam.setDriver(new FFmpegCliDriver());
</code></pre><p>More details on how to use it, how to install, and where necessary binaries can be downloaded, can be found on dedicated <a href="https://github.com/sarxos/webcam-capture/tree/master/webcam-capture-drivers/driver-ffmpeg-cli">webcam-capture-driver-ffmpeg-cli</a> page.</p><h2>History</h2><p>I initially started working on Webcam Capture as a simple proof-of-concept after I read <a href="http://fivedots.coe.psu.ac.th/~ad/">Andrew Davison</a>'s fantastic book entitled <a href="http://www.amazon.com/Killer-Game-Programming-Andrew-Davison/dp/0596007302/ref=sr_1_1?s=books&ie=UTF8&qid=1360352393&sr=1-1&keywords=killer+game+programming">Killer Game Programming</a> (which is also available <a href="http://fivedots.coe.psu.ac.th/~ad/jg/">online</a>). Thank you Andrew! Later I found that there is a complete mess in Java APIs allowing you to capture images from webcams. Once you choose specific API you cannot change it without modifying large parts of the code. I decided to change this situation and write general purpose wrapper for various different APIs (like JMF, OpenCV, OpenIMAJ, LTI-CIVIL, VLC). In such a way, Webcam Capture as we know it today, was brought to life. Today you can change underlying frameworks just by replacing webcam driver (one line code change). If there is no driver for particular framework, it's very easy to write it yourself.</p><h2>License</h2><p>Copyright (C) 2012 - 2017 Bartosz Firyn (<a href="https://github.com/sarxos">https://github.com/sarxos</a>) and contributors</p><p>Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:</p><p>The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.</p><p>THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.</p><p><img src="https://raw.github.com/sarxos/webcam-capture/master/webcam-capture/src/etc/resources/sarxos.png"  alt="sarxos"/></p>      <!-- markdown footer start -->

      </section>
      <footer>
        <p>Maintained by <a href="https://github.com/sarxos">SarXos</a></p>
      </footer>
    </div>
    <!--[if !IE]><script>fixScale(document);</script><!--<![endif]-->
    <script type="text/javascript">
    prettyPrint();
    </script>

  </body>
</html>
