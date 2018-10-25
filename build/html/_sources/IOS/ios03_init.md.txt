## SDK Initial

This part will explain in Xcode. Please refer to Xcode if you are using other project. I apologize for the inconvenience you may take from here.

Let's say if you are using AppDelegate (implement UIApplicationDelegate) as your main class file of your iOS project. Initialize SDK by following steps:

 1. Add reference in AppDelegate.m

```objective-c
#import    <UPSDK/UPSDK.h>
```

 2. SDK initial at the entrance of the app

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    
    [UPSDK initSDK];

    // your other code
    
    return YES;
}
```

if you know which areas you will publish, please use the following codes：
```objective-c
/**
 SDK Initial(based on the areas for publishing)

 @param  zone, areas for publishing
 */
+ (void)initSDK:(UPSDKGlobalZone)zone;
```

`UPSDKGlobalZone`for example

```objective-c
typedef NS_ENUM(NSUInteger, UPSDKGlobalZone) {
    UPSDKGlobalZoneForeign = 0,     //Globally except China
    UPSDKGlobalZoneDomestic = 1,    /China
    UPSDKGlobalZoneAuto = 2,        //Verifying by IPs
};
```
if you app will be published in China:

```objective-c
[UPSDK initSDK:UPSDKGlobalZoneDomestic];
```

if you app will be published globally except china:

```objective-c
[UPSDK initSDK: UPSDKGlobalZoneForeign];
```

if you app will be publish in the world and you don not konw  exact areas :

```objective-c
[UPSDK initSDK: UPSDKGlobalZoneAuto];
```
