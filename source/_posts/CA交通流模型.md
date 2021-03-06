title: CA自行车流模型
date: 2016-04-07 19:52:28
tags: 
- 元胞自动机
- NS模型
---
### 背景
如今城市的交通问题越来越突出，交通拥堵（已经受够了杭州的交通），伴随而来的交通污染问题也越来越严重（砖家称北京的雾霾天很大程度是由汽车尾气所导致，这里就不深究雾霾严重的原因了）。而自行车作为一种绿色健康的交通出行方式，在一定范围内又得到了人们的喜爱。在这里真的要为杭州的公交自行车的公共设施点赞，覆盖广，很方便。我国是人口大国，自然在道路上可以看到许许多多的自行车，还有电动车（感觉电动车才是马路杀手）。但行人和骑自行车的人的交通意识并不强，很多情况下，自行车强行超车，速度也很快，车流量大的时候也容易造成拥堵。

<!--more-->
### 元胞自动机
细胞自动机（Cellular automaton），又称格状自动机、元胞自动机。它是由无限个有规律、坚硬的方格组成，每格均处于一种有限状态。整个格网可以是任何有限维的。同时也是离散的。
元胞自动机有三个特征：

- 平行计算（parallel computation）：每一个细胞个体都同时同步的改变
- 局部的（local）：细胞的状态变化只受周遭细胞的影响。
- 一致性的（homogeneous）：所有细胞均受同样的规则所支配

### 单车道模型
#### NS模型
将元胞自动机应用于交通流仿真最早是受到了Wolfram 184号初等元胞自动机的启发。1992年Nagel和Schreckenberg提出了著名的NS模型。
#### 模型建立
思想：在骑车过程中希望自行车能以它最大速度行驶，并不会与其他车辆发生碰撞，但并不是所有的车辆都可以以最大速度行驶，因而引入随机慢化概率$\ p$，来模拟车辆行驶时受到的干扰情况。在$\ t$到$\ t+1$的过程中，具体NS模型的演化规则如下：

- 速度更新规则

$$v_i(t) = min\( v\_i(t-1)+1,\ g\_i(t-1),\ v\_\{max\} \)$$
- 随机慢化规则
$$\epsilon(t) \leq p\ 时，v_i(t) = max\(0,\ v_i(t)-1\)$$
- 位置更新规则
$$ x_i(t) = x_i(t-1) + v_i(t)$$

其中，$v_i(x)\ $表示第$\ i$辆车从$\ t-1$时刻$\ t$到时刻车辆运行的速度，$\ g_i(t-1)$表示第$\ i$辆车和其前方车的距离，$x_i(t)$表示$\ t$时刻第$\ i$辆车的位置。随机慢化规则表示的是骑车人的差异骑车行为，这是堵塞自发形成的重要因素。

#### 模型求解
道路的路口长度$\ S$为240米，若自行车都往一个方向走,自行车长度为1.2米，记为一个元胞，那一共有200个元胞。车辆的最高速度5，每分钟路口的车辆100，自行车的平均速度有3，那么相当于有100辆车在路口循环行驶。

初始化：在路段上，随机分配100个车辆，且随机速度为1-5之间。

自行车的最大速度为10，随机慢化概率$\ p=0.3$在边界条件中，假设头车在道路边界，以概率0.5离去。得到如下的自行车时空图

<!-- ![timeLocation1](http://ww3.sinaimg.cn/large/713ab781jw1f2yvrgownkj20kq0fl790.jpg) -->

![timeLocation1](http://ww1.sinaimg.cn/large/713ab781jw1f2ywcbmqbij20bn08pjtc.jpg)

可以看出刚开始道路出现了拥堵的情况，随着时间的推移，拥堵情况得到缓解，只在道路末端较为拥堵。

当自行车的最高时速降到8时，时空图如下，拥堵情况较速度8时有所好转

![timeLocation2](http://ww1.sinaimg.cn/large/713ab781jw1f2ywhck492j20bq08wq4y.jpg)

当随机慢化概率升高到$\ p=0.5$时，如下图，时空图显示道路上的自行车比上面两种情况拥堵一些，这和实际的道路状况相符。

![timeLocation3](http://ww1.sinaimg.cn/large/713ab781jw1f2ywjr9glqj20bt09ttb8.jpg)

只考虑了单车道模型，并未考虑自行车变道情况。需要改进，提出多车道模型。

### 多车道道模型
![carRoads](http://ww2.sinaimg.cn/large/713ab781jw1f2ywpqe58vj20pz07edgj.jpg)

#### 模型建立
考虑多车道模型，一共有三个车道，和单车道模型相类似，在每一时间步，自行车运动规则如下：

- 加速
$$v_i=min\(v\_i+1,\ v\_\{max\}\)$$
- 减速
	+ $$如果\ d\_i < d\_\{od\},\ v\_i=min\(v\_i,\ d\_i,\ max\(d\_\{i-1\},\ d\_c\)\)$$
	+ $$否则，\ v\_i=min\(v\_i,\ d\_i\)$$

- 随机慢化，车辆速度以概率$\ p_1$减小一个单位$\ v\_i=max\(v\_i-1,\ 0\)$
- 变换车道规则：自行车在本车道满足速度小于与前方车辆的距离时，即$\ d\_i \le v\_i$,并且平行位置左侧或者右侧车道前方车辆大于本车的速度时，即$\ d\_\{lt\} \ge v\_i$或$\ d\_\{rt\} \ge v\_i$，本自行车将以一定的概率$p_2$向两侧变道。
- 自行车向前运动，$x_i = x_i + v_i$

其中，当某辆自行车和他前面的自行车的间距小于运动间距$d\_\{od\}$时，自行车的速度不仅取决于本身的间距，还与前车的间距有关。参数$d_c$反映了前车间距的影响没有本车间距影响大。

#### 模型求解
车辆进入车道满足泊松分布$\(\lambda=200\)$，车辆最大速度$v\_\{max\} = 8$，$d\_\{od\}=15$，$d_c=2$,$\ $以$\ p_2=0.7$的概率变道,以$p_1=0.3$的概率随机慢化减速。

![timeLocation4](http://ww4.sinaimg.cn/large/713ab781jw1f2yxokhl0tj20be0960v6.jpg)

#### 总结
从上图可以看出，和单车道相比，多车道模型车辆不再那么拥堵，遵循一定交通规则，并利用多车道，可以有效缓解自行车拥堵问。交通流元胞自动机模型具有规则简单、计算速度快的特点，目前已成为交通微观模拟研究的重要工具。其在描述交通流特性方面的独特优势，必将会使它有非常广阔的发展前景。

### 参考文献
[1] 叶冬,樊镭. 一维单车道交通流元胞自动机模型综述[J]. 物联网技术 2013(5):23-25

