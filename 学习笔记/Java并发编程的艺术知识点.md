# Java并发编程的艺术知识点

## 第四章 Java并发编程基础

- 一个Java程序的运行不仅仅是main方法的运行，而是main线程和多个其他线程的同时运行

#### 为什么要使用多线程

- 更多的处理器核心
- 更快的响应时间
- 更好的编程模型

#### 线程优先级

- Java中使用一个整型成员变量来控制线程的优先级，这个变量的范围是从1到10，下面我们来通过一个例子来观察这个优先级变量的作用

```java
public class Priority {
    private static volatile boolean notStart=true;
    private static volatile boolean notEnd=true;

    public static void main(String[] args) throws Exception{
        List<Job> jobs=new ArrayList<>();
        for (int i=0;i<10;i++){
            int priority=i<5 ? Thread.MIN_PRIORITY : Thread.MAX_PRIORITY;
            Job job=new Job(priority);
            jobs.add(job);
            Thread thread=new Thread(job,"Thread:"+i);
            thread.setPriority(priority);
            thread.start();
        }
        notStart=false;
        TimeUnit.SECONDS.sleep(10);
        notEnd=false;
        for (Job job:jobs){
            System.out.println("Job Priority:"+job.priority+", Count:"+job.jobCount);
        }
    }

    static class Job implements Runnable{
        private int priority;
        private long jobCount;
        public Job(int priority){
            this.priority=priority;
        }
        public void run(){
            while (notStart){
                Thread.yield();
            }
            while(notEnd){
                Thread.yield();
                jobCount++;
            }
        }
    }
}
```

结果如下

![image-20210126103403889](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210126103403889.png)

我们可以看到与书上描述的不同，我们在win10上跑的结果还是符合我们预期的。

#### 线程的状态

Java线程在运行的生命周期中可能处于6中不同的状态

| 状态名称     | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| NEW          | 初始状态，线程被构建，但是还没有调用start（）方法            |
| RUNNABLE     | 运行状态，Java线程将操作系统中的就绪和运行两种状态笼统地称作“运行中” |
| BLOCKED      | 阻塞状态，表示线程阻塞于锁                                   |
| WAITING      | 等待状态，表示线程进入等待状态，进入该状态表示当前线程需要等待其他线程做出一些特定动作 |
| TIME-WAITING | 超时等待状态，该状态不同于WAITING,它是可以在指定的时间自行返回的 |
| TERMINATED   | 终止状态，表示当前线程已经执行完毕                           |

Java线程状态变迁如下图所示

![image-20210126112444921](C:\Users\why19991031\AppData\Roaming\Typora\typora-user-images\image-20210126112444921.png)

#### Daemon线程

- 是支持型线程，因为它主要被用作程序中后台调度以及支持性工作。这意味着，当一个Java虚拟机中不存在非Daemon线程的时候，Java虚拟机将会退出

```java
public class Daemon {
    public static void main(String[] args) {
        Thread thread=new Thread(new DaemonRunner(),"DaemonRunner");
        thread.setDaemon(true);
        thread.start();
    }
    static class DaemonRunner implements Runnable{
        public void run(){
            try{
                SleepUnits.second(10);
            }finally {
                System.out.println("DaemonThread finally run.");
            }
        }
    }
}
```

我们得到的结果是这个程序不会打印任何的值

### 线程间通信

每个线程之间如果只是孤立地运行，那么没有一点儿价值，或者说价值很少，但是如果多个线程能够相互配合的完成工作，这将会带来巨大的价值

#### 等待通知机制

#### 线程池技术及其示例

## 第五章 Java中的锁

Lock接口提供的synchronized关键字不具备的主要特性

- 尝试非阻塞的获取锁
  - 当前线程尝试获取锁，如果这一时刻锁没有被其他线程获取到，则成功获取并持有锁
- 能被中断地获取锁
  - 与synchronized不同，获取到锁地线程能够响应中断，当获取到锁的线程被中断时，中断异常将会被抛出，同时锁会被释放
- 超时获取锁
  - 在指定的截止时间之前获取锁，如果截止时间到了仍旧无法获取锁，则返回

#### 队列同步器

