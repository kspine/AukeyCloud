---
description: 【AukeyCloud】操作中心使用手册 v1.0
---

# 01 操作中心

### **1. 模块概述**

操作中心模块是运维自动化的基础模块之一，旨在提高运维效率，直观展示主机设备各类资源信息，统一的管理认证信息以及服务商信息，提供添加本地主机和收集远程云主机信息功能，批量执行脚本以及添加计划任务，通过操作中心极大提高了运维自动化效率和准确率。

###  2. 模块架构 <a id="2-mo-kuai-jia-gou"></a>

![&#x6A21;&#x5757;&#x67B6;&#x6784;&#x6982;&#x89C8;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LVNOpaOB4ciZ1n-55FE%2F-LVNPDqCNfRuTWc2rsFU%2Fimage.png?alt=media&token=cbbdde2c-2578-48e1-9003-ee4bf49f34ec)

### 3. 特点及优势 <a id="3-te-dian-ji-you-shi"></a>

操作中心主要有以下功能特性：

* 自动/手动收集本机主机以及远程主机信息（监控、磁盘、用户信息等）
* 自定义分组功能（可按业务功能划分不同分组）
* 统一凭证管理，支持密码、秘钥以及RDP方式
* 精细化权限管理与审计，可查询审计历史操作
* 支持指令以及脚本（shell、python等）批量分发执行
* 支持批量下发计划任务
* 支持文件上传

### **4. 操作中心使用流程** <a id="4-cao-zuo-zhong-xin-shi-yong-liu-cheng"></a>

![&#x4F7F;&#x7528;&#x6D41;&#x7A0B;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWA-H9Pt_oSMActbdWp%2F-LWA04z_1OWDXfNh3GgV%2F%E6%B5%81%E7%A8%8B%E5%9B%BE.png?alt=media&token=c59a3956-8590-49ec-a6fc-3286ce9e8fb4)

### 5. 功能介绍 <a id="5-gong-neng-jie-shao"></a>

#### 5.1 主机管理 <a id="51-zhu-ji-guan-li"></a>

目前主机管理可批量管控Linux以及Windows主机，收集主机的方式有「添加主机」以及「收集主机」，主机信息可作为脚本管理、计划任务管理以及文件上传的主机列表选择项。另外，绑定凭证的主机可进行远程连接。

![&#x4E3B;&#x673A;&#x7BA1;&#x7406;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LW9xdmhUekn-sXlVN62%2F-LW9yBpaZXyuyRu993IM%2F%E4%B8%BB%E6%9C%BA%E7%AE%A1%E7%90%86%E5%88%97%E8%A1%A8.png?alt=media&token=8bca7c2c-199a-405b-b2a7-a5c2e8dab42c)

**A. 搜索区**

根据「添加主机」字段进行搜索

**B. 分组**

对主机进行更精细化的管理分组，根据不同业务场景或地理位置进行分组，基本功能为增、删、改分组以及绑定主机

![&#x4E3B;&#x673A;&#x5206;&#x7EC4;&#x7BA1;&#x7406;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LW9kGvQk_brxJqZcuMu%2F-LW9koMPDg0a2sL8PuW2%2Fgroup.png?alt=media&token=930d4810-352d-4d4e-a28e-091a2ee792f4)

**C. 功能**

功能区主要包括添加主机，收集主机，编辑，删除；添加和收集主机的区别在于，收集主机主要针对是云主机信息，添加主机则是对本地主机或虚拟机管理。

* 添加主机

![&#x6DFB;&#x52A0;&#x4E3B;&#x673A;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LW9kGvQk_brxJqZcuMu%2F-LW9kr75LFB82raS0_LN%2Fadd.png?alt=media&token=8e40939f-3c9f-479d-8f54-8bfd8a23c837)

* 收集主机

![&#x6536;&#x96C6;&#x4E3B;&#x673A;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LW9xdmhUekn-sXlVN62%2F-LW9yQW2i383dfN_cotJ%2Fshouji.png?alt=media&token=53a7ba7d-71e3-4844-a233-3885ce0613ac)

注意：选择服务商之前需先在「服务商管理」中添加相关信息（ Access Key ID以及类型）方可指定，具体参考下面「服务商管理」说明。

​[以阿里云为例：如何获取AccessKey授权](https://help.aliyun.com/document_detail/28642.html?spm=5176.2020520153.0.0.789c415dXTvy6s)​

​**D. 列表区**

列表区主要展示主机的详细信息，主要包括磁盘信息、用户信息、监控数据、修改记录以及行为审计。agent状态显示`运行`的主机，可获取监控信息（CPU使用率、内存使用率以及磁盘使用率等），通过（添加主机时绑定或在堡垒机模块指定）关联凭证，可对有权限的主机进行远程连接，对主机的操作将会记录在行为审计中。

* 详情展示

![&#x4E3B;&#x673A;&#x8BE6;&#x60C5;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LW9xdmhUekn-sXlVN62%2F-LW9yWUd3U3dvW_1ge1w%2Flist.png?alt=media&token=3e41731f-1f82-4235-8868-c79995ee81f9)

* 远程连接，默认选择内部IP，也可选择外部IP（针对云主机）连接

![&#x8FDC;&#x7A0B;&#x8FDE;&#x63A5;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LW9xdmhUekn-sXlVN62%2F-LW9ya2ZIdlkAKWgtYfO%2Fremote.png?alt=media&token=15089b5a-50ce-4f33-beba-ee6979ea7aba)

凭证用户：「堡垒机」模块中分配用户凭证以及主机，只有分配了凭证和主机的用户才能进行远程连接，具体参考文档《堡垒机》说明

#### 5.2 服务商管理 <a id="52-fu-wu-shang-guan-li"></a>

服务商管理主要是添加各云平台的AccessKey，通过平台提供的API获取到云主机信息，不同的云厂商获取AccessKey的方法不同，可查找相应云平台的官方文档获取。

以阿里云为例查看AccessKey方法：点击个人头像 - accesskeys - 显示即可。

![&#x963F;&#x91CC;&#x4E91;AccessKeys](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LW9xdmhUekn-sXlVN62%2F-LW9ygdTB3LyQT0pWxhi%2Faccesskey.png?alt=media&token=13a334ae-dd8b-4cba-bbdc-09fcab035381)

查看到服务商的AccessKey信息后，添加服务器即可，如下图：

![&#x670D;&#x52A1;&#x5546;&#x7BA1;&#x7406;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LW9xdmhUekn-sXlVN62%2F-LW9ymFFqO3ZGAfwydlA%2Flistgongyings.png?alt=media&token=db3927cf-7eca-475e-8463-f06e377baabf)

#### 5.3 脚本管理 <a id="53-jiao-ben-guan-li"></a>

服务器的批量操作可以通过添加脚本执行脚本实现，添加的脚本可手动点击「启动」执行到单台或者一组主机，主机列表为主机管理的主机信息，也可通过计划任务调用，定时执行脚本，执行记录以及修改日志记录在日志中。

目前脚本类型支持：

* shell
* python
* linuxyml
* winyml
* winps1

![&#x811A;&#x672C;&#x7BA1;&#x7406;&#x754C;&#x9762;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LW9xdmhUekn-sXlVN62%2F-LW9yz7qn5OF391mXx_X%2Fjiaoben.png?alt=media&token=3fb9e638-d245-44fe-a98c-2479fdde3f25)

#### 5.4 计划任务管理 <a id="54-ji-hua-ren-wu-guan-li"></a>

计划任务管理是在指定一个或一组主机上计划性执行的指令或脚本，目前支持linux和windows平台运行，相对应添加的方式有所不同，Linux平台计划任务语法与crontab语法一致，windows平台则需要用户手动输入计划执行的间隔，然后生成触发器即可。

通过在详情页中绑定主机或者批量停止计划任务，以及记录计划任务的执行记录。

![&#x8BA1;&#x5212;&#x4EFB;&#x52A1;&#x7BA1;&#x7406;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWA09aT-u0qBNeiqwGV%2F-LWAbUoafOd8Ht0Ai0Au%2F%E8%AE%A1%E5%88%92%E4%BB%BB%E5%8A%A1%E7%AE%A1%E7%90%86.png?alt=media&token=e4cb1ac3-0c2b-4a05-8b73-e26a4f77b058)

#### 5.5 文件上传 <a id="55-wen-jian-shang-chuan"></a>

通过选择主机以及指定路径批量把文件上传至目标主机，推送方式可以为Ansible或者Salt。

![&#x6587;&#x4EF6;&#x4E0A;&#x4F20;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWFgm-XWVMs5Ee1hblT%2F-LWFsB4Pcf9xXsNdLgl5%2F%E6%96%87%E4%BB%B6%E4%B8%8A%E4%BC%A0.png?alt=media&token=2ffcd775-d9da-4028-9ee0-d47c2b9fd7a9)

### 6 结语 <a id="6-jie-yu"></a>

通过操作中心平台，能够有效的简化运维操作流程，提高运维效率以及准确率，灵活的动态分组功能让传统的反复勾选操作成为过去，实现将一个的操作流程制作成完整的作业任务，同时对云平台主机进行集中化管理与监控，对云主机的维护也将更加方便，快捷。  


