# HTTP 协议学习

熟悉网络协议将会提高开发的效率。

Netwrok 面板中会记录应用程序的每一次网络交互信息，每次交互的详细时间、HTTP 请求头和响应头、cookies、WebSocket 的数据等等...

HTTP 协议解决了什么问题？

解决 WWW 信息交互必须面对的需求:

- 低门槛
- 可拓展性: 巨大用户群体，超长的寿命
- 分布式系统下的 Hypermedia: 大粒度数据的网络传输

看下图是:

基于 2005 年 1 月 15 日在 opte.org 发现的数据的部分互联网地图。每条线画在两个节点之间，代表两个 IP 地址。线的长度表示这两个节点之间的延迟。

<img src="https://raw.githubusercontent.com/AlvinMi/2019-Pic/master/2019/20190529224113.jpg"/>

- 深蓝色: net, ca, us
- 绿色: com, org
- 红色: mil, gov, edu
- 黄色: jp, cn, tw, au, de
- 紫红色: uk, it, pl, fr
- 金黄色: br, kr, nl
- 白色: 其他

> 来自 wiki

## 评估 Web 架构的七大关键属性

- 1.性能 Performance: 影响高可用的关键因素
- 2.可伸缩性 Scalability: 支持部署可以互相交互的大量组件
- 3.简单性 Simplicity: 易于理解、易实现、易验证
- 4.可见性 Visiable: 对两个组件间的交互进行监视或者仲裁的能力。如缓存、分层设计等
- 5.可移植性 Portability: 在不同的环境下运行的能力
- 6.可靠行 Reliability: 出现部分故障时, 对整体影响的程度
- 7.可修改性 Modifiability: 对系统作出修改的难易程度, 由可进化性、可定制性、可拓展性、可配置性、可重用性构成。

### 性能

主要包括三块:

**网络性能**

- Throughput 吞吐量: 小于等于带宽 bandwidth, 吞吐量一般就是几个指标
- Overhead 开销: 首次开销, 每次开销

**用户感知到的性能**

- Latency 延迟: 发起请求到接收到响应的时间
- Completion 完成时间: 完成一个应用动作所花费的时间

**网络效率**

- 重用缓存、减少交互次数、数据传输距离更近、COD

### REST 架构下的 Web

REST 架构下, 遵循这样的一个架构

img img img img img img

浏览器通过 A、B、C 三条路径访问服务器, 找到 URL 路径对应的资源。

首先根据域名 DNS, 链接后端的 ip 地址.

### 5 中架构风格

在分布式的 Web 架构中，主要有下面 5 种架构风格。

**数据流风格 Data-flow Styles**

- 优点: 简单性、可进化性、可扩展性、可配置性、可重用性

像协议的分层, nginx 中也大量使用到了数据流风格。

管道与过滤器 Pipe And Filter， PF: 

每个 Filter 都有输入端和输出端，只能从输入端读取数据，处理后再从输出端产生数据。

统一接口的管道与过滤器 Uniform Pipe And Filter, UPF:

在 PF 上增加了统一接口的约束，所有 Filter 过滤器必须具备同样的接口。

**复制风格 Replication Styles**

- 优点: 用户可察觉的性能、可伸缩性、网络效率、可靠性


**分层风格 Hierarchical Styles**

- 优点: 简单性、可进化性、可伸缩性

**移动代码风格 Mobile Code Styles**

- 优点: 可移植性、可扩展性、网络效率

**点对点风格 Peer-to-Peer Styles**

- 优点: 可进化性、可重用性、可扩展性、可配置性

没有接触过架构相关的东西. 但是这并不影响我学习.

有的人可能会说, 5G 时代来临, 这样的性能优化，还需要关注和优化吗？

答案当然是肯定的, 5G 在硬件网络上提升了，但是 http 在应用层, 硬件再快, 应用层性能太差, 所表现出来的效果肯定也是不理想的。

## 使用 telnet 命令

telet 只是建立了 TCP 连接。

如果在请求中没有携带 Host 头部，一律返回 400 Bad Request.
