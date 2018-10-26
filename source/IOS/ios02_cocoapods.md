## CocoaPods Access Document
If you use CocoaPods to manage dependances of your iOS project, please import our SDK by following steps:

Add Avidly Repo to CocoaPods:


```
pod repo add Avidly https://github.com/guojunliu/AvidlyAdsSDK-SpecsRepo.git
```


if you have integrated our sdk ago and want to update sdk,please use these codes:

```
pod repo update Avidly
```

Add reference to your `Podfile` file in your project 

```
platform :ios, '8.0'
use_frameworks!

target ‘YourAppName’ do
  source 'https://github.com/guojunliu/AvidlyAdsSDK-SpecsRepo.git'
  pod 'UPSDK', '~> 3.0.03'
end
```

`~>  3.0.03` means version to download, we recommend to use the lastest version.

Enter the project,and run this command:
Switch into your project directory and run command `pod install`

```
pod install
```

Done.

### Project configuration 
  
#### 1 Add nodes in `info.plist` file, to allow http protocol

```objective-c
 <key>NSAppTransportSecurity </key>
 <dict>
	 <key>NSAllowsArbitraryLoads </key>
	 <true/>
 </dict>
```

#### 2 Add nodes info.plist, to require permissions
```objective-c
 <key>NSCalendarsUsageDescription </key>
 <string>Some ad content may create a calendar event. </string>
 <key>NSCameraUsageDescription </key>
 <string>Some ad content may access camera to take picture. </string>
 <key>NSPhotoLibraryUsageDescription </key>
 <string>Some ad content may require access to the photo library. </string>
```


Note: you can change description into your target language if needed.
<br>

#### 3 Bitcode
We support Bitcode, please choose use Bitcode if needed.
Note: YouLan and Domob SDK do not support Bitcode.
<br>

### Version
You can find SDK version in file *UPSDKVersion.h*

```objective-c
//sdk version
#define UPSDKVERSION  @"3003"
```
> as we see,the version of upsdk is 3003 

