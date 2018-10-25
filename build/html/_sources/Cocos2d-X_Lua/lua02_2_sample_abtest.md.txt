## A/B Test

### 1. A/B Test Initialzation and got data
Call this method to complete A/B Test initialization after initializing the SDK when performing A/B tests
```lua
-- call this method after initializing sdk
-- @param gameAccountId          string type,user's account id in the game (required)
-- @param completeTask           bool type，Whether or not the novice task in the game has been completed
-- @param isPaid                 number type，If the user pays, 0 does not pay
-- @param promotionChannelName   string type，Promotion channels, no value can be passed ""
-- @param gender                 string type，"M", "F"，Unknown can be passed" "
-- @param age                    number type，Unknown can be passed -1
-- @param tags                   String array type,tips，no value can be passed null
initAbtConfigJson : function(gameAccountId, isCompleteTask, isPaid, promotionChannelName, gender, age, tags)
```
For example：
```lua
local btninitAbtConfigJson = createBtnAt(self, left, top, fontsize, "initABtest")
btninitAbtConfigJson:addTouchEventListener(function(sender, eventType)
    if  (2 == eventType) then
        upltv:initAbtConfigJson("u89731", true, 0, "Facebook", "M", -1, {"This is the first element.", "The second one.", "The last one."})
    end
end)
```

### 2. Get the result of A/B Test
After the initialization of A/B Test, the results are obtained through this method.
```lua
-- To ensure that the results are correctly obtained, the call time is recommended to delay initAbtConfigJson() by more than 2 seconds
--  cpPlaceId ：        string type
upltv:getAbtConfig(cpPlaceId)
```
For example：
```lua
local btngetAbtConfigJson = createBtnAt(self, left, top, fontsize, "getAbtConfig")
btngetAbtConfigJson:addTouchEventListener(function(sender, eventType)
    if  (2 == eventType) then
        local r = upltv:getAbtConfig("pass")
        print("=====> getAbtConfig r:" .. type(r))
    end
end)
```
