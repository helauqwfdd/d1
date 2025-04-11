<div  align="center">
    <h1>d1: Scaling Reasoning in Diffusion Large Language Models via Reinforcement Learning</h1>
        <p>A two-stage recipe with SFT followed by a novel variant of GRPO, <i>diffu</i>-GRPO, to convert pre-trained dLLMs into strong reasoning models.</p>
</div>
****************************************************************

**Updates:**

* 04-11-2025: We released [our paper](https://dllm-reasoning.github.io/media/preprint.pdf) and [project page](https://dllm-reasoning.github.io). Additionally, the SFT code was open-sourced.

****************************************************************

## d1

![Results](media/pull_fig.png)

### SFT

We open-source our code to perform completion-only masked SFT for dLLMs. We implement the algorithm proposed in [LLaDA](https://github.com/ML-GSAI/LLaDA), and also provide it below for completeness.

![SFT Algorithm](media/algorithm_sft.png)

The framework follows a similar interface to 🤗 Transformers. `dLLMTrainer` subclasses `Trainer` and overrides the loss computation to implement the diffusion loss. `dLLMDataCollator` extends `DefaultDataCollator` by incorporating a forward noising process applied to each training batch. Additionally, we provide a custom torch dataset, `dLLMSFTDataset`, tailored for completion-only SFT of dLLMs.

To preprocess and tokenize your dataset, you will need to modify `preprocess_dataset`. Presently, it works with the s1K dataset.

SFT results can be reproduced with the command,
```
CUDA_VISIBLE_DEVICES=0,1,2,3 accelerate launch --config_file ddp_config.yaml --main_process_port 29500 --num_processes 4 sft_train.py
```

### _diffu_-GRPO
Code coming soon!

### Eval
Code coming soon!

