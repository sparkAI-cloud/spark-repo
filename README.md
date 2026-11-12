# spark info

Spark is a language model that was trained from scratch with no weights from other AI models or borrowed models. It is a project that I hope to grow much bigger. It is very small. The answers it gives are very limited, etc.

> Now it is experimental. Spark is just being built. Now it is about 110 million parameter model and it is not a good assistant. Expect output while pretraining data and training time grow.

## the idea

Every version focuses on one topic. Each new stage trains on data mixed with replay from earlier stages so Spark adds knowledge instead of replacing it.

| Version Stage | Focus |

|---|---|---|

| 0.1 | `pretrain` | Reads many plain text files to learn language and general knowledge |

| 0.2 | `conversation` Everyday chat: anything that is not code or math |

| 0.3 math_8` | Decent math skill |

| 0.4 | `math_hs` | High school math |

| 0.5 | `code_python` | Python |

| later |... Cs, C++ and whatever Spark is still weak at |

## extra info

- **Model:** a GPT‑style transformer written in PyTorch (12 layers, 768 width, 512 context about 110 million parameters)

- **Tokenizer:** byte‑level BPE trained once on your data then frozen for all versions.

- **Training:** fp16 on a T4 GPU, auto‑resume a time guard that saves model information before the session ends and a held‑out loss check so you can see memorization.

- **Data:** your.jsonl` chats and `.txt` text. See [docs/DATA_FORMAT.md](docs/DATA_FORMAT.md).

## quick start (kaggle, GPU)

1. Make a Kaggle account and verify your phone number (this unlocks GPUs).

2. Create a **dataset** with your data files (`conversation.jsonl` plus `.txt` files for pretraining).

3. New notebook → **File → Import notebook** → upload `notebooks/Spark_Kaggle_T4.ipynb`.

4. Session options: Accelerator **GPU T4 x2**. Internet can stay off.

5. **Add Input** → attach your dataset.

6. Run the cells in order. Set `STAGE` in Cell 2 (`pretrain` conversation`...).

7. After a run turn the notebook Output into a dataset (for example `spark-checkpoints`). Attach it to the next session so Spark continues where it left off.

## things to know

- The tokenizer and model shape must never change between versions or old knowledge cannot carry over.

- Replay greatly reduces forgetting. It is not a guarantee. Re‑ask old prompts after each stage.

- Data limits quality more than the GPU does. A model this size needs varied text.

- Do not commit private data or checkpoints. The `.gitignore` already blocks them.

## roadmap

basically just describes what we are doing while we continue Spark. For info see [docs/ROADMAP.md](docs/ROADMAP.md).

## support Spark

Spark is a fun project built with compute that I hope to grow into a big AI in the future. If you would like to support it press the sponsor button on this repo. Support pays for data, compute and time. Check out docs/ROADMAP.md for what comes. It means a lot if you donate or help give some advice to me I am new, to this stuff and would love to learn how to grow this. ❤️

## License

Basic MIT. See [LICENSE](LICENSE).
