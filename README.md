#  数据分析笔记分享

## I. SQL
### SQL书籍

- 必读：[《SQL必知必会》](https://github.com/SIHENG98/DA-NOTE/blob/main/part%20I%20SQL%E7%AC%94%E8%AE%B0/SQL%E5%BF%85%E7%9F%A5%E5%BF%85%E4%BC%9A-%E4%B8%AD%E6%96%87-%E7%AC%AC4%E7%89%88.pdf)
- 选读：[《SQL Cookbook》](https://github.com/SIHENG98/DA-NOTE/blob/main/part%20I%20SQL%E7%AC%94%E8%AE%B0/SQL%20Cookbook(%E4%B8%AD%E6%96%87%E7%89%88).pdf)
### 常用语法思维导图

- [SQL 常用语法思维导图](https://github.com/SIHENG98/DA-NOTE/blob/main/part%20I%20SQL%E7%AC%94%E8%AE%B0/SQL%20%E5%B8%B8%E7%94%A8%E8%AF%AD%E6%B3%95%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE.pdf)

  - 基础语法

    > 字符串的处理，时间函数的使用、分组、子查询、表联结

  - 进阶

    > 一些常见聚合函数的使用

  
---
## II. 业务分析方法论

### 基本方法(方法论)

#### 1. 指标分析

必备技能，重点包括指标体系的搭建及指标异动的分析

<img src="https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91-%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90.png" style="zoom:40%;" />

> 如何理解？
>
> - 在对齐业务目标后，会通过梳理业务流程来进行内容的梳理；
>
> - 在这个过程中，通过对各个环节进行**指标体系的搭建**，以高效地监测/衡量各个环节的状况 
>
>   这个过程中，首先明确核心指标是什么：比如在电商的用户增长期时(主要工作在拉新上)，首先重点关注用户增长指标，比如DAU、MAU等等
>
> - 在搭建完指标之后，需要定期监测各指标的变化；当某个指标发生高于阈值的变化时，需要对这个指标的异动进行解释(一般做拆解分析)，类似于统计学中的费米估计

&nbsp;

##### 1.1 指标异动分析案例-GMV下降分析

案例1: 某电商APP上个月的GMV(成交总额)下降了25%，请你分析一下具体原因

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

案例2: 假设某视频app从某日起日活DAU指标大幅下降。你会如何找出原因？

<img src="https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/DAU%E6%8B%86%E5%88%86%E5%85%AC%E5%BC%8F.png" style="zoom:20%;" />

[分析详情：DAU下降分析案例](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E5%BC%82%E5%8A%A8%E5%88%86%E6%9E%90-DAU%E4%B8%8B%E9%99%8D.pdf)

&nbsp;

##### 1.2 多指标异常分析

多个指标异常的时候，怎么判断哪个指标影响大？


**本质上就是贡献度的测算** [多指标异常归因的分析](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E5%A4%9A%E6%8C%87%E6%A0%87%E5%BC%82%E5%B8%B8%E5%BD%92%E5%9B%A0%E7%9A%84%E5%88%86%E6%9E%90.md)

&nbsp;

##### 1.3 指标的选择

用什么指标进行评估业务效果也是一个重要的课题


&nbsp;

案例1：用什么指标评估【app用户粘性】，提高用户粘性

- 用户层面
- 行为指标
- 产品指标


[分析详情：用什么指标提升用户粘度](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E6%8C%87%E6%A0%87%E9%80%89%E6%8B%A9%EF%BC%9A%E6%8F%90%E5%8D%87%E7%94%A8%E6%88%B7%E7%B2%98%E5%BA%A6.md)


&nbsp;

案例2：你觉得如何评估小红书的搜索功能做得好还是不好，可以使用哪些指标评估？

- 评估搜索功能的好坏：渗透率

- 评估搜索后质量：换query率


[分析详情：用什么指标评估搜索功能](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E6%8C%87%E6%A0%87%E9%80%89%E6%8B%A9%EF%BC%9A%E8%AF%84%E4%BC%B0%E6%90%9C%E7%B4%A2%E5%8A%9F%E8%83%BD.md)


&nbsp;

案例3：用什么指标评估【用户质量】，从而提高

首先明确产品品类，从而明确核心KPI，而后分析


[分析详情：用什么指标评估用户质量，并进行提升](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E6%8C%87%E6%A0%87%E9%80%89%E6%8B%A9%EF%BC%9A%E8%AF%84%E4%BC%B0%E7%94%A8%E6%88%B7%E8%B4%A8%E9%87%8F.md)

&nbsp;

##### 1.4 others：业务问题


案例1：指标口径和业务方不一致怎么办


[分析详情：指标口径不一致](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E6%8C%87%E6%A0%87%EF%BC%9A%E6%8C%87%E6%A0%87%E5%8F%A3%E5%BE%84%E5%92%8C%E4%B8%9A%E5%8A%A1%E6%96%B9%E4%B8%8D%E4%B8%80%E8%87%B4%E6%80%8E%E4%B9%88%E5%8A%9E.md)


&nbsp;

案例2：发现A城市充值率比B的高，怎么分析

参考指标异动分析，先横向拆解，再在每个分区中进行纵向分析(先有广度(多角度)，再深挖)


[分析详情：同指标对比](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E6%8C%87%E6%A0%87%EF%BC%9A%E5%8F%91%E7%8E%B0A%E5%9F%8E%E5%B8%82%E5%85%85%E5%80%BC%E7%8E%87%E6%AF%94B%E7%9A%84%E9%AB%98%EF%BC%8C%E6%80%8E%E4%B9%88%E5%88%86%E6%9E%90.md)


&nbsp;

案例3：广告策略带来了质量提升，但牺牲了数量，该如何抉择？

同上分析思路


[分析详情：广告策略带来了质量提升，但牺牲了数量，该如何抉择？](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E6%8C%87%E6%A0%87%EF%BC%9A%E5%B9%BF%E5%91%8A%E7%AD%96%E7%95%A5%E5%B8%A6%E6%9D%A5%E4%BA%86%E8%B4%A8%E9%87%8F%E6%8F%90%E5%8D%87%EF%BC%8C%E4%BD%86%E7%89%BA%E7%89%B2%E4%BA%86%E6%95%B0%E9%87%8F%EF%BC%8C%E8%AF%A5%E5%A6%82%E4%BD%95%E6%8A%89%E6%8B%A9%EF%BC%9F.md)


&nbsp;

案例4：业务理解：C端产品DAU与 MAU之间的差距能说明哪些问题?

不同的app 阶段，比值代表的意义是不一样的

- 产品初期，DAU/ MAU 比值越小，约说明增长空间大，比值约接近，约说明增长见顶；
- 产品中期，DAU /MAU 比值越小，说明用户粘性越小
&nbsp;

[分析详情：C端产品DAU与 MAU之间的差距能说明哪些问题](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E6%8C%87%E6%A0%87%EF%BC%9AC%E7%AB%AF%E4%BA%A7%E5%93%81DAU%E4%B8%8E%20MAU%E4%B9%8B%E9%97%B4%E7%9A%84%E5%B7%AE%E8%B7%9D%E8%83%BD%E8%AF%B4%E6%98%8E%E5%93%AA%E4%BA%9B%E9%97%AE%E9%A2%98.md)

---

### 2. 宏观分析



