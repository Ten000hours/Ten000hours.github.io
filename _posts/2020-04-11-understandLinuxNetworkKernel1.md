<!--
 * @Author: xiangrui
 * @Date: 2020-04-11 16:29:04
 * @LastEditTime: 2020-04-11 23:19:25
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \Ten000hours.github.io\_posts\2020-04-11-understandLinuxNetworkKernel1.md
 -->
# 深入理解Linux网络内核---第一章

本文作为了解Linux网络内部结构和最佳实践的intro。 将会开一个系列文章系统的介绍网络内核的实现，探讨内容主要基于两本书：`<<understanding linux networking internels>>` 和 `<<linux kernel networking-impl and theory>>` 

## 在开始之前

1. **基本术语**：

        |  L2  | link layer  |
        |  :----  | :----  |
        |  L3  | network layer  |
        |  L4  | transport layer |

    其他术语包括TCP,UDP,ICMP（运输层协议），数据（data）采用术语：segment，packet，frame，message等。

2. **内存缓存**：
   
   在内核中，使用`kmalloc`和`kfree`来的分配合释放内存。这两个方法的语法与`malloc`和`free`相似，都从libc的用户空间库中来。  

    当分配和收回经常发生的时候，相关的内核部件初始化过程会通常分配特定的内存`cache`。当内存块释放时，它就会回归到原先分配它的`cache`中。

    一些经常用于保持`memory cache`的 _数据结构_：
 
    - *Socket buffer*
    
        在`net/core/sk_buff.c`中由`skb_init`分配，用于`sk_buff`缓存的分配。

    - *Neighboring protocla mappings*
    - *Routing tables*
  
    此处不赘述了。

    一些用于处理`memory cache`的内核方法：
  
    - `kmem_cache_create`
    - `kmem_cache_destory`
    - `kmem_cache_*****`

3. **其他**

   主要包括`垃圾回收`,`方法指针和虚指针表`和`互斥锁`。


## 关键的数据结构

1. **摘要**： 
    
    将会介绍下面的数据结构，提到一些操作这些数据结构的方法和宏定义。

    `struct sk_buff`

        这是数据包packet所存放的位置。这个数据结构被用在各个网络层来存储他们的header，payload和其他同来协调他们工作的信息。
    
    `struct net_device`

        在Linux内核中，每个网络设备都被这个数据结构所表示。其中包括硬件和软件设置的信息。

2. **套接字缓存：sk_buff:**
   
   `sk_buff`可以说是Linux网络中最重要的数据结构。其中的域可以大致分为以下几个部分：

   - layout
   - general
   - feature-specific
   - management functions
  
    这个数据结构会被多个不同的网络层所应用，而且其中的`fields`也会随层之间传递所改变。L4添加头部并传给L3...以此类推。这样做的原因是这是一种比直接拷贝数据更高效的方法。这样，第一件事就是触发`sk_reserve`方法来保留头部。当buffer缓存向上传递，之前的头部就不重要了。为了更节约CPU周期，指针会直接指向下一头部，而不是删除原来的头部。


    当数据包在线上被接收，SKB 就会通过网络设备驱动分配，主要是`netdev_alloc_skb()`。 有一些情况是需要丢弃数据包，这就需要`kfree_skb()`或`dev_kfree_skb()`，有一些SKB 的成员是在链路层中决定的。例如，`pkt_type`当以太网地址为多播时，设为`PACKET_MULTICAST`. 

    **Layout Fields**

    - [x] sk_buff介绍
      - [ ] layout fields
    - [ ] net_device介绍














        