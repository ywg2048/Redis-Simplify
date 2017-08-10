# Redis-Simplify
对`Redis v3.0` 的代码做了简化,然后一步一步地往最初的代码里添加新的功能,当然,这一切都是为了方便理解源码而已,总体而言,`Redis`是很漂亮的`c`风格的代码,值得一读.



这个项目从最基本的统一事件源开始,逐步加入各式各样的命令的实现,然后加入序列化的实现,加入事务的实现,最终剥出了了一个单机版本的数据库.



如果你对它的实现原理感兴趣,推荐看<<Redis设计与实现>>这本书:

![Redis设计与实现](http://img.blog.csdn.net/20161124161052469)

# 日志

## 2016.12.03:

代码现在已经非常臃肿了.看来`C`的代码到了一定的程度之后,真的变得很难管理了.个人突然觉得1到2万的`C`代码还在掌控之内,再多就已经超过我能掌控的范围了.换句话说,你不可能做到细节与宏观都了解得一清二楚,太费劲了.

这或许也是为什么人们要提出抽象的原因吧,我只规定一套接口,我的代码依赖于这套接口之上,至于你怎么实现,那就和我没有多大的关系了.

还有一点,`C`工程写大之后,其实你去看它的代码,其实里面用了很多面向对象的思想,包括数据的封装,代码的复用,感觉越写越像`CPP`.代码我已经剥了很大的一部分了,应该用不了多久就能剥出一个单机`NoSql`数据库了.然后准备开始写`Redis`的客户端了.



## 2016.12.04:


修复了一些`bug`,然后下一步的工作是可以将内存中的数据写入文件,并且启动时可以导入文件,这样的话,一个单机版的数据库基本完工.



## 2016.12.10:

时间过得真快,最近忙到都没有时间来打理这个东西了,好了,我想说的是,这个版本实现了数据存储到磁盘的功能,`aof`以及数据库的保存都已经补完了,这个项目也接近尾声了,下一个版本,我想加入事务的功能,貌似挺有意思的.



## 2016.12.10:

好吧,今天加了一点班,将单机数据库所需要的全部东西都剥离了出来,好吧,其实就是添加了事务这样一个功能,有了事务,`Redis`才能被称作数据库.这就是说,这个项目差不多就到头了,将来可能会改一点东西,但是不会很大了,多机数据库的部分我就不添加了,再弄下去,就和源码没多大区别了,(当然,我也剥不下去了,因为代码量太大了点)所以其余的,你如果感兴趣的话,自己去看源码的,我的源码的版本是`3.0`.



## 2017.08.07:

距离上一次的代码修改,已经将近过去大半年了,事实上,上几次做的还不够彻底,因为,我并没有书写完整的 `makefile` 文件,所以,这一次,估计也是最后一次,我会将这几个版本的代码完善一下,并且将 `makefile` 文件写完.



# 关于各个版本

## 01-Contain-event-loop

这个版本基本上只包含了事件循环,是最为简单,也是最为重要的一个版本.想学习Redis的关于网络部分代码的基本上看这个版本就可以了.后面的代码更多的是关于如何实现一个数据库的.

## 02 - ~~~

在第一个版本的基础上增加了一些代码,不过增加的量不算太大.

## 03 - finished_string_command

在第二个版本的基础上,将Redis 字符操纵的命令这一块实现了.



完结撒花.用了大半个月来剥离源码,说实话,源码还是很有意思的,能学到多少东西,这是个仁者见仁智者见智的问题啦.对我来说,不亏,好像也不赚,就这样吧,下一步就是用`cpp`写一个`Redis`客户端了,相比于服务端,客户端的实现要简单太多太多.