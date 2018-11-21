## Interstitial API
### 1. Set the interstitial load callback 
Load results (success or failure) to listen for the current interstitial ad .This interface is automatically released once a callback is made, and the callback interface needs to be reset when listening again.
```lua
-- Determine if a Interstitial ad is ready based on the ad unit
-- Asynchronously returns a bool result, true means the ad is ready to be displayed,false means the ad is still in the request
-- cpPlaceId：ad unit
-- callback：callback(true)  or callback(false)
upltv:isInterstitialReadyAsyn(cpPlaceId, callback)
```
Sample：
```lua
local btnInterstitialShow = createBtnAt(self, left, top, fontsize, "iLReadyAsyn")
btnInterstitialShow:addTouchEventListener(function(sender, eventType)
    if  (2 == eventType) then
        upltv:isInterstitialReadyAsyn(ilPlaceId, function(r)
            if r == true then
                print("=====> Interstitial is ready")
            else
                print("=====> Interstitial is not ready")
            end
        end)
    end
end)
```
### 2. Set show callback of Interstitial Ad
Set up the callback interface for the display of interstitial ad which is used to listen to the callback of showing .The  interstitial ad shows that references to the callback interface are stored  and not released.
```lua
-- Set the callback interface when Interstitial ad show, which is used to monitor the event callback of the interstitial advertisement such as click, close, etc. during showing.
-- The plugin shows that the reference to the callback interface will be saved internally and will not be released.
-- Callback event type: show, click, close
-- @param cpPlaceid ad unit，showCall showCall(type, cpPlaceId)
upltv:setInterstitialShowCallback(cpPlaceId, showCall)
```
Sample：
```lua
local btnInterstitialShowCall = createBtnAt(self, left, top, fontsize, "iLShowCall")
btnInterstitialShowCall:addTouchEventListener(function(sender, eventType)
    if  (2 == eventType) then
        local function ilShowCall(type, cpadid)
            local event = "unkown"
            if type == upltv.AdEventType.INTERSTITIAL_EVENT_DID_SHOW then
                event = "Did_Show"
            elseif type == upltv.AdEventType.INTERSTITIAL_EVENT_DID_CLICK then
                event = "Did_Click"
            elseif type == upltv.AdEventType.INTERSTITIAL_EVENT_DID_CLOSE then
                event = "Did_Close"
            end
            print("=====> Interstitial ShowCall Event:" .. event ..", at :" .. cpadid)
        end
        upltv:setInterstitialShowCallback(ilPlaceId, ilShowCall)
    end
end)
```
### 3. Judge if the interstitial ad is ready
Judge if the interstitial ad is ready accroding ad unit, and  return Boolean results synchronously, true means that the AD is ready to be displayed, and false means that the AD is not show and still in the request.
```lua
upltv:isInterstitialReady(cpPlaceId)
```
Sample：
```lua
local btnInterstitialShow = createBtnAt(self, left, top, fontsize, "iLReadyAsyn")
btnInterstitialShow:addTouchEventListener(function(sender, eventType)
    if  (2 == eventType) then
        upltv:isInterstitialReadyAsyn(ilPlaceId, function(r)
            if r == true then
                print("=====> Interstitial is ready")
            else
                print("=====> Interstitial is not ready")
            end
        end)
    end
end)
```
### 4. Show interstitial AD
show a interstitial ad according to the ad ad unit.
```lua
upltv:showInterstitialAd(cpPlaceId)
```
Sample：
```lua
local btnInterstitialShow = createBtnAt(self, left, top, fontsize, "iLShow")
btnInterstitialShow:addTouchEventListener(function(sender, eventType)
    if  (2 == eventType) then
        if upltv:isInterstitialReady(ilPlaceId) == true then
            print("=====> Interstitial is ready")
            upltv:showInterstitialAd(ilPlaceId)
        else
            print("=====> Interstitial is not ready")
        end
    end
end)
```
### 5.  Debug view of Interstital Ad 
In order to help developers to view the use and loading status of ad, we provide a debug page for the ad of the screen, which can be opened to observe the configuration parameters and loading status of the ad.
```lua
upltv:showInterstitialDebugUI()
```
Sample：
```lua
local btnshowInterActivity = createBtnAt(self, left, top, fontsize, "iLDebugUI")
btnshowInterActivity:addTouchEventListener(function(sender, eventType)
    if  (2 == eventType) then
        upltv:showInterstitialDebugUI()
    end
end)
```