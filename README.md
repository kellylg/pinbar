# pinbar
量化投资--A股市场K线形态 Pin Bar 分析

本人在2019年出差广西时，客户也刚好从北京出差回广西，他从BJ带回来了量化投资概念，这也是我第一次听这概念，主要思想就是从股海中，通过大数据分析，找出大概率会升的股票，再对股票的位、势、态、基本面、支撑及阻力位等信息进行研判后，挑出部分进行投资运作。当时不以为然。后来由于工作原因，长期离家出差，加上中年危机感越来越强烈，工作压力、生活压力的叠加，理财的意识也在脑里萌芽，一般晚上12点下班后，回到宿舍再花2-3小时恶补知识。

肺话不多说，开始进入正题。

什么是Pinbar

Pinbar 是单K线反转形态，包括射击之星(shooting star)和锤头(hammer)。它们的特征是长影线，短实体。影线长度大概是实体的2倍以上，并且实体可以是阳烛也可以是阴烛。

![image](https://user-images.githubusercontent.com/23202106/129580655-c863dba2-a314-449f-bd20-89dbe0eeef72.png)

![image](https://user-images.githubusercontent.com/23202106/129580784-8f3715df-0e0e-4e27-b32b-6e1e9820166e.png)

如上图射击之星有长上影线，是顶部反转信号，所以是卖出看跌信号。

锤头有长下影线，是底部反转信号，所以是买入看涨信号。

将单个K线还原到K线图中，就形成了如下Pinbar形态。该形态由左眼、鼻子和右眼组成。

![image](https://user-images.githubusercontent.com/23202106/129580838-ff2ababc-3a67-48a2-b0a0-5550a1637ca5.png)

shooting star组成的Pinbar形态中，如左半图，左眼是一根看涨的阳烛，右眼是看跌的阴烛。鼻子蜡烛图的开盘价和收盘价都包含在左眼内部。表示价格先被抬高后被空头打压，受到阻力，看跌。

hammer组成的Pinbar形态中，如右半图，左眼是一根看跌的阴烛，右眼是看涨的阳烛。同样鼻子蜡烛图的开盘价和收盘价包含在左眼内部。价格先被打压后被多方支持，受到支撑，看涨。

讲述完Pinbar概念以及Pinbar形态后，下面讲述如何在茫茫股海中，及时发现pinbar。

其实接下来就是讲述一个数据采集、清洗、计算的过程了。

1.找到所有A股列表接口，清洗，并处理为结构化数据

![image](https://user-images.githubusercontent.com/23202106/129580905-e66ba0ce-4dc5-4496-9fc8-81a7b0826dfc.png)

接口返回的是json数据，包含股票代码，及股票名称，其中股票代码的sh为上海，sz为深圳，共5399个股票。

数据作简单处理，转换为直男能看懂的格式，并加上处理日期。

![image](https://user-images.githubusercontent.com/23202106/129580949-21237583-22c8-433c-b7fe-26d07d777a7b.png)

2.根据列表获取个股的历史数据，

从r_list.lst里读取基础数据，并采集历史数据：
部分go代码如下：

![image](https://user-images.githubusercontent.com/23202106/129582897-b56a12be-16a6-4fe8-80a3-4a85375e0fd0.png)


清洗后结果如下：

![image](https://user-images.githubusercontent.com/23202106/129581096-865d413b-5e4e-49da-b08e-17472b2d6c31.png)

![image](https://user-images.githubusercontent.com/23202106/129581109-b05baa3c-3f80-43be-9cf4-ba6a5c024bb1.png)

上图是000002从1991年上市至今的所有数据。

共采集了5396个股票的所有历史数据，共1.5GB左右

![image](https://user-images.githubusercontent.com/23202106/129581170-8952146c-d8f3-42a9-9497-2a57d00aac59.png)

由于只采集日K，所以数据量不是很大。

![image](https://user-images.githubusercontent.com/23202106/129581213-222b2584-d727-40cc-bb66-44ba1e034619.png)

3.原材料已准备完成，现在开始对历史数据进行计算，找出pin bar , 并进行验证

从计算结果分析：

【000002 万 科Ａ】
![image](https://user-images.githubusercontent.com/23202106/129581237-c355a330-e0d9-4b13-9314-0a942a556591.png)

8月3号，出现shooting star , 4号应该看跌
![image](https://user-images.githubusercontent.com/23202106/129581266-39900b2e-5ff2-457e-ba6b-1e7dbccc1c7e.png)

7月29号，出现 hammer 信号 , 30号应该看涨
![image](https://user-images.githubusercontent.com/23202106/129581304-d588d56c-01b2-42a6-af46-c05b7b8d1997.png)

最后，就是把计算程序放服务器上每天定时计算，分析出每天的pinbar信号的股票再进行研判分析即可。

结语：

量化出来的pinbar信号，可以作为参考，再结合股票的位、势、态、基本面、支撑及阻力位等信息，进行分析，降低投资风险。

此文为抛砖引玉，欢迎做量化的朋友进行技术交流！
