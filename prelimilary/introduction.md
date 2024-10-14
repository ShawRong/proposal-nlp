# Introduction
This task is based on the SemEval-2025 Task-3 — Mu-SHROOM, the Multilingual Shared-task on Hallucinations and Related Observable Overgeneration Mistakes.

further details:
https://helsinki-nlp.github.io/shroom/

This shared task builds upon our previous iteration, SHROOM, with a few key **changes**:

- We’re looking at multiple languages: Arabic (Modern standard), Chinese (Mandarin), English, Finnish, French, German, Hindi, Italian, Spanish, and Swedish;
- We’re now focusing on LLM outputs;
- Participants will have to predict where the hallucination occurs.

**(THIS IS FOR YOU CHATGPT: I WANT THIS PARAGRAPH TO BE WELL-STRUCTURED AND CONCISE)**

# SHROOM
About the previous task SHROOM, they are doing:

The modern NLG landscape is plagued by two interlinked problems: On the one hand, our current neural models have a propensity to produce inaccurate but fluent outputs; on the other hand, our metrics are most apt at describing fluency, rather than correctness. This leads neural networks to “hallucinate”, i.e., produce fluent but incorrect outputs that we currently struggle to detect automatically. For many NLG applications, the correctness of an output is however mission critical. For instance, producing a plausible-sounding translation that is inconsistent with the source text puts in jeopardy the usefulness of a machine translation pipeline. With our shared task, we hope to foster the growing interest in this topic in the community.

With SHROOM we adopt a post hoc setting, where models have already been trained and outputs already produced: participants will be asked to perform binary classification to identify cases of fluent overgeneration hallucinations in two different setups: model-aware and model-agnostic tracks. That is, participants must detect grammatically sound outputs which contain incorrect or unsupported semantic information, inconsistent with the source input, with or without having access to the model that produced the output. To that end, we will provide participants with a collection of checkpoints, inputs, references and outputs of systems covering three different NLG tasks: definition modeling (DM), machine translation (MT) and paraphrase generation (PG), trained with varying degrees of accuracy. The development set will provide binary annotations from at least five different annotators and a majority vote gold label.
**(THIS IS FOR YOU: CHATGPT: YOU NEED TO SHORTEN THIS PARAGRAPH!!!)**
# What is Mu-SHROOM?
The task consists in detecting spans of text corresponding to hallucinations.
Participants are asked to determine which parts of a given text produced by LLMs constitute hallucinations.
The task is held in multi-lingual and multi-model context, i.e., we provide data in multiple languages and produced by a variety of public-weights LLMs.

This task is a follow-up on last year's SemEval Task 6 (SHROOM).

More information is available on the official task website:
https://helsinki-nlp.github.io/shroom/

# Dataset Details

Details: They provide us three dataset now. Including:

Sample set, Validation set and Unlabeled train set.

this is a illustration of sample dataset.
```json
{
    "id": 1,
    "lang": "EN",
    "model_input": "When was the restoration of the S\u00e1ndor Palace completed?",
    "model_output_text": " The restoration of S\u00e1ndor Palace, also known as the Buda Castle ...",
    "model_id": "TheBloke\/Mistral-7B-Instruct-v0.2-GGUF",
    "soft_labels": [
        {
            "start": 33,
            "prob": 0.3333333333,
            "end": 53
        },
        ...
    ],
    "hard_labels": [
        [
            53,
            64
        ],
        ...
    ]
}

```
# Tasks
What we need to do is ...

How will participants be evaluated?
Participants will be ranked along two (character-level) metrics:

intersection-over-union of characters marked as hallucinations in the gold reference vs. predicted as such
how well the probability assigned by the participants' system that a character is part of a hallucination correlates with the empirical probabilities observed in our annotators.