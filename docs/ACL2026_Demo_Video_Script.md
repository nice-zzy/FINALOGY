# FinAlogy ACL 2026 Demo 视频脚本与剪辑思路

> **项目全称**：FinAlogy: A Vision-Language System for Candlestick Pattern Analogy and Automated Reporting  
> **参考视频**：[GenWardrobe - ACM MM 2025 Demo](https://www.youtube.com/watch?v=Y7po8Cq-R4o)  
> **ACL 2026 要求**：最长 2.5 分钟，推荐带音频旁白的 screencast  
> **GitHub**：https://github.com/nice-zzy/Kline

---

## 一、参考视频风格分析（GenWardrobe）

| 要素 | 风格特点 |
|------|----------|
| **结构** | 开场→问题动机→方案概述→三大模块逐一展示→收尾 |
| **时长** | 约 3:21（我们需控制在 2:30 内） |
| **旁白** | 英文、语速适中、专业且易懂 |
| **画面** | 标题/字幕 + 系统界面/流程图 + 实际演示 |
| **音乐** | 开场/过渡轻背景乐，不压过旁白 |
| **节奏** | 问题→方案→组件 1→组件 2→组件 3→总结 |

---

## 二、FinAlogy 视频总体结构（2:30 内）

| 时段 | 内容 | 时长 |
|------|------|------|
| 0:00–0:15 | 标题 + 一句话定位 | 15s |
| 0:15–0:45 | 问题动机（固定分类 vs. 视觉类比） | 30s |
| 0:45–1:00 | 方案概览（视觉类比 + RAG + LLM） | 15s |
| 1:00–1:50 | 系统三大模块展示 | 50s |
| 1:50–2:20 | Interactive Playground 端到端 Demo | 30s |
| 2:20–2:30 | 总结 + GitHub/致谢 | 10s |

---

## 三、分镜脚本（中英对照）

### 【0:00–0:15】开场

**画面**：黑/深色背景，白色大字标题  
**旁白（英文）**：

> FinAlogy: A Vision-Language System for Candlestick Pattern Analogy and Automated Reporting.  
> An interactive system that shifts financial analysis from rigid pattern classification to data-driven visual analogy, powered by retrieval-augmented report generation.

**字幕**：可叠加 conference 标识 "ACL 2026 Demo"

---

### 【0:15–0:45】问题动机

**画面**：传统 K 线形态图（Hammer、Engulfing 等固定命名）与真实市场多样性对比

**旁白（英文）**：

> Traditional financial analysis relies on a fixed taxonomy of candlestick patterns—such as "Hammer" or "Engulfing." Yet these predefined rules fail to cover the vast diversity of real-world candlestick sequences, limiting their practical utility.  
> Analysts need to ask: "When did the market show a similar shape before? What happened next?"—but rigid classification cannot answer this.  
> FinAlogy addresses this gap by shifting the paradigm from classification to data-driven visual analogy.

**字幕要点**：
- Limitation: fixed taxonomy cannot cover real-world diversity
- Need: find analogous market segments for arbitrary queries
- Paradigm shift: from classification to visual analogy

---

### 【0:45–1:00】方案概览

**画面**：系统架构草图（或 PPT 一页）

- 输入：任意 K 线查询图
- 流程：专用编码器 → 视觉/语义类比检索 → RAG 管道 → LLM 报告生成
- 输出：基于历史实证的专业金融报告

**旁白（英文）**：

> FinAlogy consists of three main components: a specialized encoder pre-trained on large-scale historical candlestick data for visual analogy; a retrieval module that identifies analogous market segments for any query image; and a RAG pipeline where an LLM synthesizes historical evidence into professional, interpretable reports.

---

### 【1:00–1:50】三大模块展示

#### 模块 1：Similar-Pair Construction（0:15）

**画面**：展示 main.py 步骤 1–3 的流程（或终端/日志截图）

- Step 1: 从 OHLCV 提取 52 维特征
- Step 2: 基于余弦相似度找相似对（within/cross stock）
- Step 3: 渲染蜡烛图为 224×224 图像

**旁白（英文）**：

> First, we extract 52-dimensional features from OHLCV data and use cosine similarity to find similar windows across 30 Dow stocks. We then render each window as a 224-by-224 candlestick image for visual encoder training.

---

#### 模块 2：Self-Supervised Encoder（0:15）

**画面**：训练曲线 / 架构图 / VICReg 公式示意

- VICReg： invariance + variance + covariance
- 无需负样本，Recall@3 与 52 维定义一致

**旁白（英文）**：

> Second, we train a Vision Transformer encoder with VICReg. Unlike contrastive methods, VICReg does not require negative samples—it prevents collapse via variance and covariance regularization. Our encoder achieves strong alignment with the 52-dimensional similarity definition on held-out data.

---

#### 模块 3：RAG Pipeline & LLM Report Generation（0:20）

**画面**：Interactive Playground 界面 / API 流程图

- 检索到的类比案例作为 RAG 上下文
- LLM 综合历史证据与市场结果
- 输出：专业、可解释的金融报告

**旁白（英文）**：

> Third, the retrieved analogues are integrated into a Retrieval-Augmented Generation pipeline. A Large Language Model synthesizes historical evidence and market outcomes into professional, interpretable financial reports—grounded in empirical precedents rather than fixed taxonomies.

---

### 【1:50–2:20】Interactive Playground 端到端 Demo

**画面**：Screencast 实操 Interactive Playground

1. 打开 FinAlogy Playground 网页
2. 上传一张 K 线图（或选择示例）
3. 展示实时视觉检索：Top-K 类比历史片段 + 股票代码、日期、相似度
4. 展示 LLM 生成的报告：形态类比、历史案例、市场走向、风险提示

**旁白（英文）**：

> Here is a live demo of our Interactive Playground. We upload a candlestick chart—for example, a recent window from Apple stock. The system encodes it, searches over tens of thousands of historical windows, and returns visually and semantically analogous market segments. Each result shows the ticker, date range, and similarity score. The LLM then synthesizes these retrieved precedents into a professional report—pattern analogy, historical outcomes, key levels, and risk considerations. All in real time.

**注意**：重点展示 Playground 的交互体验；若 Playground 仍在开发，可录制 API 调用 + 报告输出。

---

### 【2:20–2:30】收尾

**画面**：标题 + GitHub 链接 + 致谢

**旁白（英文）**：

> FinAlogy is publicly available at github.com/nice-zzy/Kline, along with open-source code and a demonstration video. Thank you for watching. We look forward to your feedback at ACL 2026.

---

## 四、剪辑思路

### 4.1 画面规划

| 场景 | 推荐素材 | 备注 |
|------|----------|------|
| 开场 | 标题页（PPT/Keynote 导出） | 简洁，品牌色 |
| 动机 | 交易软件 K 线图截图 / 示意图 | 避免实盘敏感数据 |
| 架构 | 流程图（draw.io / Mermaid） | 与论文图一致 |
| 模块 1 | 终端输出 / 特征/图像样例 | 可选动画 |
| 模块 2 | VICReg 公式 + 训练曲线 | 强调“无负样本” |
| 模块 3 | RAG 流程图 / Playground / LLM 报告 | 突出基于历史实证的报告生成 |
| Demo | **Screencast 主段** | 鼠标移动可适当放慢 |
| 收尾 | 标题页 + GitHub 链接 | 清晰可读 |

### 4.2 录制与剪辑工具建议

- **录屏**：OBS、QuickTime（Mac）、Windows 自带 Xbox Game Bar
- **剪辑**：DaVinci Resolve（免费）、CapCut、Premiere
- **字幕**：剪映 / Premiere 字幕、或 Whisper 自动生成后微调

### 4.3 技术要点

1. **分辨率**：1080p，16:9
2. **帧率**：30fps 即可
3. **音频**：清晰旁白，背景乐音量 < 20%
4. **时长**：严格 ≤ 2:30（ACL 2026 要求）
5. **语言**：英文为主，便于国际审稿

### 4.4 Demo 可演示内容清单

- [ ] 启动 Interactive Playground（前端 + API）
- [ ] 上传测试 K 线图（可从 `test_anchor_images.npy` 导出 PNG）
- [ ] 展示实时视觉检索结果（Top-K 类比案例 + 股票/日期/相似度）
- [ ] 展示 LLM 生成的报告（形态类比、历史证据、风险提示）
- [ ] 备选：API `/analyze-llm` 调用 + 报告输出
- [ ] 备选：`validate_model.py` 输出 Recall@1/Recall@3 + 相似对可视化

---

## 五、与 GenWardrobe 的对照

| 维度 | GenWardrobe | FinAlogy |
|------|-------------|----------|
| 领域 | 时尚/旅行 | 金融/K 线 |
| 核心技术 | RAG + 图像生成 | 视觉类比编码 + RAG + LLM |
| 创新点 | 多模态生成 | 从固定分类到数据驱动视觉类比 |
| 展示重点 | 三阶段 pipeline | 三模块 + Interactive Playground |
| 时长 | 3:21 | **≤ 2:30** |

---

## 六、检查清单（提交前）

- [ ] 视频时长 ≤ 2.5 分钟
- [ ] 含清晰英文旁白
- [ ] 展示系统核心功能（视觉类比检索 + LLM 报告生成）
- [ ] 提供 Live Demo 链接或可安装包（ACL 强制要求）
- [ ] 论文中引用的技术术语与视频一致
- [ ] 背景乐不干扰旁白，音量适中

---

*文档版本：v1.1 | 更新日期：2025-02-28 | 项目名称：FinAlogy*
