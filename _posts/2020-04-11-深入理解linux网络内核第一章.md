<!--
 * @Author: xiangrui
 * @Date: 2020-04-11 16:29:04
 * @LastEditTime: 2020-04-12 09:31:30
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \Ten000hours.github.io\_posts\2020-04-11-understandLinuxNetworkKernel1.md
 -->
# 深入理解Linux网络内核---第一章

本文作为了解Linux网络内部结构和最佳实践的intro。 将会开一个系列文章系统的介绍网络内核的实现，探讨内容主要基于两本书：`<<understanding linux networking internels>>` 和 `<<linux kernel networking-impl and theory>>` 

## 在开始之前

1. **基本术语**：

L2  | link layer       
----  | ---- 
L3  | network layer  
L4  | transport layer 

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

    内核是通过双向链表来维持`sk_buff`的，但与一般的有所不同。和其他双向链表一样，有`next`和`prev`指向前和后节点。不过，要求每个节点都有指向链表头部，由`sk_buff_head`保持。代码如下：

    ```c
    struct sk_buff_head{
        struct sk_buff *next;
        struct sk_buff *prev;
        __u32 qlen;
        spinlock_t lock;
    };
    ```

    其他fields见书p26

    **General Fields**

    .....  

    `struct net_device *dev`
    
    该域描述了网络设备，并随数据包在缓存buffer中是刚接收到或将要发送而改变。当数据包刚被接收，设备驱动会用指向该数据结构的指针更新这个field，以代表接收接口。如以下方法，该方法会被3c59x以太网驱动在接收数据包时唤醒`drivers/net/3c59x.c`。

    ```c
    static int vortex_rx(struct net_device *dev){

        .........
        skb->dev=dev;
        skb->protocol=eth_type_trans(skb,dev);
        netif_rx(skb);
    }
    
    ```
    ......



    - [x] sk_buff介绍
      - [x] layout fields
      - [x] general fields
    - [ ] net_device介绍














        