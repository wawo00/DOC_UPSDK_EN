## Interstitial API

### 1. Set the interstitial load callback 
Load results (success or failure) to listen for the current interstitial ad .This interface is automatically released once a callback is made, and the callback interface needs to be reset when listening again.
```cpp
/**
* @param cpPlaceId   placement ID
* @param loadSuccess Motivate the callback when the video is loaded successfully，successCall(cpadid, msg)
* @param loadFail     Motivate the callback when the video is loaded failed， loadFail(cpid, message)
*/
static void setInterstitialLoadCallback(const char* cpPlaceId, UpltvSdkStringCallback_2 loadSuccess, UpltvSdkStringCallback_2 loadFail);
```
For example：
```cpp
void iLLoadCallSuccess(const char *cpid, const char *msg) {
    log("====> iLLoadCallSuccess at cpid: %s", (cpid != nullptr ? cpid : ""));
}

void iLLoadCallFail(const char *cpid, const char *msg) {
    log("====> iLLoadCallFail  at cpid: %s", (cpid != nullptr ? cpid : ""));
}

void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        log("===> cpp button touch tag :%d",tag);
        string ilkey = "Interstitial_LevelPass";//define a interstitial ad‘s placementID
        switch (tag)
        {
            case 1001:
            {
                 UpltvBridge::setInterstitialLoadCallback(ilkey.c_str(), iLLoadCallSuccess, iLLoadCallFail);
            }
                break;
        }
   }
}
```
### 2. Set show callback of Interstitial Ad

Set up the callback interface for the display of interstitial ad which is used to listen to the callback of showing .The  interstitial ad shows that references to the callback interface are stored  and not released.
```cpp
/**
* @param cpPlaceId placementid
* @param callback  callback
*/
static void setInterstitialShowCallback(const char* cpPlaceId, UpltvSdkStringCallback_1 callback);
```
For example：
```cpp
void iLShowCallback(UpltvAdEventEnum::AdEventType type, const char *cpid) {
    string s = "unkown";
    switch (type) {
        case UpltvAdEventEnum::AdEventType::INTERSTITIAL_EVENT_DID_SHOW:{
            s = "Did_Show";
        }
            break;
        case UpltvAdEventEnum::AdEventType::INTERSTITIAL_EVENT_DID_CLICK:{
            s = "Did_Click";
        }
            break;
        case UpltvAdEventEnum::AdEventType::INTERSTITIAL_EVENT_DID_CLOSE:{
            s = "Did_Close";
        }
            break;
    }
    log("====> interstitial ad showCall event: %s, at cpid: %s", (s.c_str() != nullptr ? s.c_str() : ""), cpid?cpid:"");
}

void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        log("===> cpp button touch tag :%d",tag);
        string ilkey = "Interstitial_LevelPass";//define a interstitial ad‘s placementID
        switch (tag)
        {
            case 1001:
            {
                 UpltvBridge::setInterstitialShowCallback(ilkey.c_str(), iLShowCallback);
            }
                break;
        }
   }
}
```
### 3. Judge if the interstitial ad is ready
Judge if the interstitial ad is ready accroding placementid, and  return Boolean results synchronously, true means that the AD is ready to be displayed, and false means that the AD is not show and still in the request.
```cpp
 /**
* @param cpPlaceId
* @return bool
*/
static bool isInterstitialReady(const char* cpPlaceId);
```
For example：
```cpp
void iLReadyCallback(const char* cpPlaceId, bool r) {
    log("====> cpp iLReadyCallback(%s, %s)", cpPlaceId, (r ? "true" : "false"));
}

void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        log("===> cpp button touch tag :%d",tag);
        string ilkey = "Interstitial_LevelPass";//define a interstitial ad‘s placementID
        switch (tag)
        {
            case 1001:
            {
                UpltvBridge::isInterstitialReadyAsyn(ilkey.c_str(), iLReadyCallback);
            }
                break;
        }
   }
}
```
### 4. Show interstitial AD
show a interstitial ad according to the ad placement ID.
```cpp
/**
* @param cpPlaceId
*/
static void showInterstitialAd(const char* cpPlaceId);
```
For example：
```cpp
void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        log("===> cpp button touch tag :%d",tag);
        string ilkey = "Interstitial_LevelPass";//define a interstitial ad‘s placementID
        switch (tag)
        {
            case 1001:
            {
                if (UpltvBridge::isInterstitialReady(ilkey.c_str())) {
                    UpltvBridge::showInterstitialAd(ilkey.c_str());
                }
            }
                break;
        }
   }
}
```
### 5. Debug view of Interstital Ad 
In order to help developers to view the use and loading status of ad, we provide a debug page for the ad of the screen, which can be opened to observe the configuration parameters and loading status of the ad.
```cpp
static void showInterstitialDebugUI();
```
For example：
```cpp
void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        log("===> cpp button touch tag :%d",tag);
        string ilkey = "Interstitial_LevelPass";//define a interstitial ad‘s placementID
        switch (tag)
        {
            case 1001:
            {
                UpltvBridge::showInterstitialDebugUI();
            }
                break;
        }
   }
}
```
