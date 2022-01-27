# InstructGPT: Training Language Models to Follow Instructions with Human Feedback

[Paper link][LINK_TO_PAPER]

> Making language models bigger does not inherently make them better at following a user's intent. For example, large language models can generate outputs that are untruthful, toxic, or simply not helpful to the user. In other words, these models are not aligned with their users. In this paper, we show an avenue for aligning language models with user intent on a wide range of tasks by fine-tuning with human feedback. Starting with a set of labeler-written prompts and prompts submitted through the OpenAI-API, we collect a dataset of labeler demonstrations of the desired model behavior, which we use to fine-tune GPT-3 using supervised learning. We then collect a dataset of rankings of model outputs, which we use to further fine-tune this supervised model using reinforcement learning from human feedback (RLHF). We call the resulting models InstructGPT. In human evaluations on our prompt distribution, outputs from the 1.3B parameter InstructGPT model are preferred to outputs from the 175B GPT-3, despite having 100x fewer parameters. Moreover, InstructGPT models show improvements in truthfulness and reductions in toxic output generation while having minimal performance regressions on public NLP datasets. Even though InstructGPT still makes simple mistakes, our results show that fine-tuning with human feedback is a promising direction for aligning language models with human intent.


## Contents
- [model-card.md](model-card.md) - InstructGPT model card
- [automatic-eval-samples](automatic-eval-samples/) - Samples from our models (both GPT-3 and InstructGPT) on public NLP benchmarks.
- [API distribution labeling instructions](https://docs.google.com/document/d/1MJCqDNjzD04UbcnVZ-LmeXJ04-TKEICDAepXyMCBUb8/edit#) - Google doc of instructions given to contractors for final evaluations on our API prompt distribution.
- [Toxicity labeling instructions](https://docs.google.com/document/d/1d3n6AqNrd-SJEKm_etEo3rUwXxKG4evCbzfWExvcGxg/edit?usp=sharing) - Google doc of instructions given to contractors for labeling toxic outputs on the RealToxicityPrompts dataset

[LINK_TO_PAPER]: https://cdn.openai.com/papers/Training_language_models_to_follow_instructions_with_human_feedback.pdf

