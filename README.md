# I HAVE A QUESTION

仅记录一下日常的疑惑和胡思乱想

如果有小朋友跟我一样有很多疑问？

或者对这些问题有什么见解或答案？

可以添加我的工作微信闲聊探讨：iOSCodery

****

***1-20200618*** 昨天微信新出了“拍一拍”功能，突然很好奇微信用户间的昵称是如何管理的？假如一个群里500个人相互之间都是好友关系，两两有各自不同的备注昵称，那么突然有一个人在群里“拍”了另一个人一下，500个人显示的这条信息各不相同。再假如有两个人是好友，他们同在不同的100个群里，每个群有自己不同的备注，并且都给对方设置了不同的备注。这些昵称备注都是怎么管理的？群ID+用户ID作为key缓存一个在本地吗？

***2-20200620*** AOP的动态代理有JDK和CGLib两种，前者创建代理对象时效率高，后者运行性能高。以Service层为例，现在大多做法都是声明接口并写实现类。同时在Service层加声明式事务本质是AOP的环绕通知。那么创建出来Service层的实例其实就是Proxy。这样性能有最优吗？IOC管理的对象不是默认单例吗？这样考虑的话为啥Service不直接用类呢？我乱了（偷笑）

***3-20200701*** 为什么很多公司的程序推送都定在晚上8点30分？有电商平台、视频网站、新闻类的也有、甚至于钉钉

***4-20200713*** how-to-recover-a-dropped-stash-in-git
[stackoverflow](https://stackoverflow.com/questions/89332/how-to-recover-a-dropped-stash-in-git)

***5-20200715*** 假如<饿了么>的会员系统加入一个等级制度，对应不同的等级可享受的权益有所不同，这个权益当然是要入驻的商家自定义。在这个前提下，假如有一个需求是：某一天要给某个会员等级的会员给他经常光顾的几个店家送几张优惠券（不同等级优惠力度不同。这个优惠券是商家配置的，有很多种类。）。这个送券的活动一系列怎么建表？这个需求是否有意义？商家配置权益的管理端如何做到操作人性化？或者有什么奖励制度可以鼓励商家去配置？
