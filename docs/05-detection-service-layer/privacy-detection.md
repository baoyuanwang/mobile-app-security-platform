# Privacy Detection

---

# 1. Overview

Privacy Detection（隐私检测）负责识别移动应用在用户数据处理过程中的安全与合规风险，包括敏感数据采集、违规访问、超范围使用、未授权传输以及隐私保护措施缺失等问题。

Privacy Detection 基于 Analysis Engine Layer 输出的程序分析结果，包括：

* Static Analysis Result；
* Dynamic Analysis Result；
* Data Access Behavior；
* Runtime Behavior Evidence；

结合：

* Privacy Rules；
* Compliance Policy；
* Data Classification Knowledge；
* AI Analysis Capability；

对应用的数据处理行为进行判断。

Privacy Detection 不负责采集应用行为，而负责判断：

> 应用的数据处理行为是否符合安全和隐私要求。

---

# 2. Design Objectives

Privacy Detection 的设计目标包括：

* 识别敏感数据访问行为；
* 分析数据采集和使用范围；
* 判断数据处理是否符合授权要求；
* 发现隐私违规风险；
* 提供可解释检测结果；
* 支撑应用审核和隐私治理。

---

# 3. Position in Architecture

Privacy Detection 属于 Detection Service Layer。

整体关系：

```
              Detection Service Layer


                       │


              Privacy Detection


                       ▲


                       │


       Standardized Analysis Result


                       ▲


                       │


             Analysis Engine Layer
```

---

# 4. Detection Scope

Privacy Detection 主要覆盖以下风险类型。

---

## 4.1 Sensitive Data Access

检测应用是否访问敏感数据。

包括：

* 联系人；
* 短信；
* 通话记录；
* 位置信息；
* 设备标识；
* 图片与媒体；
* 剪贴板数据；
* 账户信息。

---

## 4.2 Unauthorized Data Collection

检测应用是否存在未经授权的数据采集行为。

例如：

* 未声明权限访问；
* 后台采集；
* 超出业务必要范围采集；
* 隐蔽数据获取。

---

## 4.3 Data Transmission Risk

检测敏感数据传输行为。

包括：

* 数据上传；
* 网络传输目标；
* 第三方服务共享；
* 异常外传行为。

---

## 4.4 SDK Privacy Risk

检测第三方组件带来的隐私风险。

例如：

* SDK 采集敏感信息；
* SDK 权限滥用；
* SDK 数据共享。

SDK 识别能力由 Security Knowledge Platform 提供，Privacy Detection 负责风险判断。

---

## 4.5 Privacy Compliance Risk

结合隐私规则判断应用是否符合要求。

例如：

* 权限申请是否合理；
* 数据采集是否必要；
* 数据使用是否透明；
* 是否存在超范围处理。

---

# 5. Detection Capability

Privacy Detection 主要基于以下能力完成判断。

---

## 5.1 Data Access Analysis

利用 Analysis Engine 提供的数据访问信息。

包括：

* API 调用；
* 权限使用；
* 数据访问路径；
* 数据处理逻辑。

用于识别：

应用访问了什么数据。

---

## 5.2 Data Flow Analysis

分析数据从来源到去向的流动关系。

例如：

```
User Contact

      ↓

Application

      ↓

Third Party Server
```

判断：

* 数据来源；
* 数据处理过程；
* 数据输出位置。

---

## 5.3 Runtime Privacy Behavior Analysis

结合动态分析结果。

观察：

* 实际数据访问；
* 网络请求；
* 后台行为；
* 用户交互过程。

用于发现：

静态分析无法确认的真实行为。

---

## 5.4 Policy Based Detection

结合隐私规则和合规策略。

例如：

```
Sensitive Data Access

+

No User Authorization

+

Network Upload

↓

Privacy Risk
```

---

## 5.5 AI Assisted Analysis

利用 AI 能力辅助：

* 数据流理解；
* 行为语义分析；
* 风险解释；
* 复杂场景判断。

AI 不替代隐私规则，而用于增强分析能力。

---

# 6. Detection Workflow

典型流程：

```
Application


    │


    ▼


Analysis Engine Result


    │


    ▼


Privacy Detection


    │


    ├── Sensitive Data Analysis


    │


    ├── Data Flow Analysis


    │


    ├── Runtime Behavior Analysis


    │


    └── Compliance Policy Analysis


    │


    ▼


Privacy Detection Result
```

---

# 7. Input and Output

## Input

来自 Analysis Engine：

* Static Analysis Result；
* Dynamic Analysis Result；
* Permission Information；
* API Usage；
* Data Access Behavior；
* Network Behavior。

来自 Security Knowledge Platform：

* Privacy Rules；
* Data Classification；
* SDK Knowledge；
* Compliance Requirements。

---

## Output

输出：

```
Privacy Detection Result


├── Privacy Risk Type

├── Sensitive Data Category

├── Data Processing Behavior

├── Evidence

├── Risk Level

├── Reason

└── Recommendation
```

---

# 8. Relationship with Other Modules

---

## 8.1 Relationship with Analysis Engine Layer

Analysis Engine 提供：

```
Application Data Behavior
```

例如：

```
Access Contact API

Read Device Identifier

Upload Data
```

Privacy Detection 判断：

```
是否违反隐私要求
```

---

## 8.2 Relationship with Security Knowledge Platform

Security Knowledge Platform 提供：

* 数据分类知识；
* 隐私规则；
* SDK 信息；
* 合规要求。

Privacy Detection 基于这些知识完成判断。

---

## 8.3 Relationship with Security Operation Platform

Privacy Detection 输出：

* 风险类型；
* 违规证据；
* 修复建议。

Security Operation Platform 根据结果：

* 人工审核；
* 整改通知；
* 合规治理。

---

# 9. Design Principles

---

## Behavior and Policy Combination

隐私风险判断必须结合：

* 实际行为；
* 合规策略。

---

## Evidence Driven

每一个隐私风险必须能够追溯到：

* 数据来源；
* 访问行为；
* 数据流向。

---

## Least Privilege Principle

关注：

应用是否仅访问业务必要的数据。

---

## Explainable Detection

输出：

* 访问了什么数据；
* 如何访问；
* 是否违规。

---

## Continuous Compliance Evolution

支持随着：

* 法规变化；
* 平台政策变化；
* 用户隐私要求变化；

持续更新检测能力。

---

# 10. Summary

Privacy Detection 是移动应用安全检测平台的重要业务检测能力。

它基于 Analysis Engine Layer 提供的数据访问、程序行为和运行证据，结合隐私规则、数据分类知识和 AI 能力，对应用的数据处理行为进行安全与合规判断。

Privacy Detection 关注：

> 应用如何处理用户数据。

而不是：

> 应用是否包含恶意代码。

通过静态分析、动态行为分析和合规策略结合，可以有效发现移动应用中的隐私风险，支撑应用审核、整改和生态治理。
