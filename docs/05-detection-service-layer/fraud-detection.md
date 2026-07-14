# Fraud Detection

---

# 1. Overview

Fraud Detection（涉诈检测）负责识别移动应用中的诈骗风险和黑灰产活动，包括虚假服务、诈骗引流、恶意诱导、非法获利以及其他利用应用生态实施欺诈行为的应用。

与 Malware Detection 关注恶意代码不同，Fraud Detection 更关注：

> 应用是否被用于实施诈骗或欺诈活动。

涉诈应用可能：

- 不包含明显恶意代码；
- 使用正常技术实现；
- 通过业务流程和用户交互实施欺诈。

因此，Fraud Detection 需要结合：

- Application Behavior；
- Application Profile；
- Network Intelligence；
- Threat Intelligence；
- User Feedback；
- AI Risk Analysis；

对应用进行综合风险判断。

---

# 2. Design Objectives

Fraud Detection 的设计目标包括：

- 识别涉诈应用；
- 发现黑灰产应用特征；
- 分析诈骗业务模式；
- 建立应用风险画像；
- 支撑风险处置；
- 支持未知诈骗模式发现。

---

# 3. Position in Architecture

Fraud Detection 属于 Detection Service Layer。

架构关系：
