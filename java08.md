# Task1
- Q1
  - Error往往是虚拟机或者系统的异常，没办法被捕获或者抛出
  - Exception指的是编译过程或者执行过程中出现的异常，可以被捕获和抛出
- Q2
  - unchecked异常 是在编写程序过程中出现编码错误而产生的，不要求强制处理
  - check异常 常常是外部资源问题（文件不存在等），应该进行抛出和捕获

# Task2
- Q3
```java
public class EmptyFileException extends Exception{
//创建“文件是空文件”异常
    public EmptyFileException(String message){
        super(message);
    }
}

public void main(String[] args) throws IOException {
    BufferedReader bf = null;//创建BufferedReader对象
    try {
        bf = new BufferedReader(new FileReader("data.txt"));//尝试调取文件
        System.out.println(calculate_average(bf));//调用 计算平均值 函数
    } catch (FileNotFoundException e) {//文件不存在时报出异常
        e.printStackTrace();
        System.out.println("文件找不到");
    }catch (Exception e) {//异常总类（包含数字格式错误、空文件错误以及其它未知错误）
        e.printStackTrace();
    }finally{
        bf.close();//最后finally关闭文件
    }  
}

public double calculate_average(BufferedReader bf) throws IOException, EmptyFileException{//定义函数：计算平均值
    double result = 0.0;//初始化双精度浮点型变量：result记录平均数结果
    String line;//line记录data.txt文件中每行的数据
    int sum = 0;//sum记录数字的总和
    int count = 0;//count记录数字的个数
    while ((line = bf.readLine()) != null){//每行读数
        line = line.trim();//除去每行的标识符等

        if (line.isEmpty()){//跳过空行
            continue;
        }
        try {
            int num = Integer.parseInt(line);//尝试将数据转换成整数型
            sum += num;//sum加上本行的数字
            
        } catch (NumberFormatException e) {//若数据无法转换成整数，捕获异常
            e.printStackTrace();
            System.out.println("数字格式不正确");
            sum = 0;//重置加和
            break;//跳出数据读取
        }
        count++;//数字数量+1
        
    }

    if (count == 0){//若数字数量为0，抛出异常“文件是空文件”
        throw new EmptyFileException("文件是空文件");
    }

    result = (double)sum / count;//求出平均值

    return result;
}
```
# Task4
- Q4
- 执行结果`limit = java.util.stream.SliceOps$1@7a81197d`
- 原因`limit`是中间方法，所以limit的形式是Stream流，而并不是Stream流中的数据
- Q5
```java
public class Student {
  String name;
  int score;

  public Student(String name, int score) {
    this.name = name;
    this.score = score;
  }

  public String getName() {
    return name;
  }

  public int getScore() {
    return score;
  }

  public void setName(String name) {
    this.name = name;
  }

  public void setScore(int score) {
    this.score = score;
  }
}
public void main(String[] args) {
  // 测试数据：学生列表
  List<Student> students = Arrays.asList(
    new Student("Alice", 85),
    new Student("Bob", 58),
    new Student("Charlie", 90),
    new Student("David", 45),
    new Student("Eve", 72),
    new Student("Frank", 60),
    new Student("Grace", 55),
    new Student("Heidi", 95)
  );
  // 请在这里补充代码，完成以下任务：
  // 1. 过滤分数≥60的学生
  // 2. 姓名转换成大写
  // 3. 按姓名字母顺序排序
  // 4. 收集成 List<String> 返回并打印
  // --- 你的代码开始 ---
  List<String> passingStudents = students.stream()
    .filter(student -> student.getScore() >= 60)
    .map(name -> name.getName())
    .map(name -> name.toUpperCase())
    .sorted()
    .collect(Collectors.toList());
  // TODO: 补充流操作链
  // --- 你的代码结束 ---
  // 打印结果
  System.out.println(passingStudents);
}
```