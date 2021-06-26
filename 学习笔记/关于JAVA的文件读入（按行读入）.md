## 关于JAVA的文件读入（按行读入）

作者：wwhhyy

#### 前情提要

上次发了一篇做国外某学校数据结构考试试题的文章，发现文章的阅读量非常的低。竟然只有两个阅读量，而且最让人伤心的是这两个阅读量还都是我自己。所以我这次还是老老实实发点正常的文章吧。今天我们的主题是java文件的读入，今天我主要演示的是java中怎么去一行一行的进行文件的读入，主要是使用了BufferedReader这个类进行文件的读入，它提供的readline方法能够帮助我们进行按行读入的操作。

#### 这个类的介绍

```java
BufferedReader br=new BufferedReader(new FileReader(new File("Studata.txt")));
```

基本上这个就是我们使用这个类的一个比较普遍的情形，java的流处理基本上都是这种层层的嵌套式的初始化。其实这也是一个设计模式的体现，但是我有点不记得是啥了。然后我们具体来看这个流，我们其实就是打开了一个输入流，然后我们打开的文件是当前目录下的Studata.txt，然后我们使用这个流进行读入。我们看一下读入的基本的语句。

```java
String line=null; //读入的每行
while((line=br.readLine())!=null){  //如果不是什么都没有就进行处理
    String[] elements=line.split(" ");  //使用split函数对于读到的文本进行处理
    Student student=new Student(elements[0],elements[1],elements[2],elements[3],elements[4],null,0,0);//构造学生，添加学生信息
    students.add(student);//添加学生信息
}
br.close();//关闭读入流
```

这个函数其实你把while中间的部分拿掉才是模板，但是我还是放在那了，毕竟我们后面还要使用我们的这一块函数。可以看到我们的读入就是看我们能否读到String字符串，如果读到就继续读入，然后处理我们读入的函数，如果不行那么久直接中断我们的读入过程，并且在这样的一个过程中，我们要注意流的关闭。

#### 一个小例子

![image-20210616234440510](C:\Users\why19991031\Desktop\写作中间站\image-20210616234440510.png)

这个是我们的一个Java实验的题目，我们就来看一下怎么去写这么一个Java程序，下面我们首先来看一下我们的几个准备的文件：Studata.txt、Recorddata.txt、StuCard.txt

#### Studata.txt

```java
20188374858604 宋和科 2018 电器工程 13327924254
20188369853124 吴航宇 2018 软件工程 13913604811
20188147012541 宋璋逸 2018 西语 13573404781
20187412541701 李华洋 2018 数学师范 13914758472
20181452687424 王霸 2018 法学 18841258741
20191047521499 李逍遥 2019 新能源 13914872145
```

#### Recorddata.txt

```java
0000000001 2 30.72 A
0000000001 1 130 B
0000000001 2 13.38 C
0000000002 1 100 D
0000000002 2 11 A
0000000002 2 12.9 B
0000000003 2 17.6 D
0000000003 1 66 A
0000000003 1 30 B
0000000003 1 80 A
0000000003 2 14.3 A
0000000004 1 23 A
0000000004 2 9.99 B
0000000004 1 56 C
0000000005 1 56 C
0000000005 2 6.6 B
0000000005 2 3.2 A
0000000006 1 300 B
0000000006 2 31.2 A
0000000006 2 12.6 C
0000000006 2 1.24 D
```

#### StuCard.txt

```java
20188374858604 0000000001
20188369853124 0000000002
20188147012541 0000000003
20187412541701 0000000004
20181452687424 0000000005
20191047521499 0000000006
```

然后我们看一看我们写的几个类，我的注释还是比较全的，基本上应该可以看懂

#### Record

```java
public class Record {
    String cardId;  //卡的号码
    String kind;   //消费的种类，主要就是1是存钱 2是花钱
    double money;  //行为的钱的数量
    String location;  //消费的地点，也就是ABCD之一
    public Record(String cardId,String kind,Double money,String location){ //一个简单的构造方法
        this.cardId=cardId;
        this.kind=kind;
        this.money=money;
        this.location=location;
    }
}
```

#### Student

```java
public class Student {
    public String id;  //学生的学号
    public String name;  //学生的姓名
    public String year;   //学生的入学年份
    public String major;  //学生的专业
    public String phoneNumber;  //学生的电话号码
    public String cardId;   //学生的学生卡的号码
    public double money;  //学生卡有的钱
    public double spendedMoney;  //学生卡消费掉的钱
    public Student(String id,String name,String year,String major,String phoneNumber,String cardId,double money,double spendedMoney){  //简单的构造函数
        this.id=id;
        this.name=name;
        this.year=year;
        this.major=major;
        this.phoneNumber=phoneNumber;
        this.cardId=cardId;
        this.money=money;
        this.spendedMoney=spendedMoney;
    }
}
```

#### Main

```java
import java.io.*;
import java.util.ArrayList;
import java.util.Comparator;
import java.util.HashMap;

public class Main {
    public static void main(String[] args) throws IOException {
        ArrayList<Student> students=new ArrayList<>();//这个是存放我们读取的学生信息的数据结构
        ArrayList<Record> records=new ArrayList<>();  //这个是存放我们读取记录的数据结构
        readStudentMessages(students);       //第一个方法，我们去读取学生的信息
        readRecords(records);              //第二个方法，我们去读取记录信息
        countAllTheRecords(students,records);  //第三个方法，我们去计算所有的消费记录，也就是去算余额和消费的金额
        sortStudentCards(students);     //第四个方法，对于学生的位置进行排序，按照消费金额的多少升序排序
        printStudentData(students);          //第五个方法，打印我们的学生信息，顺序就是前面第四个方法所拍好的顺序
        printTheRichestPeople(students,records);    //先找出存款最多的学生，然后去打印他的一些信息
    }

    /**
     * 这个方法是用来读取学生信息的
     * @param students
     * @throws IOException
     */
    public static void readStudentMessages(ArrayList<Student> students) throws IOException {
        BufferedReader br=new BufferedReader(new FileReader(new File("Studata.txt")));//打开一个输入流，然后准备读入数据
        String line=null; //读入的每行
        while((line=br.readLine())!=null){  //如果不是什么都没有就进行处理
            String[] elements=line.split(" ");  //使用split函数对于读到的文本进行处理
            Student student=new Student(elements[0],elements[1],elements[2],elements[3],elements[4],null,0,0);//构造学生，添加学生信息
            students.add(student);//添加学生信息
        }
        br.close();//关闭读入流
        line=null;  //继续我们下一个信息的读入
        br=new BufferedReader(new FileReader(new File("StuCard.txt"))); //这一次是学生和学生卡的对应的数据的读入
        HashMap<String,String> map=new HashMap<>(); //还是和之前一样的处理方式
        while((line=br.readLine())!=null){
            String[] elements=line.split(" ");  //分裂我们的文本
            map.put(elements[0],elements[1]);   //然后放入哈希表
        }
        br.close();   //关闭读入数据流
        for(Student student:students){
            student.cardId=map.get(student.id); //把我们的学生中的学生卡id的字段给补上去
        }
    }

    /**
     * 这个方法是用来读取消费记录的
     * @param records
     * @throws IOException
     */
    public static void readRecords(ArrayList<Record> records) throws IOException {
        BufferedReader br=new BufferedReader(new FileReader(new File("Recorddata.txt"))); //打开数据读入流
        String line=null;   //读入的数据的存放的地方
        while((line=br.readLine())!=null){    //只要不是空就继续读入
            String[] elements=line.split(" ");    //把这一行按照空格分开
            Record record=new Record(elements[0],elements[1],Double.parseDouble(elements[2]),elements[3]); //创建记录 然后加入数组
            records.add(record);
        }
        br.close();//关闭数据读入流
    }

    /**
     * 这个方法是用来加减余额和计算消费总支出的，思路就是两次遍历
     * @param students
     * @param records
     */
    public static void countAllTheRecords(ArrayList<Student> students,ArrayList<Record> records){
        for(Record record:records){//先遍历我们的消息记录
            String cid=record.cardId;  //取出我们消息记录对应的卡
            for (Student student:students){  //然后去寻找消息记录卡id对应的学生
                if(student.cardId.equals(cid)){
                    if (record.kind.equals("1")){  //判断它的性质是存钱还是消费
                        student.money+=record.money;  //进行计算
                    }else{
                        student.money-=record.money;
                        student.spendedMoney+=record.money;
                    }
                }
            }
        }
    }

    /**
     * 这个函数的作用是进行排序，我们重写了一个排序的类，然后排序的结果是根据消费总额进行升序排序
     * @param students
     */
    public static void sortStudentCards(ArrayList<Student> students){
        students.sort(new Comparator<Student>() {
            @Override
            public int compare(Student o1, Student o2) {
                if(o1.spendedMoney-o2.spendedMoney<0)
                    return -1;
                else if(o1.spendedMoney-o2.spendedMoney>0)
                    return 1;
                else
                    return 0;
            }
        });
    }

    /**
     * 这个函数就是用来打印我们之前排序好的学生集合
     * @param students
     */
    public static void printStudentData(ArrayList<Student> students){
        for (Student student:students) {
            System.out.println("******************************************");
            System.out.println("学号："+student.id);
            System.out.println("姓名："+student.name);
            System.out.println("入学年份："+student.year);
            System.out.println("专业："+ student.major);
            System.out.println("联系方式："+student.phoneNumber);
            System.out.println("卡号："+student.cardId);
            System.out.println("余额："+student.money);
            System.out.println("该卡共消费："+student.spendedMoney);
        }
    }

    /**
     * 这个也是打印学生信息，只不过是打印某一个存款最多的学生的信息，然后使用文件输出流的方式进行打印
     * @param students
     * @param records
     * @throws IOException
     */
    public static void printTheRichestPeople(ArrayList<Student> students,ArrayList<Record> records) throws IOException {
        Student student=null;  //存放存款最多的学生
        double mostMoney=Double.MIN_VALUE;  //存款最多的学生的存款
        for(Student student1:students){   //寻找的过程
            if(student1.money>mostMoney){
                student=student1;
                mostMoney=student1.money;
            }
        }
        BufferedWriter bw=new BufferedWriter(new FileWriter(new File("SaveMax.txt"))); //打开输出流
        bw.write("*************************\n");
        bw.write("学号："+student.id+"\n");
        bw.write("姓名："+student.name+"\n");
        bw.write("入学年份："+student.year+"\n");
        bw.write("专业："+student.major+"\n");
        bw.write("联系方式："+student.phoneNumber+"\n");
        bw.write("卡号："+student.cardId+"\n");
        bw.write("余额："+String.valueOf(student.money)+"\n");
        bw.write("该卡的详细消费状况\n");
        for(Record record:records){                 //用遍历的方式来找寻出该位同学的消费记录
            if (student.cardId.equals(record.cardId)){
                if (record.kind.equals("1")){
                    bw.write("存钱 金额"+String.valueOf(record.money)+"消费地点："+record.location+"\n");
                }else{
                    bw.write("消费 金额"+String.valueOf(record.money)+"消费地点："+record.location+"\n");
                }
            }
        }
        bw.write("该卡共消费："+student.spendedMoney+"\n");
        bw.close();  //关闭输出流，不关闭不会进行打印操作的
    }
}
```

然后运行Main这个类之后我们得到如下的结果

![image-20210616235459165](C:\Users\why19991031\Desktop\写作中间站\image-20210616235459165.png)

最后我们的文件如下：

#### SaveMax.txt

```java
*************************
学号：20191047521499
姓名：李逍遥
入学年份：2019
专业：新能源
联系方式：13914872145
卡号：0000000006
余额：254.95999999999998
该卡的详细消费状况
存钱 金额300.0消费地点：B
消费 金额31.2消费地点：A
消费 金额12.6消费地点：C
消费 金额1.24消费地点：D
该卡共消费：45.04
```

#### 总结

本文主要介绍了java的一个输入流，然后我们通过一个小案例去介绍了怎么去实际运用这样的一个输入流，希望大家能够一起变得更强，你的观看就是对笔者最好的支持！