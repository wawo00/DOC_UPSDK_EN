
## Unity Plugin A/B Test

#### 1.AbTest initialization
```csharp
/*
 * The AbTest must be initialized through this API before getting the ad configuration of AbTest
 */
public static void initAbtConfigJson(string gameAccountId, bool completeTask, int isPaid, string promotionChannelName,  string gender, int age, string[] tags) ;
```
Sample:

```csharp
public void onBtnInitABConfig_Click()
{
    //The following parameters have no real meaning,just for testing
    UPSDK.initAbtConfigJson("mygameAccountId_123", true, 18, "324000", "gender", 33, new string[]{"This is the first element.", "The second one.", "The last one."});
}
```
#### 2.Get Abtest configuration

```csharp
    /*
	* Get abtest configuration of upsdk ads
	* returned result could be Json character string, posiblity could be null
	* Before invoking this API, pl;ease invoke initAbtConfigJson() to finish the initialization for abtest configuration
	*/
public static string getAbtConfig(string placementId)；

```

Sample：

```csharp
public void onBtnGetABConfig_Click()
{   
	//parameter is placementId
    string r = UPSDK.getAbtConfig ("hello");
    Debug.Log ("==> onBtnGetABConfig_Click:" + r);
}
```