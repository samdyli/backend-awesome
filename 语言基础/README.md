# java 语言核心知识点

[TOC]



## 集合

- Map

- ConcurrentHashMap

  - hash算法：

    java移位： >> 右移 <<左移  >>> 无符号右移位

    1.7 

    ```java
        h ^= (h >>> 20) ^ (h >>> 12);
        return h ^ (h >>> 7) ^ (h >>> 4);
    ```

    1.8:  (h ^ (h >>> 16)) & HASH_BITS







## 并发编程

- 无锁编程

  - copyOnWrite容器

    缺点： 内存问题和数据一致性问题。 

    - 问题： 容器在写入时，老对象和新对象同时存在。 如果对象占用内存比较大时，会造成youngc或者fullgc。

    - 数据不一致问题： copyOnWirte保证读和写的最终一致性。 写入过程中会有不一致发生。 

    注意事项： 

    - 指定初始大小，防止频繁扩容。
    - 批量插入代替单次循环插入

    使用场景： 读多写少，一致性要求不高的场景。

    具体使用：CopyOnWriteArrayList 和CopyOnWriteArraySet

    原理： 写入时加RLock， 复制数组，新数组设置值，重新指向新数组。

    CopyOnWriteArraySet实现： 底层使用功能CopyOnWriteArrayList， add时首先调用addIfAbsent方法。 for循环查找是否存在存在该对象。不存在时添加。 

    

    

    

    

## IO
## JVM
  - JVM基本结构（从编译到运行全过程)
    - 堆
    - 方法区
    - 栈
  - 类加载器
    - 类的文件结构
    - 操作字节码：ASM
    - 类加载流程
    - 类加载的双亲委托机制和热替换
    - 字节码执行
      - java agent动态修改类
      - 动态函数调用
      - 静态编译优化
      - JIT优化
  - 垃圾回收
    - 对象已死：可达性分析
    - 垃圾回收算法
    - 垃圾回收器
    - 垃圾回收器实战
    - hotspot实现
      - 枚举根节点
      - 安全点
      - 安全区域
    - 性能监控工具
  - 锁和并发
    - 对象头：锁升级过程
    - 锁优化
    - 无锁
    - 内存模型：三性
    - 