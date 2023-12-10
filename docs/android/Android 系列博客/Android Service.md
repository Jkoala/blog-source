## 

## 一句话理解Service 

就是一个可以背后的activity 再后台仔细任务的东西

## Service 介绍
代码参考https://github.com/Jkoala/koala_android/tree/main/service_demo
Service不同于后台线程它是跟Activity一个层级的





## Service 使用

### 创建
1. 创建一个自定义Service 继承Service
2. 重写onCreate onBind onStartCommand
3. 在Mainfest.xml 注册我们的Service

### 启动Service 
```java
Intent intent = new Intent(this, MyService.class);
startService(intent);
```


## 前台服务
在Android中，前台服务（Foreground Service）是一种特殊类型的服务，它在用户界面上显示一个通知，并且保持唤醒状态，直到服务被停止。通常，前台服务用于执行一些与应用程序的主要任务相关的重要任务，例如下载文件、播放音乐、上传数据等。

要创建一个前台服务，你需要执行以下步骤：

创建一个服务类，并继承Service类。
在AndroidManifest.xml文件中，将服务声明为前台服务，并在标签中添加foregroundServiceType属性。
在服务中，调用startForeground()方法，并传递一个通知对象和通知的样式。
在服务中，处理与主要任务相关的逻辑。
停止服务时，调用stopForeground()方法来移除通知。
```java
public class MyForegroundService extends Service {  
    private NotificationManager mNotificationManager;  
    private int mNotificationId = 1;  
    private String mTag = "MyForegroundService";  
  
    @Override  
    public IBinder onBind(Intent intent) {  
        return null; // No binding provided  
    }  
  
    @Override  
    public void onCreate() {  
        super.onCreate();  
        mNotificationManager = (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);  
        startForeground(mNotificationId, createNotification());  
    }  
  
    @Override  
    public int onStartCommand(Intent intent, int flags, int startId) {  
        // Perform your main task here  
        // ...  
        return START_STICKY; // Service is restarted if it gets terminated  
    }  
  
    @Override  
    public void onDestroy() {  
        super.onDestroy();  
        stopForeground(true); // Removes the notification  
    }  
  
    private Notification createNotification() {  
        NotificationCompat.Builder builder = new NotificationCompat.Builder(this, CHANNEL_ID)  
                .setSmallIcon(R.drawable.ic_notification)  
                .setContentTitle("My Foreground Service")  
                .setContentText("This is a foreground service notification.")  
                .setPriority(NotificationCompat.PRIORITY_DEFAULT); // Optional, but recommended for foreground services  
        return builder.build();  
    }  
}
```






## Service 与Activity 通信

通过onBind 方法 activity绑定服务获得服务的binder来实现与之通信







##  不懂就问

### 为什么还需要Service？

我们都知道在主线程可以用Thread开启一个线程去执行一些耗时的操作，这样不会阻塞UI，但是如果当前的Activity销毁了，就没有办法获取Thread的实例，也就不能再去操作那个Thread。这样Thread的生命周期和Activity就绑定在一起了。Service不一样，只要启动了没有销毁，就一直存在后台中，多个Activity能和一个Service进行关联调用。