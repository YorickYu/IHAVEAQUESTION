# I HAVE A QUESTION

仅记录一下日常的疑惑和胡思乱想

如果有小朋友跟我一样有很多疑问？

或者对这些问题有什么见解或答案？

可以添加我的工作微信闲聊探讨：iOSCodery

****



***10-20201101*** HashMap源码记录modCount++这个计算方式在多线程操作时如果不能保证原子性，那么岂不是也有可能触发ConcurrentModificationException异常？



验证过程：

1 因为HashMap的put操作会进行modCount++

2 modCount声明时也没有指明volatile

那么多线程put是否会造成modCount的值不准确？



相关代码可以在 [***JPP***](https://github.com/YorickYu/JPP)/ConcurrentModificationExceptionDemo类中查看。

```
static void atomicTest() throws InterruptedException {
    HashMap m = new HashMap();
    new Thread(new Runnable() {
        @Override
        public void run() {
            for (int i = 0; i < 100; i++) {
                m.put(i, String.valueOf(i).hashCode());
            }
        }
    }).start();

    new Thread(new Runnable() {
        @Override
        public void run() {
            for (int i = 150; i < 200; i++) {
                m.put(i, String.valueOf(i).hashCode());
            }
        }
    }).start();

    Thread.sleep(5000);
    Iterator iterator = m.keySet().iterator();
    iterator.next(); // 对比modCount
}
```

运行的结果是，如果循环次数不多，最后可以保证modCount的数值正确。但是提升循环插入的次数，会锁住一个线程，导致其他线程的数据没有插入成功，但是modCount的值依然是正确的。

具体这个魂循环次数设定的阈值，我也没有过多尝试。至少目前我没有因为++计算不是原子性的原因出现过fast-fail



***9-20201031*** [JDK1.7 HashMap 链表头插疑问？](http://yloopdaed.icu/2020/10/31/question-of-hashmap-put/)

***8-20201029*** 看下面这段代码，循环创建一亿次Object对象，通常理解一个空Object对象创建会在栈中存在一个4字节的指针，指向堆中的对象16字节。

循环创建一亿次大概会占用1.6G的空间。

```java
long startTime = System.currentTimeMillis();
for (int i = 0; i < 100000000; i++) {
		new Object();
}
System.out.println("use time: " + (System.currentTimeMillis() - startTime) + "ms");
```

> 执行结果：use time: 38ms

**这是为什么？**

再试一下下面这段代码：

```java
long startTime = System.currentTimeMillis();
for (int i = 0; i < 100000000; i++) {
		Object o = new Object();
		o.hashCode();
}
System.out.println("use time: " + (System.currentTimeMillis() - startTime) + "ms");
```

> 执行结果：use time: 8014ms

**这是为什么？** - 指针逃逸

***7-20201029*** 今天下班在地铁站里面，一条长长的通道，密度很大。有些两三个闲谈，有些低头看手机走路，有些穿来穿去走的比较着急。不同方向不同路线的都有，我就想到一个问题：假设从上往下走的人数和从下往上走的人数相同，但是不能控制每个人行走的路线和速度，怎么样设置指引才能让这条通道的通行效率最高？
![metro](https://yloopdaed-oss.oss-cn-beijing.aliyuncs.com/metro.png)

相似的问题让我想到了“幽灵堵车”，大概的意思就是如果若干辆汽车沿着一个大圆环的公路行驶。因为驾驶习惯等种种原因会导致汽车都拥挤的集中在某一个区域，而公路的大部分路段都是没车的。

所以上面地铁通道的问题转变成了高速公路的问题，这也是为什么高速公路不设立红绿灯，而且按最高限速划分车道的原因。但是无论如何，因为“人为”因素的干预，“幽灵堵车”的问题始终存在。我认为这才是推广“自动驾驶”的意义。如果全民自动驾驶，机器会精确按照相同的速度行驶，最大化速度的同时也避免了幽灵堵车。

***6-20200807*** 今天早上使用了一个功能：从音乐平台A导出一个歌单到音乐平台B，歌单中有大概几十首歌，导入的过程很快，也过滤掉了B平台中没有的歌曲或者没有版权的歌曲。不知道对于音乐是否有什么统一的编号可以走索引？如果这个导入过程只是通过歌曲的名称检索那速度不可能这么快。这个检索的过程是如何实现的？

***5-20200715*** 假如<饿了么>的会员系统加入一个等级制度，对应不同的等级可享受的权益有所不同，这个权益当然是要入驻的商家自定义。在这个前提下，假如有一个需求是：某一天要给某个会员等级的会员给他经常光顾的几个店家送几张优惠券（不同等级优惠力度不同。这个优惠券是商家配置的，有很多种类。）。这个送券的活动一系列怎么建表？这个需求是否有意义？商家配置权益的管理端如何做到操作人性化？或者有什么奖励制度可以鼓励商家去配置？

***4-20200713*** how-to-recover-a-dropped-stash-in-git [stackoverflow](https://stackoverflow.com/questions/89332/how-to-recover-a-dropped-stash-in-git)

***3-20200701*** 为什么很多公司的程序推送都定在晚上8点30分？有电商平台、视频网站、新闻类的也有、甚至于钉钉

***2-20200620*** AOP的动态代理有JDK和CGLib两种，前者创建代理对象时效率高，后者运行性能高。以Service层为例，现在大多做法都是声明接口并写实现类。同时在Service层加声明式事务本质是AOP的环绕通知。那么创建出来Service层的实例其实就是Proxy。这样性能有最优吗？IOC管理的对象不是默认单例吗？这样考虑的话为啥Service不直接用类呢？我乱了（偷笑）

***1-20200618*** 昨天微信新出了“拍一拍”功能，突然很好奇微信用户间的昵称是如何管理的？假如一个群里500个人相互之间都是好友关系，两两有各自不同的备注昵称，那么突然有一个人在群里“拍”了另一个人一下，500个人显示的这条信息各不相同。再假如有两个人是好友，他们同在不同的100个群里，每个群有自己不同的备注，并且都给对方设置了不同的备注。这些昵称备注都是怎么管理的？群ID+用户ID作为key缓存一个在本地吗？











