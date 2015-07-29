##调用系统下载功能下载APK文件，并通过广播提示下载完成安装

####调用代码如下：
```java
DownloadManager downloadManager = (DownloadManager) getSystemService(DOWNLOAD_SERVICE);  
Uri uri = Uri.parse(linkUrl);  
Request request = new Request(uri);  
//设置允许使用的网络类型，这里是移动网络和wifi都可以    
request.setAllowedNetworkTypes(DownloadManager.Request.NETWORK_MOBILE|DownloadManager.Request.NETWORK_WIFI);    
//禁止发出通知，既后台下载，如果要使用这一句必须声明一个权限：android.permission.DOWNLOAD_WITHOUT_NOTIFICATION    
request.setNotificationVisibility(DownloadManager.Request.VISIBILITY_VISIBLE);
downloadManager.enqueue(request);
```

####在清单文件声明权限：
```xml
<uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
```

####在清单文件注册广播：
```xml
<receiver android:name=".CompleteReceiver" >
  <intent-filter>
    <action android:name="android.intent.action.DOWNLOAD_COMPLETE" />
    <action android:name="android.intent.action.DOWNLOAD_NOTIFICATION_CLICKED" />
  </intent-filter>
</receiver>
```
