# 《移动应用安全检测平台总体设计与关键技术白皮书》

> Mobile Application Security Analysis Platform (MASAP)
>
> Architecture & Technology White Paper
>
> Version 1.0

---

# 第一篇 平台总体设计（Platform Overview）

* [第1章 平台建设背景](docs/01-overview/01-background.md)
* [第2章 建设目标](docs/01-overview/02-goals.md)
* [第3章 平台定位](docs/01-overview/03-positioning.md)
* [第4章 技术挑战](docs/01-overview/04-challenges.md)
* [第5章 技术路线](docs/01-overview/05-roadmap.md)

---

# 第二篇 平台总体架构（Platform Architecture）

* [第6章 总体架构设计](docs/02-architecture/01-overall-architecture.md)
* [第7章 Infrastructure Layer](docs/02-architecture/02-infrastructure-layer.md)
* [第8章 Analysis Engine Layer](docs/02-architecture/03-analysis-engine-layer.md)
* [第9章 AI Intelligence Layer](docs/02-architecture/04-ai-layer.md)
* [第10章 Detection Service Layer](docs/02-architecture/05-detection-layer.md)
* [第11章 Application Access Layer](docs/02-architecture/06-access-layer.md)
* [第12章 Security Knowledge Platform](docs/02-architecture/07-security-knowledge-layer.md)

---

# 第三篇 Infrastructure Layer

* [第13章 基础设施总体设计](docs/03-infrastructure/01-overview.md)
* [第14章 真机云（Device Farm）](docs/03-infrastructure/02-device-farm.md)
* [第15章 沙箱集群（Sandbox Cluster）](docs/03-infrastructure/03-sandbox.md)
* [第16章 环境仿真](docs/03-infrastructure/04-environment.md)
* [第17章 自动化运行平台](docs/03-infrastructure/05-runtime.md)

---

# 第四篇 Analysis Engine Layer

* [第18章 Analysis Engine总体设计](docs/04-analysis-engine/01-overview.md)
* [第19章 Package Parser](docs/04-analysis-engine/02-package-parser.md)
* [第20章 Program Analysis](docs/04-analysis-engine/03-program-analysis.md)
* [第21章 Static Analysis](docs/04-analysis-engine/04-static-analysis.md)
* [第22章 Dynamic Analysis](docs/04-analysis-engine/05-dynamic-analysis.md)
* [第23章 Runtime Hook Framework](docs/04-analysis-engine/06-runtime-hook.md)
* [第24章 Automation Engine](docs/04-analysis-engine/07-automation.md)
* [第25章 Rule Engine](docs/04-analysis-engine/08-rule-engine.md)

---

# 第五篇 AI Intelligence Layer

* [第26章 AI总体架构](docs/05-ai-intelligence/01-overview.md)
* [第27章 OCR分析](docs/05-ai-intelligence/02-ocr.md)
* [第28章 CV分析](docs/05-ai-intelligence/03-cv.md)
* [第29章 NLP分析](docs/05-ai-intelligence/04-nlp.md)
* [第30章 LLM推理](docs/05-ai-intelligence/05-llm.md)
* [第31章 Malware AI](docs/05-ai-intelligence/06-malware-ai.md)
* [第32章 Graph Intelligence](docs/05-ai-intelligence/07-graph.md)

---

# 第六篇 Detection Service Layer

* [第33章 检测服务总体设计](docs/06-detection-service/01-overview.md)
* [第34章 恶意软件检测](docs/06-detection-service/02-malware.md)
* [第35章 隐私违规检测](docs/06-detection-service/03-privacy.md)
* [第36章 恶意广告检测](docs/06-detection-service/04-ad.md)
* [第37章 涉诈检测](docs/06-detection-service/05-fraud.md)
* [第38章 内容安全检测](docs/06-detection-service/06-content.md)
* [第39章 仿冒侵权检测](docs/06-detection-service/07-impersonation.md)
* [第40章 SDK风险检测](docs/06-detection-service/08-sdk.md)

---

# 第七篇 Application Access Layer

* [第41章 Workflow](docs/07-application-access/01-workflow.md)
* [第42章 Portal](docs/07-application-access/02-portal.md)
* [第43章 OpenAPI](docs/07-application-access/03-openapi.md)
* [第44章 报告中心](docs/07-application-access/04-report.md)
* [第45章 RBAC](docs/07-application-access/05-rbac.md)

---

# 第八篇 Security Knowledge Platform

* [第46章 平台总体设计](docs/08-security-knowledge/01-overview.md)
* [第47章 Security Facts Repository](docs/08-security-knowledge/02-security-facts.md)
* [第48章 IOC Repository](docs/08-security-knowledge/03-ioc.md)
* [第49章 SDK Knowledge Base](docs/08-security-knowledge/04-sdk.md)
* [第50章 Developer Reputation](docs/08-security-knowledge/05-developer.md)
* [第51章 Certificate Reputation](docs/08-security-knowledge/06-certificate.md)
* [第52章 Domain/IP Reputation](docs/08-security-knowledge/07-domain.md)
* [第53章 Malware Knowledge](docs/08-security-knowledge/08-malware.md)
* [第54章 Knowledge Graph](docs/08-security-knowledge/09-knowledge-graph.md)
* [第55章 Feature Store](docs/08-security-knowledge/10-feature-store.md)
* [第56章 Embedding Store](docs/08-security-knowledge/11-embedding-store.md)
* [第57章 Rule Repository](docs/08-security-knowledge/12-rule-repository.md)
* [第58章 AI Dataset](docs/08-security-knowledge/13-ai-dataset.md)
* [第59章 Detection History](docs/08-security-knowledge/14-history.md)
* [第60章 Evidence Repository](docs/08-security-knowledge/15-evidence.md)

---

# 第九篇 平台运营

* [第61章 指标体系](docs/appendices/01-kpi.md)
* [第62章 可观测性](docs/appendices/02-observability.md)
* [第63章 CI/CD](docs/appendices/03-cicd.md)
* [第64章 技术路线图](docs/appendices/04-roadmap.md)

---

# 附录

* [附录A 术语表](docs/appendices/a-glossary.md)
* [附录B 缩略语](docs/appendices/b-acronym.md)
* [附录C Android安全模型](docs/appendices/c-android-security.md)
* [附录D HarmonyOS安全模型](docs/appendices/d-harmony-security.md)
* [附录E MITRE ATT&CK Mobile](docs/appendices/e-mitre-mobile.md)
