# Serve commands

Model: [aniqsfwn/Llama-3.1-8B-triage-anthropic](https://huggingface.co/aniqsfwn/Llama-3.1-8B-triage-anthropic) (LoRA adapter on Llama 3.1 8B Instruct). System prompt: `data/system_prompt.txt`. Temperature 0.

## Download
```bash
hf download aniqsfwn/Llama-3.1-8B-triage-anthropic --local-dir serving/adapter
```

## vLLM (OpenAI-compatible API on port 8000)
```bash
vllm serve unsloth/Llama-3.1-8B-Instruct --enable-lora --lora-modules triage=aniqsfwn/Llama-3.1-8B-triage-anthropic --max-lora-rank 16
```

## Ollama
```bash
cd serving
ollama create triage -f Modelfile
ollama run triage "My parcel never arrived and I was charged twice."
```

## Unsloth (Python)
```python
from unsloth import FastLanguageModel
model, tok = FastLanguageModel.from_pretrained("aniqsfwn/Llama-3.1-8B-triage-anthropic", max_seq_length=2048, load_in_4bit=True)
FastLanguageModel.for_inference(model)
msgs = [{"role": "system", "content": open("data/system_prompt.txt").read()},
        {"role": "user", "content": "My parcel never arrived and I was charged twice."}]
ids = tok.apply_chat_template(msgs, add_generation_prompt=True, return_tensors="pt").to(model.device)
print(tok.decode(model.generate(input_ids=ids, max_new_tokens=64, do_sample=False)[0][ids.shape[1]:], skip_special_tokens=True))
```

## Evaluation against a served model
```bash
python scripts/auto_eval.py --test data/test_raw.jsonl --openai-url http://localhost:8000/v1 --model triage --out results/final_1795745604
```

Unsloth Studio: the published run (1795745604) can also be loaded in the Chat tab with the system prompt.
