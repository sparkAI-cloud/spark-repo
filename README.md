# spark info

Spark is a small language model trained completely from scratch, meaning no weights from another AI, no borrowed models. It is a small project I hope to grow much larger.
> r**ight now, it is experimental.** Spark is just being made. Right now it is around 110M-parameter model and a training pipeline, not a good assistant. Expect rough output while pretraining data and training time grow.

## the idea

Every version focuses on **one topic**. Each new stage trains on its new data *mixed with replay from earlier stages*, so Spark adds knowledge instead of replacing it.

| Version | Stage | Focus |
|---|---|---|
| 0.1 | `pretrain` | Reads lots of plain text to learn language and general knowledge |
| 0.2 | `conversation` | Everyday chat: anything that isn't code or math |
| 0.3 | `math_8` | Decent math skill |
| 0.4 | `math_hs` | High school math |
| 0.5 | `code_python` | Python |
| later | ... | CS, C++, and whatever Spark is still weak at |

## extra info

- **Model:** a gpt-style transformer written in PyTorch (12 layers, 768 width, 512 context, ~110M parameters)
- **Tokenizer:** byte-level BPE trained once on your data, then frozen for all versions
- **Training:** fp16 on a T4 GPU, auto-resume, a time guard that saves model info before the session ends, and a held-out loss check so you can see memorization.
- **Data:** your own `.jsonl` chats and `.txt` text. see [docs/DATA_FORMAT.md](docs/DATA_FORMAT.md).

## quick start (kaggle, free GPU)

1. make a kaggle account and verify your phone number (this unlocks GPUs)
2. create a private **dataset** with your data files (`conversation.jsonl`, plus `.txt` files for pretraining)
3. New notebook → **File → Import notebook** → upload `notebooks/Spark_Kaggle_T4.ipynb`
4. Session options: Accelerator **GPU T4 x2**. internet can stay off
5. **Add Input** → attach your dataset
6. run the cells in order. Set `STAGE` in Cell 2 (`pretrain`, then `conversation`, ...)
7. after a run, turn the notebook Output into a dataset (e.g. `spark-checkpoints`) and attach it next session so Spark continues where it left off.

## things to know

- The tokenizer and model shape must never change between versions, or old knowledge can't carry over.
- Replay greatly reduces forgetting, but it isn't a guarantee. Re-ask old prompts after each stage.
- Data limits quality more than the GPU does. A model this size needs lots of varied text.
- Don't commit private data or checkpoints. The `.gitignore` already blocks them.

## roadmap

basically just describes what we are doing while we countinue spark. for more info see [docs/ROADMAP.md](docs/ROADMAP.md).

## support Spark

Spark is a fun project built with free compute that I hope to grow to a big commercial AI in the future. if you'd like to support it, press the sponsor button on this repo. support pays for data, compute, and time.`check out docs/ROADMAP.md` for what comes next. it means alot if you donate ❤️

## license

Basic MIT. See [LICENSE](LICENSE).
