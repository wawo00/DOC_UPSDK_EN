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

然后进入您的工程目录，运行以下命令
Switch into your project directory and run command `pod install`

```
pod install
```

Done.

### Project configuration 
  
1 Add nodes in `info.plist` file, to allow http protocol

```objective-c
&lt;key>NSAppTransportSecurity&lt;/key>
&lt;dict>
	&lt;key>NSAllowsArbitraryLoads&lt;/key>
	&lt;true/>
&lt;/dict>
```

#### 3 Add nodes info.plist, to require permissions
```objective-c
&lt;key>NSCalendarsUsageDescription&lt;/key>
&lt;string>Some ad content may create a calendar event.&lt;/string>
&lt;key>NSCameraUsageDescription&lt;/key>
&lt;string>Some ad content may access camera to take picture.&lt;/string>
&lt;key>NSPhotoLibraryUsageDescription&lt;/key>
&lt;string>Some ad content may require access to the photo library.&lt;/string>
```


Note: you can change description into your target language if needed.
<br>

#### 4 Bitcode
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

