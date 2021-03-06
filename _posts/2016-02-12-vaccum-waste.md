---
layout: post
title: 737NG真空马桶系统概述
category: Engineering
---



737NG真空马桶系统的控制逻辑不算复杂，但这个系统的故障对运行旅服上影响比较大，有必要详细的看一下这个系统．先看看这个系统在厕所的主要部件
![toilet-assembly]({{ site.url }}/assets/imgs/737-38-toilet-assembly.png)

有些构型比较新的飞机的马桶外罩下面的两个螺钉需要专用工具，这个需要注意一下.　这张图主要看漂洗活门，冲洗活门，FCU这三个．

* 漂洗活门(rinse valve). 从引用水箱向马桶供水的一个活门，有滤子，反虹吸管防止水返回饮用水箱．

* 冲洗活门(flush valve). 这个活门打开就是客舱压力把马桶的脏物通过管道冲到污水箱．

* FCU(flush control unit). 这个组件控制了一个冲洗循环的逻辑．

有一个LCM(logic control module)，如果污水箱满了，这个组件可以向FCU提供信号抑制冲洗循环，这个组件在污水箱附近．
![lcm]({{ site.url }}/assets/imgs/737-38-lcm.png)

还有一个真空泵，这个泵在16000英尺一下工作，把污水箱抽成负压，客舱的压力把马桶的脏物通过冲洗活门压到污水箱，在16000英尺以上，这个泵就不工作了，靠客舱内外的压力来完成冲洗循环．

下面看一下FCU控制的冲洗循环．
![flush-cycle]({{ site.url }}/assets/imgs/737-38-flush-cycle.png)

FCU首先从LCM中获取逻辑信号，冲洗循环没有被抑制，按压冲洗电门(flush switch)开始冲洗循环．按压电门后，有一个15s的DUTY CYCLE INHIBIT这个是防止把按压其他电门再次启动冲洗循环，16000英尺以下真空泵开始工作，１s后漂洗活门打开0.7s，向马桶供水，2s后冲洗活门打开4s，这时客舱压力可以把马桶的脏物通过管道冲压到污水箱．

上述就是真空马桶系统的功能概述，从上述可知，如果碰到三个厕所马桶都不工作，可以考虑污水箱是否满了，LCM，真空泵的问题．如果一个马桶的控制有问题，可以考虑这个马桶下面的FCU，冲洗电门的问题．如果是马桶堵了，大部分时候是冲洗活门堵了，可以用棘爪疏通一下，或者拆下冲洗活门清理．如果是管道堵了，AMM38-32-00有vaccum line blockage inspection，提供了检查管道的方法，用硬币敲管道，听声音看哪堵了，然后拆下管道接口，清理管道，这项工作是很体现飞机维护工作者的职业精神的，:P.
![coin-tap]({{ site.url }}/assets/imgs/737-38-coin-tap.png)

由于水平有限，难免有错误或疏漏，敬请指正．
