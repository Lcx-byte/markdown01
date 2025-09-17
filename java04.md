# Task1
```java
//这个函数用于判断传入的年份是否为闰年
//是闰年返回1，不是闰年返回2
boolean isLeapYear(int year){
    if (year % 4 == 0){
        System.out.println(1);
        return true;
    }
    else{
        System.out.println(2);        
        return false;
    }
}
```
`switch-case`确实在`if-else`的基础上更加简便，但并不是其语法糖（`syntax sugar`）
底层实现原理：
- `switch-case`若在case值较集中时创造跳转表，直接跳转到相应地址；若case值较稀疏时利用二分法查找地址
- `if-else`只能按照程序逻辑一步一步往下走，运行速度较慢

# Task2
```java
void print(int n){
    int half = n / 2;
    int i = 1;
    while(i <= n){
        if(i == n || i == 1){//打印第一行和最后一行
            for(int t = half;t > 0;t--){
                System.out.print(" ");
            }
            System.out.println("*");
        }
        else if(i<=half+1){//前2/n行
            for(int t = half-i+1;t > 0;t--){
                System.out.print(" ");
            }
            System.out.print("*");
            for(int t = 2*i-3;t > 0;t--){
                System.out.print(" ");
            }
            System.out.println("*");
        }
        else{//后2/n行
            for(int t = Math.abs(half-i+1);t > 0;t--){
                System.out.print(" ");
            }
            System.out.print("*");
            for(int t = 2*(n-i)-1;t > 0;t--){
                System.out.print(" ");
            }
            System.out.println("*");
        }
        i++;    
    }
}
```
# Task3
```java
int Fibonacci(int n){//递归方式实现
    if (n == 1 || n == 2){
        return 1;
    }
    return Fibonacci(n-1)+Fibonacci(n-2);
}
```
```java
int Fibonacci(int n){//迭代方式实现
    int a = 1;
    int b = 1;
    for(int i = 1;i <= n-2;i++){
        int m =a + b;
        b = a;
        a = m;
    }
    return a;
}
```
- 递归方式在不断调用函数，可能会导致栈溢出
- 理论上循环能实现的功能，递归都能实现

# Task4
```java
void hanoi(int n,String a,String b,String c){//函数定义：有n个圆盘，要从1号String位置（起点） 移动到3号String位置（终点） 以2号String位置为中转站
    if (n == 1){
        System.out.println(a+"->"+c);//若只有一个盘或者最后一个盘，只需将其从起点移至终点（从1号String移至3号String）
    }
    else{
        hanoi(n-1,a,c,b);//将原任务分解为 1.上面n-1个盘 移至 原中转站（以 原终点 为 中转站）
        System.out.println(a+"->"+c);//2.最下面一个盘 移至终点（可以直接操作）
        hanoi(n-1,b,a,c);//3.将原中转站中的n-1个圆盘 移至终点（以 原起点 为 中转站）
    }
}
```