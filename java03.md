# Task1
1. - byte(单字节)
   - short(短整型)
   - int(整型)
   - long(长整型)
   - float(单精度浮点)
   - double(双精度浮点型)
   - char(字符型)
   - boolean(布尔型)
2. - byte(1字节，表示-128~127)
   - short(2字节，表示-32768~32767)
   - int(4字节，表示-2^31^~2^31^-1)
   - long(8字节，表示-2^63^~2^63^-1)
3. 
```java
   int a=4;
   char c='0';
   int b=a+c;
```
这个过程涉及隐式类型转换
b=52
字符型变量c在加法运算中被转换为整型48
4. 输出结果：
```java
false//使用new创建新对象，而两个对象的储存地址不一致
true//使用valueOf指令，计算机直接调用缓存池内数据，因而地址一样
false//两个对象的大小超出Integer缓存池大小（127），计算机直接创建新对象，两个对象储存地址不一致
```
# Task2
5. 
```java
int a = 5 ;
int b = 7 ;
int c = (++a) + (b++) ;//现加后用a=6 c=6+7=13 先用后加b=8 
System.out.println( c );//13
System.out.println(a+" "+b);//6 8
``` 
6. int在计算机中以补码方式储存
   - 正数补码是其二进制形式
   - 负数补码是其二进制形式取反码再加1

   float在计算机中以IEEE标准储存
   - 将数据转换位二进制科学计数法
   - 第32位：==符号位== 正数0 负数1
   - 第24到31位：==指数位== 指数+127（偏移量）
   - 第1到23位；==尾数位== 舍去默认小数点前的1 用0补全

   两正数相加为负数——整数溢出：
   - 相加结果超出储存范围，导致进位被丢弃
   - 而若补码相加后首位为1，则表现结果为负数
# Task3
1. 将错题数相加记录到map中
```java
import java.util.*;
public class java03 {
   public static void main(String[] args) {
      String input = "math:5,English:10,Chinese:10,math:20,English:10,chemistry:30,math:10,math:20";
      Map<String,Integer> map=new HashMap<>();
      String[] kvs =input.split("," );//用,分割字符串
      for (String kv:kvs) {//将subject：mistakes单独放入for
         String[] s_m = kv.split(":");//用：再次分割
         int mistake=Integer.parseInt(s_m[1]);//mistake装入错题数量
         boolean test =map.containsKey(s_m[0]);//test装入map中是否已有相同科目的判断布尔值
         if (test){//已有相同科目：将错题数量相加
            int m1 =map.get(s_m[0]);
            int m2=m1+mistake;
            map.put(s_m[0],m2);
         }
         else{//map没有相同科目：将错题数录入map
            map.put(s_m[0],mistake);
         }
      }
   }
}
```
2. 比较哪个科目错题最多
```java
Set keyset=new HashSet(map.keySet());//将map的键提出到keyset集合中
Iterator it=keyset.iterator();
List mis_list=new ArrayList<>();//创建列表储存错题数
while (it.hasNext()){
   String key=(String)it.next();
   int mis=(int) map.get(key);
   mis_list.add(mis);//将错题数放入列表mis_list
}
mis_list.sort(Comparator.naturalOrder());//将列表内的数由小到大排序
int max=(int)mis_list.getLast();//去出列表中最大的数放入max变量
Iterator it1=keyset.iterator();
String get_s = null;//get_s用于储存查找到的 错题最多科目 的名称
while (it1.hasNext()){
   String key1=(String) it1.next();
   int mis1=(int) map.get(key1);//mis1再次获得各科目的错题数
   if (mis1==max){//如果错题数与最大错题数相等
      get_s = key1;//将对应科目名称放入get_s中
   }
}
System.out.println("错题最多的科目是："+get_s);
```
3. 多次添加错题
```java
while (true){
   System.out.println("添加科目：");
   String subject = getScanner.next();//获得错题科目
   System.out.println("错题数：");
   Integer num = getScanner.nextInt();//获得错题数
   if (keyset.contains(subject)){//判断是否为已有科目
      int num0 = map.get(subject);
      int num1 = num0 + num;//错题数相加
      map.put(subject,num1);
   }
   else{
      map.put(subject,num);
   }
   System.out.println(map);//再次打印map
}
```
4. 添加同学小红
```java
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

public class java031{
   public static void main(String[] args) {
      Scanner input = new Scanner(System.in);
      Student xiaoming = new Student();//创建小明对象
      Student xiaohong = new Student();//创建小红对象
      xiaoming.name = "xiaoming";
      xiaohong.name = "xiaohong";
      xiaoming.map = new HashMap<>();
      xiaohong.map = new HashMap<>();
      while (true) { 
         System.out.print("姓名：");
         String name = input.next();
         System.out.print("科目：");
         String subject = input.next();
         System.out.print("错题数：");
         int num = input.nextInt();
         if(name.equals(xiaoming.name)){
            xiaoming.mapadd(subject, num);//调用方法
            System.out.println("小明错题"+xiaoming.map);
         }
         if(name.equals(xiaohong.name)){
            xiaohong.mapadd(subject, num);//调用方法
            System.out.println("小红错题"+xiaohong.map);
         }
         else{
            System.out.println("错误名字");//输入的名字不是xiaoming或xiaohong
         }
      }
   }
   public static class Student{//建立Student类
      String name;//属性name
      Map<String,Integer> map;//属性：map
      public void mapadd(String subject,int count){//方法：添加新错题
         if(map.containsKey(subject)){
            int num0 = map.get(subject);
            int num1 = num0 + count;
            map.put(subject, num1);
         }
         else{
            map.put(subject, count);
         }
      }
   }
}
```