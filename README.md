```
Android知识点
```

---

一.Android框架：

android系统架构，采用了分层架构。分为四个层：应用程序层、应用程序框架层、系统运行库层和Linux核心层。

（1）应用程序

（2）隐藏在每个应用后面的一系列服务和系统：包括views，Content Providers，Resource Manager，通知管理器，活动管理器。

（3）程序库和Android运行库：每一个Android应用程序都在它自己的进程中运行，都拥有一个独立的Dalvik虚拟 机实例。

（4）Linux内核：Android的核心系统服务依赖于Linux2.6内核，如安全性，内存管理，进程管理， 网络协议栈和驱动模型。

二.Android四大组件

1.Activity：

生命周期：onCreate--onStart--onRestart--onResume--onPause--onStop--onDestory

打开应用：onCreate--onStart--onResume

Back按键：onPause--onStop--onDestory

Home按键：退出onPause--onStop，进入onRestart--onStart--onResume

2.Service:

1）context.startService\(\),context.stopService\(\);

生命周期：onCreate\(\)--onStartCommand\(\)--onDestory\(\);

服务存在：onStartCommand\(\);

2）context.bindService\(\),context.unbindService\(\);

生命周期：onCreate\(\)--onBind\(\)--onUnbind\(\)--onDestory\(\);

3.Broadcast

发送广播的三种方式：普通广播，有序广播，粘性广播



Context.sendBroadcast\(\)，Context.sendOrderedBroadcast\(\)，Context.sendStickyBroadcast\(\)

注册方式：静态注册和动态注册。



