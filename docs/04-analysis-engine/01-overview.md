# 第四章 Analysis Engine Layer（应用分析引擎层）

> Chapter 4  
> Analysis Engine Layer

版本：V1.0

---

# 1. 本章概述

Analysis Engine Layer 是移动应用安全检测平台的核心分析能力层。

该层负责对开发者提交的移动应用程序进行深度分析，通过静态分析、动态分析等技术手段，提取应用程序代码、资源、运行时行为、网络通信、系统调用等安全相关信息，形成标准化的应用分析结果（Analysis Result），提供给上层 Detection Service Layer 进行业务风险判断。

本层的核心目标：

> **回答“应用做了什么”，而不是判断“应用是否违规”。**

---

# 2. Analysis Engine Layer 定位

整体架构：

```
Application Package

        |
        |
        ▼

Analysis Engine Layer

        |
        |
        ▼

Analysis Result

        |
        |
        ▼

Detection Service Layer

        |
        |
        ▼

Risk Decision
```

---

Analysis Engine Layer 与 Detection Service Layer 的职责边界：

|模块|职责|
|-|-|
|Analysis Engine|发现、采集、分析应用行为|
|Detection Service|基于业务规则判断安全风险|

例如：

Analysis Engine 输出：

```
Application accessed location data

Application uploaded data

Application loaded dynamic code

Application displayed overlay window
```

Detection Service 判断：

```
Privacy Violation

Malware

Malicious Advertisement

Fraud Risk
```

---

# 3. 总体架构

Analysis Engine Layer 采用双流水线架构：

```
                         APK/HAP

                            |
              +-------------+-------------+
              |                           |
              ▼                           ▼


      Static Analysis Pipeline     Dynamic Analysis Pipeline


              |                           |
              |                           |
              ▼                           ▼


       Static Analysis Result      Dynamic Analysis Result


              +-------------+-------------+

                            |
                            ▼


                Analysis Result Management


                            |
                            ▼


                 Unified Analysis Result

```

---

# 4. Static Analysis Engine（静态分析引擎）

## 4.1 功能定位

Static Analysis Engine 在不运行应用的情况下，对应用安装包、代码、配置文件、依赖组件等进行分析。

主要目标：

- 理解应用程序结构；
- 发现潜在风险能力；
- 提取代码级安全证据。

---

# 4.2 输入对象

支持：

- Android APK
- Android AAB
- HarmonyOS HAP
- 应用资源文件
- Manifest配置
- 签名文件
- 第三方SDK


---

# 4.3 Static Analysis Pipeline

```
Application Package

        |
        ▼

Package Parser

        |
        ▼

Program Representation

        |
        +----------------+
        |                |
        ▼                ▼

Control Flow      Data Flow

Analysis          Analysis


        |
        ▼

Security Analysis

        |
        ▼

Static Result

```

---

# 5. Program Representation（程序表示）

## 5.1 定位

Program Representation 是 Static Analysis Engine 的核心基础能力。

它负责将应用代码转换为适合程序分析的中间表示（Intermediate Representation）。

---

# 5.2 为什么需要 Program Representation

移动应用代码通常包含：

- Java/Kotlin代码；
- Smali代码；
- Native代码；
- 动态加载代码；
- 混淆代码。


直接分析源代码困难。

因此需要转换：

```
APK

↓

DEX

↓

IR

↓

CFG

↓

Call Graph

↓

Data Flow Graph

```

形成统一程序模型。

---

# 5.3 核心能力

## Control Flow Graph（CFG）

描述：

程序执行路径。


用于：

- 路径分析；
- 可达性分析；
- 恶意代码定位。


---

## Call Graph

描述：

函数调用关系。


用于：

- API调用追踪；
- SDK分析；
- 风险函数定位。


---

## Data Flow Graph（DFG）

描述：

数据传播路径。


用于：

- 敏感数据流分析；
- 隐私泄露分析。


---

## Taint Analysis

描述：

敏感数据传播。


例如：

```
IMEI

↓

Variable

↓

Network API

↓

Server

```

---

# 5.4 Static Analysis输出

输出：

Static Analysis Result。


示例：

```json
{
"type":"static",

"finding":[

{
"category":"permission",
"value":"READ_CONTACTS"
},

{
"category":"sdk",
"value":"xxx_sdk"
},

{
"category":"dynamic_load",
"value":"DexClassLoader"
}

]

}
```

---

# 6. Dynamic Analysis Engine（动态分析引擎）

## 6.1 功能定位

Dynamic Analysis Engine 通过在真实设备或模拟环境运行应用，捕获应用运行过程中的真实行为。

核心目标：

> 发现静态分析无法确认的运行时行为。

---

# 6.2 输入

```
APK/HAP

+

Runtime Environment

```

运行环境包括：

- 真机；
- 沙箱；
- 云手机环境。


---

# 6.3 Dynamic Analysis Pipeline

```
Application

      |
      ▼

Runtime Environment

      |
      ▼

Runtime Instrumentation

      |
      ▼

Runtime Event Collection

      |
      ▼

Behavior Reconstruction

      |
      ▼

Dynamic Analysis Result

```

---

# 7. Runtime Instrumentation Framework（运行时插桩框架）

## 7.1 定位

Runtime Instrumentation Framework 是动态检测的数据采集基础。

负责：

> 在应用运行过程中获取关键运行行为。

---

# 7.2 核心技术

包括：

## Java / Android Framework Hook

监控：

- API调用；
- 权限访问；
- 文件访问。


---

## ART Runtime Instrumentation

监控：

- 方法调用；
- 参数；
- 返回值。


---

## Native Layer Instrumentation

监控：

- JNI调用；
- Native函数。


---

## Network Instrumentation

监控：

- HTTP/HTTPS；
- DNS；
- Socket。


---

# 7.3 Runtime Event

采集：

```
API Call

File Access

Network Request

Permission Usage

Process Behavior

UI Event

Memory Behavior

```

---

# 8. Behavior Reconstruction（行为重建）

## 8.1 定位

Behavior Reconstruction 是 Dynamic Analysis Engine 的后处理能力。

负责：

将大量离散 Runtime Event 转换为连续行为描述。

---

# 8.2 为什么需要

原始事件：

```
Location API

Network API

SDK Call

```

无法直接表达业务行为。


经过重建：

```
Application collected location data

and transmitted it externally

```

---

# 8.3 行为重建能力

包括：

## Event Correlation

事件关联。


例如：

```
Read Contact

+

HTTP Upload

```

---

## Execution Trace Reconstruction

恢复执行路径。


例如：

```
Login

↓

Permission Request

↓

Data Upload

```

---

## Behavior Sequence Analysis

分析行为序列。


---

# 8.4 Dynamic Analysis Result

示例：

```json
{
"type":"dynamic",

"behavior":[

{
"action":"collect",

"object":"location"
},

{
"action":"upload",

"destination":"xxx.com"
}

]

}
```

---

# 9. Analysis Result Management

## 9.1 定位

负责管理静态分析和动态分析输出结果。

核心能力：

- 结果汇聚；
- 数据标准化；
- 结果存储；
- 查询服务。


---

# 9.2 Result Model

统一模型：

```
Analysis Result

├── Static Result

├── Dynamic Result

├── Runtime Trace

├── Network Evidence

├── Screenshot

├── File Evidence

└── Metadata

```

---

# 10. 与 Detection Service Layer 的关系

Analysis Engine 输出：

```
Analysis Result
```

Detection Service 消费：

```
Analysis Result
```

例如：

---

## 隐私检测

输入：

```
Location Collection

+

Network Upload

```

判断：

```
Privacy Violation
```

---

## 恶意广告检测

输入：

```
Overlay Window

+

Auto Click

+

Background Launch

```

判断：

```
Malicious Advertisement
```

---

## 木马检测

输入：

```
Dynamic Loading

+

Remote Download

+

Execution

```

判断：

```
Malware Risk
```

---

# 11. 技术指标

|能力|指标|
|-|-:|
|APK解析成功率|≥99%|
|DEX解析覆盖率|≥95%|
|静态代码分析覆盖率|≥90%|
|动态行为采集覆盖率|≥95%|
|Runtime API监控覆盖率|≥95%|
|网络行为采集覆盖率|100%|
|行为重建准确率|≥90%|
|单应用分析时间|≤15分钟|

---

# 12. 本章总结

Analysis Engine Layer 是移动应用安全检测平台的核心技术基础。

通过：

```
Static Analysis

+

Dynamic Analysis

↓

Analysis Result

```

完成应用安全信号采集。

其中：

- Static Analysis 负责理解程序结构；
- Dynamic Analysis 负责观察运行行为；
- Program Representation 支撑静态程序分析；
- Runtime Instrumentation 支撑动态行为采集；
- Behavior Reconstruction 提升动态结果语义化能力。

最终输出标准化 Analysis Result，供 Detection Service Layer 完成：

- 恶意软件检测；
- 隐私合规检测；
- 恶意广告检测；
- 涉诈检测；
- 内容安全检测；
- 仿冒侵权检测。

```
