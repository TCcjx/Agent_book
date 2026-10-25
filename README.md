# 深入理解 AI Agent —— 学习仓库

本仓库是《深入理解 AI Agent：设计原理与工程实践》的学习版仓库，包含：

- 📕 **电子书**：`AI-Agents-in-Depth-zh-CN.pdf`（全书 10 章，推荐从这里开始阅读）
- 📖 **书稿源文件**：`book/`（中文）、`book-en/`（英文），与 PDF 内容一一对应
- 🧪 **109 个配套实验**：`chapter1/` ~ `chapter10/`，与书中章节一一对应，可亲手运行
- 📦 **共享依赖包**：`agentbook/`，各实验共用的模型提供商适配与工具函数

## 推荐学习路线

> 核心公式：**Agent = LLM + 上下文 + 工具**

每一章按「读正文 → 跑实验 → 读代码」三步走：

1. **读正文**：阅读 PDF 中对应章节（或 `book/chapterN.md`），理解概念与书中给出的简化代码。
2. **跑实验**：打开 `chapterN/`，按该章 `README.md` 中「第一次阅读的顺序」运行配套实验，观察真实模型的行为。
3. **读代码**：从实验目录的 `main.py` 入手，在 `agent.py` / `tools.py` 中跟踪消息组装、工具调用与结果回传的完整链路。

> 提示：书中正文使用简化代码解释流程，实验目录中的代码才是可直接运行的完整版本。

### 章节与实验对照

| 章 | 书稿 | 实验 | 主题 |
| :--: | --- | --- | --- |
| 1 | [book/chapter1.md](book/chapter1.md) | [chapter1/](chapter1/) | Agent 基础知识：执行轨迹、上下文消融、搜索与代码生成 |
| 2 | [book/chapter2.md](book/chapter2.md) | [chapter2/](chapter2/) | 上下文工程：提示工程、基准与压缩 |
| 3 | [book/chapter3.md](book/chapter3.md) | [chapter3/](chapter3/) | 用户记忆和知识库：RAG、向量检索、长期记忆 |
| 4 | [book/chapter4.md](book/chapter4.md) | [chapter4/](chapter4/) | 工具：工具构建、MCP、感知与执行工具 |
| 5 | [book/chapter5.md](book/chapter5.md) | [chapter5/](chapter5/) | Coding Agent 与代码生成 |
| 6 | [book/chapter6.md](book/chapter6.md) | [chapter6/](chapter6/) | 交互：观察与动作空间的扩展（多模态、异步） |
| 7 | [book/chapter7.md](book/chapter7.md) | [chapter7/](chapter7/) | Agent 的评估 |
| 8 | [book/chapter8.md](book/chapter8.md) | [chapter8/](chapter8/) | 模型后训练（含微调实验，需 GPU） |
| 9 | [book/chapter9.md](book/chapter9.md) | [chapter9/](chapter9/) | Agent 的持续进化 |
| 10 | [book/chapter10.md](book/chapter10.md) | [chapter10/](chapter10/) | 多 Agent 协作 |

## 环境准备

### 1. 安装依赖

要求 **Python 3.11 – 3.13**。推荐使用 [uv](https://docs.astral.sh/uv/)：

```bash
# 只安装某一章的依赖（推荐，按需安装）
uv sync --locked --python 3.12 --extra ch1

# 没有 uv 也可以用 pip
python -m pip install -e ".[ch1]"
```

把 `ch1` 换成 `ch2` … `ch10` 即可安装对应章节的依赖。少数实验依赖较重的本地训练/GPU 栈（主要在第 7、8 章），其实验 README 中有单独的安装说明。

### 2. 配置模型提供商

```bash
cp .env.example .env
```

编辑 `.env`，配置**任意一个**你有 Key 的提供商即可（不需要全部配置）：

- **零成本方案**：
  - [OpenRouter](https://openrouter.ai/) 免费模型（模型 ID 以 `:free` 结尾，如 `google/gemma-4-31b-it:free`）；
  - 本地 [Ollama](https://ollama.com/)，无需联网与 Key；
  - Google Gemini 有免费额度（`GEMINI_API_KEY`）。
- **国内直连**：DeepSeek、阿里云百炼（DashScope）、SiliconFlow、字节 Doubao（ARK）、月之暗面 Kimi、智谱 GLM 等。
- 注意：个别实验依赖特定能力（如第 1 章实验 1-2 的联网搜索需要 `MOONSHOT_API_KEY`），以实验 README 的说明为准。

### 3. 运行一个实验

每个实验都是一个独立的小项目，典型结构：

```text
chapter1/context/
├── README.md      # 先读我：目的、运行步骤、预期现象
├── main.py        # 命令行入口
├── agent.py       # Agent 实现
├── fixtures/      # 测试数据
└── requirements.txt
```

```bash
uv sync --locked --python 3.12 --extra ch1   # 仓库根目录执行一次
.venv\Scripts\activate                        # Windows 激活虚拟环境
cd chapter1/context
python main.py --help                         # 按实验 README 的示例运行
```

## 目录结构

```text
.
├── AI-Agents-in-Depth-zh-CN.pdf   # 电子书（从这里开始）
├── book/                          # 中文书稿（book/chapterN.md 与 PDF 章节对应）
├── book-en/                       # 英文书稿
├── chapter1/ ~ chapter10/         # 各章配套实验
├── agentbook/                     # 实验共享库：模型提供商适配等
├── docs/                          # 实验规范与状态记录
├── pyproject.toml / uv.lock       # 依赖清单（按章节 extras 分组）
└── .env.example                   # 提供商密钥配置模板
```

## 实用文档

- [docs/EXPERIMENT_CONVENTIONS.md](docs/EXPERIMENT_CONVENTIONS.md)：实验目录的统一结构与运行约定。
- [docs/EXPERIMENT_STATUS.md](docs/EXPERIMENT_STATUS.md)：跨章节重点实验的完成状态与证据索引。
- 各章的 `chapterN/EXPERIMENT_LEDGER.md`：实验运行条件与结果记录。
- 各章 `chapterN/README.md` 是该章实验的权威清单（含编号、类型与一句话说明）。

## 注意事项

- 部分实验会产生真实 API 调用费用，运行前请确认所用模型与配额。
- 带 ✅ 标记的实验可独立运行；📖 标记的实验是外部仓库复现指南；🚧 标记的实验仍在完善中。
- 第 7、8 章的微调类实验需要 Linux + NVIDIA GPU，CPU 机器可跳过或只读代码。
- 书中实验结论来自作者的真实运行记录，模型与时间点不同，复现结果可能有差异，重在理解机制。

## License

[Apache-2.0](LICENSE)
