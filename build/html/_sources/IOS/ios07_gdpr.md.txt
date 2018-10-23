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

#### 2.checkIsEuropeanUnionUser
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

#### 3.the developer can not request the user to authorize the use of private information.

In response to this situation, UPSDK provides an API for using Alter to request authorization to use private information from users, as following:

```objective-c
/**
 Alert to request access to private information from users
 
 @param viewController 
 @param completionBlock Callback,  YES means the user agrees to use the private information, and NO means the user does not agree to use the private information.
 */
+ (void)requestAuthorizationWithAlert:(UIViewController *)viewController completion:(void (^)(BOOL isAccepted))completionBlock;
```


Sample:

```objective-c
[UPSDK requestAuthorizationWithAlert:vc completion:^(BOOL isAccepted) {
    if (isAccepted) {

    }
    else {

    }
}];
```

--------

#### 4.Developers want to know the current status of the GDPR authorization

UPSDK provides an API to obtain current GDPR authorization status

```objective-c
/**
 
 @return Status of GDPR authorization
 */
+ (UPAccessPrivacyInfoStatus)getCurrentAccessPrivacyInfoStatus;
```


Return value : `UPAccessPrivacyInfoStatusAccepted` means the user agrees, `UPAccessPrivacyInfoStatusDenied` means the user refuses, `UPAccessPrivacyInfoStatusNone` indicates that the user is unknown or has not requested authorization from the user.

#### 5.Overall Sample:

```objective-c
//Step1 
[UPSDK checkIsEuropeanUnionUser:^(BOOL isEuropeanUnion) {
    if (isEuropeanUnion) {
    
        // Step2 Request  authorization to use information
        [UPSDK requestAuthorizationWithAlert:vc completion:^(BOOL isAccepted) {
            if (isAccepted) {

                // Step3 Update GDPR Authorization Status of UPSDK (Agree)
                [UPSDK updateAccessPrivacyInfoStatus:UPAccessPrivacyInfoStatusAccepted];
            }
            else {
                
                 // Step3 Update GDPR Authorization Status of UPSDK (Deny)
                [UPSDK updateAccessPrivacyInfoStatus:UPAccessPrivacyInfoStatusDenied];
            }

            // Step4 Initialization
            [UPSDK initSDK:UPSDKGlobalZoneForeign];
        }];
    }
    else {

        // Step4 Initialization
        [UPSDK initSDK:UPSDKGlobalZoneForeign];
    }
}];
```

The first step and the second step that can be implemented by developer to improve the user experience. And you alson can use the corresponding API of UPSDK to achieve it.