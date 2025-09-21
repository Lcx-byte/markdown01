# Task1
java不支持多继承的原因
1. 钻石继承问题（两个父类若拥有相同成员方法时 不知道继承哪一个）
2. 若要实现多继承需要额外引入新机制（使开发者操作更复杂）
3. 需要多继承的操作往往可以被多接口实现

# Task2
1. 重写方法
```java
public void main(String[] args) {
    Circle c1 = new Circle(1);
    System.out.println(c1.C_calculate()+"  "+c1.S_calculate());//其余打印方法同
}
public class Formula{
    public float S_calculate(){
        return 0;//计算面积公式
    }
    public float C_calculate(){
        return 0;//计算周长公式
    }
}
public class Circle extends Formula{//创建Circle为Formula的子类
    private int r;
    public Circle(int r){
        this.r = r;
    }
    @Override
    public float S_calculate(){//重写面积计算公式
        return (float)(3.14*r*r);
    }
    @Override
    public float C_calculate(){//重写周长计算公式
        return (float)(3.14*2*r);
    }
}
public class Triangle extends Formula{
    private int a;
    private int b;
    private int c;
    private float p;//三角形半周长
    public Triangle(int a,int b){
        this.a = a;
        this.b = b;
        this.c = c;
        this.p =(float) 0.5*(a+b+c);
    }
    @Override
    public float  S_calculate(){
        double ds = (p*(p-a)*(p-b)*(p-c));
        return (float) Math.sqrt(ds);//开方
    }
    @Override
    public float C_calculate(){
        return (float)(a+b+c);
    }
}
public class Rectangle extends Formula{
    private int a;
    private int b;
    public Rectangle(int a,int b){
        this.a = a;
        this.b = b;
    }
    @Override
    public float S_calculate(){
        return (float)(a*b);
    }
    @Override
    public float C_calculate(){
        return (float)((a+b)*2);
    }
}
```
2. 接口方法
```java
public void main(String[] args) {
    Circle c1 = new Circle(1);
    System.out.println(c1.C_calculate()+"  "+c1.S_calculate());
}
interface Formula{
    float S_calculate();
    float C_calculate();
}
class Circle implements Formula{
    private int r;
    public Circle(int r){
        this.r = r;
    }
    @Override
    public float S_calculate(){
        return (float)(3.14*r*r);
    }
    @Override
    public float C_calculate(){
        return (float)(3.14*2*r);
    }
}
class Triangle implements Formula{
    private int a;
    private int b;
    private int c;
    private float  p;
    public Triangle(int a,int b){
        this.a = a;
        this.b = b;
        this.c = c;
        this.p =(float) 0.5*(a+b+c);
    }
    @Override
    public float  S_calculate(){
        double ds = (p*(p-a)*(p-b)*(p-c));
        return (float) Math.sqrt(ds);
    }
    @Override
    public float C_calculate(){
        return (float)(a+b+c);
    }
}
class Rectangle implements Formula{
    private int a;
    private int b;
    public Rectangle(int a,int b){
        this.a = a;
        this.b = b;
    }
    @Override
    public float S_calculate(){
        return (float)(a*b);
    }
    @Override
    public float C_calculate(){
        return (float)((a+b)*2);
    }
}    
```
# Task3
```java
public class BankAccount {
    // TODO 修改属性的可见性
    private String accountNumber;
    private String accountHolder;
    private double balance;
    private String password; // 敏感信息，需要严格保护
    
    public BankAccount(String accountNumber, String accountHolder, double initialBalance, String password) {
        //TODO 创建实例化方法
        this.accountNumber = accountNumber;
        this.accountHolder = accountHolder;
        this.balance = initialBalance;
        this.password = password;
    }
    
    public void deposit(double amount) {
        //TODO 存款
        if (amount >= 0){
            balance += amount;
            System.out.println("存款成功，余额："+ balance);
        }
        else{
            System.out.println("存款失败");
        }
    }
    
    public boolean withdraw(double amount, String inputPassword) {
        //TODO 取钱
        if(validatePassword(inputPassword)){
            if (validateAmount(amount)){
                balance -= amount;
                System.out.println("取款成功，余额：" + balance);
            }
            else{
                System.out.println("取款失败，余额不足");
            }
        }
        else {
            System.out.println("密码错误");
        }
        return true;
    }
    
    public boolean transfer(BankAccount recipient, double amount, String inputPassword) {
        //TODO 转账
        if(validatePassword(inputPassword)){
            if (validateAmount(amount)){
                balance -= amount;
                System.out.println("转出"+amount+"给账户"+recipient);
                recipient.deposit(amount);
                System.out.println("余额："+balance);
            }
            else{
                System.out.println("转账失败，余额不足");
            }
        }
        else {
            System.out.println("密码错误");
        }
        return true;
    }
    
    public double getBalance() {
        //TODO 看存款
        return balance;
    }
    
    public String getAccountInfo() {
        //TODO 看账户信息
        return "accountnumber： "+ accountNumber +"accountholder: "+ accountHolder +"balance: "+balance;
    }
    // 只需修改可见性
    private boolean validatePassword(String inputPassword) {
        if(inputPassword == password){
        return true; 
        }
        else{
            return false;
        }
    }
    // 只需修改可见性
    private boolean validateAmount(double amount) {
        if (amount <= balance && amount > 0){
            return true;
        }
        else{
            return false;
        }
    }
}
```