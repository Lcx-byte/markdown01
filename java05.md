# Task1
```java
public class java05 {
    public void main(String[] args) {
        Person original = new Person("a",1,2);//创建初始对象
        Person copy = new Person(original);//创建复制对象
    }
    public class Person{
        private String name;
        private int age;
        private int sex;

        private void eat() {
            System.out.println(name+"正在吃东西");
        }
        private void sleep() {
        }  
        private void dadoudou() {
        }
        public Person(String name,int age,int sex){
            this.name = name;
            this.age = age;
            this.sex = sex;
        }
        public Person(Person other){
            this.name = other.name;
            this.age = other.age;
            this.sex = other.sex;
        }
    } 
}
```
1. `this`关键字指当前对象的相关属性，防止混淆
2. 类是创建对象的蓝图，对象是类的实例化
3. 访问修饰符
   - private 仅当前类可以使用
   - default 当前类，同package可以使用
   - protect 当前类，同package，子类可以使用
   - public 完全公开，其它package也可以访问