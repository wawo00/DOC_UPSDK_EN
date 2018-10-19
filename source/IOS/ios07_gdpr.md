## GDPR

`GDPR "The General Data Protection Regulation" is a data protection program issued by the European Union. `
If your product is intended for EU users, we offer the following solutions to ensure that `UPSDK` complies with the `GDPR' rules.

`UPSDK` supports the EU `GDPR` rules in the `3.0.03` version, and developers who will distribute in EU region must handle this logic.

### GDPR Samples
#### Customizing implementation
Customized dialog of GDPR according to the style of your game to ensure the best product experience.
When adopting this scheme, it is only necessary to inform the UPSDK of the authorization result before initializing the UPSDK.

Sample：
```objective-c
{
    // old code for initialization
    // AvidlyAdsSdk.init(xxxx);

    // new code for GDPR
    UPAccessPrivacyInfoStatus result1 = [UPSDK getCurrentAccessPrivacyInfoStatus];
    if (result1 == UPAccessPrivacyInfoStatusNone) {
        [UPSDK checkIsEuropeanUnionUser:^(BOOL isEuropeanUnion) {
            if (isEuropeanUnion) {
             // if the user is in the EU
                [Test yourOwnMethod:nil completion:^(BOOL isAccepted) {
                    NSLog(@"TODO");
                    if (isAccepted) {
                        [UPSDK updateAccessPrivacyInfoStatus:UPAccessPrivacyInfoStatusAccepted];
                    }
                    else {
                        [UPSDK updateAccessPrivacyInfoStatus:UPAccessPrivacyInfoStatusDenied];
                    }
              
                    [UPSDK initSDK:UPSDKGlobalZoneForeign];
                }];
            }
            else {
              
                [UPSDK initSDK:UPSDKGlobalZoneForeign];
            }
        }];
    }
    else {
       
        [UPSDK initSDK:UPSDKGlobalZoneForeign];
    }
}
```
#### Quick implementation
If you use the standard authorization process provided by UPSDK, please refer to the following code .


Sample：
```objective-c
{
    // old code for initialization
    // AvidlyAdsSdk.init(xxxx);

    // new code for GDPR
    UPAccessPrivacyInfoStatus result = [UPSDK getCurrentAccessPrivacyInfoStatus];
    if (result == UPAccessPrivacyInfoStatusNone) {
      
        [UPSDK checkIsEuropeanUnionUser:^(BOOL isEuropeanUnion) {
            if (isEuropeanUnion) {
                // 是欧盟用户
                [UPSDK requestAuthorizationWithAlert:nil completion:^(BOOL isAccepted) {
                    [UPSDK initSDK:UPSDKGlobalZoneForeign];
                }];
            }
            else {
                [UPSDK initSDK:UPSDKGlobalZoneForeign];
            }
        }];
    }
    else {
        [UPSDK initSDK:UPSDKGlobalZoneForeign];
    }
}
```
### GDPR API

#### 1.notifyAccessPrivacyInfoStatus

The authorization window pops up to explain to the user that we will collect data and ask the user whether to approve the authorization.
 If the user refuses to authorize, the collection of related data will be abandoned. Please call before initializing the UPSDK.
 
```objective-c

+ (void)updateAccessPrivacyInfoStatus:(UPAccessPrivacyInfoStatus)status;
```

`UPAccessPrivacyInfoStatus`:
```objective-c
typedef NS_ENUM (NSInteger, UPAccessPrivacyInfoStatus) {
    UPAccessPrivacyInfoStatusNone = 0,      //unknown
    UPAccessPrivacyInfoStatusAccepted = 1,  //agree
    UPAccessPrivacyInfoStatusDenied = 2,    //disagree
};
```

Notice:Do not send `UPAccessPrivacyInfoStatusNone `

Sample:

```objective-c

[UPSDK updateAccessPrivacyInfoStatus:UPAccessPrivacyInfoStatusAccepted];
//SDK init
[UPSDK initSDK:UPSDKGlobalZoneForeign];
```

---------

#### 2、checkIsEuropeanUnionUser
Determine whether the user belongs to the EU region,which can be called before initializing the UPSDK 

```objective-c

+ (void)checkIsEuropeanUnionUser:(void (^)(BOOL isEuropeanUnion))completionBlock;
```



Sample:

```objective-c
[UPSDK checkIsEuropeanUnionUser:^(BOOL isEuropeanUnion) {
    if (isEuropeanUnion) {
    }
    else {
}];
```

---------

#### 3、the developer can not request the user to authorize the use of private information.

In response to this situation, UPSDK provides an API for using Alter to request authorization to use private information from users, as following:

```objective-c
/**
 使用弹窗向用户请求访问隐私信息授权
 
 @param viewController 当前视图控制器
 @param completionBlock 回调，其中isAccepted为YES表示用户同意使用隐私信息，为NO表示用户不同意使用隐私信息
 */
+ (void)requestAuthorizationWithAlert:(UIViewController *)viewController completion:(void (^)(BOOL isAccepted))completionBlock;
```

其中`isAccepted`为`YES`表示用户同意使用隐私信息。为`NO`表示用户拒绝使用隐私信息

demo示例

```objective-c
[UPSDK requestAuthorizationWithAlert:vc completion:^(BOOL isAccepted) {
    if (isAccepted) {
        //同意授权
    }
    else {
        //拒绝授权
    }
}];
```

--------

#### 四、开发者想获知当前GDPR授权状态的

针对此种情况，UPSDK提供了获取当前GDPR授权状态的API，即

```objective-c
/**
 获取当前访问用户隐私信息状态
 
 @return 访问用户隐私信息状态
 */
+ (UPAccessPrivacyInfoStatus)getCurrentAccessPrivacyInfoStatus;
```

其中若返回值为`UPAccessPrivacyInfoStatusAccepted`表示用户同意，`UPAccessPrivacyInfoStatusDenied`表示用户拒绝，`UPAccessPrivacyInfoStatusNone`表示未知或尚未向用户请求授权

--------

#### 五、整体逻辑示例

```objective-c
// 第一步 准备查询用户归属
[UPSDK checkIsEuropeanUnionUser:^(BOOL isEuropeanUnion) {
    if (isEuropeanUnion) {
        // 是欧盟用户
        // 第二步 向用户请求使用隐私信息授权
        [UPSDK requestAuthorizationWithAlert:vc completion:^(BOOL isAccepted) {
            if (isAccepted) {
                // 用户同意使用隐私信息
                // 第三步 向SDK更新GDPR授权状态（同意）
                [UPSDK updateAccessPrivacyInfoStatus:UPAccessPrivacyInfoStatusAccepted];
            }
            else {
                // 用户拒绝使用隐私信息
                // 第三步 向SDK更新GDPR授权状态（拒绝）
                [UPSDK updateAccessPrivacyInfoStatus:UPAccessPrivacyInfoStatusDenied];
            }
            // 第四步  初始化SDK
            [UPSDK initSDK:UPSDKGlobalZoneForeign];
        }];
    }
    else {
        // 非欧盟用户
        // 第四步  初始化SDK
        [UPSDK initSDK:UPSDKGlobalZoneForeign];
    }
}];
```

其中`第一步`和`第二步`均`建议开发者自行实现`以提高用户体验，如无法自行处理的，可以使用SDK提供的对应API处理