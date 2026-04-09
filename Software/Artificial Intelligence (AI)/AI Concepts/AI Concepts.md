---
date: "2026-04-09"
tags: 
link:
---

# AI Concepts

- ## **Foundations:**
    
    - **Large Language Model (LLM)** : A neural network trained to predict the next token in a sequence.
    - **Tokenization** (1:28): Breaking input text into discrete units for processing.
    - **Vectorization** (2:53): Mapping words/tokens into an n-dimensional coordinate space where meaning is represented by distance.
    - **Attention** (4:15): A mechanism for adding contextual meaning to ambiguous words based on surrounding tokens.
    - **Self-Supervised Learning** (7:22): An efficient training method where models learn by masking and predicting parts of input data without human labels.
    - **Transformer** : The underlying architectural method (utilizing attention) used to process tokens effectively.
- ## **Optimization & Deployment:**
    
    - **Fine-tuning** : Updating a base model's weights using specific Q&A pairs to specialize its behavior.
    - **Few-shot Prompting** : Including examples in the prompt to guide model responses during inference.
    - **Retrieval Augmented Generation (RAG)**: Augmenting model input with relevant external documents retrieved in real-time.
    - **Vector Database** (20:33): A storage system optimized for similarity searching to support RAG workflows.
    - **Distillation** (40:24): Training a smaller, faster model (a student) to mimic a larger model (a teacher).
    - **Quantization** (41:47): Reducing the precision of neural network weights to save memory and reduce inference costs.
- ## **Advanced Frameworks & Agents:**
    
    - **Model Context Protocol (MCP)** : A standard protocol for connecting models to external data sources and tools.
    - **Context Engineering** (25:43): Managing and summarizing user history, preferences, and external data to maintain long-term model state.
    - **Agents** (28:17): Long-running processes that use LLMs to perform complex tasks by interacting with external systems.
    - **Reinforcement Learning** (29:19): Training models using feedback (rewards/penalties) to encourage desirable outputs.
    - **Chain of Thought** (34:42) & **Reasoning Models** (35:55): Techniques where models break down problems into steps to solve them more logically.
    - **Multi-modal Models** (36:36): Models capable of processing and generating multiple data types like text, images, and video.
    - **Small Language Models (SLM)** (38:21): Efficient models designed for specific tasks or private deployments.