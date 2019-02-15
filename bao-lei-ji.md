---
description: 【AukeyCloud】堡垒机使用手册 v1.0
---

# 03 堡垒机

### 1. 模块介绍 <a id="1-mo-kuai-jie-shao"></a>

AukeyCloud堡垒机是一种运维安全审计系统。主要的功能是对运维人员的运维操作进行审计和权限控制。同时堡垒机还有账号集中管理，单点登陆的功能。 堡垒机在安全运维中的主要功能是，通过堡垒机进行事前资源授权，事中录像监控，事后指令审计，来保障自身业务安全。

**概念和术语**

* 凭证，用于管理远程主机时的账号、密码，及使用的远程协议

### 2. 特点及优势 <a id="2-te-dian-ji-you-shi"></a>

* 集中账号管理，普通用户以及管理用户管理
* 统一凭证管理，主机密码/密钥集中化管理，精细化授权
* 多云的资产纳管，对私有云、公有云资产统一纳管
* 主机授权管理，使用主机树形式，主机或主机组灵活授权
* 多维度授权，可对用户、主机分别授权
* 会话管理，标签页形式展开，在线会话管理
* 安全审计，Linux指令记录，Windows录像支持
* 体验极佳的Web Terminal

### 3. 堡垒机操作流程 <a id="3-bao-lei-ji-cao-zuo-liu-cheng"></a>

![&#x5821;&#x5792;&#x673A;&#x64CD;&#x4F5C;&#x6D41;&#x7A0B;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWOdfllbbCMoZeSp_a5%2F-LWOiIIfYu7DuN7CXmcw%2F%E5%A0%A1%E5%9E%92%E6%9C%BA%E6%93%8D%E4%BD%9C%E6%B5%81%E7%A8%8B.png?alt=media&token=ea1d47b2-5b3e-4b8a-95eb-05e0d89f6500)

堡垒机具体操作流如下：

（1）主机，**操作中心**模块中收集主机，如已经存在主机则跳过

（2）用户，**用户管理**中添加用户，如已经存在用户则跳过

（3）协议，添加协议，协议分为密码和密钥

（4）凭证，添加凭证 - 关联协议 - 关联用户 - 关联主机

（5）远程连接主机，关联凭证的主机自动显示在远程连接组中，可进行远程连接

（6）录像回放，远程操作的主机会生成日志信息，使用回放功能可进行历史操作查看

### 4. 功能介绍 <a id="4-gong-neng-jie-shao"></a>

#### 4.1 远程连接 <a id="41-yuan-cheng-lian-jie"></a>

远程连接是对当前用户有权限远程操作的主机进行一个展示，主机目录树同步操作中心目录树，具体的操作步骤如图：

![&#x8FDC;&#x7A0B;&#x8FDE;&#x63A5;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWPRKQZfj2UnM2dXcEQ%2F-LWPSFu6sBzhtKGzPQXG%2F%E8%BF%9C%E7%A8%8B%E8%BF%9E%E6%8E%A5.png?alt=media&token=8abca709-8a81-4470-81d6-089d13129bf6)

**注意：**此处连接IP默认以内部IP连接，如需要使用外部IP连接（如云主机）则选择外部IP。

#### 4.2 凭证管理 <a id="42-ping-zheng-guan-li"></a>

凭证主要用于管理远程主机时的用户名、密码，及使用的远程协议，对用户授权使用某个凭证登录主机也是在这里进行，同时为了保证凭证密码/秘钥安全，增加解密凭证的功能，解密时需要输入当前用户的密码。

![&#x51ED;&#x8BC1;&#x7BA1;&#x7406;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWPTajVXe7H2BzXa37R%2F-LWPWRzcnZtTTHroeBQS%2F%E5%87%AD%E8%AF%81%E5%85%B3%E9%97%AD.png?alt=media&token=b87f2e20-d468-498a-89c6-e108b1f0e972)

#### 4.3 安全审计 <a id="43-an-quan-shen-ji"></a>

安全审计实现对运维人员操作行为的控制和审计，使用堡垒机过程中如果有误操作、违规操作导致的操作事故，通过录像回放以及录屏回放功能快速定位原因和责任人。

![&#x5B89;&#x5168;&#x5BA1;&#x8BA1;](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LVLxprI5lcqcXwrFU-B%2F-LWPTajVXe7H2BzXa37R%2F-LWPamp-jMs3TDXf3yRW%2F%E5%AE%89%E5%85%A8%E5%AE%A1%E8%AE%A1.png?alt=media&token=9ae8aa6f-8e3a-417c-9e08-565323929297)

**注意：** 为了安全起见，安全审计功能目前仅对超级管理员开放，如需开放需在**「用户管理」-「账号管理」**中打开超级管理员选项。

### 5. 结语 <a id="5-jie-yu"></a>

AukeyCloud堡垒机支持Windows/Linux系统操作指令审计的堡垒机，多云支持、混合云管理是该模块的基础，对于企业而言，使用堡垒机模块的凭证管理，可以对运维人员的权限做更细粒度的控制，通过安全审计功能，对解决生产事故提供了有力依据，总之通过堡垒机模块可以极大方便操作，更简便，更快速，更安全。



