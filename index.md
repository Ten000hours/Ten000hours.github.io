<!--

 * @Author: your name
 * @Date: 2020-03-02 22:10:49
 * @LastEditTime: 2020-07-28 15:00:11
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \Ten000hours.github.io\index.md
--> 

  {% seo %}
## 这是徐翔睿的博客





<u>**业务拥塞时，sdn如何实时验证其网络性能 ML？ Bayesian Optimization?**</u>


<u>**在不同业务如神经网络训练，如何用SDProber发现delay和控制？社交网**</u>

<u>**verfication forwarding loops & black holes**</u>


（2A）在这个领域内最常被引述的方法有哪些？
- HSA , 
- Anteater [397],
- NetPlumber [398], 
- VeriFlow [381],
- assertion languages [399] 


（2B）这些方法可以分为哪些主要的派别？

  - model checking (unexpected behaviors)
  - emulating large-scale network
  - Theorem proving
  - Symbolic Execution
  - testing( control plane and data plane)

![](2020-07-23-11-08-28.png)


（2C）每个角色派别的主要特色（含优缺点）是什么？


（3A）这篇论文的主要假设是什么（在什么条件下它是有效的），并且评估一下这些假设在现实条件下有多容易（多难）成立。越难成立的假设，越不好用，参考价值也越低。


（3B）在这些假设下，这篇论文主要有什么好处。


（3C）这些好处主要表现在那些公式的哪些项目的简化上。

---

## Digest 



| sentence                                                     | reference                                                    | reason                                                       |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Minerva is able to ameliorate the drawbacks of connection-level fairness by dynamically modifying a video's rate allocation to optimize a QoE fairness metric. | "End-to-End Transport for Video QoE Fairness"SigComm'19      | 1.学到新表达: ameliorate the drawbacks      2.句式简单但表达内容丰富(设计Minera的目的以及实现Minera的方式)，一句话的总结 |
| This naturalls the question of where to execute each service so as to better reap the benefits of available resources to serve as many requests as possible. | "Joint Service Placement and Request Routing in Multi-cell Mobile Edge Computing Networks" infocom'19 | 一.这句话出现在正文开头处，在介绍完必要的背景知识后，作者就用这样一句话，让读者很清楚的知道文章需要解决的是什么问题：1.文章需要解决的是一个优化问题   2.优化目标： serve as many request as possible. 3.限制条件：available resources 4.变量(待求参数)：where to execute each services 二.适用范围： 如果文章中需要解决的问题可以规约到一个优化问题，推荐使用该句式，帮助读者更快的理解作者思路，使得整个文章更容易follow. This naturally raises the question of ...(待求参数)... so as to better reap the benefits of ...(限制条件)... to .....(优化目标).....as..as possible. |
| Once a knowledge base is in place, semantic techniques can be used to analyse and suggest optimizations to service quality. | "Using a Semantic Knowledge Base for Communication Service Quality Management in Home Area Networks" | 简单表明两者关系，可以用于abstract的写作中                   |

---

## Tasks 

| Task                                                         | Due  |
| ------------------------------------------------------------ | ---- |
| how machine learning applied in SDN area                     |      |
| how SDProber perform in neural network training task         |      |
| 如何设计实验 ？模拟神经网络训练                                                                                                                                          <br>    *在Efficient measurement of round-trip link delays in software-defined networks中，实验环境搭建基于6个SDN switch，用1gbps的NIC （OVS)  通过floodlight做controller，算法跑在controller和monitor中，在Mininet平台上。* |      |
| 有相关工作吗 ？ SDN 和probe packet， **知识图谱**  有什么问题，如何用知识图谱解决的 |      |
|                                                              |      |
| ## 工作日志                                                  |      |

**有相关工作吗 ？ SDN 和probe packet， 知识图谱  有什么问题，如何用知识图谱解决的** : 未找到相关工作，仅找到Knowledge defined network 比较相关。传统的知识图谱应用比较少。                                                          

   在A Managing QoE Approach for Provisioning User Experience Aware Services Using SDN中，ontology构建的policy数*据库被用于比较提供的质量和预期质量*，来<u>检测QoE的降低</u>。

在Using a Semantic Knowledge Base for Communication Service Quality Management in Home Area Networks中，作者构建knowledge base来实现QoE的质量管理，这个知识库基于ontology和语义references。启示： 从terminal reports中的语义信息产生knowledge base用于报告终端。







**如何设计实验 ？模拟神经网络训练                                                                                                                                          **

​    在Efficient measurement of round-trip link delays in software-defined networks中，实验环境搭建基于6个SDN switch，用1gbps的NIC （OVS)  通过floodlight做controller，算法跑在controller和monitor中，在Mininet平台上。