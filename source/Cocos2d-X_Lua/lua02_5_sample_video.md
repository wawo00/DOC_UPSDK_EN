## Reward video Ad

### 1. Load callback of Reward video
This API is used to listen for the loading results of the current excited video. Once this interface is called back, the internal will be automatically released, and the callback interface needs to be reset when listening again.

```lua

-- @param loadsuccess  Motivate the callback when the video is loaded loadsuccess(cpadid, msg)
-- @param failCall    Motivate the callback when the video is loaded failed，locadfail(cpadid, msg)
upltv:setRewardVideoLoadCallback(loadsuccess, locadfail)
```
Sample：
```lua
local btnshowvideoActivity = createBtnAt(self, left, top, fontsize, "rdLoadCall")
btnshowvideoActivity:addTouchEventListener(function(sender, eventType)
    if  (2== eventType) then
        upltv:setRewardVideoLoadCallback(function(cpadid,msg)
            print("=====>RewardVideoLoadCallback success at " .. cpadid)         
        end,
        function(cpadid, msg)
            print("=====> RewardVideoLoadCallback fail at " .. cpadid .. " because of " .. msg) 
        end)
    end
end)
```
#### 2. Show callback of Reward video Ad
    Set up the callback interface of video show to listen to the callback of the event (click, close, reward, etc.) of the video advertisement. Reward video shows that the reference to the callback interface is stored internally and not released, so you only need to set it once.
```lua
-- Set the Reward video display callback interface to monitor the event callbacks such as clicks, closes, rewards, etc.
-- References will be saved internally and will not be released
-- Callback event type: display, click, close, reward success, reward failed
-- @param：showCall ,showCall(type, cpadid)
upltv:setRewardVideoShowCallback(showCall)
```

Sample：
```lua
local btnshowvideoActivity = createBtnAt(self, left, top, fontsize, "rdShowCall")
btnshowvideoActivity:addTouchEventListener(function(sender, eventType)
    if  (2 == eventType) then
        local function rewardShowCall(type, cpadid)
            local event = "unkown"
            if type == upltv.AdEventType.VIDEO_EVENT_DID_SHOW then
                event = "Did_Show"
            elseif type == upltv.AdEventType.VIDEO_EVENT_DID_CLICK then
                event = "Did_Click"
            elseif type == upltv.AdEventType.VIDEO_EVENT_DID_CLOSE then
                event = "Did_Close"
            elseif type == upltv.AdEventType.VIDEO_EVENT_DID_GIVEN_REWARD then
                event = "Did_Given_Reward"
            elseif type == upltv.AdEventType.VIDEO_EVENT_DID_ABANDON_REWARD then
                event = "Did_Abandon_Reward"
            end
            print("=====> RewardVideo show call Event:" .. event ..", at :" .. cpadid)
        end
        upltv:setRewardVideoShowCallback(rewardShowCall)
    end
end)
```
#### 3. Judge if the Reward Video ad is ready
Synchronously return Boolean results, true indicates that the AD is ready to be displayed, and false indicates that the AD is not show and still  in the request
  ```lua

upltv:isRewardReady()
```

Sample：
```lua
local btnloadvideo = createBtnAt(self, left, top, fontsize, "rdReady")
btnloadvideo:addTouchEventListener(function(sender, eventType)
    if  (2 == eventType) then
        local r = upltv:isRewardReady()
        if (r==true) then
            print("=====> btn up isRewardReady: true")
        else
            print("=====> btn up isRewardReady: false")
        end
    end
end)
```
#### 4. Show Reward Video Ad 
When show the Reward Video ad, you need to upload a cpPlaceId, which is the ad unit , used for business management, in order to distinguish the source of revenue.
```lua
upltv:showRewardVideo(cpPlaceId)
```
Sample：
```lua
local btnloadvideo = createBtnAt(self, left, top, fontsize, "rdShow")
btnloadvideo:addTouchEventListener(function(sender, eventType)
    if  (2 == eventType) then
        local r = upltv:isRewardReady()
        if (r==true) then
            upltv:showRewardVideo("show_reward")
            print("=====> btn up isRewardReady: true")
        else
            print("=====> btn up isRewardReady: false")
        end
    end
end)
```
#### 5. Debug view of Reward Video Ad
In order to help developers to view the use and loading status of ad, we provide a debug page for the ad of the screen, which can be opened to observe the configuration parameters and loading status of the ad.

```lua
upltv:showRewardDebugUI()
```
Sample：
```lua
local btnshowvideoActivity = createBtnAt(self, left, top, fontsize, "rdDebugUi")
btnshowvideoActivity:addTouchEventListener(function(sender, eventType)
    if  (2 == eventType) then
        upltv:showRewardDebugUI()
    end
end)
```

