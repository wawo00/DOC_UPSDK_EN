## Reward video Ad

#### 1. Load callback of Reward video
  This API is used to listen for the loading results of the current excited video. Once this interface is called back, the internal will be automatically released, and the callback interface needs to be reset when listening again.
```cpp
/**
* Set the reward video load callback interface method
* @param successCall Motivate the callback when the video is loaded successfully，successCall(cpadid, msg)
* @param failCall    Motivate the callback when the video is loaded failed，failCall(cpadid, msg)
*/
static void setRewardVideoLoadCallback(UpltvSdkStringCallback_2 successCall, UpltvSdkStringCallback_2 failCall);
```
For example：
```cpp
// This method is called back when the video is loaded successfully
void rdLoadCallSuccess(const char *cpid, const char *msg) {
    log("====> reward video didLoad Success at cpid: %s", (cpid != nullptr ? cpid : ""));
}

// This method is called back when the video is loaded failed
void rdLoadCallFail(const char *cpid, const char *msg) {
    log("====> reward video didLoad Fail at cpid: %s", (cpid != nullptr ? cpid : ""));
}

void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        switch (tag)
        {
            case 1001:
            {
                // Set the reward video load callback interface
                UpltvSdkStringCallback_2 loadSuccess = rdLoadCallSuccess;
                UpltvSdkStringCallback_2 loadFail = rdLoadCallFail;
                UpltvBridge::setRewardVideoLoadCallback(loadSuccess, loadFail);
            }
                break;
        }
   }
}
```
#### 2. Show callback of Reward video Ad
  Set up the callback interface of video show to listen to the callback of the event (click, close, reward, etc.) of the video advertisement. Reward video shows that the reference to the callback interface is stored internally and not released, so you only need to set it once.
```cpp
/**
* @param callback(type, cpid)
*/
static void setRewardVideoShowCallback(UpltvSdkStringCallback_1 callback);
```

For example：
```cpp
// Call back this method to listen for the event type when the video is showing
void rdShowCallback(UpltvAdEventEnum::AdEventType type, const char *cpid) {
    string s = "unkown";
    switch (type) {
        case UpltvAdEventEnum::AdEventType::VIDEO_EVENT_DID_SHOW:{
            s = "Did_Show";
        }
            break;
        case UpltvAdEventEnum::AdEventType::VIDEO_EVENT_DID_CLICK:{
            s = "Did_Click";
        }
            break;
        case UpltvAdEventEnum::AdEventType::VIDEO_EVENT_DID_CLOSE:{
            s = "Did_Close";
        }
            break;
        case UpltvAdEventEnum::AdEventType::VIDEO_EVENT_DID_GIVEN_REWARD:{
            s = "Did_Give";
        }
            break;
        case UpltvAdEventEnum::AdEventType::VIDEO_EVENT_DID_ABANDON_REWARD:{
            s = "Did_Abandon";
        }
            break;
    }
    log("====> reward video showCall event: %s, at cpid: %s", (s.c_str() != nullptr ? s.c_str() : ""), cpid?cpid:"");

}

void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        switch (tag)
        {
            case 1001:
            {
                {
                //Set up the callback interface of the video show to listen to the callback of events such as click, close, and award during a display of the video advertisement
                UpltvBridge::setRewardVideoShowCallback(rdShowCallback);
            }
                break;
        }
   }
}
```
#### 3. Judge if the Reward Video ad is ready
Synchronously return Boolean results, true indicates that the AD is ready to be displayed, and false indicates that the AD is not show and still  in the request
  ```cpp
 /**
* This method is usually called before showRewardVideo(cpPlaceId)
* @return bool
*/
static bool isRewardReady();
```

For example：
```cpp
void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        switch (tag)
        {
            case 1001:
            {
                {
                // judge if the video ad is ready
                bool r = UpltvBridge::isRewardReady();
                log("====> cpp print isRewardReady : %s",(r?"true":"false"));
            }
                break;
        }
   }
}
```
#### 4. Show Reward Video Ad 
When show the Reward Video ad, you need to upload a cpPlaceId, which is the placementid , used for business management, in order to distinguish the source of revenue.
```cpp
/**
* @param cpPlaceId placementid
*/
static void showRewardVideo(const char* cpPlaceId);

```
For example：
```cpp
void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        switch (tag)
        {
            case 1001:
            {
                {
               if (UpltvBridge::isRewardReady()) {
               UpltvBridge::showRewardVideo(nullptr);
                }
            }
                break;
        }
   }
}
```
#### 5. Debug view of Reward Video Ad
In order to help developers to view the use and loading status of ad, we provide a debug page for the ad of the screen, which can be opened to observe the configuration parameters and loading status of the ad.
```cpp
static void showRewardVideoDebugUI();
```
For example：
```cpp
void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        switch (tag)
        {
            case 1001:
            {
                {
                  UpltvBridge::showRewardVideoDebugUI();
                }
            }
                break;
        }
   }
}
```

