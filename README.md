# I HAVE A QUESTION

仅记录一下日常的疑惑和胡思乱想

如果有小朋友跟我一样有很多疑问？

或者对这些问题有什么见解或答案？

可以添加我的工作微信闲聊探讨：iOSCodery

****

***1-20200618*** 昨天微信新出了“拍一拍”功能，突然很好奇微信用户间的昵称是如何管理的？假如一个群里500个人相互之间都是好友关系，两两有各自不同的备注昵称，那么突然有一个人在群里“拍”了另一个人一下，500个人显示的这条信息各不相同。再假如有两个人是好友，他们同在不同的100个群里，每个群有自己不同的备注，并且都给对方设置了不同的备注。这些昵称备注都是怎么管理的？群ID+用户ID作为key缓存一个在本地吗？

***1-20200620*** AOP的动态代理有JDK和CGLib两种，前者创建代理对象时效率高，后者运行性能高。以Service层为例，现在大多做法都是声明接口并写实现类。同时在Service层加声明式事务本质是AOP的环绕通知。那么创建出来Service层的实例其实就是Proxy。这样性能有最优吗？IOC管理的对象不是默认单例吗？这样考虑的话为啥Service不直接用类呢？我乱了（偷笑）
