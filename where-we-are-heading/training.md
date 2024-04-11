# Training engine

The training engine component or set of components would enable to use your [development data](https://www.notion.so/Training-engine-7c128653aa36484aa38be07001c8d372?pvs=21) to improve the LLMs you use. This could involve fine-tuning, domain adaptive continued pre-training, and / or pre-training models from scratch.

## Fine-tuning

This approach is the most accessible to organizations in the near-term. A good rule of thumb is that this requires domain-specific instruction data and hundreds of GPU hours. The benefit of this approach is that it can shape the style and format of the suggestions for your organization and maybe even for particular teams or individual developers. This likely happens on a server using [development data](https://continue.dev/docs/development-data), though it could happen locally eventually. It could also become a continuous process that runs periodically like [smol.ai](http://smol.aihttps://smol.ai/) and [Arcee](https://www.arcee.ai/) are aiming to do.

## Domain adaptive continued pre-training

This approach is likely to become more accessible to organizations in the medium-term. A good rule of thumb today is that this requires an open-source base model, billions of tokens of relevant company data, and thousands of GPU hours. Due to these requirements, this will almost certainly take place on a server. The benefit of this approach is that you can have a lot more control over model capabilities than what fine-tuning offers. This is how [ChipNeMo was created by Nvidia](https://research.nvidia.com/publication/2023-10_chipnemo-domain-adapted-llms-chip-design) and how [Code Llama was created by Meta](https://arxiv.org/pdf/2308.12950.pdf), which both used Llama 2 as their base model.

## Pre-training models from scratch

This approach is likely to become more accessible to organizations in the long-term. A good rule of thumb today is that this requires trillions of tokens of Internet data, billions of tokens of relevant company data, and millions of GPU hours. The benefit of this approach is that you get complete control over model capabilities by determining what data is used for training. It could also be the case that you use vendors to help with this. For example, today OpenAI [will create custom GPT-4 models for you](https://openai.com/form/custom-models) with prices starting at $2-3M, MosaicML has trained models for organizations like [Replit](https://blog.replit.com/llm-training), and Together will [help you build models from scratch](https://www.together.ai/products#custom-models) too.