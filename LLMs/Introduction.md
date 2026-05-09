An LLM or large language model is a machine learning model that is used to train on identifying patterns. The basic concept that is executed is to find the most probable next token given a set of pre tokens.
***
## The Old way
#### 1. N-grams
Historically, if we wanted to predict the next token in "The cat sat on the <span>___</span>", ***we just counted how many times "mat" followed "on the" in our training data. ***

**It was purely statistical memorization.**

The problem: It doesn't scale. If you see a brand new sentence structure, the probability is 0. It also doesn't understand that "feline" and "cat" are related.

#### 2. Neural Language Models: 
Instead of counting exact word matches, we started passing words through neural networks to learn their meaning based on their context.

The Breakthrough: Researchers realized that if you make the model large enough, and the dataset large enough, "predicting the next word" forces the model to learn grammar, logic, coding syntax, and world facts just to be accurate.

***
## So why do LLMs hallucinate?
LLM's only fundamental goal is to calculate the most probable next token, it doesn't actually have a concept of "true" or "false". 
- It doesn't query a database of facts before answering. It just outputs text that looks mathematically plausible.

So if the model just starts assembling tokens that look like a Python library name (e.g., import advanced_data_scraper_pro). 
**It's statistically probable, but factually completely made up.**

***
## "Attention is all you need" - Google's 2017 paper that changed everything.

So attention mechanism is just looking at all tokens within the context window and comparing it with the current word to interpret its meaning. That is self attention.
### Encoders
Reads the entire input at once using self-attention to build a deep understanding (a _representation_) of the text. E.g., BERT. Great for classification or search.
### Decoders
Generates text one token at a time. It uses _masked_ self-attention, meaning it can only attend to tokens appearing _before_ it, not after it (because it hasn't generated them yet). E.g., GPT, LLaMA, Claude. Excellent for next-token prediction.

Modern LLMs like GPT-4 or LLaMA are **decoder-only** transformers. They tossed the encoder and just scaled up the decoder to massive proportions.
***
## Tokenization
- A token is a learned text unit (often subword), not always a full word.
- Character-level modeling makes sequences too long and inefficient.
- Whole-word modeling makes vocabulary huge and breaks on unseen words.
- Subword tokenization (like BPE) is the balance: compact vocabulary + can compose rare words (`great` + `est`).
***
## Pre-training vs Fine-tuning vs Prompting
1. **Pre-training:** It is the actual _creation_ of that model. It's when an AI lab like OpenAI takes an empty neural network that knows absolutely nothing and trains it on the entire internet for months using next-token prediction. This teaches it grammar, logic, coding, and general world knowledge. It costs millions of dollars. The result is the "out-of-the-box" base model. _(Analogy: Teaching a child to read, write, and understand the world for 18 years.)_
2. **Fine-tuning:** Taking that massive, pre-trained base model and updating its internal weights strictly on a targeted dataset (like medical journals, or a specific Q&A format) so it acts exactly how you want. Costs hundreds to thousands of dollars. _(Analogy: Sending that 18-year-old to law school so they speak and write specifically like a lawyer.)_
3. **Prompting:** No internal weights are changed here. You are just giving the model instructions and context at inference time. Costs fractions of a cent. _(Analogy: Handing that lawyer a brief on a specific case and asking them to summarize it.)_
***
## Context Window
Context window is the maximum amount of tokens an LLM can consider during a prompt run

- Increasing the context window from 4k to 128k or 1M tokens would result in a quadruple increase in terms of computation and memory. 

- It scales quadratically `O(N^2)`
	- If your context is 4 tokens, the model does 4×4=164×4=16 attention calculations.
	- If your context is 8 tokens, the model does 8×8=648×8=64 calculations.


