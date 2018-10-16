## IOS 

This access document is based on cocos2d-x 3.16. If you have problems when using other versions of cocos2d-x, please contact us.

### 1 Download SDK package
First from [UPSDK Download](http://ads-sdk-doc.haloapps.com/docs/show/13 "SDK下载页面") download UPSDK JsPlugin package，The uncompressed directory contains the following three files：
- `UPSDK.framework` This is the UPSDK master package, so be sure to add it to your current project
- `UPSDK.bundle` Be sure to add the external file resources  because that the UPSDK master package needs to access to the current project
- `UpltvJsBridge` This directory contains *. CPP source files for bridging the current cocos2d-x JS project and UPSDK AD interface calls
</br>


### 2  Add the UPSDK main package and source 
Add UPSDK. Framework, UPSDK. Bundle, and UpltvCppBridge folders to your Xcode project directory at the same time.
UpltvJsBridge folder contains to ` UpltvCppBridge ` and ` UpltvIos ` *. H and *. CPP file exists.
The UpltvJsBridge folder contains Object-C++ source code and *.js script files, as shown below：

![](http://docs.upltv.com/uploads/201805/5b02724dc9bb5_5b02724d.png)

Please add `UPLTV.js`、`UPLTVIos.js` into your project，suggested to add to `src -> upltv`，as shown below：

![](http://docs.upltv.com/uploads/201805/5b02734555c95_5b027345.png)

Add `UPAdsBrigeJs.h` and `UPAdsBrigeJs.mm` to the current project, it is recommended to add to the `ios->upltv` directory，as shown below：

![](http://docs.upltv.com/uploads/201805/5b02736e0f931_5b02736e.png)

### 3 Add third-party dependency libraries
UPSDK will rely on third-party advertising unions when it runs, so you'll need to manually import the alliance's dependent library files into your project. To ensure that you can properly add third-party dependency packages, please click here[Download UPSDK union package](http://ads-sdk-doc.haloapps.com/docs/show/13 "SDK第三方包下载") 。

UPSDK currently relies on the following third-party advertising union：

![Add all third party SDK packages](http://docs.upltv.com/uploads/201709/59afafb9143e9_59afafb9.png "添加所有第三方SDK包")

> Each alliance corresponds to a folder, and the name is prefixed with the name of the advertising coalition and suffixed with the version number, so it is easy to identify. The folder may contain supporting resource files in addition to the other dependent library or source file, so the dependent library should be added in conjunction with the corresponding supporting resource.

Although it is not required to add all third party affiliate ads to the current project, we still recommend that you add as many of the above affiliate AD dependency libraries and their accompanying resource packages as possible in your project in order to increase revenue. In practice, please contact our technical support staff if you have any questions.

When you finish after add third party alliance advertising, check in the XCode project ` Linked Frameworks Libraries ` is properly introduced corresponding library files, avoid unnecessary mistakes.

for example in the current project access Applovin, Unity, Vungle, tapjoy like the four ads, need to put the four advertising library file (in turn isAppLovinSDK.framework,UnityAds.framework,VungleSDK.framework,Tapjoy.framework  like four static library framework) is added to the project, after successful add rendering is as follows：
![](http://docs.upltv.com/uploads/201804/5acc6644c33a5_5acc6644.png)

In the above hypothesis, because the Tapjoy AD needs to access some of its external resource files, it needs to add its supporting resource files to the project, which can be viewed from TARGETS -- General -- Copy Bundle Resources：
<br>
![](http://docs.upltv.com/uploads/201804/5acc70803fec8_5acc7080.png)


### 4 Add system dependencies
Add dependency libraries form TARGETS → General → Linked Frameworks Libraries
- `QuartzCore.framework`
- `MediaPlayer.framework`
- `libsqlite3.tbd`
- `libz.tbd`
- `CoreMedia.framework`
- `CoreGraphics.framework`
- `CFNetwork.framework`
- `WebKit.framework` (Optional)
- `WatchConnectivity.framework`	(Optional)
- `SystemConfiguration.framework`
- `StoreKit.framework`
- `Social.framework`
- `MessageUI.framework`
- `JavaScriptCore.framework`	(Optional)
- `EventKit.framework`
- `CoreTelephony.framework`
- `AVFoundation.framework`
- `AudioToolbox.framework`
- `AdSupport.framework`
- `GLKit.framework`
- `CoreMotion.framework`
- `libxml2.tbd`
- `libc++.tbd`
- `SafariServices.framework`
- `CoreLocation.framework`
- `EventKitUI.framework`
- `MobileCoreServices.framework`
- `GameController.framework`
<br>

### Project configuration
#### 1 Add the classification compiler

- Add  `-ObjC` on `TARGETS` → `Build Setting` → `Linking` → `Other Linker Flags` such as:
![](http://docs.upltv.com/uploads/201804/5ae28f14f217a_5ae28f14.png)

#### 2 Add the following nodes to the info.plist to be compatible with HTTP mode

```objective-c
&lt;key>NSAppTransportSecurity&lt;/key>
&lt;dict>
	&lt;key>NSAllowsArbitraryLoads&lt;/key>
	&lt;true/>
&lt;/dict>
```

#### 3 Add the following nodes to the info.plist to obtain permissions (if you use AdColony union, you must add; if you do not use AdColony union, you may not add it)
```objective-c
&lt;key>NSCalendarsUsageDescription&lt;/key>
&lt;string>Some ad content may create a calendar event.&lt;/string>
&lt;key>NSCameraUsageDescription&lt;/key>
&lt;string>Some ad content may access camera to take picture.&lt;/string>
&lt;key>NSPhotoLibraryUsageDescription&lt;/key>
&lt;string>Some ad content may require access to the photo library.&lt;/string>
```

tips：Depending on the language and usage scenario, the user can adjust the description of the access permission appropriately.
<br>

#### 4 Bitcode
Support Bitcode mode, please select whether to use Bitcode according to the requirement(Domob does not support Bitcode mode) .

#### 5 cocos project configuration
If you are using the cocos created project, please check project ` Version ` have filled such as in the following figure：
（Because the Version of the project created by cocos is not filled by default, it will affect the subsequent use）

![cocos project Version field configuration](http://docs.upltv.com/uploads/201709/59afb01ec7612_59afb01e.png "cocos项目Version字段配置")
<br>
