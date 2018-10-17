## A/B Testing

### 1. A/B Test Initialzation and got data
Call this method to complete A/B Test initialization after initializing the SDK when performing A/B tests
```cpp
/**
* @param gameAccountId          const char*type，user's account id in the game (required)
* @param completeTask           bool type，Whether or not the novice task in the game has been completed
* @param isPaid                 int type，If the user pays, 0 does not pay
* @param promotionChannelName   const char* type，Promotion channels, no value can be passed ""
* @param gender                 const char*，"M", "F"，Unknown can be passed""
* @param age                    int type，Unknown can be passed -1
* @param tags                   vector type，tips，no value can be passed nullptr
*/
static void initAbtConfigJson(const char* gameAccountId, bool completeTask, int isPaid,const char* promotionChannelName, const char* gender, int age, vector<string> *tags);
```
For example：
```cpp
void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        log("===> cpp button touch tag :%d",tag);
        switch (tag)
        {
            case 1001:
            {
                // The following parameters do not make any sense, but are used to demonstrate how to invoke the API
                vector<string> tags = {"This is the first element.","The second one.","The last one."};
                UpltvBridge::initAbtConfigJson("u89731", true, 0, "Facebook", "", -1, &tags);
            }
                break;
        }
   }
}
```
### 2. Get the result of A/B Test
After the initialization of A/B Test, the results are obtained through this method.
```cpp
/**
* To ensure that the results are correctly obtained, the call time is recommended to delay initAbtConfigJson() by more than 2 seconds
* @param cpPlaceId  string type
* @return const char*
*/
static const char* getAbtConfig(const char* cpPlaceId);
```
For example：
```cpp
void HelloWorld::touchEvent(cocos2d::Ref *pSender, cocos2d::ui::Widget::TouchEventType type, int tag)
{
    if (type == cocos2d::ui::Widget::TouchEventType::ENDED) {
        log("===> cpp button touch tag :%d",tag);
        switch (tag)
        {
            case 1001:
            {
                // Get config configuration
                string r = UpltvBridge::getAbtConfig("pass");
                log("===> cpp getABtConfig r :%s",r.c_str());
            }
                break;
        }
   }
}
```
