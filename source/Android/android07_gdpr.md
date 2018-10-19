
## GDPR

`GDPR "The General Data Protection Regulation" is a data protection program issued by the European Union. `
If your product is intended for EU users, we offer the following solutions to ensure that `UPSDK` complies with the `GDPR' rules.

`UPSDK` supports the EU `GDPR` rules in the `3.0.03` version, and developers who will distribute in EU region must handle this logic.

### GDPR Samples
#### Customizing implementation
Customized dialog of GDPR according to the style of your game to ensure the best product experience.
When adopting this scheme, it is only necessary to inform the UPSDK of the authorization result before initializing the UPSDK.

Sample：
```csharp
{
    // old code for initialization
    // AvidlyAdsSdk.init(xxxx);

    // new code for GDPR
    AccessPrivacyInfoManager.UPAccessPrivacyInfoStatusEnum result=UPAdsSdk.getAccessPrivacyInfoStatus(MainActivity.this);
    if (result ==  AccessPrivacyInfoManager.UPAccessPrivacyInfoStatusEnum.UPAccessPrivacyInfoStatusUnkown
        || result ==  AccessPrivacyInfoManager.UPAccessPrivacyInfoStatusEnum.UPAccessPrivacyInfoStatusDefined) {
         // if the user is in the EU
        UPAdsSdk.isEuropeanUnionUser (MainActivity.this,isEuropeanUserCallback);
    } else {
        
        UPAdsSdk.init(MainActivity.this, UPAdsSdk.UPAdsGlobalZone.UPAdsGlobalZoneForeign);
    }

    // .....
}

UPAdsSdk.UPEuropeanUnionUserCheckCallBack isEuropeanUserCallback=new UPAdsSdk.UPEuropeanUnionUserCheckCallBack(){
    @Override
    public void isEuropeanUnionUser(boolean result) {
        if (result) {
            // client in the EU，ask for authorizing
            // ......
            // ......
    
            // please use this method
            // if people deny this protocol,tell upsdk throught following method
            UPAdsSdk.updateAccessPrivacyInfoStatus(this, AccessPrivacyInfoManager.UPAccessPrivacyInfoStatusEnum.UPAccessPrivacyInfoStatusDefined);
  
            //  if people agree this protocol,tell upsdk throught following method
            UPAdsSdk.updateAccessPrivacyInfoStatus(this, AccessPrivacyInfoManager.UPAccessPrivacyInfoStatusEnum.UPAccessPrivacyInfoStatusAccepted);

            // initializing after calling  updateAccessPrivacyInfoStatus()
            UPAdsSdk.init(MainActivity.this, UPAdsSdk.UPAdsGlobalZone.UPAdsGlobalZoneForeign);

        } else {
            // if client is not in the EU,just initializing upsdk
            UPAdsSdk.init(MainActivity.this, UPAdsSdk.UPAdsGlobalZone.UPAdsGlobalZoneForeign);
        }
    }
};

```

#### Quick implementation
If you use the standard authorization process provided by UPSDK, please refer to the following code .

Sample：

```csharp

{
    // old code for initialization
    // AvidlyAdsSdk.init(xxxx);

    // new code for GDPR
    AccessPrivacyInfoManager.UPAccessPrivacyInfoStatusEnum result=UPAdsSdk.getAccessPrivacyInfoStatus(MainActivity.this);
    if (result ==  AccessPrivacyInfoManager.UPAccessPrivacyInfoStatusEnum.UPAccessPrivacyInfoStatusUnkown
        || result ==  AccessPrivacyInfoManager.UPAccessPrivacyInfoStatusEnum.UPAccessPrivacyInfoStatusDefined) {

        //if the user is in the EU
        UPAdsSdk.isEuropeanUnionUser (MainActivity.this,isEuropeanUserCallback);
    } else {
        UPAdsSdk.init(MainActivity.this, UPAdsSdk.UPAdsGlobalZone.UPAdsGlobalZoneForeign);
    }
    // .....
}

UPAdsSdk.UPEuropeanUnionUserCheckCallBack isEuropeanUserCallback = new UPAdsSdk.UPEuropeanUnionUserCheckCallBack(){
    @Override
    public void isEuropeanUnionUser(boolean result) {
        if (result) {
            // result: true means that client in the EU
            // ......
            // ......

            //pop up Dialog to ask authorizing
             UPAdsSdk.notifyAccessPrivacyInfoStatus(MainActivity.this,myAccessPrivacyStatusInfoCallBack);
        } else {
            // if client is not in the EU,just initializing upsdk
            UPAdsSdk.init(MainActivity.this, UPAdsSdk.UPAdsGlobalZone.UPAdsGlobalZoneForeign);
        }
    }
};

private UPAdsSdk.UPAccessPrivacyInfoStatusCallBack myAccessPrivacyStatusInfoCallBack = new UPAdsSdk.UPAccessPrivacyInfoStatusCallBack() {
    @Override
    public void onAccessPrivacyInfoAccepted() {
        Log.i(TAG, "onAccessPrivacyInfoAccepted:");
        // ......
        // ......
        UPAdsSdk.init(MainActivity.this, UPAdsSdk.UPAdsGlobalZone.UPAdsGlobalZoneForeign);
    }

    @Override
    public void onAccessPrivacyInfoDefined() {
        Log.i(TAG, "onAccessPrivacyInfoDefined:");
        // ......
        // ......
        UPAdsSdk.init(MainActivity.this, UPAdsSdk.UPAdsGlobalZone.UPAdsGlobalZoneForeign);
    }

};
```
### GDPR API

#### 1.notifyAccessPrivacyInfoStatus

The authorization window pops up to explain to the user that we will collect data and ask the user whether to approve the authorization. If the user refuses to authorize, the collection of related data will be abandoned. Please call before initializing the UPSDK.

```csharp
public static void notifyAccessPrivacyInfoStatus(final Context context, final UPAdsSdk.UPAccessPrivacyInfoStatusCallBack callback)
```
Sample：

```csharp
UPAdsSdk.notifyAccessPrivacyInfoStatus(MainActivity.this,myAccessPrivacyStatusInfoCallBack);

private UPAdsSdk.UPAccessPrivacyInfoStatusCallBack myAccessPrivacyStatusInfoCallBack =new UPAdsSdk.UPAccessPrivacyInfoStatusCallBack() {
   @Override
   public void onAccessPrivacyInfoAccepted() {
       Log.i(TAG, "onAccessPrivacyInfoAccepted: ");
   }

   @Override
   public void onAccessPrivacyInfoDefined() {
       Log.i(TAG, "onAccessPrivacyInfoDefined");
   }
};
  
```


#### 2.updateAccessPrivacyInfoStatus
When externally asking GDPR authorization, this method is called to inform the UPSDK of the user authorization result, and UPSDK will no longer perform authorization popup management. Please call before initializing the UPSDK.

```csharp
public static void updateAccessPrivacyInfoStatus(final Context context,UPConstant.UPAccessPrivacyInfoStatusEnum enumValue)
```

Sample：

```csharp
/**
* agree to collect data
*/
UPAdsSdk.updateAccessPrivacyInfoStatus(this, AccessPrivacyInfoManager.UPAccessPrivacyInfoStatusEnum.UPAccessPrivacyInfoStatusAccepted);

/**
 * disagree to collect data
 */
UPAdsSdk.updateAccessPrivacyInfoStatus(this, AccessPrivacyInfoManager.UPAccessPrivacyInfoStatusEnum.UPAccessPrivacyInfoStatusDefined);

```


#### 3.getAccessPrivacyInfoStatus
Obtain the user authorization result, which can be called before initializing the UPSDK.

```groovy
public static UPAccessPrivacyInfoStatusEnum getAccessPrivacyInfoStatuss(Context context)
```

Sample：
```csharp
AccessPrivacyInfoManager.UPAccessPrivacyInfoStatusEnum result=UPAdsSdk.getAccessPrivacyInfoStatus(MainActivity.this);
```

#### 4.isEuropeanUnionUser
Determine whether the user belongs to the EU region,which can be called before initializing the UPSDK 

```csharp
public static void isEuropeanUnionUser(Context context, UPAdsSdk.UPEuropeanUnionUserCheckCallBack callback)
```
Sample：
```csharp
 UPAdsSdk.isEuropeanUnionUser(MainActivity.this, new UPAdsSdk.UPEuropeanUnionUserCheckCallBack() {
    @Override
    public void isEuropeanUnionUser(boolean isEurope) {
        if (isEurope) {
            //TODO
        } else {
            //TODO
        }
    }
});
```

