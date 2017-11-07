一.Android框架：

android系统架构，采用了分层架构。分为四个层：应用程序层、应用程序框架层、系统运行库层和Linux核心层。

（1）应用程序

（2）隐藏在每个应用后面的一系列服务和系统：包括views，Content Providers，Resource Manager，通知管理器，活动管理器。

（3）程序库和Android运行库：每一个Android应用程序都在它自己的进程中运行，都拥有一个独立的Dalvik虚拟 机实例。

（4）Linux内核：Android的核心系统服务依赖于Linux2.6内核，如安全性，内存管理，进程管理， 网络协议栈和驱动模型。

二.Android四大组件：

1.Activity：

生命周期：onCreate--onStart--onRestart--onResume--onPause--onStop--onDestory

打开应用：onCreate--onStart--onResume

Back按键：onPause--onStop--onDestory

Home按键：退出onPause--onStop，进入onRestart--onStart--onResume

2.Service

```
开启关闭服务：（1）context.startService\(\),context.stopService\(\);

                               生命周期：oncreate\(\)--onStartCommand\(\)--onDestory\(\);

                   服务存在：onStartCommand\(\);

                          （2）context.bindService\(\),context.unbindService\(\);

                   生命周期：onCreate\(\)--onBind\(\)--onUnbind\(\)--onDestory\(\);
```

3.Broadcast

```
发送广播的三种方式：普通广播，有序广播，粘性广播

                   Context.sendBroadcast\(\)，Context.sendOrderedBroadcast\(\)，Context.sendStickyBroadcast\(\)

注册方式：静态注册和动态注册。
```

4.ContentProvider：

```
共享数据

创建的步骤：（1）继承ContentProvider

                         （2）定义一个名为CONTENT\_URI，并且是public static final的Uri类型的类变量， 你必须为其指定一个

                 唯一的字符串值，最好的方案是以类的全名称。

            （3）定义返回给客户端的数据列名，保证唯一性

            （4）创建数据存储系统

            （5）如果要存储字节型的数据，比如位图文件等，保存的实际保存文件的URI。

            （6）声明public static String型的变量，用于指定要从游标处返回的数据列。

            （7）查询返回一个Cursor类型的对象。通过使用ContentResover\(\).notifyChange\(\)方法来通知监听器关于

                                    数据更新的信息

            （8）在AndroidMenifest.xml中使用&lt;provider&gt;标签来设置Content Provider。
```

三.Android常见问题：

1.intent传递的数据类型：Serializable，基本数据类型、Parcelable、Bundle。

2.Anr出现的原因及解决方法：

```
原因：主线程5s内没有响应，broadcastReceiver 10s内没有完成返回。
```

3.五种布局：FrameLayout，RelativeLayout，LinearLayout，AbsoluteLayout，TableLayout。

4.数据存储的方式：

```
                              使用SharedPreferences存储：

                               文件存储：

                               数据库存储：
```

使用ContentProvider存储：

网络存储：

5.横竖屏切换的生命周期：竖屏--横屏：onSaveInstanceState--onPause--onStop--onDestory--onCreate--onStart--

```
                                                                onRestoreInstanceSave--onResume

                                          横屏--竖屏：上面步骤执行两次
```

修改AndroidManifest.xml，把该Activity添加 android:configChanges="orientation"

同上，不过横屏到竖屏只执行一次，不重复了，并最后执行一次onConfigurationChanged

```
            修改AndroidManifest.xml，把该Activity添加 android:configChanges="orientation\|KeyboardHidden"

            竖屏--横屏：onConfigChanged--onConfigurationChanged;

            横屏--竖屏：onConfigurationChanged--onConfigurationChanged
```

6.Handler的消息机制：Looper负责创建一个MessageQuene对象，然后进入一个循环体中无限循环的从MessageQuene中读取消

```
                                     息，而消息的创建者就是Handler或者多个Handler。

                                    andriod提供了 Handler 和 Looper 来满足线程间的通信。Handler 先进先出原则。Looper类用来管理特定线

                                    程内对象之间的消息交换\(Message Exchange\)。

         1\)Looper: 一个线程可以产生一个Looper对象，由它来管理此线程里的Message Queue\(消息队列\)。

         2\)Handler: 你可以构造Handler对象来与Looper沟通，以便push新消息到Message Queue里;或者接收Looper从

                            Message Queue取出\)所送来的消息。

         3\) Message Queue\(消息队列\):用来存放线程放入的消息。

         4\)线程：UI thread 通常就是main thread，而Android启动程序时会替它建立一个Message Queue。
```

7.AsyncTask：常用方法doInBackGround（Params....）,onPostExecute\(Result\),onProgressUpdate\(Params...\),onPreExecute\(\)

```
                      ,onCancelled\(\);
```

8.内存泄露的原因：（1）资源文件未关闭（cursor,file等）；

```
                              （2）构造Adapter时，没有使用缓存的convertView；

                              （3）Bitmap对象在没有使用时调用recycle\(\)释放内存；

                              （4）注册没取消造成的内存泄露
```

（5）集合对象没清理造成的内存泄露

9.java对象的四种引用：

                                       （1）强引用：创建一个对象并把这个对象直接赋给一个变量，

```
                          eg ：Person person = new Person\(“sunny”\); 不管系统资源有么的紧张，

                           强引用的对象都绝对不会被回收，即使他以后不会再用到。

                   （2）软引用：通过SoftReference类实现，

                            eg : SoftReference&lt;Person&gt; p = new SoftReference&lt;Person&gt;\(new Person\(“Rain”\)\);,

                             内存非常紧张的时候会被回收，其他时候不会被回收，所以在使用之前要判断是否为null从而判断他

                             是否已经被回收了。

                  （3）弱引用：通过WeakReference类实现，

                            eg : WeakReference&lt;Person&gt; p = new WeakReference&lt;Person&gt;\(new Person\(“Rain”\)\);

                             不管内存是否足够，系统垃圾回收时必定会回收。

                  （4）虚引用：不能单独使用，主要是用于追踪对象被垃圾回收的状态。

                            通过PhantomReference类和引用队列ReferenceQueue类联合使用实现。
```

10.android垃圾回收机制：回收优先级：Empty process、Background process、Service process、

```
                                          Visible process、Foreground process。
```

11.java垃圾回收机制：。。。。。。

12.android动画：Tween和Frame动画。

13.Android程序运行时权限与文件系统权限的区别：apk程序是运行在虚拟机上的,对应的是Android独特的权限机制，

```
                     只有体现到文件系统上时才使用linux的权限设置。
```

android系统有的权限是基于签名的。

14.Android的IPC机制:IPC是内部进程通信的简称， 是共享”命名管道”的资源。Android中的IPC机制是为了让Activity和

```
                                  Service之间可以随时的进行交互，
```

故在Android中该机制，只适用于Activity和Service之间的通信，

```
                                 类似于远程方法调用，类似于C/S模式的访问。通过定义AIDL接口文件来定义IPC接口。Servier端

                                 实现IPC接口，Client端调用IPC接口本地代理。
```

15.java面向对象的方法：分装，继承，多态。

16.堆和栈的区别：在函数中定义的一些基本类型的变量和对象的引用变量都是在函数的栈内存中分配。

```
              堆内存用于存放由new创建的对象和数组。
```

从堆和栈的功能和作用来通俗的比较,堆主要用来存放对象的，

```
              栈主要是用来执行程序的.
```

17.进程和线程的区别：进程之间不能共享内存，单线程之间共享内存非常的容易。

18.多线程：

19.Android程序目录结构：assets：诸如MP3、视频类文件。

20.Android刷新界面的两种方法：Invalidate--只能在UI中操作。postInvalidate--线程中刷新界面。

21.switch中支持的数据类型：byte，char，int，short，枚举（1.7后支持String）；

22.枚举：带有相同类型的一组数据，比如--一周星期，一年四季，一年十二个月等等。

23.java的基本类型：int，byte，char，float，double，boolean，long，short。

24.栈：一个先进后出的数据结构，通常保存方法中的参数，局部变量。

```
堆：一个可动态申请的内存空间,NEW的对象。
```

25.数据库的优化：使用索引，使用事务，异步线程，其他（StringBuffer代替String，直接用static标记index）。

26.aidl对应的接口名称必须与aidl文件名相同不然无法自动编译，aidl对应的接口的方法不能加访问权限修饰符。

27.RemoteView会用在两个地方：一个是在AppWidget,另外一个是在Notification.

28.进程的优先级：前台进程，可见进程，服务进程，后台进程和空进程。

29.sharepreference:四种操作模式MODE\_PRIVATE/MODE\_WORLD\_READABLE/MODE\_WORLAD\_WRITEABLE/MODE\_APPEND;

30.android解析方式：pull、sax、dom解析。

31.屏幕适配：1px=1像素，dip是根据160dpi来计算的，dip和dp是密度无关像素，sp与dp相似，可以根据文字大小进行缩放。

```
五中主流的像素密度：M、H、XH、XXH、XXXH。安装2：3:4:6:8的比例设置图片
```

32.layout\_weight：如果设置了该属性，并且有效，那么该view的宽度就等于当前设置的宽度加上剩于空间的占比，一般设置为（wrap\_content或者0）。

33.重载和重写：

```
重载：一个类中有多个方法，方法相同，参数不同，返回值可定义。

重写：子类的修饰符权限不能小于父类的，参数相同，方法相同，返回值相同，需重写父类方法。
```

34.mvp、mvc、mvvm模式的区别：

```
mvc：通过controller去控制mode操作数据，model直接返回结果给View显示。View指的是一些布局文件，model指的是java bean

以及一些数据操作，Controller指的就是Activity了。

mvp：model、view、present，直接通过present去相互之间操作，而present可以通过接口和view交互，减少耦合。

mvvm:view、viewmodel、model。通过data binding框架绑定数据。
```



