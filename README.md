数据分析笔记分享

# I. SQL
## SQL书籍

- 必读：[《SQL必知必会》](https://github.com/SIHENG98/DA-NOTE/blob/main/part%20I%20SQL%E7%AC%94%E8%AE%B0/SQL%E5%BF%85%E7%9F%A5%E5%BF%85%E4%BC%9A-%E4%B8%AD%E6%96%87-%E7%AC%AC4%E7%89%88.pdf)
- 选读：[《SQL Cookbook》](https://github.com/SIHENG98/DA-NOTE/blob/main/part%20I%20SQL%E7%AC%94%E8%AE%B0/SQL%20Cookbook(%E4%B8%AD%E6%96%87%E7%89%88).pdf)
## 常用语法思维导图

- [SQL 常用语法思维导图](https://github.com/SIHENG98/DA-NOTE/blob/main/part%20I%20SQL%E7%AC%94%E8%AE%B0/SQL%20%E5%B8%B8%E7%94%A8%E8%AF%AD%E6%B3%95%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE.pdf)

  - 基础语法

    > 字符串的处理，时间函数的使用、分组、子查询、表联结

  - 进阶

    > 一些常见聚合函数的使用

  
---
# II. 业务分析方法论


## 1. 指标分析

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

### 1.1 指标异动分析案例-GMV下降分析

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

### 1.2 多指标异常分析

多个指标异常的时候，怎么判断哪个指标影响大？


**本质上就是贡献度的测算** [多指标异常归因的分析](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/1-%E6%8C%87%E6%A0%87%E5%88%86%E6%9E%90/%E5%A4%9A%E6%8C%87%E6%A0%87%E5%BC%82%E5%B8%B8%E5%BD%92%E5%9B%A0%E7%9A%84%E5%88%86%E6%9E%90.md)

&nbsp;

### 1.3 指标的选择

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

### 1.4 others：业务问题


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

## 2. 行业、公司层面分析

<img src="https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91-%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE/7-%E8%A1%8C%E4%B8%9A%E3%80%81%E5%85%AC%E5%8F%B8%E5%88%86%E6%9E%90.png" style="zoom:40%;" />

&nbsp;

### 2.1 宏观市场分析

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

分析思路：[如何判断某行业的发展状况](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E8%A1%8C%E4%B8%9A%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B-%E5%A6%82%E4%BD%95%E5%88%A4%E6%96%AD%E6%9F%90%E8%A1%8C%E4%B8%9A%E5%8F%91%E5%B1%95%E6%83%85%E5%86%B5.md)

&nbsp;

### 2.2 公司层面分析

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

[分析思路：抖音VS快手](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E8%A1%8C%E4%B8%9A%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E5%A6%82%E4%BD%95%E8%AF%84%E4%BB%B7%E6%8A%96%E9%9F%B3%E5%92%8C%E5%BF%AB%E6%89%8B%E7%9A%84%E7%AB%9E%E4%BA%89.md)


&nbsp;

**案例2：你觉得腾讯为什么会这么成功？**

分析思路：[案例：公司优势分析-腾讯](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E8%A1%8C%E4%B8%9A%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E5%85%AC%E5%8F%B8%E4%BC%98%E5%8A%BF%E5%88%86%E6%9E%90-%E8%85%BE%E8%AE%AF.pdf)

&nbsp;

### 2.3 思维风暴：如何理解互联网思维

> 回答仅表示个人理解

[如何理解互联网思维](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E8%A1%8C%E4%B8%9A%E5%88%86%E6%9E%90/%E5%A6%82%E4%BD%95%E7%90%86%E8%A7%A3%E4%BA%92%E8%81%94%E7%BD%91%E6%80%9D%E7%BB%B4.pdf)


&nbsp;


---

## 3. 产品层面分析 

<img src="https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91-%E6%80%9D%E7%BB%B4%E5%AF%BC%E5%9B%BE/2-%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90.png" style="zoom:40%;" />

&nbsp;

### 3.1 产品评价

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

&nbsp;

> 详细分析思路：
>
> [方法论：评价产品/产品功能的好坏]()


&nbsp;

**案例1：评价小红书这个app**

[分析思路：评价小红书](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E6%97%A5%E5%B8%B8%E4%BD%BF%E7%94%A8%E7%9A%84%E4%BA%A7%E5%93%81%E8%AF%84%E4%BB%B7.pdf)

&nbsp;


**[思维发散] 案例2：分析产品/产品功能的缺点及提出改进方法**

> 关注在战略角度及产品使用流程改进

- 分析ATM机的缺点及改建建议

  [案例分析：ATM机](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E5%88%86%E6%9E%90ATM%E6%9C%BA%E7%9A%84%E7%BC%BA%E7%82%B9%E5%92%8C%E6%94%B9%E8%BF%9B%E6%96%B9%E6%B3%95.pdf)

&nbsp;

- 给出滴滴打车功能的改进建议(先进行缺点分析)

  [案例分析：滴滴打车](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E5%88%86%E6%9E%90%E6%BB%B4%E6%BB%B4%E6%89%93%E8%BD%A6%E7%BC%BA%E7%82%B9%E5%92%8C%E6%94%B9%E8%BF%9B%E6%96%B9%E6%B3%95.pdf)

&nbsp;

**[数据表现]案例3：作为数据分析师如何衡量淘宝推荐系统好还是不好**

> 重点：特定领域指标的选取

分析思路：[案例分析：作为数据分析师如何衡量淘宝推荐系统好还是不好](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E4%BD%9C%E4%B8%BA%E6%95%B0%E6%8D%AE%E5%88%86%E6%9E%90%E5%B8%88%E5%A6%82%E4%BD%95%E8%A1%A1%E9%87%8F%E6%B7%98%E5%AE%9D%E6%8E%A8%E8%8D%90%E7%B3%BB%E7%BB%9F%E5%A5%BD%E8%BF%98%E6%98%AF%E4%B8%8D%E5%A5%BD.pdf)

&nbsp;

### 3.2 竞品分析

> 方法论参考上图思维导图

&nbsp;

**案例1：产品对比分析**

怎么看微信的公众号和百度的直达号，哪个更有优势？

[案例：竞品分析腾讯公众号vs百度直达号](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E7%AB%9E%E5%93%81%E5%88%86%E6%9E%90%E8%85%BE%E8%AE%AF%E5%85%AC%E4%BC%97%E5%8F%B7vs%E7%99%BE%E5%BA%A6%E7%9B%B4%E8%BE%BE%E5%8F%B7.pdf)

&nbsp;

百度知道和知乎的区别在哪里？

[案例：竞品分析百度vs知乎](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E7%AB%9E%E5%93%81%E5%88%86%E6%9E%90%E7%99%BE%E5%BA%A6vs%E7%9F%A5%E4%B9%8E.pdf)

&nbsp;

### 3.3 产品需求迭代&产品改版

方法论参考上图思维导图

> 具体方法论：[方法论：产品改版](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9A%E4%BA%A7%E5%93%81%E6%94%B9%E7%89%88.pdf)

&nbsp;

### 3.4 产品需求分析/产品设计

用户提出需求/存在潜在需求，如何通过进一步分析用户需求满足产品功能

> 1. 分析需求
> 2. 分析满足需求的路径
> 3. 给出效果图。

[方法论：需求分析和结果设计](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9A%E9%9C%80%E6%B1%82%E5%88%86%E6%9E%90%E5%92%8C%E7%BB%93%E6%9E%9C%E8%AE%BE%E8%AE%A1.pdf)

[方法论：需求分析详解（用户痛点分析）](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9A%E7%94%A8%E6%88%B7%E7%97%9B%E7%82%B9%E5%88%86%E6%9E%90.pdf)

&nbsp;

PS：在进行分析的时候，适当参考互联网层面的产品模式以及不同载体(移动端/PC端)的特点

> 互联网层面产品模式及不同载体特点：
>
> [参考：互联网产品模式及各载体特点](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E5%8F%82%E8%80%83%EF%BC%9A%E4%BA%92%E8%81%94%E7%BD%91%E4%BA%A7%E5%93%81%E6%A8%A1%E5%BC%8F.pdf)

&nbsp;

**案例1：分析‘‘小蛮腰’’被搜索的时候的需求，满足需求的路径是什么，并给出搜索结果效果图**

> 思路：[案例：产品需求分析-小蛮腰](https://github.com/SIHENG98/DA-NOTE/blob/17ca8f74a98ca8b81c8dec380a1e1a55cbe7d30e/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%96%B9%E6%B3%95%E8%AE%BA%EF%BC%9A%E4%BA%A7%E5%93%81%E9%9C%80%E6%B1%82%E5%88%86%E6%9E%90-%E5%B0%8F%E8%9B%AE%E8%85%B0.pdf)

&nbsp;

**案例2：满足用户痛点**

> 1. 整理产品的基本功能
>
> 2. 分析目标用户特点
>
> 3. 产品设计

&nbsp;

- **为失明的人设计一款钟表** 

  分析思路：[案例：为失明的人设计一款钟表](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E4%B8%BA%E5%A4%B1%E6%98%8E%E7%9A%84%E4%BA%BA%E8%AE%BE%E8%AE%A1%E4%B8%80%E6%AC%BE%E9%92%9F%E8%A1%A8.pdf)



- **如果男生有可能怀孕，会产生什么新的诉求，新的产品出现？**

  分析思路：[案例：用户需求脑洞拓展](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E6%A1%88%E4%BE%8B%EF%BC%9A%E7%94%A8%E6%88%B7%E9%9C%80%E6%B1%82%E8%84%91%E6%B4%9E%E6%8B%93%E5%B1%95.pdf)

&nbsp;

### 其他案例

 **分析：如何证明一部分用户的增长是由某一个功能带来的**

分析思路：[分析：如何证明一部分用户的增长是由某一个功能带来的](https://github.com/SIHENG98/DA-NOTE/blob/main/Part%20II%20%E4%B8%9A%E5%8A%A1%E9%80%BB%E8%BE%91/%E4%BA%A7%E5%93%81%E5%88%86%E6%9E%90/%E5%88%86%E6%9E%90%EF%BC%9A%E5%A6%82%E4%BD%95%E8%AF%81%E6%98%8E%E4%B8%80%E9%83%A8%E5%88%86%E7%94%A8%E6%88%B7%E7%9A%84%E5%A2%9E%E9%95%BF%E6%98%AF%E7%94%B1%E6%9F%90%E4%B8%80%E4%B8%AA%E5%8A%9F%E8%83%BD%E5%B8%A6%E6%9D%A5%E7%9A%84.pdf)



---





















