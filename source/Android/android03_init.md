## SDK Initializating

Put the following code in your `Application` section
```java
UPAdsSdk.init(final Context context, final UPAdsGlobalZone zone);

    public enum UPAdsGlobalZone {
        UPAdsGlobalZoneForeign,     //Global
        UPAdsGlobalZoneDomestic   //China
    }
```

### SetCustomeId 

If you want to release products in China, because the GAID cannot be collected  normally. Please call this method before `UPAdsSdk.init()`,and the customerId parameter takes the value of AndroidId.
```java
public static void setCustomerId(String customerId)
```
### Debug Model

You can open debug model to get verbose log information during the integration works. Make sure you closed it before release to production.

    UPAdsSdk.setDebuggable(true);