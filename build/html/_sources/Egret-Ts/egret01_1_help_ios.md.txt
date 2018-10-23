## IOS

This access document is based on Egret v5.2.8.

### 1 Download SDK package

First from [UPSDK Download](http://doc.upltv.com/en/master/chapters/chapter09.html "SDKDownLoad") download UPSDK JsPlugin package，The uncompressed directory contains the following three files：
- `UPSDK.framework` This is the UPSDK master package, so be sure to add it to your current project
- `UPSDK.bundle` Be sure to add the external file resources  because that the UPSDK master package needs to access to the current project
- `UpltvEgretTsBridge` This directory contains *.ts source files for bridging the current EgretTs project and UPSDK AD interface calls
</br>


### 2 Poject setting of EgretIDE 

1) Copy `UpltvEgretTsBridge` to the `src` folder of the Layabox project, leaving only the `.ts` file

As following:

![](http://docc.upltv.com/uploads/201809/5ba096f858faf_5ba096f8.png)
</br>

### 3 Project Setting of XCode

#### 1.Add the UPSDK main package and source 

Add UPSDK. Framework, UPSDK. Bundle, and UpltvEgretTsBridge folders to your Xcode project directory at the same time.

Remove *.ts files in  UpltvEgretTsBridge folder,leave Object-C++ source，as following：

![](http://docc.upltv.com/uploads/201809/5ba095754ee34_5ba09575.png)


#### 2 Add third-party dependency libraries

UPSDK will rely on third-party advertising unions when it runs, so you'll need to manually import the alliance's dependent library files into your project. To ensure that you can properly add third-party dependency packages, please click here[Download UPSDK union package](http://doc.upltv.com/en/master/chapters/chapter09.html ) .

UPSDK currently relies on the following third-party advertising union：

![Add all third party SDK packages](http://docc.upltv.com/uploads/201709/59afafb9143e9_59afafb9.png)

> Each alliance corresponds to a folder, and the name is prefixed with the name of the advertising coalition and suffixed with the version number, so it is easy to identify. The folder may contain supporting resource files in addition to the other dependent library or source file, so the dependent library should be added in conjunction with the corresponding supporting resource.

Although it is not required to add all third party affiliate ads to the current project, we still recommend that you add as many of the above affiliate AD dependency libraries and their accompanying resource packages as possible in your project in order to increase revenue. In practice, please contact our technical support staff if you have any questions.

When you finish after add third party alliance advertising, check in the XCode project ` Linked Frameworks Libraries ` is properly introduced corresponding library files, avoid unnecessary mistakes.

for example in the current project access Applovin, Unity, Vungle, tapjoy like the four ads, need to put the four advertising library file (in turn isAppLovinSDK.framework,UnityAds.framework,VungleSDK.framework,Tapjoy.framework  like four static library framework) is added to the project, after successful add rendering is as follows：
![](http://docc.upltv.com/uploads/201804/5acc6644c33a5_5acc6644.png)

In the above hypothesis, because the Tapjoy AD needs to access some of its external resource files, it needs to add its supporting resource files to the project, which can be viewed from TARGETS -- General -- Copy Bundle Resources：
<br>
![](http://docc.upltv.com/uploads/201804/5acc70803fec8_5acc7080.png)


#### 3 Add system dependencies
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

### 4 Project configuration
#### 1 Add the classification compiler


- Add  all third-party dependency libraries UPSDK.framework in  `-force_load（space）library path` on `TARGETS` → `Build Setting` → `Linking` → `Other Linker Flags` such as:

![](http://docc.upltv.com/uploads/201809/5ba21766e18e1_5ba21766.png)

#### 2 Add the following nodes to the info.plist to be compatible with HTTP mode

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
Support Bitcode mode, please select whether to use Bitcode according to the requirement(Domob does not support Bitcode mode).

<br>

### 5 Version
You can check the version of the UPSDK in *UPSDKVersion.h*.

```objective-c
##define AvidlyAdsSDKVERSION  @"3005"
```

<br>

### 6 Modify code
#### 1 Add window attribute in AppDelegate
```objective-c
@interface AppDelegate : UIResponder <UIApplicationDelegate>
@property (strong, nonatomic) UIWindow *window;
@end

@implementation AppDelegate {
    EgretNativeIOS* _native;
}
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions{
_native = [[EgretNativeIOS alloc] init];
self.window = _native.window;
... ...
}
```
#### 2 Register  notice
```objective-c
[UpAdsBridgeEgretTs registWithEgretNative:_native];
```

