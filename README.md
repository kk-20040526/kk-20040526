# 徐康 · AI 产品项目作品集

2027 届 · 智能科学与技术 · 求职方向：AI 产品经理实习生

三个独立完成的项目，均为可运行的本地原型。每个仓库包含完整代码、项目介绍、运行截图与演示视频。

## 项目一：车型识别 Agent

自训练 ResNet18 51 类车型分类模型，配合 qwen-flash 的 Function Calling 编排 9 个工具，完成"拍照识别 → 查资料 → 对比 → 相似推荐 → 收藏"的业务闭环。处理了识别不确定与写操作边界两类产品问题：双阈值三档分流，unknown 不编造车型，收藏只由用户指令触发。

- 关键结果：922 张留出测试集 Macro-F1 0.8527、Accuracy 0.8384；unknown 检出率 0.7667
- 技术栈：PyTorch · ResNet18 / qwen-flash / FastAPI / SQLite
- 代码与介绍：[kk-20040526/car-recognition-agent](https://github.com/kk-20040526/car-recognition-agent)
- 演示视频：[video/car-agent-demo.mp4](https://github.com/kk-20040526/car-recognition-agent/blob/main/video/car-agent-demo.mp4)

## 项目二：文档 RAG 问答系统

面向小规模文档知识库的 RAG 问答原型，围绕"检索命中、答案溯源、域外兜底"三个问题设计。BM25 支持邻接片段扩展，另保留 Elasticsearch 单节点分支验证规模增长后的扩展路径，并用 Dify 搭建语义 + 关键词混合检索工作流做对比。

- 关键结果：14 篇文档、86 段知识库；索引 1.03 秒、单次检索 0.6—1.1 毫秒；4 个域内问题 Top-1 全部命中，域外按规则拒答
- 技术栈：rank_bm25 / jieba / Elasticsearch / Dify / Streamlit / qwen-flash
- 代码与介绍：[kk-20040526/rag-doc-qa](https://github.com/kk-20040526/rag-doc-qa)
- 演示视频：[Releases v1.0.0](https://github.com/kk-20040526/rag-doc-qa/releases/tag/v1.0.0)

## 项目三：自然场景 OCR 端到端识别系统

面向门店招牌录入与数据不宜出内网的场景，设计"检测 → 四点透视校正 → 识别 → 阅读顺序还原"的离线链路，处理 8000 张街景图并两阶段微调 DB 检测与 SVTR_LCNet 识别模型。自建三层评测，FastAPI 提供识别接口，完成微信小程序局域网真机联调与内网离线部署。

- 关键结果：150 图 / 2000 样本实测，检测 F1 0.556（召回 0.483）、整句准确率 0.727、CER 0.121、端到端 F1 0.314，CPU 1.9 秒/张
- 技术栈：PaddleOCR（DB / SVTR_LCNet）/ FastAPI / 微信小程序
- 代码与介绍：[kk-20040526/scene-ocr](https://github.com/kk-20040526/scene-ocr)
- 演示视频：[video/ocr-demo.mp4](https://github.com/kk-20040526/scene-ocr/blob/main/video/ocr-demo.mp4)

## 说明

以上项目均为个人独立完成的项目原型，开发过程使用了 AI 工具辅助。各仓库 README 中如实标注了当前边界与不足（封闭集、单节点验证、样本规模限制等），未作企业级产品的表述。
