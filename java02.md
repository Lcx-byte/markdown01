# Task1
## 第一题
1. 包声明：定义包
2. 导入工具
3. 主类：程序主要部分
4. 辅助类：辅助主类

- 包（就像文件夹） 将相关文件放在一起，起到组织作用
- main函数是程序开始的地方

```java
package com.Example;
import com.Example.tool.Print;
public class HelloWorld {
        public static void main(String[] args){
            for (String arg : args){
                System.out.println(arg);
                //添加for循环指令逐个打印参数
            }
            Test.test();
        }
}
class Test{
    public static void test(){
        Print.print("Hello World");
    }
}
```
- 输入指令时输入`java HelloWorld 111 222 333`
## 第二题
```java
package com.Example.tool;
public class Print{
    public static void print(String word){//设置变量装入“Hello World”
        System.out.println(word);
    }
}
```