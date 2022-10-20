# 参考内容
https://github.com/Wang-Jun-Chao/java-concurrency
https://github.com/Fadezed/concurrency
[yontube视频]([https://www.youtube.com/watch?v=TCd8QIS-2KI](https://www.youtube.com/watch?v=mTGdtC9f4EU&list=PLL8woMHwr36EDxjUoCzboZjedsnhLP1j4))


![](https://gitee.com/Jkaolo/pico-go/raw/master/202210210256976.png)
![](https://gitee.com/Jkaolo/pico-go/raw/master/202210210257873.png)

# 学习笔记

# 学习日志
## Java 的三种创建方式

### 代码

```java
// 创建方式1
public class Start1 {
    public static void main(String[] args) {
        System.out.println("main start");
        new Thread(()->{
            for(int i = 0;i < 10 ;i++){
                System.out.println(i);
            }
        }).start();
        System.out.println("main end");
    }
}
// 创建方式2
public class MyThread implements Runnable {
    public static int tickets = 20;
    @Override
    public void run() {
        if(tickets > 0){
            System.out.println("current tickets :" + tickets);
        }
    }

    public static void main(String[] args) {
        System.out.println("main start");
        MyThread thread = new MyThread();
        Thread mThread1=new Thread(thread,"线程1");
        Thread mThread2=new Thread(thread,"线程2");
        Thread mThread3=new Thread(thread,"线程3");
        mThread1.start();
        mThread2.start();
        mThread3.start();
        System.out.println("main end");
    }
}
// 创建方式3
public class MyThreadCall implements Callable<Integer> {
    @Override
    public Integer call() throws Exception {
        System.out.println("即将返回给你 一个数字");
        return RandomUtil.randomInt();
    }

    public static void main(String[] args) throws Exception {
        System.out.println("main start");
        MyThreadCall callable = new MyThreadCall();
        //Integer call = callable.call();
        //System.out.println(call);
        FutureTask <Integer>futureTask=new FutureTask<>(callable);
        Thread thread = new Thread(futureTask);
        thread.start();
        System.out.println("main end");
    }
}
```

### 问题

-   为什么有了继承Thread 还要实现Runnable
  
    避免单继承的局限性 更好提现共享的概念
    
-   线程的设计模式是什么样的
  
    创建线程任务→ 放进线程里面
    

## Java 的内存模型

### 参考内容

Java 并发编程的艺术 → Java 的内存模型

### 笔记

-   并发编程的两个关键问题
  
    线程之间的同步和通信 通信可以通过**共享内存**或者**消息传递**
    

### 什么叫可见性 什么叫有序性

线程修改变量对其他线程可见

### 草稿

1.  如果编写多线程程序的Java程序员不理解隐式进行的线程之间通信的工作机制，很可能会遇到各种奇怪的内存可见性问题
  
2.  Java 中静态域数组元素都存在堆内存中, 堆内存线程之间共享，局部变量线程之间不共享不存在可见性问题。
  
3.  JMM 控制Java 的线程通信，定义了线程和主内存的抽象关系。
  
4.  每个线程都有一个私有的本地内存（Local Memory），本地内存中存储了该线程以读/写共享变量的副本
  
5.  本地内存只是一个抽象存在 包含了缓存、写缓冲区、寄存器以及其他的硬件和编译器优化
  
    -   缓存图片
      
        ![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/407b54a6-04ef-4626-bc8f-253d497ec94d/Untitled.png)
    
6.  重排序的三种类型 编译器优化重排序 指令集并行重排序 内存系统重排序
  
    1.  不改变单线程语义的前提下，重新安排语句的执行顺序。
    2.  其他两个不知道什么意思
7.  before-after关系 前一个操作对后一个操作可见
  
    -   参考
      
        [happens-before是什么？JMM最最核心的概念，看完你就懂了 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/126275344)
        

## Java 并发编程的基础

### 代码

-   优雅的中断代码
  
    ```java
    package com.koala.chapter4;
    
    import java.util.concurrent.TimeUnit;
    
    /**
     *
     * 优雅的中止线程
     * @author yantingrui
     * @date 2022/2/22   22:03
     */
    public class ShutDown {
        public static void main(String[] args) throws InterruptedException {
            Runner run1 = new Runner();
            Thread one = new Thread(run1, "one");
            one.start();
            SleepUtils.second(1);
            one.interrupt();
            Runner run2 = new Runner();
            one = new Thread(run2, "two");
            one.start();
            SleepUtils.second(1);
            run2.cancel();
        }
    
        private static class Runner implements Runnable{
            protected long i;
            private volatile boolean on = true;
    
            @Override
            public void run() {
                while(on & !Thread.currentThread().isInterrupted()){
                    i++;
                }
                System.out.println("count : " + i );
            }
    
            public void cancel(){
                this.on = false;
            }
        }
    }
    ```
    
-   等待通知
  
    ```java
    package com.koala.chapter4;
    
    import lombok.SneakyThrows;
    import lombok.extern.slf4j.Slf4j;
    
    /**
     * 描述场景
     * 宿舍一张空调卡 舍友拿着去空调卡去冲空调  冲到空调让室友通知是否冲上
     * @author yantingrui
     * @date 2022/2/22   23:23
     */
    @Slf4j
    public class NotifyTest {
        // 是否空调有电
        static boolean flag = false;
        // 锁住空调卡
        static Object lock = new Object();
    
        public static void main(String[] args) {
            Thread sitian1 = new Thread(new Waiter(), "思甜1");
            Thread sitian2 = new Thread(new Waiter(), "思甜2");
            Thread sitian3 = new Thread(new Waiter(), "思甜3");
            sitian1.start();
            sitian2.start();
            sitian3.start();
            Thread qingjia = new Thread(new Friend(), "卿家");
            qingjia.start();
        }
    
        static class Waiter implements Runnable{
    
            @SneakyThrows
            @Override
            public void run() {
                // 进入客户的房间把房间锁住
                synchronized (lock){
                    // 判断客户是否需要水
                    while(!flag){
                        log.info("{} 给空调冲了电费",Thread.currentThread().getName());
                        // 把空调卡放回去
                        lock.wait();
                    }
                    log.info("空调有电了 {}被通知回来",Thread.currentThread().getName());
                }
            }
        }
    
        static class Friend implements Runnable{
    
            @Override
            public void run() {
                // 室友在宿舍看是否可以拿到空调卡
                synchronized (lock){
                    log.info("室友{}拿到空调卡 插入卡槽 宿舍来电通知充卡的",Thread.currentThread().getName());
                    flag = true;
                    lock.notifyAll();
                }
            }
        }
    
    }
    ```
    
-   管道通信
  
    ```java
    package com.koala.chapter4;
    
    import lombok.SneakyThrows;
    
    import java.io.*;
    
    /**
     * 管道流通信
     * 定义一个人给另外一个人发微信
     * @author yantingrui
     * @date 2022/2/23   9:06
     */
    public class Piped {
        public static void main(String[] args) throws IOException {
            // 写信
            PipedWriter out = new PipedWriter();
            // 读信的人
            PipedReader in = new PipedReader();
            out.connect(in);
            Thread sitian = new Thread(new Person(in), "sitian");
            sitian.start();
            int reveive = 0;
            while((reveive = System.in.read()) != -1){
                out.write(reveive);
            }
        }
    
        static class Person implements Runnable{
            //人有阅读的能力
            private PipedReader in;
    
            public Person(PipedReader in) {
                this.in = in;
            }
    
            @SneakyThrows
            @Override
            public void run() {
                int receive = 0;
                while((receive=in.read()) != 0){
                    System.out.print((char)receive);
                }
            }
        }
    }
    ```
    

### 问题

-   Thread.sleep(1000) 的操作
  
    线程不会释放锁 其他线程还是进不去
    
-   有了synchronize 为什么还要Lock
  

## Java中的锁

双胞胎锁

## Java并发容器和框架

并发容器 阻塞队列 Join fork 方法

## Java 13个并发原子类
## Java 并发工具类

CyclicBarrier `CountDownLatch`

CountDownLatch的计数器只能使用一次，而CyclicBarrier的计数器可以使用reset()方法重 置。所以CyclicBarrier能处理更为复杂的业务场景。例如，如果计算发生错误，可以重置计数 器，并让线程重新执行一次。







# 学习全图

![test](https://gitee.com/Jkaolo/pico-go/raw/master/202210210309462.png)


# 问题
synchronized 和 Lock 的区别

Synchronized和Lock比较. Synchronized是关键字，内置语言实现，Lock是接口。. Synchronized在线程发生异常时会自动释放锁，因此不会发生异常死锁。. Lock异常时不会自动释放锁，所以需要在finally中实现释放锁。. Lock是可以中断锁，Synchronized是非中断锁，必须等待线程执行完成释放锁。. Lock可以使用读锁提高多线程读效率