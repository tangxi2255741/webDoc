# Minor GC？Full GC？Major GC？

**Minor GC：从年轻代回收内存**

触发条件
	1、Eden区域满

​	2、新创建的对象大小 > Eden所剩空间

**Full GC：清理整个堆空间，包括年轻代和老年代**

触发条件

​	1、每次晋升到老年代的对象平均大小>老年代剩余空间

​	2、MinorGC后存活的对象超过了老年代剩余空间

​	3、永久代空间不足

​		避免Perm Gen占满造成Full GC现象，可采用的方法为增大Perm Gen空间或转为使用CMS GC

​	4、System.gc()

​		通过-XX:+ DisableExplicitGC来禁止RMI调用System.gc

​	5、CMS GC异常

​		promotion failed:MinorGC时，survivor空间放不下，对象只能放入老年代，而老年代也放不下造成

​		concurrent mode failure:GC时，同时有对象要放入老年代，而老年代空间不足造成

6、堆内存分配很大的对象

**Major GC：清理老年代**

Java在什么时候会出现内存泄漏；
几种常用的内存调试工具：jmap、jstack、jconsole；
G1停顿吗，CMS回收步骤，CMS为什么会停顿，停顿时间；
软引用和弱引用的使用场景（软引用可以实现缓存，弱引用可以用来在回调函数中防止内存泄露）；
什么是Java内存模型？

类加载的双亲委托机制



# GC收集器有哪些？



# CMS收集器与G1收集器的特点



# Java中的大对象如何进行存储

