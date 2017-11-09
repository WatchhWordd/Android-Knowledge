Fragment生命周期:

setUserVisibleHint()：设置Fragment可见或者不可见

getUserVisibleHint()：获取fragment可见或者不可见

onAttach(Context context)：和Activity的绑定，context是Activity对象

onCreate()：创建Fragment，操作传递数据

onCreateView():初始化Fragment布局，不能做耗时操作。

onActivityCreated()：执行该方法时，与Fragment绑定的Activity的onCreate方法已经执行完成并返回，
                     在该方法内可以进行与Activity交互的UI操作，所以在该方法之前Activity
					 的onCreate方法并未执行完成，如果提前进行交互操作，会引发空指针异常。
					 
onStart()：Fragment由不可见变为可见状态。

onResume()：Fragment处于可见状态。

onPause()：Fragment处于暂停状态，不能操作

onSaveInstanceState()：保存当前Fragment的状态。该方法会自动保存Fragment的状态，
                       比如EditText键入的文本，即使Fragment被回收又重新创建，
					   一样能恢复EditText之前键入的文本。
					   
onStop()：Fragment不可见

onDestoryView():销毁Fragment视图

onDestory():销毁Fragment（按返回键）

onDetach():解绑Activity