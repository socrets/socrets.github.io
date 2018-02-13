---
layout: post
title: 737NG引气系统排故分析
category: Engineering
---



737NG引气系统故障相对来说是比较多的，排故起来也比较麻烦，针对引气故障，FIM里有一句话说的很好，＂The most valuable tool in the fault isolation of the pneumatic system is a thorough knowledge　of the system＂,其实这句话对其他系统也适用，你如果对系统不了解，你所设计的排故方案也就会比较盲目．

引气系统ssm有一张图，基本上包含了引气的所有部件，还有相应的关系．拿来一看

![penumatic]({{ site.url }}/assets/imgs/737-36-penumatic.png)

可以看出引气的来源就是高压压气机的5级和9级,这两级引气也不是同时供的，在发动机功率比较低的时候用的是9级引气，发动机功率高的时候用的就是5级引气了．9级引气出来有个高压级活门(HSV),还有个高压机调节器(HSR),这个高压机活门和高压机调节器的原理有必要详细的说一下，后面的压力调节器(BAR)和压力调节关断活门(PRSOV)原理和这个控制原理也有点像，这个原理对理解整个引气系统的控制有很大帮助．来看这个图

![hsr]({{ site.url }}/assets/imgs/737-36-hsr.png)

9级引气进入hsr之后，经过reference pressure regulator调整之后，进入高压级活门A腔，A腔的压力比高压级活门的弹簧力和B腔的压力之和大，高压级活门就会打开了．当5级引气压力比高压级调节器调节后的压力大时，B腔的压力加弹簧力比A腔的压力大，这样就会把高压级活门关闭，由此可见，高压级调节器和高压级活门是全自动的，完全靠引气系统自身来控制．当然还有一些penumatic shutoff mechanism,relief valve和reverse flow check这些组件，这些组件的功能都是防止返流，保护高压级调机器，这些组件就不展开了，SDS里有详细的描述．下面这张图是BAR和PRSOV的原理

![bar]({{ site.url }}/assets/imgs/737-36-bar.png)

再来看看BAR和PRSOV，BAR控制PRSOV．BAR的控制比HSR稍微复杂一点，BAR里面可以接受ACAU(air conditioning accessory unit)的信号来控制PRSOV，发动机引气电门也是通过ACAU来控制BAR，还有发动机火警电门也可以不通过ACAU控制这个PRSOV．PRSOV本体里也有A腔B腔弹簧力，这个控制和高压级活门是一样的．

现在到450F这个恒温器了，这个450F也是纯机械的，到了450F后膨胀，释放PRSOV的control pressure的压力，其实就是释放了A腔的压力，所以PRSOV走向关的方向，从而控制引气流量，进一步控制引气系统温度．

现在来看看预冷器系统，预冷器系统包含预冷器控制活门，预冷器，390F．预冷器控制活门和390F的控制和PRSOV结合450F的控制原理是差不多的，只不过预冷器控制活门是弹簧预载到开位的．390F从温度390F开始释放活门作动筒的压力，弹簧力使活门向开位，到440F时，活门全开．至于预冷器就是个热交换器，预冷器控制活门的开度决定了冷空气的流量，引气通过预冷器进行热交换，这个预冷器系统的目的就是控制预冷器出口温度到390F~440F．

在预冷器的下游就是490F超温电门，这个电门就是监控预冷器下游的温度，有一些改装过后的还会向ACMS发送温度，超温之后，就会触发bleed trip off灯亮，超温之后ACAU会关掉PRSOV,防止管道被超温损坏．BAR上面有一个220psi里的超压电门，也会触发bleed trip off超压跳出．

引气的主要系统原理就在上面了，航线上会经常碰到引气跳开，为什么引气会跳开，无非是超温超压，还有线路的问题了．针对引气跳开，你要向尽可能详细的向机组了解引气跳开时候，引气系统的状态，譬如引气跳开的时候发动机的功率状态，跳开时候的管道压力．还有在引气系统排故是绕不开的一项测试就是引气系统健康测试，理解了上述引气部件原理之后这个引气系统健康测试也很好理解．

举个例子看看BAR和PRSOV的引气健康测试，看看BAR.

![bar-prsov]({{ site.url }}/assets/imgs/737-36-bar-prsov.png)

BAR有SUPPLY AIR PORT和CONTROL AIR PORT，BAR的CONTROL AIR PORT和PRSOV上的CONTROL AIR PORT相连,其实就是SUPPLY PRESSURE经过BAR降压之后到CONTROL PRESSURE其实就是到PRSOV的A腔的压力来打开PRSOV．理解了这一点引气健康测试设备也就是氮气瓶连接到SUPPLY AIR PORT，另一边把BAR的CONTROL PORT和PRSOV的CONTROL PORT中间用带压力表的管路连接起来．举个例子如果你提供SUPPLY PRESSURE(Ps)75psi,CONTROL PRESSURE(Pc)应该在20-28psi（不同的件号的BAR这些具体数值可能不同，具体参考AMM），这样可以测试出BAR是好的，然后看PRSOV有没有完全打开（或者接近完全打开），可以看出PRSOV是否工作正常．测试HSR，HSV，PCCV(预冷器控制活门)的原理和上述是相似的．

碰到引气系统的故障，需要了解引气故障发生的阶段，做引气健康测试确定故障件，不过就航线的经验来看预冷器控制活门，预冷器，390F,PRSOV更换的概率是比较高的．若是线路故障BAR上的插头，AACU更换的概率比较大．

以上就是引气系统的总结，由于水平有限，难免会有错误，敬请指正
