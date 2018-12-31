---
layout: default
title: Information Extraction
permalink: /InformationExtraction/
---

I worked as a Research assistant under [Dr. Davood Rafiei](https://webdocs.cs.ualberta.ca/~drafiei/) during Summer 2018 along side with [Peter Elliot](https://gitlab.com/petelliott) to build a tool to extract "facts" from articles. We employed the used of [SpaCy](https://spacy.io/) as a library for Natural Language Processing in Python as well as [neuralcoref](https://github.com/huggingface/neuralcoref) for coreference resolution. Using spaCy, we built the dependancy trees of given sentences, and then based on some hand-coded rules, selected and formed facts in the form of triplets. Afterwards, the facts are categorized into non-mutual exclusive groups: Time-based, Past-tense, Transactions, Personnel, Communications and Organizational.

## Example
```
Tervita's new CEO, John Cooper, is committed to providing employees with regular communication updates.
```

Our program produces the following relations.

```
Personnel relations: 2
ID:1 (John Cooper; [is] CEO [of]; Tervita)
ID:3 (John Cooper; [is]; Tervita's new CEO)

PastTense Contact relations: 1
ID:0 (Tervita's new CEO, John Cooper,; is committed; to providing employees with regular communication updates)
```

![Flowchart](/assets/IEflowchart.png)

![spaCy Visualizer](/assets/Visualizer.png)
