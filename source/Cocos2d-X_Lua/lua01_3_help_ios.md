
## IOS Xcode

This access document is based on cocos2d-x 3.16. If you have problems when using other versions of cocos2d-x, please contact us.

### 1 Download SDK package
First from [UPSDK Download](http://doc.upltv.com/en/master/chapters/chapter09.html "SDKDownLoad") download UPSDK LuaPlugin package，The uncompressed directory contains the following three files：
- `UPSDK.framework` This is the UPSDK master package, so be sure to add it to your current project
- `UPSDK.bundle` Be sure to add the external file resources  because that the UPSDK master package needs to access to the current project
- `UpltvLuaBridge` This directory contains *. lua source files for bridging the current cocos2d-x Lua project and UPSDK AD interface calls
</br>

### 2 The XCode project adds the UPSDK master package and source files
Add UPSDK. Framework, UPSDK. Bundle, and UpltvLuaBridge folders to your Xcode project directory at the same time. It is important to note that the check UpltvLuaBridge folder contains to ` UPAdsBridgeLua ` and ` UpltvIos ` *. H and *. CPP file exists.

The full files included with the UPSDK is shown below：
</br>
![](http://docc.upltv.com/uploads/201805/5afe86ea12eac_5afe86ea.png)

Will you can add  ` UPLTV. Lua `, ` UPLTVIos. Lua ` introduce engineering, suggest introducing in Resources - > SRC > app - > views directory, as shown in the figure below：

![](http://docc.upltv.com/uploads/201804/5ae28500aafd8_5ae28500.png)

Will  ` UPAdsBrigeLua. h ` and ` UPAdsBrigeLua. mm ` introduced in engineering, proposal introduced in ios directory, it is best to create a new folder as upltv, facilitate management project, as shown in the figure below：

![](http://docc.upltv.com/uploads/201804/5ae18fc73aa86_5ae18fc7.png)

### 3 Add third-party dependency libraries
UPSDK will rely on third-party advertising unions when it runs, so you'll need to manually import the alliance's dependent library files into your project. To ensure that you can properly add third-party dependency packages, please click here[Download UPSDK union package](http://doc.upltv.com/en/master/chapters/chapter09.html "SDK第三方包下载") 。

UPSDK currently relies on the following third-party advertising union：

![Add all third party SDK packages](http://docc.upltv.com/uploads/201709/59afafb9143e9_59afafb9.png "添加所有第三方SDK包")

> Each alliance corresponds to a folder, and the name is prefixed with the name of the advertising coalition and suffixed with the version number, so it is easy to identify. The folder may contain supporting resource files in addition to the other dependent library or source file, so the dependent library should be added in conjunction with the corresponding supporting resource.

Although it is not required to add all third party affiliate ads to the current project, we still recommend that you add as many of the above affiliate AD dependency libraries and their accompanying resource packages as possible in your project in order to increase revenue. In practice, please contact our technical support staff if you have any questions.

When you finish after add third party alliance advertising, check in the XCode project ` Linked Frameworks Libraries ` is properly introduced corresponding library files, avoid unnecessary mistakes.

for example in the current project access Applovin, Unity, Vungle, tapjoy like the four ads, need to put the four advertising library file (in turn isAppLovinSDK.framework,UnityAds.framework,VungleSDK.framework,Tapjoy.framework  like four static library framework) is added to the project, after successful add rendering is as follows：
![](http://docc.upltv.com/uploads/201804/5acc6644c33a5_5acc6644.png)

In the above hypothesis, because the Tapjoy AD needs to access some of its external resource files, it needs to add its supporting resource files to the project, which can be viewed from TARGETS -- General -- Copy Bundle Resources：
<br>
![](http://docc.upltv.com/uploads/201804/5acc70803fec8_5acc7080.png)

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
![](http://docc.upltv.com/uploads/201804/5ae28e70be73c_5ae28e70.png)

#### 2  Add the following nodes to the info.plist to be compatible with HTTP mode

```objective-c
 <key>NSAppTransportSecurity </key>
 <dict>
	 <key>NSAllowsArbitraryLoads </key>
	 <true/>
 </dict>
```

#### 3 Add the following nodes to the info.plist to obtain permissions (if you use AdColony union, you must add; if you do not use AdColony union, you may not add it)
```objective-c
 <key>NSCalendarsUsageDescription </key>
 <string>Some ad content may create a calendar event. </string>
 <key>NSCameraUsageDescription </key>
 <string>Some ad content may access camera to take picture. </string>
 <key>NSPhotoLibraryUsageDescription </key>
 <string>Some ad content may require access to the photo library. </string>
```

tips：Depending on the language and usage scenario, the user can adjust the description of the access permission appropriately.
<br>

#### 4 Bitcode
Support Bitcode mode, please select whether to use Bitcode according to the requirement(Domob does not support Bitcode mode) .

#### 5 cocos project configuration
If you are using the cocos created project, please check project ` Version ` have filled such as in the following figure：
（Because the Version of the project created by cocos is not filled by default, it will affect the subsequent use））

![cocos project Version field configuration](http://docc.upltv.com/uploads/201709/59afb01ec7612_59afb01e.png "cocos项目Version字段配置")
<br>

### 6 View version number
In *AvidlyAdsSDKVersion.h*，you can view the version number of the current SDK directly。

```objective-c
//version of sdk
#define AvidlyAdsSDKVERSION  @"3003"
```
> AvidlyAdsSDKVERSION，3003 represents the current version number number.

