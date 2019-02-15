---
description: 【AukeyCloud】监控使用手册 v1.0
---

# 02 监控

### 1. 模块介绍 <a id="1-mo-kuai-jie-shao"></a>

监控系统是整个运维环节，乃至整个产品生命周期中最重要的一环，事前及时预警发现故障，事后提供翔实的数据用于追查定位问题。监控系统作为一个成熟的运维产品，业界有很多开源的实现可供选择。当公司刚刚起步，业务规模较小，运维团队也刚刚建立的初期，选择一款开源的监控系统，是一个省时省力，效率最高的方案。之后，随着业务规模的持续快速增长，监控的对象也越来越多，越来越复杂，监控系统的使用对象也从最初少数的几个SRE，扩大为更多的DEVS，SRE。这时候，监控系统的容量和用户的“使用效率”成了最为突出的问题。 AukeyCloud监控系统是一款针对主机/容器和互联网应用进行监控系统，监控服务可用于收集主机/容器资源（系统性能、组件服务、数据库、日志等）的监控指标，探测互联网应用服务的可用性，并对指标进行告警和自动执行处理。

#### 概念和术语 <a id="gai-nian-he-shu-yu"></a>

* 指标，行业里一般称为Metric\(s\)、Item或度量，即监控的内容，一般是坐标系中的纵坐标，比如CPU使用率、在线人数等，在SQL语句中一般是 `select 指标`
* 视角，行业里一般称为Dimension，区分指标的条件，比如`设备视角`、`指标视角`、`组合视角`等
* 监控模板（Dashboard），通俗的说就是监控大屏

出图设置

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LVqlUTagxhS4K1qGhSa%2F-LVqn0uM4T4lf74qhGvp%2Fimage.png?alt=media&token=f121f5c6-f223-489d-b4f1-6d2e7018ac77)

### 2. 模块架构 <a id="2-mo-kuai-jia-gou"></a>

依托AukeyCloud操作中心实现对主机、网络设备等数据源的数据采集能力，通过监控平台对数据计算、存储，实现告警检测、收敛、通知的闭环。

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LVkmSElSGOdoFLjIKPr%2F-LVkmTLwYeVfLq5XLUk0%2Fimage.png?alt=media&token=113a6463-90a4-4f39-9447-bfb544112403)

* 采集器：agent用于采集机器负载监控指标，比如cpu.idle、load.1min、disk.io.util等等，每隔60秒push一次数据。agent提供了一个http接口/v1/push用于接收用户手工push的一些数据，只要安装了agent的机器，就会自动开始采集各项指标，主动上报，agent是一个golang开发的daemon程序，用于自发现的采集单机的各种数据和指标，这些指标包括不限于以下几个方面，共计200多项指标。
  * CPU相关
  * 磁盘相关
  * IO
  * Load
  * 内存相关
  * 网络相关
  * 端口存活、进程存活
  * ntp offset（插件）
  * 某个进程资源消耗（插件）
  * netstat、ss 等相关统计项采集
  * 机器内核配置参数

### 3. 特点及优势 <a id="3-te-dian-ji-you-shi"></a>

* 强大灵活的数据采集：自动发现，支持agent、snmp、支持用户主动push、用户自定义监控支持
* 水平扩展能力：支持数据采集、告警判定、历史数据存储和查询
* 高效率的告警策略管理：支持策略模板、模板继承和覆盖、多种告警方式、支持callback调用
* 人性化的告警设置：最大告警次数、告警级别、告警恢复通知
* 高效率的graph组件：单机支撑上万metric的上报、归档、存储（周期为1分钟）
* 高效的历史数据query组件：采用rrdtool的数据归档策略，快速返回上百个metric的历史数据
* dashboard：多维度的数据展示，用户自定义模板
* 支持Nodata监控、主机存活监控等
* 开发语言： 使用前后端分离架构，整个系统的后端，由Python+Go语言编写，前端使用vue.js编写。

### 4. 功能介绍 <a id="4-gong-neng-jie-shao"></a>

#### 4.1 监控查询 <a id="41-jian-kong-cha-xun"></a>

监控查询的操作流程如下：

![&#x76D1;&#x63A7;&#x67E5;&#x8BE2;&#x6D41;&#x7A0B;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWJcTBwGvvxDOZ6O2xr%2F-LWJcXOu5hNqSgyqugx7%2F%E7%9B%91%E6%8E%A7%E6%9F%A5%E8%AF%A2%E6%B5%81%E7%A8%8B.png?alt=media&token=127bf904-5e54-4a9a-baed-44e6dfd4f79e)

**1）指标管理**

* 添加指标， 自定义的监控项需要手动添加指标
* 收集指标， 收集参考设备下的所有指标，选择所需要的指标
* 编辑，可对指标进行自定义编辑添加描述信息
* 所添加或收集的指标被类型或设备关联使用

![&#x6307;&#x6807;&#x7BA1;&#x7406;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWJdNU-_tq2cIKlWkY-%2F-LWJhamgavnwQZCq6iBA%2F%E6%8C%87%E6%A0%87%E7%AE%A1%E7%90%86.png?alt=media&token=d71439eb-0055-41e8-ab6b-5b77022a558f)

**2）类型管理**

* 按功能或业务分类的一组设备类型
* 添加类型时可给改类型分配一组初始化指标（指标管理中添加）
* 加入该组的设备将默认拥有此类型下的所有指标
* 类型指标可以进行分配或者回收

![&#x7C7B;&#x578B;&#x7BA1;&#x7406;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWFzDU9qAA2sJr5W8Fi%2F-LWG-iDLiRXKl1Icrm3_%2F%E7%9B%91%E6%8E%A7%E6%9F%A5%E8%AF%A2.png?alt=media&token=af38b71f-dc61-47d5-af28-b39419ecee40)

**3）设备管理**

* 设备安装Agent将自动展示在可选设备列表
* 给设备分配指定指标
* 通过收集设备将该设备添加进平台监控，收集设备可关联类型，此设备将拥有此类型下的所有指标

![&#x8BBE;&#x5907;&#x7BA1;&#x7406;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWJifQ6T6JgCGIz-O6R%2F-LWJofwWN9oJ8zCAHEnY%2F%E8%AE%BE%E5%A4%87%E7%AE%A1%E7%90%86.png?alt=media&token=40f74ea1-aefa-432f-8acb-9d3734e3d64c)

**4）监控查询**

* 选择过滤设备和指标查询
* 查询指定时间区间的监控图表
* 以不同的维度展示监控信息（设备视角、指标视角和组合视角）
* 生成图表展示
* 生成的图表可添加到监控模板（**4.2 监控模板**）
* 图表详细信息，可修改展示方式，例如折线图、柱状图等

![&#x76D1;&#x63A7;&#x67E5;&#x8BE2;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWJifQ6T6JgCGIz-O6R%2F-LWJpHDgl_4cKNB6pUld%2F%E7%9B%91%E6%8E%A7%E6%9F%A5%E8%AF%A21.png?alt=media&token=926bf6a6-7cec-455b-b489-19a30b195375)

#### 4.2 监控模板 <a id="42-jian-kong-mo-ban"></a>

监控模板类似于监控大屏（Dashboard），将一组业务相关的主机汇总聚合到一起展示，直观的显示某一时刻某一资源的使用情况。

* 下拉可选择更多模板，可对模板进行修改或删除
* 图表相关操作：区域缩放，视图切换，下载图表
* 图表的主题可根据需要自行选择

![&#x76D1;&#x63A7;&#x6A21;&#x677F;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWJsRjfhaknW7l4aQO5%2F-LWJtynLUlAJ6MgdXrzZ%2F%E7%9B%91%E6%8E%A7%E6%A8%A1%E6%9D%BF.png?alt=media&token=3d437fb9-ee84-479c-95fd-e61f2fad87a5)

#### 4.3 告警策略 <a id="43-gao-jing-ce-lve"></a>

告警策略是监控的核心功能之一，通过对主机上的指标新增告警策略产生告警，关联通知的用户实现告警通知的闭环，目前通知方式有短信、邮件和IM\(目前已对接企业微信）方式。

以下是告警策略设置的主要流程：

![&#x544A;&#x8B66;&#x7B56;&#x7565;&#x8BBE;&#x7F6E;&#x6D41;&#x7A0B;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWKFG-Ek2lLFXIX2L4T%2F-LWKT89wnBUC1pEdKtgY%2F%E5%91%8A%E8%AD%A6%E7%AD%96%E7%95%A5.png?alt=media&token=b6a63f61-89ed-4ce4-8f23-96a4880e12b9)

告警策略的具体设置如下：

（1）策略模板，新增告警策略

（2）策略列表，选择需要告警的指标

（2）告警动作，选择需要接收告警用户

（3）绑定设备组，将告警策略绑定主机或主机组

![&#x544A;&#x8B66;&#x7B56;&#x7565;&#x8BBE;&#x7F6E;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWKU-4zm780VQHtwMWm%2F-LWKp57SJLOAFXKKEiH1%2F%E7%AD%96%E7%95%A5%E6%A8%A1%E6%9D%BF.png?alt=media&token=7913e29b-b54d-4146-995f-eb30824b16d6)

**报警函数说明**

配置报警策略的时候支持多种报警触发函数，比如`all(#3)` `diff(#10)`等等。 这些\#后面的数字表示的是最新的历史点，比如`#3`代表的是最新的三个点。该数字默认不能大于`10`，大于`10`将当作`10`处理，即只计算最新`10`个点的值。

```text
all(#3): 最新的3个点都满足阈值条件则报警max(#3): 对于最新的3个点，其最大值满足阈值条件则报警min(#3): 对于最新的3个点，其最小值满足阈值条件则报警sum(#3): 对于最新的3个点，其和满足阈值条件则报警avg(#3): 对于最新的3个点，其平均值满足阈值条件则报警diff(#3): 拿最新push上来的点（被减数），与历史最新的3个点（3个减数）相减，得到3个差，只要有一个差满足阈值条件则报警pdiff(#3): 拿最新push上来的点，与历史最新的3个点相减，得到3个差，再将3个差值分别除以减数，得到3个商值，只要有一个商值满足阈值则报警lookup(#2,3): 最新的3个点中有2个满足条件则报警；
```

**设备组**

告警设备（主机）可在设备组中管理，对告警设备（主机）的增删改查，在设置告警策略中调用。

![&#x8BBE;&#x5907;&#x7EC4;&#x7BA1;&#x7406;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWKqFHuzpLbMkgwVGZu%2F-LWKvw5QlT5q-diOq8t4%2F%E8%AE%BE%E5%A4%87%E7%BB%84.png?alt=media&token=35eadd63-0303-4808-abe0-18aebee847d8)

**用户组**

用户组是一组告警用户的集合，告警用户接收告警通知，对告警用户的增删改查在用户组中进行。

![&#x7528;&#x6237;&#x7EC4;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWKqFHuzpLbMkgwVGZu%2F-LWKwvRpOoVBaDsN4AI3%2F%E7%94%A8%E6%88%B7%E7%BB%84.png?alt=media&token=253ae8f5-fcc8-4dac-9ef5-18dbbb9cf1ac)

#### 4.4 告警记录 <a id="44-gao-jing-ji-lu"></a>

告警事件的查询和记录都在告警记录中展示，如下图：

![&#x544A;&#x8B66;&#x8BB0;&#x5F55;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWKqFHuzpLbMkgwVGZu%2F-LWL41UKgEcmua-p3cw7%2F%E5%91%8A%E8%AD%A6%E8%AE%B0%E5%BD%95.png?alt=media&token=7b629a47-d15f-45f4-8ce8-9001518d8c6b)

#### 4.1 监控查询 <a id="41-jian-kong-cha-xun-1"></a>

AukeyCloud监控系统能够监控服务器主机/容器资源的基础性能指标，同时也支持用户自定义指标数据的采集上报做监控；借助监控系统，您可以全方位了解主机的资源使用情况和运行状态，并对应用程序的日志数据做监控以保障业务的可用性。通过告警服务您可以及时作出响应，保证应用程序顺畅运行，业务无忧。

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWEPwRlqOlru9sZVbGz%2F-LWER54HjDPC5AtPAgdc%2F%E7%9B%91%E6%8E%A7%E6%9F%A5%E8%AF%A2%E6%93%8D%E4%BD%9C%E6%B5%81%E7%A8%8B1.png?alt=media&token=53aafe75-ad8b-4ca9-8db7-0a0e910991c0)

**4.1.1 类型管理**

* 按功能或业务分类的一组设备类型
* 添加类型时可给改类型分配初始化指标（关联指标管理中的指标）
* 加入该组的设备将默认拥有此类型下的所有指标
* 可对已分配指标的设备进行再分配回收指标
* 新增加指标需要首选添加到类型才能给设备分配

​

### 5. 结语 <a id="5-jie-yu"></a>

### [ ](https://694748391.gitbook.io/aukeybooks/02-jian-kong-v1.0#5-jie-yu) <a id="5-jie-yu"></a>

