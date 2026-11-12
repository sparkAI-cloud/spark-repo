# Data format

## Chat data (`.jsonl`, one conversation per line)

multi-turn format (preferred):

```json
{"messages": [{"role": "user", "content": "Hey!"}, {"role": "assistant", "content": "Hi! What's on your mind?"}]}
```

simple pair format (also accepted):

```json
{"prompt": "Hey!", "response": "Hi! What's on your mind?"}
```

notes:
- roles must alternate: user, assistant, user, assistant, ...
- Spark only learns from the assistant turns; user turns are context.
- exact duplicate conversations are removed automatically.

## Pretraining text (`.txt`)

any plain text files (books, articles, encyclopedia-style text).

## Privacy

NEVER put personal or private information in training data or in this repo.
