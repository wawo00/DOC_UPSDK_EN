## Banner AD
Banner ads are divided into top banner and bottom banner, and CppPlugin further simplifies the implementation of banner ads, providing interfaces such as show, hiding, removal, and event callbacks.

### 1. Callback of banner
Banner ad needs to set up the show of banner ad, click and remove the callback interface of events. The callback interface is saved internally by the plug-in, so you don't need to set it up multiple times, only calling 用upltv:removeBannerAdAt(cpPlaceId) will be deleted.

```lua
-- Set the display callback interface for a banner AD bit, and the callback interface will be saved and only removed by calling upltv:removeBannerAdAt(cpPlaceId)
-- cpPlaceId：banner placementID
-- showCall：Show ads, click to jump or remove callbacks
-- callback parameter：event type，placementID，such as showCall(type, cpPlaceId)
 upltv:setBannerShowCallback(cpPlaceId, showCall)
```
For example：
```lua
local btnsetbannercall = createBtnAt(self, left, top, fontsize, "bannerCall")
btnsetbannercall:addTouchEventListener(function(sender, eventType)
    if  (2 == eventType) then
        local function bannerShowCall(type, cpadid)
            local event = "unkown"
            if type == upltv.AdEventType.BANNER_EVENT_DID_SHOW then
                event = "Did_Show"
            elseif type == upltv.AdEventType.BANNER_EVENT_DID_CLICK then
                event = "Did_Click"
            elseif type == upltv.AdEventType.BANNER_EVENT_DID_REMOVED then
                event = "Did_Removed"
            end
            print("=====> banner ShowCall Event:" .. event ..", at :" .. cpadid)
        end
        upltv:setBannerShowCallback("BannerAd",bannerShowCall)
        upltv:setBannerShowCallback("banner_bbb",bannerShowCall)
    end
end)
```

### 2. Show top banner ads
Show the banner at the top of the screen according to the placementID.
```lua
-- According to  'cpPlaceId' show banner ads at the top of the current screen
upltv:showBannerAdAtTop(cpPlaceId)
```

For example：
```lua
-- show top banner
top = top - disht
local btnshowtopbanner = createBtnAt(self, left, top, fontsize, "topBanner")
btnshowtopbanner:addTouchEventListener(function(sender,eventType)
    if  (2 == eventType) then
        upltv:showBannerAdAtTop("BannerAd")
    end
end)
```

**It should be noted that when the top Banner of the Iphonex phone is blocked by the status bar, it can be solved by adjusting the displacement of the top Banner.**
```lua
-- @param padding: On an Iphonex phone, when the top Banner is blocked by the status bar, you can solve this problem by adjusting the displacement of the top banner
* @param padding: The top Banner's offset value, such as 32, will shift down 32 pixels
-- This feature is not supported on the Android platform
-- supported from 3003
upltv:setTopBannerPadingForIphonex(padding)
```
For example：
```lua
top = top - disht
local btnshowtopbanner = createBtnAt(self, left, top, fontsize, "topBanner")
btnshowtopbanner:addTouchEventListener(function(sender,eventType)
    if  (2 == eventType) then
        upltv:setTopBannerPadingForIphonex(50)
    end
end)
```

### 3. Hide top banner ads

```lua
upltv:hideBannerAdAtTop() 
```
For example：
```lua
local btnhideallbanner = createBtnAt(self, left, top, fontsize, "hideAll")
btnhideallbanner:addTouchEventListener(function(sender,eventType)
    if  (2 == eventType) then
        upltv:hideBannerAdAtTop()
    end
end)
```
### 4. Show bottom banner ads
Show the banner at the bottom of the screen according to the placementID.
```lua
upltv:showBannerAdAtBottom(cpPlaceId)
```
For example：
```lua
local btnshowbottombanner = createBtnAt(self, left, top,fontsize, "bottomBanner")
btnshowbottombanner:addTouchEventListener(function(sender,eventType)
    if  (2 == eventType) then
        upltv:showBannerAdAtBottom("banner_bbb")
    end
end)
```
### 5. Hide bottom banner ads

```lua
upltv:hideBannerAdAtBottom()
```
For example：
```lua
local btnhideallbanner = createBtnAt(self, left, top, fontsize, "hideAll")
btnhideallbanner:addTouchEventListener(function(sender, eventType)
    if  (2 == eventType) then
        upltv:hideBannerAdAtBottom()
    end
end)
```
### 6. Remove banner ads
UPSDK supports removing Banner ads from an ad placement ID.
```lua
upltv:removeBannerAdAt(cpPlaceId)
```
For example：
```lua
local btnremoveallbanner = createBtnAt(self, left, top, fontsize, "removeAll")
btnremoveallbanner:addTouchEventListener(function(sender,eventType)
    if  (2 == eventType) then
        upltv:removeBannerAdAt("banner_bbb")
        upltv:removeBannerAdAt("BannerAd")
    end
end)
```
