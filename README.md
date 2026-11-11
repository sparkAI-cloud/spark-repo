# ⚡ Spark

Spark is a small language model **trained completely from scratch**: no pretrained weights, no borrowed models. It is a learning project: build an AI one skill at a time, and keep every skill it learns.

> **Status: experimental.** Spark is early. Right now it is a ~110M-parameter model and a training pipeline, not a polished assistant. Expect rough output while pretraining data and training time grow.

## The idea

Every version focuses on **one topic**. Each new stage trains on its new data *mixed with replay from earlier stages*, so Spark adds knowledge instead of replacing it.

| Version | Stage | Focus |
|---|---|---|
| 0.1 | `pretrain` | Reads lots of plain text to learn language and general knowledge |
| 0.2 | `conversation` | Everyday chat: anything that isn't code or math |
| 0.3 | `math_8` | Math up to 8th grade |
| 0.4 | `math_hs` | High school math |
| 0.5 | `code_python` | Python |
| later | ... | CS, C++, and whatever Spark is still weak at |

A switch in the notebook (`MODE`) controls memory: `add` (keep old skills, default), `replace` (new data only), or `fresh` (start over).

## How it works

- **Model:** a GPT-style transformer written in plain PyTorch (12 layers, 768 width, 512 context, ~110M parameters).
- **Tokenizer:** byte-level BPE trained once on your data, then frozen for all versions.
- **Training:** fp16 on a single T4, auto-resume, a time guard that saves before the session ends, and a held-out loss check so you can see memorization.
- **Data:** your own `.jsonl` chats and `.txt` text. See [docs/DATA_FORMAT.md](docs/DATA_FORMAT.md).

## Quick start (Kaggle, free GPU)

1. Make a Kaggle account and verify your phone number (this unlocks GPUs).
2. Create a private **Dataset** with your data files (`conversation.jsonl`, plus `.txt` files for pretraining).
3. New notebook → **File → Import notebook** → upload `notebooks/Spark_Kaggle_T4.ipynb`.
4. Session options: Accelerator **GPU T4 x2**. Internet can stay off.
5. **Add Input** → attach your dataset.
6. Run the cells in order. Set `STAGE` in Cell 2 (`pretrain`, then `conversation`, ...).
7. After a run, turn the notebook Output into a dataset (e.g. `spark-checkpoints`) and attach it next session so Spark continues where it left off.

## Things to know

- The tokenizer and model shape must never change between versions, or old knowledge can't carry over.
- Replay greatly reduces forgetting, but it isn't a guarantee. Re-ask old prompts after each stage.
- Data limits quality more than the GPU does. A model this size needs lots of varied text.
- Don't commit private data or checkpoints. The `.gitignore` already blocks them.

## Roadmap

See [docs/ROADMAP.md](docs/ROADMAP.md).

## Support Spark

Spark is a hobby project built with free compute. If you'd like to support it, see the Sponsor button on this repo. Support pays for data, compute, and time. See `docs/ROADMAP.md` for what comes next.

## License

MIT. See [LICENSE](LICENSE).
