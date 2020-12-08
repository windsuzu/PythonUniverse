# Philosophy

https://huggingface.co/transformers/philosophy.html

1. configuration
2. models
3. tokenizer

All of these classes can be initialized in a simple and unified way from pretrained instances by using a common `from_pretrained()`
`save_pretrained()` lets you save a model/configuration/tokenizer locally so that it can be reloaded using `from_pretrained()`

1. `pipeline()` for quickly using a model
2. `Trainer()` or `TFTrainer()` to quickly train or fine-tune a given model.

