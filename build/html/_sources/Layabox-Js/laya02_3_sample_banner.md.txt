## Banner Ad

Banner ads are divided into top banner and bottom banner, and JavascriptPlugin further simplifies the implementation of banner ads, providing interfaces such as display, hide, remove, and event callbacks.


### 1.Callback of Banner
Banner ad needs to set up the show of banner ad, click and remove the callback interface of events. The callback interface is saved internally by the plug-in, so you don't need to set it up multiple times, only calling upltv:removeBannerAdAt(cpPlaceId) will be deleted.

```cpp

/**
* @param cpPlaceId  ad unit
* @param callback
*/
setBannerShowCallback : function(cpPlaceId, bannerCall)
```
Sample：

```cpp
var bnCallButton = this.createButton(x, y, "SetBNCall");
bnCallButton.addTouchEventListener(function(sender, type) {
    if (type == 2) {
        var bannerCall = function(type, cpadid) {
            var event = "unkown";
            if (type == upltv.AdEventType.BANNER_EVENT_DID_SHOW) {
                event = "Did_Show";
            }
            else if (type == upltv.AdEventType.BANNER_EVENT_DID_CLICK) {
                event = "Did_Click";
            }
            else if (type == upltv.AdEventType.BANNER_EVENT_DID_REMOVED) {
                event = "Did_Removed";
            }
        };

        upltv.setBannerShowCallback(topCpId, bannerCall);
        upltv.setBannerShowCallback(bottomCpId, bannerCall);
    }
}, this);
```

### 2.Show top banner ads
Show the banner at the top of the screen according to the ad unit.

```cpp
/**
* @param cpPlaceId palcementid
*/
showBannerAdAtTop : function(cpPlaceId)
```

Sample：

```cpp
var bnTopButton = this.createButton(x, y, "TopBNShow");
bnTopButton.addTouchEventListener(function(sender, type) {
    if (type == 2) {
        upltv.showBannerAdAtTop(topCpId);
    }
}, this);
```

**It should be noted that when the top Banner of the Iphonex phone is blocked by the status bar, it can be solved by adjusting the displacement of the top Banner.**

```cpp
/**
* On an Iphonex phone, when the top Banner is blocked by the status bar, you can solve this problem by adjusting the displacement of the top banner
* @param padding: The top Banner's offset value, such as 32, will shift down 32 pixels
* This feature is not supported on the Android platform
* supported from 3002
*/
setTopBannerPadingForIphoneX : function(padding);
```

### 3.Hide top banner ads

```cpp
hideBannerAdAtTop : function()
```

Sample:
```javascript
var bnHideButton = this.createButton(x, y, "hideAllBN");
bnHideButton.addTouchEventListener(function(sender, type) {
    if (type == 2) {
        upltv.hideBannerAdAtTop();
    }
}, this);
```

### 4. Show bottom banner ads
Show the banner at the bottom of the screen according to the ad unit.
```javascript
// @param cpPlaceId ad unit
showBannerAdAtBottom : function(cpPlaceId)
```

Sample:
```javascript
var bnBottomButton = this.createButton(x, y, "BottomBNShow");
bnBottomButton.addTouchEventListener(function(sender, type) {
    if (type == 2) {
        upltv.showBannerAdAtBottom(bottomCpId);
    }
}, this);
```

### 5. Hide bottom banner ads

```javascript
hideBannerAdAtBottom : function()
```

Sample:
```javascript
var bnHideButton = this.createButton(x, y, "hideAllBN");
bnHideButton.addTouchEventListener(function(sender, type) {
    if (type == 2) {
        upltv.hideBannerAdAtBottom();
    }
}, this);
```

### 6.Remove banner ads
Remove a banner ad accroding to ad unit
```javascript
// @param cpPlaceId ad unit
removeBannerAdAt : function(cpPlaceId)
```

Sample：
```javascript
var bnRemoveButton = this.createButton(x, y, "removeAllBn");
bnRemoveButton.addTouchEventListener(function(sender, type) {
    if (type == 2) {
        upltv.removeBannerAdAt(topCpId);
        upltv.removeBannerAdAt(bottomCpId);
    }
}, this);
```