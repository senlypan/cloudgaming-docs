# 问题背景

![访问统计](https://visitor-badge.glitch.me/badge?page_id=senlypan.cloudgaming.02-problem-background&left_color=blue&right_color=red)

> 作者: 大厂研究员
>
> 更新: 2022-07-25

## 概述

### 云游戏

云游戏，有时称为按需游戏或游戏即服务或游戏流媒体，是一种在线游戏，它在远程服务器上运行视频游戏并将其直接 **流式传输** 到用户的设备，或者更通俗地说，远程玩游戏从云。它与传统的游戏方式形成对比，其中游戏在用户的视频游戏控制台、个人计算机或移动设备上本地运行。

### 背景

云游戏平台的运行方式与 **远程桌面** 和 **视频点播服务** 类似；游戏在提供商的专用硬件上远程存储和执行，并通过客户端软件作为视频流式传输到玩家的设备。客户端软件处理玩家的输入，这些输入被发送回服务器并在游戏中执行。一些云游戏服务基于对虚拟化 Windows 环境的访问，允许用户像通常在本地计算机上一样下载和安装服务客户端和游戏。

云游戏可能具有优势，因为它无需购买昂贵的计算机硬件或将游戏直接安装到本地游戏系统上。云游戏可以在各种计算设备上使用，包括智能手机和平板电脑等移动设备、数字媒体播放器或专有的类似瘦客户端的设备。一些服务可能会提供额外的功能来利用这个模型，包括观众加入玩家会话并临时控制游戏的能力。

但是，云游戏需要可靠的 **高速互联网连接**。对于缺乏此类选项或数据上限可能会限制使用的地区的用户来说，这可能是一个限制。即使有可用的高速连接，流量拥塞和其他影响网络延迟的问题也会影响云游戏的性能。此外，云游戏的成本从通过零售店和数字店面的传统分销转移到运行云游戏服务的数据服务器。与传统分销相比，需要新的成本结构来支付这些运营成本。这通常是基本订阅模式，但服务还包括购买要在云服务上运行的游戏的成本，即使用户不像零售或数字发行那样拥有游戏。

### 基础设施考虑

云游戏需要大量基础设施才能使服务按预期工作，包括用于运行游戏的 **数据中心** 和 **服务集群**，以及用于将流传输给用户的 **高带宽** 互联网连接和 **低延迟**。多年来，使云游戏可行所需的网络基础设施在大多数地理区域都无法使用，或者消费者市场无法使用。由于它们对高质量流视频的依赖，定期使用服务的能力也可能受到某些互联网服务提供商强制执行的数据上限的限制。

云游戏服务质量的一个主要因素是延迟，因为用户输入之间的延迟量以及它们何时生效会影响游戏玩法——尤其是在依赖精确输入的快节奏游戏中（例如第一人称射击游戏和格斗游戏）。减少延迟的尝试包括使用缓存，因为缓存的数据可以“存储在本地......并且可以在需要时检索”。

提供商的专用硬件可以随着时间的推移进行升级，以支持渲染和流的更高分辨率和帧速率。在云游戏的开发阶段也需要考虑衡量用户总体满意度的体验质量。

### 国内案例

例如 [阿里云 - 云游戏 PaaS 平台](https://www.aliyun.com/product/industryengine/cloudgamingplatform) 则为游戏云化量身打造的一站式服务平台，具备游戏快速适配、资源弹性伸缩、全局智能调度、可视化数据运营和完善的平台运维能力。平台支持海量游戏稳定运行，量身打造的容器技术和协议确保游戏体验，多样化的SDK支持各类终端APP开发。满足用户联机互动、即点即用、微端试玩等创新需求。能力核心：

- 游戏适配
- 资源伸缩
- 全局调度
- 数据运营
- 平台运维 

## 问题与挑战

### 终端成本高

玩家购买高端主机设备来适应游戏不断提升的硬件要求，极大程度地加重了玩家成本

### 游戏包越来越大，下载安装成本高

游戏画面越来越精细的同时也带来了不断膨胀的游戏包体，给游戏存储与推广都带来了更大的压力和成本

### 游戏无法在多种终端间自由切换

各类终端（PC、主机、手机）上的游戏内容往往是无法共享的，玩家的体验方式也被锁定在了单一的环境里

### 外挂和破解程序多

由于游戏在本地运行，往往会给外挂或破解软件留下可乘之机，而云端运行的游戏可以避免绝大多数此类威胁





## 应用场景

### 游戏内容商，游戏渠道

- 便捷试玩，提高推广效率
- 跨端体验，覆盖更多场景
- 即点即玩，免除游戏下载
- 免除外挂干扰，创造公平竞技环境

### 运营商

- 5G核心体验场景，手机畅玩主机大作
- 流量杀手，用户数据流量使用大幅提升
- 为家庭端带来主机级游戏体验及3A作品

👉 [更多应用场景](https://help.aliyun.com/document_detail/176364.htm)


## 技术挑战

### 1、实时性

游戏的整体延迟包括了游戏逻辑运算时间、音画渲染的时间，加上编码的延时、网路传输的延时、客户端解码的延时、客户端向服务端发送控制信息的延时，云游戏的实时性要达到一个可令玩家接受的程度，这个技术挑战是非常高的，当然也要依靠 **硬件** 和 **网络** 本身的性能，如果没有足够的带宽也不可能做到。

### 2、虚拟化技术

虚拟化在服务端已经非常成熟，有虚拟机技术以及各种容器技术，但是在桌面上就不是那么成熟，普通的虚拟桌面不支持 GPU 的虚拟化，而游戏非常依赖 GPU 渲染，若没有 GPU 的虚拟化就没办法实现云游戏了，所以虚拟化是一个很大的技术瓶颈。

### 3、经济性

每个并发用户的服务器硬件成本关系到这个模式能否成功商业化，如果成本超出了用户可接受的范围，那就没有办法实现盈利。

### 4、运维管理

云游戏的运维管理跟传统的服务器运维管理不一样，因为用到的服务器硬件不一样，同时硬件负载又很高，这对运维管理提出了新的挑战，所以在技术上就要解决这些问题。

## 解决方案优势

- 之于用户
    - 低延迟高画质
        - 支持1080P、4K画质，60帧率；智能码率控制，流畅不卡顿
    - 低配设备跨平台随意玩高配游戏
        - 无需高配置电脑，PC、手机、电视等多终端随时随地畅玩 3A 级游戏大作
    - 防外挂
        - 游戏完全在云端运行，不用再担心外挂，减少客户端开发成本
    - 轻量客户端
        - 下载轻量级的游戏客户端，即点即玩，免下载安装，告别庞大的游戏客户端，减少用户流失
- 之于游戏运营商
    - 快速接入、平稳上线
        - 帮助客户快速上线运营
    - 丰富的云资源，优化成本
        - 全国高性能服务节点与高效调度策略，多维度降低成本


## 参考资料

- [CSDN - 云游戏的架构设计和技术实现](https://blog.csdn.net/tonnychu/article/details/113842624)