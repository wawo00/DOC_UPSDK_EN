## GDPR
`GDPR "The General Data Protection Regulation" is a data protection program issued by the European Union. 
f your product is intended for EU users, we offer the following solutions to ensure that `UP ADSDK` complies with the `GDPR' rules.

### GDPR Samples
#### Customizing implementation
Customized dialog of GDPR according to the style of your game to ensure the best product experience.
When adopting this scheme, it is only necessary to inform the UPSDK of the authorization result before initializing the UPSDK.

Sample:
```csharp
{
     // old code for initialization
    // AvidlyAdsSdk.init(xxxx);

    // new code for GDPR
    UPConstant.UPAccessPrivacyInfoStatusEnum result = Polymer.UPSDK.getAccessPrivacyInfoStatus();
    if (result == UPConstant.UPAccessPrivacyInfoStatusEnum.UPAccessPrivacyInfoStatusUnkown
        || result == UPConstant.UPAccessPrivacyInfoStatusEnum.UPAccessPrivacyInfoStatusFailed) {
        // if the user is in the EU
        UPSDK.isEuropeanUnionUser (new Action <bool, string>(isEuropeanUserCallback));
    } else {
        UPSDK.initPolyAdSDK (UPConstant.SDKZONE_FOREIGN);
    }

    // .....
}

private void isEuropeanUserCallback(bool result, string msg) {
    // result: true 表示欧盟地区用户，否则非欧盟地区用户
    if (result) {
           // client in the EU，ask for authorizing
            // ......
            // ......
    
        // callYourOwnGDPRDialog() is your method
        // yourOwnGDPRCallback() is your callback
        // Replace this code according to actual situation
        callYourOwnGDPRDialog(yourOwnGDPRCallback);

    } else {
      // if client is not in the EU,just initializing upsdk
        UPSDK.initPolyAdSDK (UPConstant.SDKZONE_FOREIGN);
    }
}

private void yourOwnGDPRCallback(bool result) {
    //  if people agree this protocol,tell upsdk throught following method
    if (result) {
        UPSDK.updateAccessPrivacyInfoStatus(UPConstant.UPAccessPrivacyInfoStatusEnum.UPAccessPrivacyInfoStatusAccepted);
    } else {
    // if people deny this protocol,tell upsdk throught following method
        UPSDK.updateAccessPrivacyInfoStatus(UPConstant.UPAccessPrivacyInfoStatusEnum.UPAccessPrivacyInfoStatusDefined);
    }
 
   // initializing after calling  updateAccessPrivacyInfoStatus()
    UPSDK.initPolyAdSDK (UPConstant.SDKZONE_FOREIGN);
}
```

#### Quick implementation
If you use the standard authorization process provided by UPSDK, please refer to the following code .

Sample:

```csharp

{
    // .....

    // old code for initialization
    // AvidlyAdsSdk.init(xxxx);

    // new code for GDPR
    UPConstant.UPAccessPrivacyInfoStatusEnum result = Polymer.UPSDK.getAccessPrivacyInfoStatus();
    if (result == UPConstant.UPAccessPrivacyInfoStatusEnum.UPAccessPrivacyInfoStatusUnkown
        || result == UPConstant.UPAccessPrivacyInfoStatusEnum.UPAccessPrivacyInfoStatusFailed) {
        UPSDK.isEuropeanUnionUser (new Action <bool, string>(isEuropeanUserCallback));
    } else {
        UPSDK.initPolyAdSDK (UPConstant.SDKZONE_FOREIGN);
    }

    // .....
}

private void isEuropeanUserCallback(bool result, string msg) {
     // result: true means that client in the EU
    if (result) {
    //pop up Dialog to ask authorizing
        UPSDK.notifyAccessPrivacyInfoStatus (new Action <UPConstant.UPAccessPrivacyInfoStatusEnum, string> (accessPrivacyInforCallback));
    } else {
        UPSDK.initPolyAdSDK (UPConstant.SDKZONE_FOREIGN);
    }
}

private void accessPrivacyInforCallback(UPConstant.UPAccessPrivacyInfoStatusEnum result, string msg) {
    // result of authorizing,and then initialize UPSDK 

    UPSDK.initPolyAdSDK (UPConstant.SDKZONE_FOREIGN);
  
    Debug.Log ("===> accessPrivacyInforCallback Event result: " + result + "," + msg);
}
```

### GDPR API

#### 1.notifyAccessPrivacyInfoStatus
The authorization window pops up to explain to the user that we will collect data and ask the user whether to approve the authorization. If the user refuses to authorize, the collection of related data will be abandoned. Please call before initializing the UPSDK.

```csharp
public static void notifyAccessPrivacyInfoStatus(Action <UPConstant.UPAccessPrivacyInfoStatusEnum, string> callback)
```
Sample：

```csharp
public void onBtnNotifyAccessStatus_Click() {
    Polymer.UPSDK.notifyAccessPrivacyInfoStatus (new Action <UPConstant.UPAccessPrivacyInfoStatusEnum, string>(accessPrivacyInforCallback));
}

private void accessPrivacyInforCallback(UPConstant.UPAccessPrivacyInfoStatusEnum result, string msg) {
     Debug.Log ("===> accessPrivacyInforCallback Event result: " + result + "," + msg);
}
```


#### 2.updateAccessPrivacyInfoStatus
When externally asking GDPR authorization, this method is called to inform the UPSDK of the user authorization result, and UPSDK will no longer perform authorization popup management. Please call before initializing the UPSDK.

```csharp
public static void updateAccessPrivacyInfoStatus(UPConstant.UPAccessPrivacyInfoStatusEnum enumValue)
```

Sample：

```csharp

public void onBtnUpdateAccessStatus_Click() {
    Polymer.UPSDK.updateAccessPrivacyInfoStatus(UPConstant.UPAccessPrivacyInfoStatusEnum.UPAccessPrivacyInfoStatusDefined);
}
```


#### 3.getAccessPrivacyInfoStatus
Obtain the user authorization result, which can be called before initializing the UPSDK.

```csharp
public static UPConstant.UPAccessPrivacyInfoStatusEnum getAccessPrivacyInfoStatus()
```

Sample：
```csharp
public void onBtnGetAccessStatus_Click() {
    UPConstant.UPAccessPrivacyInfoStatusEnum e = Polymer.UPSDK.getAccessPrivacyInfoStatus();
    Debug.Log ("==> getAccessPrivacyInfoStatus :" + e);
}
```

#### 4.isEuropeanUnionUser
Determine whether the user belongs to the EU region,which can be called before initializing the UPSDK.

```csharp
public static void isEuropeanUnionUser(Action <bool, string> callback)
```
Sample：
```csharp
public void onBtnIsEuropeanUnionUser_Click() {
    Polymer.UPSDK.isEuropeanUnionUser (new Action <bool, string>(isEuropeanUserCallback));
}

private void isEuropeanUserCallback(bool result, string msg) {
    Debug.Log ("===> isEuropeanUserCallback Event result: " + result + "," + msg);
}
```
