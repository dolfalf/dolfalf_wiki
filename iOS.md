
## Lifecycle Methods

push通知が来た時callbackされるメソッド順番

```
Our testing for iOS 10 revealed the following sequences of lifecycle methods for the various cases:

DELEGATE METHODS CALLED WHEN OPENING APP  

Opening app when system killed or user killed  
    didFinishLaunchingWithOptions  
    applicationDidBecomeActive    

Opening app when backgrounded  
    applicationWillEnterForeground  
    applicationDidBecomeActive  

DELEGATE METHODS WHEN OPENING PUSH

Opening push when system killed
    [receiving push causes didFinishLaunchingWithOptions (with options) and didReceiveRemoteNotification:background]
    applicationWillEnterForeground
    didReceiveRemoteNotification:inactive
    applicationDidBecomeActive

Opening push when user killed
    didFinishLaunchingWithOptions (with options)
    didReceiveRemoteNotification:inactive [only completionHandler version]
    applicationDidBecomeActive

Opening push when backgrounded
    [receiving push causes didReceiveRemoteNotification:background]
    applicationWillEnterForeground
    didReceiveRemoteNotification:inactive
    applicationDidBecomeActive
```
