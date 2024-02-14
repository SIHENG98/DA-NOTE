数据分析笔记分享
---
<details>

<summary>目录</summary>

- [I、SQL](#I、sql)
  - [SQL书籍](#sql书籍)
  - [常用语法思维导图](#常用语法思维导图)
  - [LeetCode刷题](#leetcode刷题)
- [II.业务分析方法论](#ii业务分析方法论)
  - [1、指标分析](#1、指标分析)
    - [1.1指标异动分析案例-GMV下降分析](#11指标异动分析案例-gmv下降分析)
    - [1.2多指标异常分析](#12多指标异常分析)
    - [1.3指标的选择](#13指标的选择)
    - [1.4others：业务问题](#14others：业务问题)
  - [2、行业、公司层面分析](#2、行业、公司层面分析)
    - [2.1宏观市场分析](#21宏观市场分析)
    - [2.2公司层面分析](#22公司层面分析)
    - [2.3思维风暴：如何理解互联网思维](#23思维风暴：如何理解互联网思维)
  - [3、产品层面分析](#3、产品层面分析)
    - [3.1产品评价](#31产品评价)
    - [3.2竞品分析](#32竞品分析)
    - [3.3产品需求迭代&产品改版](#33产品需求迭代产品改版)
    - [3.4产品需求分析/产品设计](#34产品需求分析产品设计)
    - [其他案例](#其他案例)
  - [4、用户体验分析](#4、用户体验分析)
    - [4.1用户画像建立](#41用户画像建立)
      - [标签类型](#标签类型)
    - [4.2通过产品，拆解用户使用的生命周期](#42通过产品，拆解用户使用的生命周期)
    - [4.3用户体验评估](#43用户体验评估)
      - [1）常见模型](#1）常见模型)
      - [2）用户体验分析框架](#2）用户体验分析框架)
  - [5、用户经营](#5、用户经营)
    - [5.1种子用户如何获取(用户增长/拉新)](#51种子用户如何获取用户增长拉新)
    - [5.2用户留存](#52用户留存)
      - [(1)如何判断即将流失的用户、已流失用户](#1如何判断即将流失的用户、已流失用户)
      - [(2)用户留存一般步骤](#2用户留存一般步骤)
      - [(3)保证用户粘性](#3保证用户粘性)
  - [6、活动评价](#6、活动评价)
  - [7、其他内容](#7、其他内容)
    - [7.1一些模型总结](#71一些模型总结)
    - [7.2早期文档(未梳理)](#72早期文档未梳理)
- [III实验方法](#iii实验方法)
  - [1.预备知识：数理统计](#1预备知识：数理统计)
  - [2.AB实验](#2ab实验)
  - [3.因果推断方法](#3因果推断方法)
  
</details>

---

# I、SQL
## SQL书籍

- 必读：[《SQL必知必会》](https://github.com/SIHENG98/DA-NOTE/blob/main/part%20I%20SQL%E7%AC%94%E8%AE%B0/SQL%E5%BF%85%E7%9F%A5%E5%BF%85%E4%BC%9A-%E4%B8%AD%E6%96%87-%E7%AC%AC4%E7%89%88.pdf)
- 选读：[《SQL Cookbook》](https://github.com/SIHENG98/DA-NOTE/blob/main/part%20I%20SQL%E7%AC%94%E8%AE%B0/SQL%20Cookbook(%E4%B8%AD%E6%96%87%E7%89%88).pdf)
## 常用语法思维导图

- [SQL 常用语法思维导图](https://github.com/SIHENG98/DA-NOTE/blob/main/part%20I%20SQL%E7%AC%94%E8%AE%B0/SQL%20%E5%B8%B8%E7%94%A8%E8%AF%AD%E6%B3%95%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE.pdf)

  - 基础语法

    > 字符串的处理，时间函数的使用、分组、子查询、表联结

  - 进阶

    > 一些常见聚合函数的使用

## LeetCode刷题
[LeetCode SQL题库](https://leetcode.cn/problemset/database/?status=AC)
  
---
# II.业务分析方法论


## 1、指标分析

必备技能，重点包括指标体系的搭建及指标异动的分析

<img src="https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/0-%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91-%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90.png" style="zoom:40%;" />

> 如何理解？
>
> - 在对齐业务目标后，会通过梳理业务流程来进行内容的梳理；
>
> - 在这个过程中，通过对各个环节进行**指标体系的搭建**，以高效地监测/衡量各个环节的状况 
>
>   要达到上述的目标，首先明确核心指标是什么：比如在电商的用户增长期时(主要工作在拉新上)，首先重点关注用户增长指标，比如DAU、MAU等等
>
> - 在搭建完指标之后，需要定期监测各指标的变化；当某个指标发生高于阈值的变化时，需要对这个指标的异动进行解释(一般做拆解分析)，类似于统计学中的费米估计

&nbsp;

### 1.1指标异动分析案例-GMV下降分析

**案例1: 某电商APP上个月的GMV(成交总额)下降了25%，请你分析一下具体原因**

> 拆分思路：
>
> 1. 对GMV 的计算方式进行拆解
>
>    $$
>    GMV=订单数\times 订单均价
>    $$
>
> 2. 针对订单数及订单均价进行下钻分析


[分析详情：GMV下降分析案例](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E5%BC%82%E5%8A%A8%E5%88%86%E6%9E%90-GMV%E4%B8%8B%E9%99%8D.pdf)


&nbsp;

**案例2: 假设某视频app从某日起日活DAU指标大幅下降。你会如何找出原因？**

<img src="https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/DAU%E6%8B%86%E5%88%86%E5%85%AC%E5%BC%8F.png" style="zoom:5%;" />

[分析详情：DAU下降分析案例](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E5%BC%82%E5%8A%A8%E5%88%86%E6%9E%90-DAU%E4%B8%8B%E9%99%8D.pdf)

&nbsp;

### 1.2多指标异常分析

多个指标异常的时候，怎么判断哪个指标影响大？
> 详细地说，就是**当多个因素混合导致整体指标下跌的情境下，各个因素对指标波动的影响程度分别是多少？**

**本质上就是贡献度的测算** [多指标异常归因的分析](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E5%A4%9A%E6%8C%87%E6%A0%87%E5%BC%82%E5%B8%B8%E5%BD%92%E5%9B%A0%E7%9A%84%E5%88%86%E6%9E%90.md)

&nbsp;

### 1.3指标的选择

用什么指标进行评估业务效果也是一个重要的课题，但核心思想还是一致地，就是基于业务的最终目标(甚至是部门的定位)以确定具体的北极星指标。
> 例如，对于华为的用户体验团队，对于用户的口碑比较看重，因此能够反映该业务目标的现网舆情(好评率/风险舆情)以及NPS是我们考察的指标；对于美团的客服及体验团队，团队目标是尽可能接通以及降低相关投诉率，因此客服接通率及相关万服(万订单服务量)就是需要考核的核心指标。


&nbsp;

**案例1：用什么指标评估【app用户粘性】，提高用户粘性**

- 用户层面
- 行为指标
- 产品指标


[分析详情：用什么指标提升用户粘度](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E6%8C%87%E6%A0%87%E9%80%89%E6%8B%A9%EF%BC%9A%E6%8F%90%E5%8D%87%E7%94%A8%E6%88%B7%E7%B2%98%E5%BA%A6.md)


&nbsp;

**案例2：你觉得如何评估小红书的搜索功能做得好还是不好，可以使用哪些指标评估？**

- 评估搜索功能的好坏：渗透率

- 评估搜索后质量：换query率


[分析详情：用什么指标评估搜索功能](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E6%8C%87%E6%A0%87%E9%80%89%E6%8B%A9%EF%BC%9A%E8%AF%84%E4%BC%B0%E6%90%9C%E7%B4%A2%E5%8A%9F%E8%83%BD.md)


&nbsp;

**案例3：用什么指标评估【用户质量】，从而提高**

首先明确产品品类，从而明确核心KPI，而后分析


[分析详情：用什么指标评估用户质量，并进行提升](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E6%8C%87%E6%A0%87%E9%80%89%E6%8B%A9%EF%BC%9A%E8%AF%84%E4%BC%B0%E7%94%A8%E6%88%B7%E8%B4%A8%E9%87%8F.md)

&nbsp;

### 1.4others：业务问题


**案例1：指标口径和业务方不一致怎么办**


[分析详情：指标口径不一致](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E6%8C%87%E6%A0%87%EF%BC%9A%E6%8C%87%E6%A0%87%E5%8F%A3%E5%BE%84%E5%92%8C%E4%B8%9A%E5%8A%A1%E6%96%B9%E4%B8%8D%E4%B8%80%E8%87%B4%E6%80%8E%E4%B9%88%E5%8A%9E.md)


&nbsp;

**案例2：发现A城市充值率比B的高，怎么分析**

参考指标异动分析，先横向拆解，再在每个分区中进行纵向分析(先有广度(多角度)，再深挖)


[分析详情：同指标对比](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E6%8C%87%E6%A0%87%EF%BC%9A%E5%8F%91%E7%8E%B0A%E5%9F%8E%E5%B8%82%E5%85%85%E5%80%BC%E7%8E%87%E6%AF%94B%E7%9A%84%E9%AB%98%EF%BC%8C%E6%80%8E%E4%B9%88%E5%88%86%E6%9E%90.md)


&nbsp;

**案例3：广告策略带来了质量提升，但牺牲了数量，该如何抉择？**

同上分析思路


[分析详情：广告策略带来了质量提升，但牺牲了数量，该如何抉择？](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E6%8C%87%E6%A0%87%EF%BC%9A%E5%B9%BF%E5%91%8A%E7%AD%96%E7%95%A5%E5%B8%A6%E6%9D%A5%E4%BA%86%E8%B4%A8%E9%87%8F%E6%8F%90%E5%8D%87%EF%BC%8C%E4%BD%86%E7%89%BA%E7%89%B2%E4%BA%86%E6%95%B0%E9%87%8F%EF%BC%8C%E8%AF%A5%E5%A6%82%E4%BD%95%E6%8A%89%E6%8B%A9%EF%BC%9F.md)


&nbsp;

**案例4：业务理解：C端产品DAU与 MAU之间的差距能说明哪些问题?**

不同的app 阶段，比值代表的意义是不一样的

- 产品初期，DAU/ MAU 比值越小，约说明增长空间大，比值约接近，约说明增长见顶；
- 产品中期，DAU /MAU 比值越小，说明用户粘性越小

&nbsp;

[分析详情：C端产品DAU与 MAU之间的差距能说明哪些问题](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E6%8C%87%E6%A0%87%EF%BC%9AC%E7%AB%AF%E4%BA%A7%E5%93%81DAU%E4%B8%8E%20MAU%E4%B9%8B%E9%97%B4%E7%9A%84%E5%B7%AE%E8%B7%9D%E8%83%BD%E8%AF%B4%E6%98%8E%E5%93%AA%E4%BA%9B%E9%97%AE%E9%A2%98.md)

---

## 2、行业、公司层面分析

<img src="https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/0-%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91-%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE/7-%E8%A1%8C%E4%B8%9A%E3%80%81%E5%85%AC%E5%8F%B8%E5%88%86%E6%9E%90.png" style="zoom:40%;" />

&nbsp;

### 2.1宏观市场分析

**通常用来分析外部环境对某一业务指标的影响，以及是否开拓新市场等问题**

**方法1: 宏观环境：PEST方法**

- Politics: 政策变化
- Economy：短期内竞争环境，以及市场整体经济情况
- Society：行业舆论、用户生活方式变化、消费心理、价值观
- Technology：创新方案的出现，分销方式的变化

&nbsp;

**方法2: 行业发展分析**

- 行业发展周期
- 用户需求：能满足什么样的用户需求，痛点是什么
- 利润水平
- 行业壁垒、行业风险
- 国际化战略（未来

&nbsp;

**案例：如何判断某行业的发展状况**

分析思路：[如何判断某行业的发展状况](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/2-%E8%A1%8C%E4%B8%9A%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E5%A6%82%E4%BD%95%E5%88%A4%E6%96%AD%E6%9F%90%E8%A1%8C%E4%B8%9A%E5%8F%91%E5%B1%95%E6%83%85%E5%86%B5.md)

&nbsp;

### 2.2公司层面分析

**公司评估**

1. **公司层面**

   - 公司产品线、各产品定位
   - 市场份额
   - 用户组成：用户画像

2. **产品层面** 

   方法：用户体验五要素

3. **威胁与未来** 

   - 技术壁垒
   - 创新潜力
   - 国际化战略
   - 当前/未来资金情况

&nbsp;

**公司对比**

1. 两个公司所在**行业分析**
2. 公司评估(参考上述方法)
3. 产品层面分析
4. 收入来源、产品/战略布局、长期适应性

&nbsp;


**案例1：如何评价抖音和快手的竞争**

本质上就是两个公司的对比

[分析思路：抖音VS快手](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/2-%E8%A1%8C%E4%B8%9A%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E5%A6%82%E4%BD%95%E8%AF%84%E4%BB%B7%E6%8A%96%E9%9F%B3%E5%92%8C%E5%BF%AB%E6%89%8B%E7%9A%84%E7%AB%9E%E4%BA%89.md)


&nbsp;

**案例2：你觉得腾讯为什么会这么成功？**

分析思路：[案例：公司优势分析-腾讯](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/2-%E8%A1%8C%E4%B8%9A%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E5%85%AC%E5%8F%B8%E4%BC%98%E5%8A%BF%E5%88%86%E6%9E%90-%E8%85%BE%E8%AE%AF.pdf)

&nbsp;

### 2.3思维风暴：如何理解互联网思维

> **回答仅表示个人理解**
>
> &nbsp;
> 
> 注意：思考的时候也要有相关的行业分析框架，如何去评价/衡量一个行业的发展


[如何理解互联网思维](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/2-%E8%A1%8C%E4%B8%9A%E5%88%86%E6%9E%90/%E5%A6%82%E4%BD%95%E7%90%86%E8%A7%A3%E4%BA%92%E8%81%94%E7%BD%91%E6%80%9D%E7%BB%B4.pdf)


&nbsp;


---

## 3、产品层面分析 

<img src="https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/0-%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91-%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE/2-%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90.png" style="zoom:30%;" />

&nbsp;

### 3.1产品评价
<details>

<summary>产品评价思路</summary>


1. **明确产品定位**  

   - 目标群体是谁 $\Rightarrow$ 他们的痛点是什么 
   - 以此，我们的赢利点在哪里

2. **产品使用场景及使用逻辑**

   通过总结用户使用场景及使用习惯，回答以下问题：

   - 用户使用需求频率及强度如何
   - 产生需求的场景有哪些

3. **市场分析**

   - 市场现状：规模、当前利润率
   - 市场进一步的发展方向

4. 总体数据表现（指标体系）

   - 使用情况
   - 口碑
   - 经营情况

5. 产品的痛点问题
   参考用户体验五要素

6. 竞品对比
   - 非功能性方面
     - 安全/性能
     - 运营情况、口碑
   - 功能性
     - 视觉/UI
     - 交互
     - 产品功能

</details>


&nbsp;

> 详细分析思路：
>
> [方法论：评价产品/产品功能的好坏](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/3-%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9A%E8%AF%84%E4%BB%B7%E4%BA%A7%E5%93%81%E5%A5%BD%E5%9D%8F.pdf)


&nbsp;

**案例1：评价小红书这个app**

[分析思路：评价小红书](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/3-%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E6%97%A5%E5%B8%B8%E4%BD%BF%E7%94%A8%E7%9A%84%E4%BA%A7%E5%93%81%E8%AF%84%E4%BB%B7.pdf)

> *用户体验五要素方法，如何穿插在分析中
>
> 案例：[用户体验五要素分析——微信读书](https://www.woshipm.com/evaluating/3119632.html)

&nbsp;


**[思维发散] 案例2：分析产品/产品功能的缺点及提出改进方法**

> 关注在战略角度及产品使用流程改进

- 分析ATM机的缺点及改建建议

  [案例分析：ATM机](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/3-%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E5%88%86%E6%9E%90ATM%E6%9C%BA%E7%9A%84%E7%BC%BA%E7%82%B9%E5%92%8C%E6%94%B9%E8%BF%9B%E6%96%B9%E6%B3%95.pdf)

&nbsp;

- 给出滴滴打车功能的改进建议(先进行缺点分析)

  [案例分析：滴滴打车](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/3-%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E5%88%86%E6%9E%90%E6%BB%B4%E6%BB%B4%E6%89%93%E8%BD%A6%E7%BC%BA%E7%82%B9%E5%92%8C%E6%94%B9%E8%BF%9B%E6%96%B9%E6%B3%95.pdf)

&nbsp;

**[数据表现]案例3：作为数据分析师如何衡量淘宝推荐系统好还是不好**

> 重点：特定领域指标的选取

分析思路：[案例分析：作为数据分析师如何衡量淘宝推荐系统好还是不好](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/3-%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E4%BD%9C%E4%B8%BA%E6%95%B0%E6%8D%AE%E5%88%86%E6%9E%90%E5%B8%88%E5%A6%82%E4%BD%95%E8%A1%A1%E9%87%8F%E6%B7%98%E5%AE%9D%E6%8E%A8%E8%8D%90%E7%B3%BB%E7%BB%9F%E5%A5%BD%E8%BF%98%E6%98%AF%E4%B8%8D%E5%A5%BD.pdf)

&nbsp;

### 3.2竞品分析

> 方法论参考上图思维导图

&nbsp;

**案例1：产品对比分析**

怎么看微信的公众号和百度的直达号，哪个更有优势？

[案例：竞品分析腾讯公众号vs百度直达号](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E7%AB%9E%E5%93%81%E5%88%86%E6%9E%90%E8%85%BE%E8%AE%AF%E5%85%AC%E4%BC%97%E5%8F%B7vs%E7%99%BE%E5%BA%A6%E7%9B%B4%E8%BE%BE%E5%8F%B7.pdf)

&nbsp;

百度知道和知乎的区别在哪里？

[案例：竞品分析百度vs知乎](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E7%AB%9E%E5%93%81%E5%88%86%E6%9E%90%E7%99%BE%E5%BA%A6vs%E7%9F%A5%E4%B9%8E.pdf)

&nbsp;

### 3.3产品需求迭代&产品改版

方法论参考上图思维导图

> 具体方法论：[方法论：产品改版](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/3-%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9A%E4%BA%A7%E5%93%81%E6%94%B9%E7%89%88.pdf)

&nbsp;

### 3.4产品需求分析/产品设计

用户提出需求/存在潜在需求，如何通过进一步分析用户需求满足产品功能

> 1. 分析需求
> 2. 分析满足需求的路径
> 3. 给出效果图。

[方法论：需求分析和结果设计](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/3-%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9A%E9%9C%80%E6%B1%82%E5%88%86%E6%9E%90%E5%92%8C%E7%BB%93%E6%9E%9C%E8%AE%BE%E8%AE%A1.pdf)

[方法论：需求分析详解（用户痛点分析）](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/3-%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9A%E7%94%A8%E6%88%B7%E7%97%9B%E7%82%B9%E5%88%86%E6%9E%90.pdf)

&nbsp;

PS：在进行分析的时候，适当参考互联网层面的产品模式以及不同载体(移动端/PC端)的特点

> 互联网层面产品模式及不同载体特点：
>
> [参考：互联网产品模式及各载体特点](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/3-%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E5%8F%82%E8%80%83%EF%BC%9A%E4%BA%92%E8%81%94%E7%BD%91%E4%BA%A7%E5%93%81%E6%A8%A1%E5%BC%8F.pdf)

&nbsp;

**案例1：分析‘‘小蛮腰’’被搜索的时候的需求，满足需求的路径是什么，并给出搜索结果效果图**

> 思路：[案例：产品需求分析-小蛮腰](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/3-%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E4%BA%A7%E5%93%81%E9%9C%80%E6%B1%82%E5%88%86%E6%9E%90-%E5%B0%8F%E8%9B%AE%E8%85%B0.pdf)

&nbsp;

**案例2：满足用户痛点**

> 1. 整理产品的基本功能
>
> 2. 分析目标用户特点
>
> 3. 产品设计

&nbsp;

- **为失明的人设计一款钟表** 

  分析思路：[案例：为失明的人设计一款钟表](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/3-%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E4%B8%BA%E5%A4%B1%E6%98%8E%E7%9A%84%E4%BA%BA%E8%AE%BE%E8%AE%A1%E4%B8%80%E6%AC%BE%E9%92%9F%E8%A1%A8.pdf)



- **如果男生有可能怀孕，会产生什么新的诉求，新的产品出现？**

  分析思路：[案例：用户需求脑洞拓展](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/3-%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E7%94%A8%E6%88%B7%E9%9C%80%E6%B1%82%E8%84%91%E6%B4%9E%E6%8B%93%E5%B1%95.pdf)

&nbsp;

### 其他案例

 **分析：如何证明一部分用户的增长是由某一个功能带来的**

分析思路：[分析：如何证明一部分用户的增长是由某一个功能带来的](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/3-%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E5%88%86%E6%9E%90%EF%BC%9A%E5%A6%82%E4%BD%95%E8%AF%81%E6%98%8E%E4%B8%80%E9%83%A8%E5%88%86%E7%94%A8%E6%88%B7%E7%9A%84%E5%A2%9E%E9%95%BF%E6%98%AF%E7%94%B1%E6%9F%90%E4%B8%80%E4%B8%AA%E5%8A%9F%E8%83%BD%E5%B8%A6%E6%9D%A5%E7%9A%84.pdf)



---



## 4、用户体验分析

### 4.1用户画像建立

用户画像的本质是**打标签**，也就是将用户的每个具体信息抽象成标签，利用这些标签将用户形象具体化，从而为用户提供有针对性的服务。他对于业务分析的意义在于，当建立起某一类用户的画像后，代入该群体，以该群体的视角去分析具体的业务问题，也就是**建立用户同理心**。



#### 标签类型

一般来说，画像的标签分为以下三类：

- 基于用户自身的天然维度，包括用户特征以及社会特征
- 给定使用app/产品的行为，并统计用户在使用这些行为的数据表现(使用率、使用频次等等)
- 总结出用户在使用产品时的偏好

<img src="https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/0-%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91-%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE/3-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90.png" style="zoom:40%;" />

> 如何串联起来进行理解：
>
> xxx类型的用户，在使用我们的产品时他们在A、B、C、D的消费行为的强度分别是…..，因此可以总结出，该类用户群体有xxx的行为偏好，对于激活/留存/盈利转化的参考意义是…

&nbsp;

<details>

<summary>Example：某一类用户群体有这样的特征</summary>

- 基础特征
  > 男，25-30岁，未婚，收入2-3万(白领)，爱美食，科技控，喜欢美女、喜欢旅游、有车
- 行为特征
  > 一周以内在社交类、影音类、游戏类、办公类的时间分配占比为….，消费金额占比为…
- 偏好特征
  > 偏好游戏类app，体现在日均使用时长长，且充值频率高，充值金额大

</details>

&nbsp;


### 4.2通过产品，拆解用户使用的生命周期

<img width="656" alt="image" src="https://github.com/SIHENG98/DA-NOTE/assets/141550400/793194e2-d318-49d4-bbb9-2cff3b0722f5">


具体介绍：[方法论：用户的生命周期及其划分](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/4-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/4.1-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9A%E7%94%A8%E6%88%B7%E7%9A%84%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E5%8F%8A%E5%85%B6%E5%88%92%E5%88%86.pdf)

&nbsp;

### 4.3用户体验评估

#### 1）常见模型

- **漏斗模型**

  用来监测用户使用的各个流程转化率，找出有问题的环节

  [方法论：漏斗模型](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/4-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/4.1-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9A%E6%BC%8F%E6%96%97%E6%A8%A1%E5%9E%8B.pdf)

- **AARRR模型**

  主要关注用户参与度和收益
  [方法论：AARRR](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/4-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/4.1-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9AAARRR.pdf)
  

#### 2）用户体验分析框架

<img width="464" alt="image" src="https://github.com/SIHENG98/DA-NOTE/assets/141550400/57a56dd5-7354-493f-9206-f5531dc28e9b">

<details>

<summary>总结来说，就是在建立用户同理心的基础上，分析产品/功能的体验问题，具体为 </summary>


- 明确分析目的
- 当前使用表现(指标体系)、用户口碑、主观数据反映的问题(舆情/客诉)
- 建立用户同理心的基础上(用户画像)，梳理产品使用逻辑并归纳各个流程的问题，并进行拆解分析
- 总结问题，升华问题
- 问题解决闭环(沟通能力)

</details>


PS：这一块算是数据分析师核心能力的体现，笔主也没有在较短的篇章内很好的梳理其中的细节，并且提供的案例因为涉及保密信息，会比较晦涩而简短，但方法论还是一样的，需要各个同学在实习中总结感悟。

**我的终极理解是：数据分析就像讲故事，把背景、起因、经过、结果讲清楚（自行体会）**

&nbsp;

案例分享：在华子时分析的某个项目

[案例：用户体验分析](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/4-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/4.1-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E7%94%A8%E6%88%B7%E4%BD%93%E9%AA%8C%E5%88%86%E6%9E%90.pdf)



---



## 5、用户经营

包括用户的拉新及留存

<img src="https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/0-%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91-%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE/4-%E7%94%A8%E6%88%B7%E7%BB%8F%E8%90%A5.png" style="zoom:40%;" />

### 5.1种子用户如何获取(用户增长/拉新)

仅限参考，因为笔主之前的经历主要在用户体验上，在用户增长方面就类似于小白

[方法论：种子用户的获取](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/4-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/4.2-%E7%94%A8%E6%88%B7%E7%BB%8F%E8%90%A5%26%E7%94%A8%E6%88%B7%E6%B5%81%E5%A4%B1/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9A%E7%A7%8D%E5%AD%90%E7%94%A8%E6%88%B7%E7%9A%84%E8%8E%B7%E5%8F%96.pdf)

&nbsp;

**案例1：如何快速满足客户需求**

刚下班的小明接到了远在广西南宁的老爸的电话，他这个月刚学会用电脑，今天终于托人帮忙装了台新电脑，并办好了上网，他问小明现在用电脑和上网都能玩些啥。假如你是小明，需要在最短的时间内满足老爸的需求，你会怎么做？

[案例：如何快速满足客户需求](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/4-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/4.2-%E7%94%A8%E6%88%B7%E7%BB%8F%E8%90%A5%26%E7%94%A8%E6%88%B7%E6%B5%81%E5%A4%B1/%E6%A1%88%E4%BE%8B%EF%BC%9A%E5%A6%82%E4%BD%95%E5%BF%AB%E9%80%9F%E6%BB%A1%E8%B6%B3%E5%AE%A2%E6%88%B7%E9%9C%80%E6%B1%82.pdf)

&nbsp;

**案例2：xxx用户为什么更喜欢xxx产品**

为何年轻人用QQ邮箱的居多？

[案例：xxx用户更喜欢xxx产品](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/4-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/4.2-%E7%94%A8%E6%88%B7%E7%BB%8F%E8%90%A5%26%E7%94%A8%E6%88%B7%E6%B5%81%E5%A4%B1/%E6%A1%88%E4%BE%8B%EF%BC%9Axxx%E7%94%A8%E6%88%B7%E6%9B%B4%E5%96%9C%E6%AC%A2xxx%E4%BA%A7%E5%93%81.pdf)

&nbsp;

**方法论：用什么指标评估【用户质量】，提高用户质量**

[方法论：用什么指标评估【用户质量】，提高用户质量](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/4-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/4.2-%E7%94%A8%E6%88%B7%E7%BB%8F%E8%90%A5%26%E7%94%A8%E6%88%B7%E6%B5%81%E5%A4%B1/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9A%E7%94%A8%E4%BB%80%E4%B9%88%E6%8C%87%E6%A0%87%E8%AF%84%E4%BC%B0%E3%80%90%E7%94%A8%E6%88%B7%E8%B4%A8%E9%87%8F%E3%80%91%EF%BC%8C%E6%8F%90%E9%AB%98%E7%94%A8%E6%88%B7%E8%B4%A8%E9%87%8F.pdf)

RFM模型：用以对用户分类，识别出有价值的用户 [参考：RFM模型](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/4-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/4.2-%E7%94%A8%E6%88%B7%E7%BB%8F%E8%90%A5%26%E7%94%A8%E6%88%B7%E6%B5%81%E5%A4%B1/%E5%8F%82%E8%80%83%EF%BC%9ARFM%E6%A8%A1%E5%9E%8B.pdf)

&nbsp;

### 5.2用户留存

<img src="https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/0-%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91-%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE/5-%E7%94%A8%E6%88%B7%E6%B5%81%E5%A4%B1%E5%88%86%E6%9E%90.png" style="zoom:40%;" />



#### (1)如何判断即将流失的用户、已流失用户

[方法论：如何判断即将流失的用户，以及已流失用户](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/0-%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91-%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE/7-%E8%A1%8C%E4%B8%9A%E3%80%81%E5%85%AC%E5%8F%B8%E5%88%86%E6%9E%90.xmind)

&nbsp;

#### (2)用户留存一般步骤

[方法论：用户留存一般步骤 ](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/4-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/4.2-%E7%94%A8%E6%88%B7%E7%BB%8F%E8%90%A5%26%E7%94%A8%E6%88%B7%E6%B5%81%E5%A4%B1/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9A%E7%94%A8%E6%88%B7%E7%95%99%E5%AD%98%E4%B8%80%E8%88%AC%E6%AD%A5%E9%AA%A4%20.pdf)

- 评估留存难度
- 确定留存思路/方案

&nbsp;

> 如何做流失用户召回？
>
> [方法论：如何召回流失用户](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/4-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/4.2-%E7%94%A8%E6%88%B7%E7%BB%8F%E8%90%A5%26%E7%94%A8%E6%88%B7%E6%B5%81%E5%A4%B1/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9A%E5%A6%82%E4%BD%95%E5%8F%AC%E5%9B%9E%E6%B5%81%E5%A4%B1%E7%94%A8%E6%88%B7.pdf)

&nbsp;

**案例1：新老用户流失分析**

[案例：用户流失分析](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/4-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/4.2-%E7%94%A8%E6%88%B7%E7%BB%8F%E8%90%A5%26%E7%94%A8%E6%88%B7%E6%B5%81%E5%A4%B1/%E6%A1%88%E4%BE%8B%EF%BC%9A%E7%94%A8%E6%88%B7%E6%B5%81%E5%A4%B1%E5%88%86%E6%9E%90.pdf)

&nbsp;

#### (3)保证用户粘性

**TAM模型**

技术接受模型（TAM）是一种用于评估和解释人们使用新技术的意愿和行为的模型。

[方法论：TAM模型](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/4-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/4.2-%E7%94%A8%E6%88%B7%E7%BB%8F%E8%90%A5%26%E7%94%A8%E6%88%B7%E6%B5%81%E5%A4%B1/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9ATAM%E6%A8%A1%E5%9E%8B.md)

&nbsp;

**提高用户参与度与用户使用时长**

[方法论：提高用户参与度与用户使用时长](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/4-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/4.2-%E7%94%A8%E6%88%B7%E7%BB%8F%E8%90%A5%26%E7%94%A8%E6%88%B7%E6%B5%81%E5%A4%B1/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9A%E6%8F%90%E9%AB%98%E7%94%A8%E6%88%B7%E5%8F%82%E4%B8%8E%E5%BA%A6%E4%B8%8E%E7%94%A8%E6%88%B7%E4%BD%BF%E7%94%A8%E6%97%B6%E9%95%BF.pdf)

&nbsp;

**提升用户价值**

梳理使用路径 $\Rightarrow$ 使用路径优化 $\Rightarrow$ 用户分层运营(RFM)

[方法论：如何提升用户价值](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/4-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/4.2-%E7%94%A8%E6%88%B7%E7%BB%8F%E8%90%A5%26%E7%94%A8%E6%88%B7%E6%B5%81%E5%A4%B1/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9A%E5%A6%82%E4%BD%95%E6%8F%90%E5%8D%87%E7%94%A8%E6%88%B7%E4%BB%B7%E5%80%BC.pdf)

&nbsp;

**提升指标：活跃点评用户数**

从用户体验的生命周期：吸引用户、转化用户、留住用户

[方法论：提升指标【活跃点评用户数】](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/4-%E7%94%A8%E6%88%B7%E5%88%86%E6%9E%90/4.2-%E7%94%A8%E6%88%B7%E7%BB%8F%E8%90%A5%26%E7%94%A8%E6%88%B7%E6%B5%81%E5%A4%B1/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9A%E6%8F%90%E5%8D%87%E6%8C%87%E6%A0%87%E3%80%90%E6%B4%BB%E8%B7%83%E7%82%B9%E8%AF%84%E7%94%A8%E6%88%B7%E6%95%B0%E3%80%91.pdf)

&nbsp;

---

## 6、活动评价

<img src="https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/0-%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91-%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE/6-%E6%B4%BB%E5%8A%A8%E8%AF%84%E4%BB%B7.png" style="zoom:40%;" />


**案例：预估电商大促效果**

[案例：预估电商大促效果](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/5-%E6%B4%BB%E5%8A%A8%E6%95%88%E6%9E%9C%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E9%A2%84%E4%BC%B0%E7%94%B5%E5%95%86%E5%A4%A7%E4%BF%83%E6%95%88%E6%9E%9C.pdf)

&nbsp;

---

## 7、其他内容



### 7.1一些模型总结



<img src="https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/0-%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91-%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE/8-%E5%85%B6%E4%BB%96%E6%96%B9%E6%B3%95.png" style="zoom:40%;" />



### 7.2早期文档(未梳理)

产品sense培养：[产品sense](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/6-others/%E4%BA%A7%E5%93%81sense.pdf)

数据分析方法：[数据分析方法](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/6-others/%E6%95%B0%E6%8D%AE%E5%88%86%E6%9E%90%E6%96%B9%E6%B3%95.pdf)、[业务面试准备](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/6-others/%E4%B8%9A%E5%8A%A1%E9%9D%A2%E8%AF%95%E5%87%86%E5%A4%87.pdf)

&nbsp;

---

# III实验方法

## 1.预备知识：数理统计

## 2.AB实验

## 3.因果推断方法
































