# 第四章 Analysis Engine Layer（应用分析引擎层）

> Chapter 4  
> Analysis Engine Layer

---

## 1. 本章概述

Analysis Engine Layer 是移动应用安全检测平台的核心分析能力层。

该层负责对移动应用进行程序分析和运行时分析，提取应用程序的结构信息、代码特征、运行行为以及安全证据，为上层 Detection Service Layer 提供统一、标准化的 Analysis Result。

Analysis Engine 不直接判断应用是否违规，而是回答：

> **应用包含什么？应用运行过程中做了什么？**

安全风险判定、业务规则匹配、AI 推理等能力均属于 Detection Service Layer。

因此，Analysis Engine 是整个检测平台的数据生产者（Producer），Detection Service 是分析结果的消费者（Consumer）。

---

## 2. 在整体架构中的位置

```text
                         Mobile Application

                                │
                                ▼

                 Analysis Engine Layer（Chapter 4）

     ┌────────────────────────────────────────────┐
     │                                            │
     │  Package Parser                            │
     │                                            │
     │  Static Analysis Engine                    │
     │                                            │
     │  Dynamic Analysis Engine                   │
     │                                            │
     │  Analysis Result Management                │
     │                                            │
     └────────────────────────────────────────────┘

                                │
                                ▼

                    Unified Analysis Result

                                │
                                ▼

                Detection Service Layer（Chapter 5）

                                │
                                ▼

                         Risk Decision
```

Analysis Engine 与 Detection Service 之间采用统一的数据契约（Analysis Result）进行解耦。

这种设计使分析能力和业务能力能够独立演进：

- 新增分析能力时，不影响检测规则；
- 新增检测服务时，不需要修改分析引擎；
- AI 模型升级时，不影响底层分析流程。

---

## 3. 核心设计原则

### 3.1 分析与检测分离

Analysis Engine：

负责发现事实（Fact Discovery）。

包括：

- 应用结构解析；
- 程序分析；
- API 调用分析；
- 数据流分析；
- 运行行为采集；
- 网络行为采集；
- 系统调用分析。

输出：

```text
Analysis Result
```

Detection Service：

负责业务判断（Risk Decision）。

包括：

- 恶意软件检测；
- 隐私违规检测；
- 内容安全检测；
- 恶意广告检测；
- 涉诈检测；
- 仿冒侵权检测。

输出：

```text
Risk Decision
```

---

### 3.2 静态分析与动态分析并行

静态分析与动态分析互相独立。

两条分析流水线不存在依赖关系。

```text
                  Application Package

                         │
          ┌──────────────┴──────────────┐
          ▼                             ▼

 Static Analysis Engine         Dynamic Analysis Engine

          ▼                             ▼

 Static Analysis Result        Dynamic Analysis Result

          └──────────────┬──────────────┘
                         ▼

             Analysis Result Management

                         ▼

               Unified Analysis Result
```

静态分析主要回答：

> 应用代码中可能存在什么能力？

动态分析主要回答：

> 应用运行时实际执行了什么行为？

两类分析结果最终统一汇聚，由上层 Detection Service 综合判断。

---

### 3.3 分层解耦

Analysis Engine 内部进一步划分为四个组件：

| 组件 | 职责 |
|------|------|
| Package Parser | 解析应用安装包及元数据 |
| Static Analysis Engine | 程序静态分析 |
| Dynamic Analysis Engine | 应用运行分析 |
| Analysis Result Management | 分析结果统一管理 |

各组件职责清晰、接口稳定，可独立演进。

---

## 4. Analysis Engine 内部架构

```text
Analysis Engine Layer

├── Package Parser
│
├── Static Analysis Engine
│      ├── Program Representation
│      ├── Control Flow Analysis
│      ├── Data Flow Analysis
│      ├── Call Graph Analysis
│      ├── Taint Analysis
│      ├── SDK Analysis
│      └── Static Analysis Result
│
├── Dynamic Analysis Engine
│      ├── Runtime Instrumentation Framework
│      ├── Runtime Event Collection
│      ├── Network Behavior Analysis
│      ├── Behavior Reconstruction
│      └── Dynamic Analysis Result
│
└── Analysis Result Management
```

需要注意：

Program Representation、Taint Analysis 等并不是独立模块，而是 Static Analysis Engine 的内部技术能力。

同样，Runtime Instrumentation、Behavior Reconstruction 也是 Dynamic Analysis Engine 的内部组成部分。

---

## 5. 数据流

Analysis Engine 的整体数据流如下：

```text
          Application Package

                  │

                  ▼

          Package Parser

                  │

     ┌────────────┴────────────┐
     ▼                         ▼

Static Analysis         Dynamic Analysis

     ▼                         ▼

Static Result           Dynamic Result

      └────────────┬────────────┘

                   ▼

      Analysis Result Management

                   ▼

      Unified Analysis Result
```

整个过程中不进行业务风险判断，仅输出标准化分析结果。

---

## 6. 与 Detection Service 的关系

Analysis Engine 输出：

```text
Application accesses contacts

Application uploads location

Application loads external dex

Application opens overlay window
```

Detection Service 判断：

```text
Privacy Violation

Malware

Malicious Advertisement

Fraud Risk
```

因此：

- Analysis Engine 负责采集事实；
- Detection Service 负责解释事实。

这是平台可扩展性的核心设计原则。

---

## 7. 本章组成

本章由以下四个模块组成：

| 文件 | 内容 |
|------|------|
| 01-package-parser.md | 应用包解析组件 |
| 02-static-analysis-engine.md | 静态分析引擎 |
| 03-dynamic-analysis-engine.md | 动态分析引擎 |
| 04-analysis-result-management.md | 分析结果管理 |

后续章节将分别介绍各模块的设计、关键技术、实现流程及技术指标。
