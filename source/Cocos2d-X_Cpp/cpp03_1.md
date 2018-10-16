## Initial SDK

Only used Xcode engineering  as an example for explanation. If you are using other projects, please refer to Xcode engineering operation. Sorry for any inconvenience.

The UPLTV SDK is very simple to initialize.

### Add the following reference to your project
```cpp
#include "UpltvBridge.h"
```

### Initial UPSDK
There are two ways to initialize, and we recommend the first one:

#### 1. Initialize the UPSDK based on the region parameters
```cpp
/**
* Initial SDK
*/
static void initSdkByZone(int zone);
```
For example：

```cpp
/**
* Please be sure to complete the SDK initialization before using the other API interfaces of the SDK
* @param zone product distribution area, 0 overseas, 1 mainland China, 2 automatically according to IP positioning
*/
UpltvBridge::initSdkByZone(0);
```

#### 2. Initialize the UPSDK based on the zone parameters and callback functions

If you want to listen to the initialization results, you can use this method.
```cpp
/**
* @param callback The callback interface after the SDK initialization is completed. The callback interface contains a Boolean parameter callback(Boolean). True means success
*/
initSdkByZoneWithCall(int zone, UpltvSdkBoolCallback callback);
```
For example：
```cpp
/**
* The SDK initializes the callback interface, and the parameter true indicates successful initialization, otherwise the initialization fails
*/
void sdkCallback(bool r)
{
   log("====> cpp initSdkCallback(%s)", (r ? "true" : "false"));
}

void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        switch (tag)
        {
            case 1001:
            {
                //Initialize the SDK and listen for the callback results
                UpltvSdkBoolCallback callback = sdkCallback;
                UpltvBridge::initSdkByZoneWithCall(0, callback);
            }
                break;

        }
   }
}

```

#### 3. setCustomerId()
Only support Android platform, for non-gp packages, androidid can be passed to avoid additional statistical errors.
```asp
/**
* please call this method before Initializing
* Version 3004(subversion 5) and above support this method
* @param androidid
*/
UpltvBridge::setCustomerId(androidid);
```

#### 4. Add onApplicationFocus()
Refer to the following code to correctly add the onApplicationFocus() method in the AppDelegate class of the current project to notify the UPSDK game foreground to switch changes.

```cpp
void AppDelegate::applicationDidEnterBackground() {
    // Call UpltvBridge::onApplicationFocus(false) when you go into the background
    UpltvBridge::onApplicationFocus(false);

    Director::getInstance()->stopAnimation();
#if USE_AUDIO_ENGINE
    AudioEngine::pauseAll();
#elif USE_SIMPLE_AUDIO_ENGINE
    SimpleAudioEngine::getInstance()->pauseBackgroundMusic();
    SimpleAudioEngine::getInstance()->pauseAllEffects();
#endif
}

// this function will be called when the app is active again
void AppDelegate::applicationWillEnterForeground() {
    // Call UpltvBridge::onApplicationFocus(true) when you enter the foreground
    UpltvBridge::onApplicationFocus(true);

    Director::getInstance()->startAnimation();
#if USE_AUDIO_ENGINE
    AudioEngine::resumeAll();
#elif USE_SIMPLE_AUDIO_ENGINE
    SimpleAudioEngine::getInstance()->resumeBackgroundMusic();
    SimpleAudioEngine::getInstance()->resumeAllEffects();
#endif
}
```
