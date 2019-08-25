## lmproof - Language Model Proof Reader

Library to do proof-reading corrections for Grammatical Errors, spelling errors, confused word errors and other errors using pre-trained Language Models.

Currently, we use the language model based approach mentioned in [Christopher Bryant and Ted Briscoe. 2018](http://aclweb.org/anthology/W18-0529) with few changes.

Unlike many approaches to GEC, this approach does NOT require annotated training data and mainly depends on a monolingual language model. The program works by iteratively comparing certain words in a text against alternative candidates and applying a correction if one of these candidates is more probable than the original word. These correction candidates are variously generated by a word inflection library or are otherwise defined manually. Currently, this system only corrects:

    Non-words (e.g. freind and informations)
    Morphology (e.g. eat, ate, eaten, eating, etc.)
    Common Determiners and Prepositions (e.g. the, a, in, at, to, etc.)
    Commonly Confused Words (e.g. bear/bare, lose/loose, etc.)

This work builds upon https://github.com/chrisjbryant/lmgec-lite/

## Components

### Language Models
* [pytorch-transformers](https://github.com/huggingface/pytorch-transformers)
### Inflection generators
* [LemmInflect](https://github.com/bjascob/LemmInflect) is used to lemmatize and generate inflections for candidate proposals to the language model.
### Spell Checker
* [symspellpy](https://github.com/mammothb/symspellpy) is used for obtaining spell check candidates.

The components are highly modularised to facilitate experimentation with newer scorers and support more languages.
Pre-trained language models for other languages, inflectors, common error patterns can be easily added to support more languages.

## TODOs

* Research on distilling gpt-2 to a smaller model (LSTM?) to reduce the horrendous latency.
* Experiment on GEC dev sets to obtain optimal thresholds.
* Anyway to handle insertions.
* Add more languages.
* Check whether LemmInflect proposals are actually better than just using [AGID](https://github.com/sai-prasanna/lmgec-lite/tree/master/resources/agid-2016.01.19).