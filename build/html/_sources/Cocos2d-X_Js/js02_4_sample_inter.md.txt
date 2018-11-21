## Interstitial API

### 1. Set the interstitial load callback 
Load results (success or failure) to listen for the current interstitial ad .This interface is automatically released once a callback is made, and the callback interface needs to be reset when listening again.

```javascript
// @param cpPlaceId   ad unit
// @param loadSuccess Motivate the callback when the video is //loaded successfully，successCall(cpadid, msg)
// @param loadFail    Motivate the callback when the video is //loaded failed， loadFail(cpid, message)
//Once this interface is called back, the internal will be //automatically released, and the callback interface needs to //be reset when listening again.
setInterstitialLoadCallback : function(cpPlaceId, loadsuccess, locadfail)
```

Sample：
```javascript
var ilLoadCallUIButton = this.createButton(x, y, "ilLoadCall");
ilLoadCallUIButton.addTouchEventListener(function(sender, type) {
    if (type == 2) {
        upltv.setInterstitialLoadCallback(cpPlaceId,
            function(cpid, msg) {
                cc.log("===> js il load callback success: %s at ad unit:%s", msg, cpid);
            },
            function(cpid, msg) {
                cc.log("===> js il load callback fail: %s at ad unit:%s", msg, cpid);
            });
    }
}, this);
```

### 2. Set show callback of Interstitial Ad

Set up the callback interface for the display of interstitial ad which is used to listen to the callback of showing .The  interstitial ad shows that references to the callback interface are stored  and not released.

```javascript
/**
* @param cpPlaceId ad unit
* @param showCall  callback
*/
setInterstitialShowCallback : function(cpPlaceId, showCall)
```
Sample:
```javascript
var ilShowCallUIButton = this.createButton(x, y, "ilShowCall");
ilShowCallUIButton.addTouchEventListener(function(sender, type) {
    if (type == 2) {
        upltv.setInterstitialShowCallback(cpPlaceId, 
            function(type, cpid) {
                var event = "unkown";
                if (type == upltv.AdEventType.INTERSTITIAL_EVENT_DID_SHOW) {
                    event = "Did_Show";
                }
                else if (type == upltv.AdEventType.INTERSTITIAL_EVENT_DID_CLICK) {
                    event = "Did_Click";
                }
                else if (type == upltv.AdEventType.INTERSTITIAL_EVENT_DID_CLOSE) {
                    event = "Did_Close";
                }
            }
        );
    }
}, this);
```

### 3. Judge if the interstitial ad is ready
Judge if the interstitial ad is ready accroding ad unit, and  return Boolean results synchronously, true means that the AD is ready to be displayed, and false means that the AD is not show and still in the request.
```javascript
// @param cpPlaceId  cpPlaceId
isInterstitialReady : function(cpPlaceId)
```

Sample:
```javascript
var ilReadyAsynUIButton = this.createButton(x, y, "ilReadyAsyn");
ilReadyAsynUIButton.addTouchEventListener(function(sender, type) {
    if (type == 2) {
        upltv.isInterstitialReadyAsyn(cpPlaceId, function(r) {
            cc.log("===> js il ad isreadyasyn: %s at ad unit:%s", r, cpPlaceId);
        });
    }
}, this);
```

### 4. Show interstitial AD
show a interstitial ad according to the ad ad unit.
```javascript
// @param cpPlaceId ad unit
showInterstitialAd : function(cpPlaceId)
```

Sample：
```javascript
var ilShowUIButton = this.createButton(x, y, "ilShow");
ilShowUIButton.addTouchEventListener(function(sender, type) {
    if (type == 2) {
        var r = upltv.isInterstitialReady(cpPlaceId);
        if (r == true) {
            upltv.showInterstitialAd(cpPlaceId);
        }
    }
}, this);
```

### 5. Debug view of Interstital Ad 
In order to help developers to view the use and loading status of ad, we provide a debug page for the ad of the screen, which can be opened to observe the configuration parameters and loading status of the ad.
```javascript
showInterstitialDebugUI : function()
```
sample：
```javascript
var ilShowUIButton = this.createButton(x, y, "ilShowUI");
ilShowUIButton.addTouchEventListener(function(sender, type) {
    if (type == 2) {
        upltv.showInterstitialDebugUI();
    }
}, this);
```