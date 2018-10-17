## Reward video Ad

### 1. Load callback of Reward video
This API is used to listen for the loading results of the current excited video. Once this interface is called back, the internal will be automatically released, and the callback interface needs to be reset when listening again.

```javascript
//@param loadsuccess  Motivate the callback when the video is //loaded loadsuccess(cpadid, msg)
//@param failCall    Motivate the callback when the video is //loaded failed，locadfail(cpadid, msg)
setRewardVideoLoadCallback : function(loadsuccess, locadfail)
```

Sample：
```javascript
var rdLoadCallButton = this.createButton(x, y, "rdLoadCall");
rdLoadCallButton.addTouchEventListener(function(sender, type) {
    if (type == 2) {
        upltv.setRewardVideoLoadCallback(function(cpid, msg) {
            cc.log("===> js RewardVideo LoadCallback Success at: %s", cpid);
        }, function(cpid, msg) {
            cc.log("===> js RewardVideo LoadCallback Fail at: %s", cpid);
        });
    }
}, this);
```

#### 2. Show callback of Reward video Ad
    Set up the callback interface of video show to listen to the callback of the event (click, close, reward, etc.) of the video advertisement. Reward video shows that the reference to the callback interface is stored internally and not released, so you only need to set it once.
```javascript

setRewardVideoShowCallback : function(showCall)
```

Sample：
```javascript
var rdShowCallButton = this.createButton(x, y, "rdShowCall");
rdShowCallButton.addTouchEventListener(function(sender, type) {
    if (type == 2) {
        upltv.setRewardVideoShowCallback(function(type, cpid) {
            var event = "unkown";
            if (type == upltv.AdEventType.VIDEO_EVENT_DID_SHOW) {
                event = "Did_Show";
            }
            else if (type == upltv.AdEventType.VIDEO_EVENT_DID_CLICK) {
                event = "Did_Click";
            }
            else if (type == upltv.AdEventType.VIDEO_EVENT_DID_CLOSE) {
                event = "Did_Close";
            }else if (type == upltv.AdEventType.VIDEO_EVENT_DID_GIVEN_REWARD) {
                event = "Did_Given_Reward";
            }else if (type == upltv.AdEventType.VIDEO_EVENT_DID_ABANDON_REWARD) {
                event = "Did_Abandon_Reward";
            }
        });
    }
}, this);
```

#### 3. Judge if the Reward Video ad is ready
Synchronously return Boolean results, true indicates that the AD is ready to be displayed, and false indicates that the AD is not show and still  in the request
```javascript
isRewardReady : function()
```

Sample：
```javascript
var readyRdUIButton = this.createButton(x, y, "rdReady");
readyRdUIButton.addTouchEventListener(function(sender, type) {
    if (type == 2) {
        var r = upltv.isRewardReady();
        cc.log("===> js isRewardReady r: %s", r.toString());
    }
}, this);
```

#### 4. Show Reward Video Ad 
When show the Reward Video ad, you need to upload a cpPlaceId, which is the placementid , used for business management, in order to distinguish the source of revenue.
```javascript
// @param cpPlaceId placementid
showRewardVideo : function(cpPlaceId)
```

Sample：
```javascript
var showRdUIButton = this.createButton(x, y, "rdShow");
showRdUIButton.addTouchEventListener(function(sender, type) {
    if (type == 2) {
        var r = upltv.isRewardReady();
        if (r == true) {
            upltv.showRewardVideo();
        }
    }
}, this);
```

#### 5. Debug view of Reward Video Ad
In order to help developers to view the use and loading status of ad, we provide a debug page for the ad of the screen, which can be opened to observe the configuration parameters and loading status of the ad.
```javascript
showRewardDebugUI : function()
```

Sample：
```javascript
var showRdUIButton = this.createButton(x, y, "rdDebugUI");
showRdUIButton.addTouchEventListener(function(sender, type) {
    if (type == 2) {
        upltv.showRewardDebugUI();
    }
}, this);
```

