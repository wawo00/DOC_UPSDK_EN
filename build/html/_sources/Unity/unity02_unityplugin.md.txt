
## How to add plugin in Unity project

The downloaded UPSDK Unity Plugin, is a kind of *.unitypackage file. This document will give typical examples in two different platforms, please refer them as followed:

> Egineer who is familiar with this procedure, please skpi this section.

### 1. Updating the plugin
If you have integrated UPSDK Unity Plugin before, to make sure the correctness of plugin library after updating, we suggest that please completely delete UPSDK Unity Plugin before the updating.

In your Unity project, please check whether `Assets/PolyADSDK/Plugins/` and `Assets/StreamingAssets/UPSDK_android/` exist. Generally, when you delete `PolyADSDK` and `UPSDK_android` folder(including its subcatalog), the whole import plugin will be completely deleted.

If you have edit the name of `PolyADSDK` catalog or the location of its subcatalog, please find out its corrected location and delete it. Specially, if you added some files after updating `PolyADSDK` and those files need to be retained, please be careful in case deleting them.

Please continue **NEXT STEP**.

### 2. In your project, select Assets, right click and select: Import Package -> Custom Package

![import](http://docc.upltv.com/uploads/201705/592e66a727d89_592e66a7.png "import")

### 3. Choose your downloaded plugin package: such as  export.unitypackage. Then please click "open" button, Unity will automatically load the plugin package.

![open file](http://docc.upltv.com/uploads/201705/592e684f54573_592e684f.png "open file")

### 4.When Untiy finishes loading the plugin package, you will see a pop-up window that shows you which plugin resources to import, like the picture below:

![import plugin](http://docc.upltv.com/uploads/201705/592e69ba77ebf_592e69ba.png "import plugin")


Generally select "All" button, then click "Import" to import. If your project only supports Android, you should ignore “**IOS**” button; if your project only supports iOS, please ignore “**Android**” button.

### 5. After importing plugin for UPSDK successfully, you could see a folder named **PolyADSDK******in your project. Among the examples, all resources for plugin will be imported completely as we considered about the supports for both Android and iOS.


![load ok](http://docc.upltv.com/uploads/201705/592e6b65dd56e_592e6b65.png "load ok")

