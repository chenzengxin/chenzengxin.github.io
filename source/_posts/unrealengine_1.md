---
title: "虚幻引擎学习1"
author: "Chenzengxin"
date: 2019.08.29
---


## 常用术语
> __Project__：保存所有组成单独游戏的所有内容和代码。<br />
> __Object__：虚幻引擎中，最基础的构建单元。<br />
> __Class__：用于定义在创建虚幻引擎游戏中使用的特定Actor或对象的行为和属性。<br />
> __Actors__：Actor是支持三维转换（如平移、旋转和缩放）的泛型类 (类似Unity GameObject?)<br />
> __Component__：组件，可为Actor添加新的功能。<br />
> __Pawn__：Actor的子类，充当游戏中的角色。<br />
> __Character__：角色（Character） 是Pawn Actor的子类，旨在用作玩家角色。
> __PlayerController__：玩家控制器，获取玩家输入并将其转换为交互。<br />
> __AIController__：AI控制器，用以控制游戏中的非玩家角色。<br />
> __Brush__：用以描述关卡中的三维体积信息。（根据附加在它们上的效果，体积具有多种用途，例如：阻塞体积（Blocking Volume）（它们是不可见的，用于阻止Actor穿过它们）、伤害产生体积（Pain Causing Volume）（随着时间的推移，会对与其重叠的Actor造成伤害）或触发器体积（Trigger Volume）（用作在Actor进入或退出它们时引发事件的一种方式）。）<br />
> __Level__：是用户定义的游戏区域。 我们主要通过放置、变换及编辑Actor的属性来创建、查看及修改关卡。 在虚幻编辑器中，每个关卡都被保存为单独的.umap文件，所以它们有时也被称为“地图”。<br />
> __World__：世界场景（World） 中包含载入的关卡列表。它可处理关卡流送和动态Actor的生成（创建）。
> __GameState__：包含要复制到游戏中的每个客户端信息，表示每个联网玩家的“游戏状态”。<br />
---
## 工具和编辑器

#### 关卡编辑器
