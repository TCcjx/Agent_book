# AI Agents in Depth — Study Repository

This is a trimmed study repository for the open-source book *AI Agents in Depth: Design Principles and Engineering Practice*. It contains:

- 📕 **Ebook**: `AI-Agents-in-Depth-zh-CN.pdf` (10 chapters, start here — text is in Chinese)
- 📖 **Book sources**: `book/` (Chinese) and `book-en/` (English), matching the PDF chapters
- 🧪 **Companion experiments**: `chapter1/` – `chapter10/`, one folder per chapter, all runnable
- 📦 **Shared library**: `agentbook/`, common model-provider plumbing used by the experiments

## Suggested study loop

> Core formula: **Agent = LLM + Context + Tools**

For each chapter: read the book → run the experiment → read the code.

1. **Read** the corresponding chapter in the PDF (or `book-en/chapterN.md`).
2. **Run** the companion experiments in `chapterN/`, following the reading order in that chapter's `README.md`.
3. **Read the code** starting from each experiment's `main.py`, tracing how messages are assembled, tools are called, and results flow back.

## Chapters

| Ch | Book (EN) | Experiments | Topic |
| :--: | --- | --- | --- |
| 1 | [book-en/chapter1.md](book-en/chapter1.md) | [chapter1/](chapter1/) | Agent basics: traces, context ablation, search & codegen |
| 2 | [book-en/chapter2.md](book-en/chapter2.md) | [chapter2/](chapter2/) | Context engineering: prompting, benchmarks, compression |
| 3 | [book-en/chapter3.md](book-en/chapter3.md) | [chapter3/](chapter3/) | Memory & knowledge bases: RAG, retrieval, long-term memory |
| 4 | [book-en/chapter4.md](book-en/chapter4.md) | [chapter4/](chapter4/) | Tools: tool building, MCP, perception & execution tools |
| 5 | [book-en/chapter5.md](book-en/chapter5.md) | [chapter5/](chapter5/) | Coding agents & code generation |
| 6 | [book-en/chapter6.md](book-en/chapter6.md) | [chapter6/](chapter6/) | Interaction: extended observation & action spaces |
| 7 | [book-en/chapter7.md](book-en/chapter7.md) | [chapter7/](chapter7/) | Agent evaluation |
| 8 | [book-en/chapter8.md](book-en/chapter8.md) | [chapter8/](chapter8/) | Post-training (fine-tuning experiments, GPU required) |
| 9 | [book-en/chapter9.md](book-en/chapter9.md) | [chapter9/](chapter9/) | Continuous agent improvement |
| 10 | [book-en/chapter10.md](book-en/chapter10.md) | [chapter10/](chapter10/) | Multi-agent collaboration |

## Setup

Requires **Python 3.11 – 3.13**. With [uv](https://docs.astral.sh/uv/):

```bash
uv sync --locked --python 3.12 --extra ch1   # install one chapter's deps
# pip fallback:
python -m pip install -e ".[ch1]"
```

Replace `ch1` with `ch2` … `ch10` as needed. Heavy local-training/GPU extras (mostly chapters 7–8) have their own instructions in the experiment READMEs.

Configure a model provider:

```bash
cp .env.example .env
```

One provider is enough: OpenRouter `:free` models, a local [Ollama](https://ollama.com/) server, or any of DeepSeek / DashScope (Qwen) / SiliconFlow / Doubao / Moonshot Kimi / Zhipu GLM / OpenAI / Gemini. Some experiments need specific capabilities (e.g. experiment 1-2 web search requires `MOONSHOT_API_KEY`) — follow each experiment's README.

Run an experiment:

```bash
.venv\Scripts\activate          # Windows; `source .venv/bin/activate` on macOS/Linux
cd chapter1/context
python main.py --help
```

## Notes

- Some experiments make real API calls — check your quota before running.
- Fine-tuning experiments (chapters 7–8) need Linux + NVIDIA GPU; on CPU-only machines, read the code instead.
- Book conclusions come from the authors' real runs; exact results may vary with models and time. Focus on the mechanisms.
- See `docs/EXPERIMENT_CONVENTIONS.md` and `docs/EXPERIMENT_STATUS.md` for experiment conventions and status.

## License

[Apache-2.0](LICENSE)
