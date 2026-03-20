# Godot 存档与联机学习设计文档

**日期：** 2026-03-24

## 1. 目标

面向一名有约一年游戏服务器开发经验、当前负责战斗模块、准备参与一个从 0 开始的 Godot 小项目，并承担 `存档 + 联机` 职责的开发者，设计一条 `3 个月`、低时间成本、可执行的学习路线。

本路线的目标不是把 Godot 所有功能学完，而是做出一个 `2D 像素风、种田 + 战斗、单机优先、后续可迁移联机` 的工程原型，并在过程中建立正确的：

- Godot 开发心智模型
- 游戏状态建模能力
- 存档结构设计能力
- 未来联机迁移边界意识

## 2. 个人背景与项目约束

### 个人背景

- 游戏服务器开发经验约一年
- 当前主要负责战斗模块
- 对状态流转、模块边界、运行时逻辑已有一定理解
- 对 Godot 客户端开发仍是新手

### 项目条件

- 引擎：Godot
- 团队主要语言：`GDScript`
- 平台：`PC 桌面`
- 玩法：`2D 像素风，种田 + 战斗，类似星露谷物语`
- 第一阶段目标：`工程原型`
- 时间：工作日较忙，整体学习周期按 `3 个月` 规划
- 资料偏好：`中文优先`

### 结论

路线不能走“大而全”的学习方式，必须强调：

- 学一点就能转化成项目产出
- 严格控制范围
- 先单机闭环，再做联机预留
- 不在第一阶段混用太多技术路线

## 3. 语言与技术选择建议

### 推荐主线：GDScript

建议第一阶段完全使用 `GDScript`。

原因：

- 团队已经决定使用 GDScript，协作成本最低
- Godot 官方与社区资料对 GDScript 支持最完整
- 对新手来说，更容易建立 Godot 的场景、节点、信号、资源等基础认知
- 你当前最需要补的是 Godot 开发方式，而不是语言多样性

### 关于 C#

Godot 支持项目内同时存在 `GDScript` 和 `C#`，两者可以交互，但当前不建议作为主线：

- 会增加编辑器、构建、调试和团队协作复杂度
- 两种语言脚本不能互相继承
- 对当前项目阶段收益不高

结论：

- `3 个月主线只学 GDScript`
- `C# 保持了解，不作为当前必学项`

## 4. 学习策略总览

推荐采用：`项目里程碑优先 + 少量架构预埋`

也就是：

- 主线围绕一个最小工程原型推进
- 不是先把所有引擎知识学完
- 也不是一上来过度设计完整架构
- 只在三个关键位置提前埋结构：
  - 数据模型
  - 存档边界
  - 联机迁移边界

### 不推荐的两种路线

#### 1. 引擎基础优先

优点：上手平缓。  
缺点：容易学很多但没有项目产出，时间成本高。

#### 2. 架构预埋优先

优点：理论上结构最完整。  
缺点：对 Godot 新手前期成本过高，容易卡在引擎细节里。

## 5. 3 个月路线结构

学习和实现分成四层：

1. `Godot 工程基本功`
2. `单机玩法闭环`
3. `存档系统`
4. `联机预留设计`

真正需要提前思考的只有三个边界：

- 玩家、地块、作物、怪物、背包的数据模型
- 运行时状态与持久化状态的分离
- 输入、状态变更、表现层反馈的分离

## 6. 时间预算适配方案

考虑到工作日通常到晚上 9 点，建议按低时间预算执行：

- 工作日：`2 次 x 45-60 分钟`
- 周末：`1 次 x 3-4 小时`
- 每周只追 `1 个可见产出`
- 每 2 周为一个 Sprint

重点不是学得多，而是持续推进。

## 7. 六个双周 Sprint 规划

### Sprint 1，第 1-2 周：Godot 最小工作流

目标：建立最基本的 Godot 心智模型。

学习内容：

- 场景、节点、脚本、信号
- CharacterBody2D 移动
- TileMapLayer 基础
- typed GDScript 基础写法

产出：

- 一个测试地图
- 玩家移动、碰撞、交互键
- 初版目录结构

不做：

- 复杂 UI
- Shader
- 高级动画系统

### Sprint 2，第 3-4 周：种田最小闭环

目标：用种田系统练状态建模。

学习内容：

- 地块状态设计
- 作物状态设计
- 基础交互与背包流转

产出：

- 锄地
- 播种
- 浇水
- 生长
- 收获
- 背包拿到作物

不做：

- 多作物体系
- 土地肥力
- 季节系统
- 复杂工具组合

### Sprint 3，第 5-6 周：战斗最小闭环

目标：做出最简单的战斗系统，并适配 Godot 的表现与碰撞组织。

学习内容：

- 攻击与受击流程
- 基础 hitbox / hurtbox
- 怪物最小状态集

产出：

- 玩家普攻
- 怪物受击
- 血量与死亡
- 掉落物进入背包

不做：

- 技能系统
- 复杂 AI
- 属性成长
- 多武器流派

### Sprint 4，第 7-8 周：存档 V1

目标：让核心玩法状态可以保存和恢复。

学习内容：

- JSON / Dictionary 序列化
- FileAccess
- 存档加载与恢复流程
- save_version

产出：

- 保存和读取玩家基础状态
- 保存和读取背包
- 保存和读取地块和作物
- 一个 `save_version`

不做：

- 多存档槽高级功能
- 压缩与加密
- 增量存档
- 云存档

### Sprint 5，第 9-10 周：工程整理

目标：把已经有的功能收成可维护结构。

学习内容：

- 模块边界
- Autoload 的克制使用
- 信号与直接调用的分层

产出：

- `player`、`farm`、`combat`、`inventory`、`save` 模块初步拆分
- 目录结构整理
- 一份简短数据说明文档

不做：

- 过度抽象
- 提前为未来所有玩法设计框架

### Sprint 6，第 11-12 周：联机预留

目标：不做正式联机，但提前看清改造边界。

学习内容：

- authoritative 状态意识
- 输入与状态变更解耦
- Godot 高层多人概念理解

产出：

- 一份“未来联机改造点”笔记
- 一份同步对象清单：玩家、怪物、地块、掉落物
- 有余力时做一个隔离的小型双人同步实验

不做：

- 正式房间系统
- 断线重连
- 完整多人玩法同步
- 专服

## 8. 必须优先补的知识树

### 第一层：必须尽早学

#### 1. Godot 的场景 / 节点思维

你必须尽快搞清楚：

- 什么逻辑挂在 Node 上
- 什么数据应该单独存放
- 什么东西只是表现，不应该当业务状态来源

#### 2. GDScript 的工程化写法

重点不是学语法大全，而是会用：

- typed GDScript
- `@export`
- `class_name`
- signal
- 场景实例化
- 节点引用
- 少量 Autoload

#### 3. 2D 项目最小能力集

- CharacterBody2D
- 碰撞体
- TileMapLayer
- AnimatedSprite2D 或 AnimationPlayer
- Camera2D
- 输入映射

#### 4. 状态建模

这是你这条路线最重要的能力。

必须区分：

- 运行时状态
- 持久化状态
- 表现状态

例子：

- 地块是否被锄过：持久化状态
- 作物当前成长阶段：持久化状态
- 玩家挥锄动画播到哪一帧：表现状态

### 第二层：你可以直接复用的服务端经验

- 模块边界意识
- 事件流 / 状态流转拆分
- 存档版本意识
- authoritative 思维

### 第三层：前 3 个月明确先不系统学习

- 复杂 UI
- 高级动画树
- Shader 与特效
- 正式多人联机实装
- 过重的通用框架设计

## 9. 建议的项目范围

3 个月工程原型只保留以下系统：

- 玩家移动
- 地块交互
- 播种 / 浇水 / 收获
- 简单背包
- 简单战斗
- 怪物掉落
- 存档与加载

明确不做：

- 日夜循环
- NPC 关系 / 任务系统
- 地图切换
- 装备系统
- 技能树
- 大量 UI 打磨
- 正式联机

## 10. 存档设计建议

不要直接把节点树当存档结构。更稳的做法是：

1. 先定义统一的 `save_data`
2. 各系统把状态写入 `save_data`
3. 统一序列化到 `user://`
4. 加载时先恢复数据，再恢复表现

建议最少保存：

- 玩家基础数据
- 背包数据
- 地块数据
- 作物数据
- 世界时间 / 阶段数据
- `save_version`

## 11. 联机预留建议

虽然 3 个月不做完整联机，但从一开始应避免：

- 直接从 UI 读取业务状态
- 直接从动画状态推导核心状态
- 把关键状态散落到多个节点里
- 输入、逻辑、表现高度耦合

应该预留：

- 输入命令边界
- 状态变更入口
- 持久化写入入口
- 表现刷新入口

## 12. 资料清单与推荐顺序

优先使用 `Godot 官方中文稳定文档`。

### 必看入口

- 官方中文稳定文档首页  
  https://docs.godotengine.org/zh-cn/stable/
- Godot 简介  
  https://docs.godotengine.org/zh-cn/stable/getting_started/introduction/introduction_to_godot.html
- 2D 游戏起步教程  
  https://docs.godotengine.org/zh-cn/stable/getting_started/first_2d_game/index.html
- GDScript 基础  
  https://docs.godotengine.org/zh-cn/stable/tutorials/scripting/gdscript/gdscript_basics.html
- GDScript 静态类型  
  https://docs.godotengine.org/zh-cn/stable/tutorials/scripting/gdscript/static_typing.html
- Signal 基础  
  https://docs.godotengine.org/zh-cn/stable/getting_started/step_by_step/signals.html
- 实例化与信号  
  https://docs.godotengine.org/zh-cn/stable/tutorials/scripting/instancing_with_signals.html
- 使用 CharacterBody2D  
  https://docs.godotengine.org/zh-cn/stable/tutorials/physics/using_character_body_2d.html
- 使用 TileMap  
  https://docs.godotengine.org/zh-cn/stable/tutorials/2d/using_tilemaps.html
- 单例（Autoload）  
  https://docs.godotengine.org/zh-cn/stable/tutorials/scripting/singletons_autoload.html
- Resource 教程  
  https://docs.godotengine.org/zh-cn/stable/tutorials/scripting/resources.html
- 保存游戏  
  https://docs.godotengine.org/zh-cn/stable/tutorials/io/saving_games.html
- FileAccess  
  https://docs.godotengine.org/zh-cn/stable/classes/class_fileaccess.html
- JSON  
  https://docs.godotengine.org/zh-cn/stable/classes/class_json.html
- 高级多人游戏  
  https://docs.godotengine.org/zh-cn/stable/tutorials/networking/high_level_multiplayer.html

### 建议顺序

1. 文档首页
2. Godot 简介
3. 2D 游戏起步教程
4. GDScript 基础
5. GDScript 静态类型
6. Signal 基础
7. 实例化与信号
8. CharacterBody2D
9. TileMap
10. Resource
11. Autoload
12. 保存游戏
13. FileAccess
14. JSON
15. 高级多人游戏

### 使用原则

- 只看当前 Sprint 真会用到的页面
- 官方文档为主，视频只做补充
- 卡住时查类参考，不顺读类参考全集

## 13. 成功标准

3 个月结束时，达到以下结果就说明路线成功：

- 能用 GDScript 独立维护 Godot 2D 小项目代码
- 做出一个 `种田 + 战斗 + 存档` 的最小单机工程原型
- 存档结构带有基本版本意识
- 能清晰说明未来联机需要改造的边界
- 建立一套适合自己时间预算的学习方式
