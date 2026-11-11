# Data format

## Chat data (`.jsonl`, one conversation per line)

Multi-turn format (preferred):

```json
{"messages": [{"role": "user", "content": "Hey!"}, {"role": "assistant", "content": "Hi! What's on your mind?"}]}
```

Simple pair format (also accepted):

```json
{"prompt": "Hey!", "response": "Hi! What's on your mind?"}
```

Notes:
- Roles must alternate: user, assistant, user, assistant, ...
- Spark only learns from the assistant turns; user turns are context.
- Exact duplicate conversations are removed automatically. Varied data matters far more than a big file full of near-copies.

## Pretraining text (`.txt`)

Plain text files (books, articles, encyclopedia-style text). Only use text you have the right to use, and check each dataset's license.

## Privacy

Never put personal or private information in training data or in this repo.
