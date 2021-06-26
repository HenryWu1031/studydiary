# Java并发编程实战知识点

## written by problem? why will kill it

## 第二章 线程安全性

- 如果当多个线程访问同一个可变的状态变量时没有使用合适的同步，那么程序就会出现错误。有三种方式可以修复这个问题
  - 不在线程之间共享该状态变量
  - 将状态变量修改为不可变的变量
  - 在访问状态变量时使用同步
- 首先使代码运行正确，然后再提高代码的速度
- 线程安全的程序不一定不一定完全由线程安全类构成
- 线程安全类中可以包含非线程安全的类

#### 线程类如何是安全的

定义：当多个线程访问某个类时，不管运行时环境采用何种调度方式或者这些线程将如何交替执行，并且在主调代码中不需要任何额外的同步或协同，这个类都能表现出正确的行为，那么就称这个类是线程安全的

- 无状态对象一定是线程安全的

#### 原子性

++count这个操作是由三个独立的操作组成的

- 读取count的值
- 把值+1
- 把计算结果写入count中

它会导致出现错误，它是不安全的，我们把这样的由于不恰当的执行时许导致的错误叫做竞态条件

##### 竞态条件

竞态条件的本质：

- 基于一种可能失效的观察结果来做出判断或执行某个计算
- 典型的情况是先检查后执行，先观察到某个条件为真，之后做出某个行为，但是很有可能在你做出行为之前这个条件已经是不存在的了。（出现错误）

##### 例子

延迟初始化

```java
public class LazyInitRace{
	private ExpensiveObject instance=null;
	public ExpensiveObject getInstance(){
		if(instance==null)
			instance=new ExpensiveObject();
		return instance;
	}
}
```

说明：如果我有两个线程A和B都需要执行这一段代码，那么一开始的时候两个都认为这个对象没有实例化，这样的话，在A实例化了对象之后，B有可能就会再次实例化一个对象，这样就造成了错误。

##### 复合操作

我们可以用一个线程安全类来解决上面可能出现的问题

```java
@ThreadSafe
public class CountingFactorizer implements Servlet{
	private final AtomicLong count=new AtomicLong(0);
	public long getCount(){
		return count.get();
	}
	public void service(ServletRequest req,ServletResponse resp){
		BigInteger i=extractFromRequest(req);
		BigInteger[] factors=factor(i);
		count.incrementAndGet();
		encodeIntoResponse(resp,factors);
	}
}
```

- 在实际情况中，应尽可能地使用现有的线程安全对象来管理类的状态。与非线程安全的对象相比，判断线程安全对象的可能状态及其状态转换情况要更为容易，从而也更容易验证和维护线程安全性

#### 加锁机制

- 要保持状态的一致性，就需要在单个原子操作中更新所有相关的状态变量

##### 内置锁

- 使用Java的内置锁只允许一个线程使用这个锁，如果这个锁被线程B使用，那么线程A在请求使用这个锁的时候会进入阻塞状态等待线程B使用完毕，这种方法的缺点是过于极端，并发性很差

```java
@ThreadSafe//不推荐使用这种加锁方式对于同步问题进行处理
public class SynchronizedFactorizer implements Servlet{
	private BigInteger lastNumber;
	private BigInteger[] lastFactors;
	public synchronized void service(ServletRequest req,ServletResponse resp){
		BigInteger i=extractFromRequest(req);
		if(i.equals(lastNumber))
			encodeIntoResponse(resp,lastFactors);
		else{
			BigInteger[] factors=factor(i);
			lastNumber=i;
			lastFactors=factors;
			encodeIntoResponse(resp,factors);
		}
	}
}
```

##### 重入

- 意味着获取锁的操作的粒度是“线程”而不是“调用”

机制：

- 为每个锁关联一个获取计数值和一个所有者线程。当计数值为0时，这个锁就被认为是没有被任何线程持有。当线程请求一个未被持有的锁时，JVM将记下锁的持有者，并且将获取值置为1.如果同一个线程再次获取这个锁，计数值将递增，而当线程退出同步代码块时，计数器会相应地递减。当计数值为0时，这个锁将被释放

##### 用锁来保护状态

- 并非所有数据都需要锁的保护，只有被多个线程同时访问的可变数据才需要通过锁来保护。

##### 活跃性与性能

- 另外一种缓存最近执行因数分解的数值及其计算结果的Servlet

```java
@ThreadSafe
public class CachedFactorizer implements Servlet{
	private BigInteger lastNumber;
	private BigInteger[] lastFactors;
	private long hits;
	private long cacheHits;
	public synchronized long getHits(){return hits;}
	public synchronized double getCacheHitRadio(){
		return (double) cacheHits/(double) hits;
	}
	public void service(ServletRequest req,ServletResponse resp){
		BigInteger i=extrcatFromRequest(req);
		BigInteger[] factors=null;
		synchronized(this){
			++hits;
			if(i.equals(lastNumber)){
				++cacheHits;
				factors=lastFactors.clone();
			}
		}
		if(factors==null){
			factors=factor(i);
			synchronized(this){
				lastNumber=i;
				lastFactors=factors.clone();
			}
		}
		encodeIntoResponse(resp,factors);
	}
}
```

- 通常，在简单性与性能之间存在着相互制约因素。当实现某个同步策略时，一定不要盲目地为了性能而牺牲简单性（这可能会破坏安全性）
- 当执行时间较长的计算或者可能无法快速完成的操作时（例如，网络I/O或控制台I/O），一定不要持有锁

## 第三章 对象的共享

#### 可见性

##### 失效数据

失效数据就是一个数据在发生改变的情况下提前被一个线程读入，导致那个线程中出现的数据就是失效数据

非线程安全的可变整数类

```java
@NotThreadSafe
public class MutableInteger{
	private int value;
	public int get(){
		return value;
	}
	public void set(int value){
		this.value=value;
	}
}
```

线程安全的可变整数类

```java
@ThreadSafe
public class SynchronizedInteger{
	private int value;
	public synchronized int get(){
		return value;
	}
	public synchronized void set(int value){
		this.value=value;
	}
}
```

##### 加锁与可见性

- 加锁的含义不仅仅局限于互斥行为，还包括内存可见性。为了确保所有线程都能看到共享变量的最新值，所有执行读操作或者写操作的线程都必须在同一个锁上同步。

##### Volatile变量

- 当把变量声明为volatile类型后，编译器与运行时都会注意到这个变量是共享的，因此不会将该变量上的操作与其他内存操作一起重排序。
- 把这些变量的行为想象成上面的set和get方法，但是在访问volatile变量时不会执行加锁操作，因此也就不会使线程阻塞，因此volatile变量是一种比sychronized关键字更轻量级的同步机制
- 加锁机制既可以确保可见性又可以确保原子性，而volatile变量只能确保可见性

#### 发布与逸出

- 发布的定义：使对象能够在当前作用域之外的代码中使用。例如，将一个指向该对象的引用保存到其他代码可以访问的地方，或者在某一个非私有的方法中返回该引用。

#### 线程封闭

##### ad-hoc线程封闭

##### 栈封闭

##### ThreadLocal类

#### 不变性

- 不可变对象一定是线程安全的
- 当满足一下条件时，对象才是不可变的：
  - 对象创建以后其状态就不能修改
  - 对象的所有域都是final类型
  - 对象是正确创建的（在对象的创建期间，this引用没有逸出）

#### 安全发布

我们不仅要考虑如何确保对象不被发布，例如让对象封闭在线程或另一个对象的内部。当然我们在某些情况下希望在多个线程间共享对象，此时必须确保安全地进行共享。

错误示例

```java
public Holder holder;
public void initialize(){
	holder=new Holder(42);
}
```

- 任何线程都可以在不需要额外同步的情况下安全地访问不可变对象，即使在发布这些对象时没有使用同步

##### 如何安全地发布一个对象

要安全地发布一个对象，对象的引用以及对象的状态必须同时对其他线程可见。一个正确构造的对象可以通过以下方式来安全地发布：

- 在静态初始化函数中初始化一个对象引用
- 将对象的引用保存到volatile类型的域或者AtomicReference对象中
- 将对象的引用保存到某个正确构造的final类型域中
- 将对象的引用保存到一个由锁保护的域中

##### 对象的发布需求取决于它的可变性

- 不可变对象可以通过任意机制来发布
- 事实不可变对象必须通过安全方式来发布
- 可变对象必须通过安全方式来发布，并且必须是线程安全的或者由某个锁保护起来

## 第四章 对象的组合

#### 设计线程安全的类

在设计线程安全类的过程中，需要包含以下三个基本要素：

- 找出构成对象状态的所有变量
- 找出约束状态变量的不变性条件
- 建立对象状态的并发访问管理策略

