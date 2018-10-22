## Banner Ad
Banner ads are divided into top banner and bottom banner, and CppPlugin further simplifies the implementation of banner ads, providing interfaces such as display, hide, remove, and event callbacks.

### 1.Callback of Banner
Banner ad needs to set up the show of banner ad, click and remove the callback interface of events. The callback interface is saved internally by the plug-in, so you don't need to set it up multiple times, only calling upltv:removeBannerAdAt(cpPlaceId) will be deleted.

```cpp
/**
* @param cpPlaceId banner placementID
* @param callback
*/
static void setBannerShowCallback(const char* cpPlaceId, UpltvSdkStringCallback_1 callback);
```
For example：
```cpp
void bannerCallback(UpltvAdEventEnum::AdEventType type, const char *cpid) {
    string s = "unkown";
    switch (type) {
        case UpltvAdEventEnum::AdEventType::BANNER_EVENT_DID_SHOW:{
            s = "Did_Show";
        }
            break;
        case UpltvAdEventEnum::AdEventType::BANNER_EVENT_DID_CLICK:{
            s = "Did_Click";
        }
            break;
        case UpltvAdEventEnum::AdEventType::BANNER_EVENT_DID_REMOVED:{
            s = "Did_Removed";
        }
            break;
    }
    log("====> Banner ad call event: %s, at cpid: %s", (s.c_str() != nullptr ? s.c_str() : ""), cpid?cpid:"");
}

void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        log("===> cpp button touch tag :%d",tag);
        const char* bannertopkey = "BannerAd"; //Define the banner placementID
        switch (tag)
        {
            case 1001:
            {
                UpltvBridge::setBannerShowCallback(bannertopkey, bannerCallback);
            }
                break;
        }
   }
}
```
### 2. Show top banner ads
Show the banner at the top of the screen according to the placementID.

```cpp
/**
* @param cpPlaceId palcementid
*/
static void showBannerAdAtTop(const char*cpPlaceId);
```
Sample：
```cpp
void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        log("===> cpp button touch tag :%d",tag);
        const char* bannertopkey = "BannerAd"; //Define the banner placementID
        switch (tag)
        {
            case 1001:
            {
               UpltvBridge::showBannerAdAtTop(bannertopkey);
            }
                break;
        }
   }
}
```
**It should be noted that when the top Banner of the Iphonex phone is blocked by the status bar, it can be solved by adjusting the displacement of the top Banner.**
```cpp
/**
* On an Iphonex phone, when the top Banner is blocked by the status bar, you can solve this problem by adjusting the displacement of the top banner
* @param padding: The top Banner's offset value, such as 32, will shift down 32 pixels
* This feature is not supported on the Android platform
* supported from 3002
*/
static void setTopBannerPadingForIphonex(int padding);
```
### 3.Hide top banner ads

```cpp
static void hideBannerAdAtTop();
```
For example：
```cpp
void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        log("===> cpp button touch tag :%d",tag);
        const char* bannertopkey = "BannerAd"; //Define the banner placementID
        switch (tag)
        {
            case 1001:
            {
              UpltvBridge::hideBannerAdAtTop();
            }
                break;
        }
   }
}
```
### 4. Show bottom banner ads
Show the banner at the bottom of the screen according to the placementID.
```cpp
/**
* @param cpPlaceId
*/
static void showBannerAdAtBottom(const char*cpPlaceId);
```
For example：
```cpp
void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        log("===> cpp button touch tag :%d",tag);
        const char* bannerbottomkey = "BannerAd"; //Define the banner placementID
        switch (tag)
        {
            case 1001:
            {
              UpltvBridge::showBannerAdAtBottom(bannerbottomkey);
            }
                break;
        }
   }
}
```
### 5. Hide bottom banner ads

```cpp
static void hideBannerAdAtBottom();
```
For example：
```cpp
void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        log("===> cpp button touch tag :%d",tag);
        const char* bannerbottomkey = "BannerAd"; //Define the banner placementID
        switch (tag)
        {
            case 1001:
            {
              UpltvBridge::hideBannerAdAtBottom();
            }
                break;
        }
   }
}
```
### 6. Remove banner ads
```cpp
/**
* @param cpPlaceId banner placementID
*/
static void removeBannerAdAt(const char*cpPlaceId);
```
For example：
```cpp
void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        log("===> cpp button touch tag :%d",tag);
        const char* bannerbottomkey = "BannerAd"; //Define the banner placementID
        switch (tag)
        {
            case 1001:
            {
              UpltvBridge::removeBannerAdAt(bannerbottomkey);
            }
                break;
        }
   }
}
```
