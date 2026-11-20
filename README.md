# 徐康 · AI 产品项目作品集

**2027 届 · 智能科学与技术 · 求职方向：AI 产品经理实习生**

三个端到端项目，覆盖 **模型训练 → 服务部署 → 前端交互 → 指标评测** 完整链路。每个仓库包含可运行代码、设计说明、运行截图与演示视频。

![Python](https://img.shields.io/badge/Python-3.11-3776AB?style=flat-square&logo=python&logoColor=white)
![PyTorch](https://img.shields.io/badge/PyTorch-ResNet18-EE4C2C?style=flat-square&logo=pytorch&logoColor=white)
![PaddlePaddle](https://img.shields.io/badge/PaddlePaddle-OCR-0062B0?style=flat-square)
![FastAPI](https://img.shields.io/badge/FastAPI-Backend-009688?style=flat-square&logo=fastapi&logoColor=white)
![LLM](https://img.shields.io/badge/qwen--flash-Function%20Calling-6B4FBB?style=flat-square)

---

## 项目一 · 车型识别 Agent

> 拍照识别车型，并围绕识别结果完成查资料、对比、相似推荐与收藏的对话式闭环。

自训练 ResNet18 51 类车型分类模型，通过 qwen-flash 的 Function Calling 编排 9 个工具。重点解决两类产品问题：**识别不确定时如何表达**，以及**写操作的触发边界**。

- **双阈值三档分流**：高置信直接给结论，中置信给候选让用户确认，低置信不猜
- **unknown 拒识**：非目标车型不编造结果，不执行确定性写操作
- **收藏只由用户指令触发**，模型不自行代劳

| 评测集 | Macro-F1 | Accuracy | unknown 检出率 |
|---|---|---|---|
| 验证集（1338 张） | 0.9153 | 0.9051 | 0.8650 |
| 留出测试集（922 张） | 0.8527 | 0.8384 | 0.7667 |

`PyTorch / ResNet18` · `qwen-flash + Function Calling` · `FastAPI` · `SQLite`

**[代码与设计说明 →](https://github.com/kk-20040526/car-recognition-agent)** ｜ [演示视频](https://github.com/kk-20040526/car-recognition-agent/blob/main/video/car-agent-demo.mp4)

---

## 项目二 · 文档 RAG 问答系统

> 让答案有出处，让系统在没有依据时敢说自己不知道。

围绕 **检索命中、答案溯源、域外兜底** 三个问题设计。BM25 内存检索作为默认方案并支持邻接片段扩展；另实现 Elasticsearch 分支，验证文档规模增长后的扩展路径。

- **答案可核对**：界面同时展示命中片段、来源文件与相关性得分
- **邻接扩展**：命中段落自动补同源上下文，缓解切分造成的语义断裂
- **无依据拒答**：无命中直接提示知识库无相关内容，不生成编造答案

| 指标 | 结果 |
|---|---|
| 知识库规模 | 14 篇文档 / 86 段落 |
| 索引构建 | 冷启动 0.6—0.9 秒，预热后 30—50 毫秒 |
| 单次检索 | 0.45—1.7 毫秒 |
| 域内问题 | 4 个预设问题 Top-1 全部命中 |

`rank_bm25 + jieba` · `Elasticsearch` · `Streamlit` · `qwen-flash`

**[代码与设计说明 →](https://github.com/kk-20040526/rag-doc-qa)** ｜ [演示视频](https://github.com/kk-20040526/rag-doc-qa/releases/tag/v1.0.0)

---

## 项目三 · 自然场景 OCR 识别系统

> 面向门店招牌录入场景，数据不出内网的离线识别方案。

自建 8000 张街景招牌数据集，两阶段微调 DBNet 检测与 SVTR + CTC 识别模型，打通 **检测 → 四点透视校正 → 识别 → 阅读顺序还原** 链路。FastAPI 提供推理接口，原生微信小程序完成局域网真机联调。

- **完整链路工程化**，而非直接调用现成 OCR 接口
- **三层评测体系**：检测 F1、识别 CER / 整句准确率、端到端 F1
- **严格评测口径**：IoU ≥ 0.5 匹配、文本 NFC 规范化、匈牙利算法一对一匹配

| 指标（800 张验证集） | 微调前 | 微调后 |
|---|---|---|
| 检测 F1 | 0.487 | **0.557** |
| 检测 Recall | 0.411 | **0.480** |
| 端到端 F1 | 0.303 | **0.328** |

识别整句准确率 0.727，CER 0.121。

`PaddlePaddle 2.6.2` · `DBNet / SVTR + CTC` · `FastAPI` · `微信小程序`

**[代码与设计说明 →](https://github.com/kk-20040526/scene-ocr)** ｜ [演示视频](https://github.com/kk-20040526/scene-ocr/blob/main/video/ocr-demo.mp4)

---

## 能力覆盖

| 环节 | 具体实践 |
|---|---|
| 数据与训练 | 自建数据集与标注、ResNet18 / DBNet / SVTR 微调、消融实验 |
| 大模型应用 | Function Calling 工具编排、RAG 检索增强、提示词与拒答策略 |
| 工程落地 | FastAPI 服务、SQLite 存储、Streamlit 与原生 HTML 界面、微信小程序真机联调 |
| 效果评估 | 分层评测集设计、Macro-F1 / CER / 端到端 F1、阈值分流与误拒率分析 |
| 产品设计 | 需求拆解、交互流程、边界规则定义、PRD 撰写 |