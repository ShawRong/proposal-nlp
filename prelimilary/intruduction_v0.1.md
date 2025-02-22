# Introduction

This task is part of SemEval-2025 Task-3 — Mu-SHROOM, the Multilingual Shared-task on Hallucinations and Related Observable Overgeneration Mistakes. This iteration builds upon the previous SHROOM task with some key **changes**:

- **Multilingual Focus**: The task covers multiple languages, including Arabic (Modern Standard), Chinese (Mandarin), English, Finnish, French, German, Hindi, Italian, Spanish, and Swedish.
- **LLM Outputs**: The emphasis is now on detecting hallucinations in outputs from instruction-tuned language models.
- **Hallucination Detection**: Participants will predict the locations of hallucinations within the generated text.

For more details, visit the [official task website](https://helsinki-nlp.github.io/shroom/).

# SHROOM

The previous SHROOM task addressed two interlinked challenges within the modern NLG landscape: the tendency of neural models to produce fluent yet inaccurate outputs and the inadequacy of current metrics to assess correctness. This often results in "hallucinations," where models generate plausible-sounding responses that are factually incorrect. This issue is critical for applications like machine translation, where accuracy is essential.

In SHROOM, participants engaged in a post hoc setting, performing binary classification to identify fluent but incorrect outputs. This involved two tracks: model-aware and model-agnostic. Participants detected grammatically correct outputs that contained unsupported or incorrect information, using a dataset that included various NLG tasks: definition modeling, machine translation, and paraphrase generation. The dataset featured binary annotations from multiple annotators, ensuring a robust evaluation.

# What is Mu-SHROOM?

Mu-SHROOM focuses on detecting spans of text that represent hallucinations in outputs from large language models (LLMs). Participants will identify which parts of the generated text are hallucinations, working within a multilingual and multi-model context that includes data from various LLMs.

This task follows last year's SemEval Task 6 (SHROOM). More information can be found on the [official task website](https://helsinki-nlp.github.io/shroom/).

**(COMBINE THIS SECTION WITH INTRODUCTION SECTION, I DONT WANT TO SEE THIS SECTION SEPARATED.)**

# Dataset Details

The datasets provided include:

- Sample set
- Validation set
- Unlabeled train set

The data file is formatted as a JSON lines. Each line is a JSON dict object and corresponds to an individual datapoint.

Each datapoint corresponds to a different annotated LLM production, and contains the following information:

a unique datapoint identifier (`id')
a language (`lang');
a model input question (model_input), the input passed to the models for generation;
a model identifier (model_id) denoting the HuggingFace identifier of the corresponding model;
a model output (model_output_text), the output generated by a LLM when provided the aforementiond input;
binarized annotations (hard_labels), provided as a list of pairs, where each pair corresponding to the start (included) and end (excluded) of a hallucination;
continuous annotations (soft_labels), provided as a list of dictionary objects, where each dictionary objects contains the following keys:
start, indicating the start of the hallucination span,
end, indicating the end of the hallucination span,
prob, the empirical probabilty (proportion of annotators) marking the span as a hallucination
The hard labels (hard_labels) will be used to assess the intersection-over-union accuracy, whereas the soft labels (soft_labels) will be used to measure correlation.
In the evaluation phase, participants will be tasked with reconstructing the soft labels and provide the start, end and prob keys of all the spans they detect.
**(SHORTEN THIS PARAGRAPH TO 3-6 SENTENCE, ONLY THE IMPORTANT THING NEEDED.)**

### Sample Dataset Illustration

```json
{
    "id": 1,
    "lang": "EN",
    "model_input": "When was the restoration of the Sándor Palace completed?",
    "model_output_text": "The restoration of Sándor Palace, also known as the Buda Castle ...",
    "model_id": "TheBloke/Mistral-7B-Instruct-v0.2-GGUF",
    "soft_labels": [
        {
            "start": 33,
            "prob": 0.3333333333,
            "end": 53
        }
    ],
    "hard_labels": [
        [53, 64]
    ]
}
```

# Tasks

Participants are tasked with detecting hallucinations in the provided text. 

### Evaluation Metrics

Participants will be evaluated based on two character-level metrics:

1. **Intersection-over-Union**: This measures the overlap between characters marked as hallucinations in the gold reference and those predicted by the participants.
2. **Probability Correlation**: This assesses how well the probabilities assigned by the participants' systems align with the empirical probabilities observed by annotators.

This is a preliminary overview of our proposal; further refinements will be made as the task develops.