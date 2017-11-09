Top1. 数组转换为数组列表
原：List<string> list=Arrays.asList(arr);
改定：ArrayList<String> arrayList = new ArrayList<String>(Arrays.asList(arr));

Top2. 检查一个数组包含一个值
原：Set<String> set = new HashSet<String>(Arrays.asList(arr));  
    return set.contains(targetValue);
改定：Arrays.asList(arr).contains(targetValue);  

   或for(String s: arr){  
    if(s.equals(targetValue))  
        return true;  
   }  
   return false;  
   
Top3.抽象类和抽象方法
(1)抽象类就是把相同但不确定方法提取出来在子类中实现
(2)用abstract修饰的类，即抽象类；用abstract修饰的方法，即抽象方法
(3)抽象类不能被实例化，未确定的类，没有必要实例化
(4)抽象类中没有必要一定包括abstract方法，可以实现非抽象方法
(5)类中如果包括抽象方法，必须是抽象类
(6)只能继承一个抽象方法
Top4.接口
作用：特殊的抽象
(1)接口中可以含有变量和方法，只能存在public abstract方法
(2)接口成员变量只能是public static final类型
(3)接口中不能含有静态模块
(4)一个类可以实现多个接口
(5)不能够实例化接口