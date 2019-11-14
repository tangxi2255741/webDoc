知道了问题出在哪里，我们才能更的去解决问题，写好并发程序；

# CPU、内存、I/O运行速度差异

**形象描述：**

CPU 耗时1天 =  内存 耗时 1年  =  io设备 耗时100年

**木桶理论**
因此程序整体执行性能取决于io设备的性能，为了合理运用，对此进行优化

1. CPU 增加了缓存，以均衡与内存的速度差异；
2. 操作系统增加了进程、线程，以分时复用 CPU，进而均衡 CPU 与 I/O 设备的速度差
3. 编译程序优化指令执行次序，使得缓存能够得到更加合理地利用



# 缓存导致的可见性问题

> 可见性：一个线程对共享变量的修改，另外一个线程能够立刻看见；

单核：每个线程都操作的同一个CPU的缓存，都是可见的；

![1564665056100](C:\Users\86136\AppData\Roaming\Typora\typora-user-images\1564665056100.png)







多核：线程A和线程B在不同的CPU上，线程A对变量V的操作对于B是不可见的；

![1564665131152](C:\Users\86136\AppData\Roaming\Typora\typora-user-images\1564665131152.png)



```java
public class Test {
private long count = 0;
private void add10K() {
int idx = 0;
    while(idx++ < 10000) {
        count += 1;
    }
}

public static long calc() {
	final Test test = new Test();
    // 创建两个线程，执行 add() 操作
    Thread th1 = new Thread(()->{
    test.add10K();
    });
    Thread th2 = new Thread(()->{
    test.add10K();
    });
    // 启动两个线程
    th1.start();
    th2.start();
}
```



# 线程切换带来的原子性问题

> 我们把一个或者多个操作在 CPU 执行的过程中不被中断的特性称为原子性

高级语言里一条语句往往需要多条 CPU 指令完成，列如count += 1，至少需要三条 CPU 指令:

指令 1：把变量 count 从内存加载到 CPU 的寄存器；

指令 2：在寄存器中执行 +1 操作；

指令 3：将结果写入内存（缓存机制导致可能写入的是 CPU 缓存而不是内存）；

操作系统做线程切换可以发生在任何一条CPU指令执行完成时，

![1564667072730](C:\Users\86136\AppData\Roaming\Typora\typora-user-images\1564667072730.png)



# 编译优化带来的有序性问题

> 有序性指的是程序按照代码的先后顺序执行。编译器为了优化性能，有时候会改变程序中语句的先后顺序；有时候编译器及解释器的优化可能导致意想不到的 Bug

例如：`` a=6；b=7；`` 编译器优化后可能变成 ``b=7；a=6；``

以下代码多线程时可能会出问题：

~~~java
public class Singleton {
    static Singleton instance;
    static Singleton getInstance(){
        if (instance == null) {
            synchronized(Singleton.class) {
            if (instance == null)
                instance = new Singleton();
            }
    	}
    	return instance;
    }
}

// 我们认为的执行顺序：
1. 分配一块内存 M；
2. 在内存 M 上初始化 Singleton 对象；
3. 然后 M 的地址赋值给 instance 变量;

// 实际可能执行顺序：
1. 分配一块内存 M；
2. 将 M 的地址赋值给 instance 变量；
3. 最后在内存 M 上初始化 Singleton 对象;
~~~



线程A执行2时，如果发生线程切换，B执行到instance == null判断时，会判断为不为空，这时就会出现空指针异常；

![1564668187356](C:\Users\86136\AppData\Roaming\Typora\typora-user-images\1564668187356.png)

