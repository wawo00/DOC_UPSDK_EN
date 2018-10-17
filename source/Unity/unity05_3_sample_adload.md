

## Unity Plugin Ad load

#### 1.Callback of Intersitial AD Loading 
```csharp

/*
* Adding callback API for loading Intersitial ads
* @param cpPlaceId:  the symbol of interstitial ads, could not be empty or null
* @param success  callback of successful loading
* @param fail t   callback of failed loading
* 
* Types of callback parameters: Action&lt;string,string>
* The first one is cpPlaceId, placementId of ads, could be empty or null: The second parameter is described info, could be empty or null
* supported from 2028
*/static void setIntersitialLoadCallback(string cpPlaceId, Action&lt;string,string> success, Action&lt;string, string> fail)
```

Sample:

```csharp

//Call this method to set the success and failure callback  for the "inter_aaa" .
public void onBtn_ClickForIntsLoadCallback() {
    // "inter_aaa" is placementId
    UPSDK.setIntersitialLoadCallback ("inter_aaa", 
        new System.Action&lt;string, string>(actionForIntsLoadSuccess),
        new System.Action&lt;string, string>(actionForIntsLoadFail) 
    );
}

private void actionForIntsLoadFail(string placeId, string msg)
{
    Debug.Log ("===> actionForIntsLoadFail Callback at: " + placeId);
}

private void actionForIntsLoadSuccess(string placeId, string msg)
{
    Debug.Log ("===> actionForIntsLoadSuccess Callback at: " + placeId);
}


```

#### 2.Callback of RewardVideo AD Loading 

```csharp
/*
 * Adding callback API for loading rewarded video ads 
 * @param success  callback of successful loading
 * @param fail     callback of failed loading
 * 
 * Types of callback parameters: Action&lt;string,string>
 * The first one is cpPlaceId, placementid of ads, could be empty or 
null; The second parameter is the decribed info, could be empty or null
 * supported from 2028
 */
public static void setRewardVideoLoadCallback(Action&lt;string,string> success, Action&lt;string, string> fail)


```
Sample：
```csharp

//There is no paramter for this method
public void onBtn_ClickForRewardLoadCallback() {
    Polymer.PolyADSDK.setRewardVideoLoadCallback ( 
        new System.Action&lt;string, string>(actionForRewardLoadSuccess),
        new System.Action&lt;string, string>(actionForRewardLoadFail) 
    );
}

//Call this method after RewardVideo Ad loading unsuccessfully
//parameters：placeId is not required or a specific placementid，msg means the reason of failture
private void actionForRewardLoadFail(string placeId, string msg)
{
    Debug.Log ("===> actionForRewardLoadFail Callback at: " + placeId + ", fail reason: " + msg);
}

//Call this method after RewardVideo Ad loading successfully
//parameters：placeId is not required or a specific placementid，msg is alwayes  empty
private void actionForRewardLoadSuccess(string placeId, string msg)
{
    Debug.Log ("===> actionForRewardLoadSuccess Callback at: " + placeId);
}


```
