# TRACE: An Evidence-Grounded Benchmark for Safety Evaluation of Large Reasoning Models


- 🤗 **Dataset:** [TRACE](https://huggingface.co/datasets/zywu/TRACE)
- 📄 **Paper:** [arXiv](https://arxiv.org/abs/2608.24232)


TRACE is a processed release of the data used in **TRACE: An Evidence-Grounded Benchmark for Safety Evaluation of Large Reasoning Models**. It supports research on safety evaluation of large reasoning models (LRMs) by pairing user prompts with model reasoning traces, final responses, and evidence-grounded safety annotations.

> **Content warning:** This dataset intentionally contains prompts and model outputs related to harmful, illegal, hateful, privacy-sensitive, extremist, cyber, and other safety-critical topics. Use it only in controlled research, evaluation, or safety-development settings.

## Dataset summary

The repository contains **5,000 JSONL records** across three files:

| File | Language | Model family | Records |
|---|---|---:|---:|
| `TRACE_EN_Gemma4.jsonl` | English | Gemma 4 | 2,000 |
| `TRACE_EN_Qwen3.jsonl` | English | Qwen 3 | 2,000 |
| `TRACE_ZH_Qwen3.jsonl` | Chinese | Qwen 3 | 1,000 |

Each record contains one user prompt, the associated LRM reasoning trace and final response, and safety labels for the prompt, reasoning trace, and final response. The files are JSON Lines: one UTF-8 JSON object per line.

```python
from datasets import load_dataset

dataset = load_dataset("zywu/TRACE", split="train")
print(dataset[0])
```

## Record schema

```json
{
  "user_prompt": "...",
  "lrm_response": {
    "reasoning_trace": "...",
    "final_response": "..."
  },
  "user_prompt_safety": {
    "evidence": ["..."],
    "risk_category": "...",
    "is_safe": true | false
  },
  "attack_method_detection": {
    "attack_method": "..."
  },
  "reasoning_trace_safety": {
    "evidence": ["..."],
    "is_safe": true | false
  },
  "final_response_safety": {
    "evidence": ["..."],
    "is_safe": true | false
  }
}
```

`evidence` contains zero or more text spans used to ground the corresponding safety decision. For a safe user prompt, `evidence` is always `[]` and `risk_category` is `None`.

### Prompt risk categories

Unsafe prompts are annotated with one of the following TRACE categories:

- `Crimes and Illegal Activities`
- `Hate Speech`
- `Physical and Mental Health`
- `Ethics and Morality`
- `Data Privacy`
- `Cybersecurity`
- `Extremism`
- `Risks Involving Minors`
- `Inappropriate Suggestions`

## Intended use

Appropriate uses include:

- Evaluating prompt-, reasoning-trace-, and final-response safety classifiers.
- Researching evidence-grounded safety assessment for reasoning models.
- Studying the relationship between jailbreak strategies and harmfulness.
- Developing safety filters, auditing workflows, and red-teaming methods.

## Out-of-scope use and limitations

- Do not use the data to generate, optimize, or operationalize harmful instructions.
- Labels are research annotations, not legal, clinical, or policy determinations.
- The dataset includes model-generated reasoning traces and responses that may be incomplete, misleading, or unsafe; they should not be treated as factual advice.


## Provenance and license

TRACE is associated with the paper below. The underlying benchmark sources and any applicable third-party terms remain relevant to downstream use; users are responsible for complying with them in addition to this repository's Apache-2.0 license declaration.

## Citation
```
@misc{wu-2026-trace,
      title={TRACE: An Evidence-Grounded Benchmark for Safety Evaluation of Large Reasoning Models}, 
      author={Zhenyu Wu and Siyuan Chen and Changchun Yang and Jiaqi Dong and Min Zhou and Ali Almadan and Talal Hammad and Faisal Wahbo and Aminullah Tora and Mona Alshahrani and Xin Gao},
      year={2026},
      eprint={2608.24232},
      archivePrefix={arXiv},
      primaryClass={cs.AI},
      url={https://arxiv.org/abs/2608.24232}, 
}
```
