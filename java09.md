# Task1
- Q1
```java
public static void main(String[] args) throws FileNotFoundException, IOException {
    FileInputStream fis = new FileInputStream("C:\\java_learning\\doro.jpg");//创建input字节流实现对象
    FileOutputStream fos = new FileOutputStream("C:\\java_learning\\doro_copy.jpg");//创建output字节流实现对象

    int len;//len记录字节数组长度
    byte[] bytes = new byte[1024];//创建长度为1024的字节数组
    while ((len = fis.read(bytes)) != -1 ){
        fos.write(bytes, 0, len);//将字节数组中的内容写入copy中
    }
    fos.close();
    fis.close();
}
```

# Task2
- Q2
```java
public static void main(String[] args) throws FileNotFoundException, IOException {
    File source = new File("C:\\java_learning\\name.txt");
    BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(new FileInputStream(source), StandardCharsets.UTF_8));//创建字符缓冲流，用转换流将字节流转换为字符流
    
    String line1;//line1储存文件每一行的数据
    ArrayList<String> list = new ArrayList<>();
    while ( (line1 = bufferedReader.readLine()) != null ){
        String line2 = line1.trim();//去除每一行中的空格
        list.add(line2);//将去除空格的数据分别放入list中
    }
    bufferedReader.close();
    list.removeIf(filter -> filter.isEmpty());//list去除空元素（空行）
    BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter("C:\\java_learning\\name_sorted.txt"));
    for (String name : list){//将list中的元素分别写进C:\\java_learning\\name_sorted.txt
        bufferedWriter.write(name);
        bufferedWriter.newLine();//使用newline()换行避免不同系统换行符的差异
    }
    bufferedWriter.close();
}
```
# Task3
- Q3
```java
public static void main(String[] args) throws IOException, ClassNotFoundException {
    Student student = new Student(1, "doro", 2, "114514");
    ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("C:\\java_learning\\student.dat"));
    oos.writeObject(student);//将student对象写入C:\\java_learning\\student.dat
    oos.close();

    ObjectInputStream ois = new ObjectInputStream(new FileInputStream("C:\\java_learning\\student.dat"));
    Student doro = (Student) ois.readObject();//将C:\\java_learning\\student.dat中的student取出，传递给doro
    System.out.println(doro.toString());//打印doro
    ois.close();
}


public static class Student implements Serializable {//Serializable没有抽象方法，能使Student类可以被序列化

    private Integer id;
    private String name;
    private Integer gender; //1表示男性 2表示女性
    private String phone;

    public Student(Integer id, String name, Integer gender, String phone) {
        this.id = id;
        this.name = name;
        this.gender = gender;
        this.phone = phone;
    }

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Integer getGender() {
        return gender;
    }

    public void setGender(Integer gender) {
        this.gender = gender;
    }

    public String getPhone() {
        return phone;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }

    @Override
    public String toString() {
        return "Student{" +
                "id=" + id +
                ", name='" + name + '\'' +
                ", gender=" + gender +
                ", phone='" + phone + '\'' +
                '}';
    }
}
```