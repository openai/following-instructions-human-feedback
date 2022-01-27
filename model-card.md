# InstructGPT Model Card

Last updated: January 2022

Based on [Model Cards for Model Reporting (Mitchell et al.)](https://arxiv.org/abs/1810.03993), we’re providing some accompanying information about InstructGPT.

## Model Details

InstructGPT is a GPT-style language model. Researchers at OpenAI developed the model by fine-tuning GPT-3 to follow instructions using human feedback. There are three model sizes: 1.3B, 6B, and 175B parameters.

### Model date
January 2022

### Model type
Language model

### Paper & samples
[Training language models to follow instructions with human feedback][LINK_TO_PAPER]

We release samples from our models on public NLP datasets that require sampling [here](automatic-eval-samples/).

### Model version
InstructGPT is described in the [above paper][LINK_TO_PAPER].

The versions deployed on the OpenAI API are fine-tuned using the same human feedback data, using a slightly different procedure, which will be detailed in a forthcoming publication.

## Model Use
The intended direct users of InstructGPT are developers who access its capabilities via the OpenAI API. Through the OpenAI API, the model can be used by those who may not have AI development experience, to build and explore language modeling systems across a wide range of functions. We also anticipate that the model will continue to be used by researchers to better understand the behaviors, capabilities, biases, and constraints of large-scale language models.

Due to InstructGPT’s limitations (described below), and the breadth and open-ended nature of its capabilities, access and use are subject to OpenAI’s API Usage Guidelines, and API Terms of Use, which are designed to prohibit the use of the API in a way that causes societal harm. We review all use cases before customers deploy API models in production, and have systems in place to revoke access if necessary after moving to production. Additionally, we provide guidance to users on some of the potential safety risks they should consider - and related mitigations.

## Data and Performance

### Data

InstructGPT models are initialized from GPT-3 models, whose training dataset is composed of text posted to the internet or uploaded to the internet (e.g., books). The internet data that the GPT-3 models were trained on and evaluated against includes:

1. a version of the [CommonCrawl dataset](https://commoncrawl.org/the-data/) filtered based on similarity to high-quality reference corpora,
2. [an expanded version of the Webtext dataset](https://d4mucfpksywv.cloudfront.net/better-language-models/language_models_are_unsupervised_multitask_learners.pdf),
3. two internet-based book corpora, and
4. [English-language Wikipedia](https://en.wikipedia.org/wiki/Main_Page).

InstructGPT is then further fine-tuned on a dataset labeled by human labelers. The labelers comprise a team of about 40 contractors whom we hired through Upwork and ScaleAI. Our aim was to select a group of labelers who were sensitive to the preferences of different demographic groups, and who were good at identifying outputs that were potentially harmful. Thus, we conducted a screening test designed to measure labeler performance on these axes. We selected labelers who performed well on this test. We collaborated closely with the labelers over the course of the project. We had an onboarding process to train labelers on the project, wrote detailed instructions for each task, and answered labeler questions in a shared chat room.

The dataset consists of input prompts (from the OpenAI API or written by labelers), demonstrations of the desired model behavior written by our labelers, and labeler rankings of outputs from multiple models. The text prompts submitted to the OpenAI API were from an earlier version of the InstructGPT models (trained via supervised learning on a subset of our demonstration data on the Playground interface). Customers using the Playground were informed that their data could be used to train further models via a recurring notification any time InstructGPT models were used. To reduce the risk of the models learning potentially sensitive customer details, we filtered all prompts in the training split for personally identifiable information (PII). Some of our prompts were also written by contractors themselves, because we needed an initial source of instruction-like prompts to bootstrap the process, and these kinds of prompts weren't often submitted to the regular GPT-3 models on the API.

### Performance
We measure InstructGPT’s performance on two categories of tasks: prompts submitted to the OpenAI API, and public academic datasets. Results on each can be found in the [paper][LINK_TO_PAPER]. Overall, InstructGPT outputs are significantly preferred by labelers over outputs from GPT-3 on our API distribution. In our paper, we show that InstructGPT produces fewer toxic outputs than GPT-3 on the RealToxicityPrompts dataset, generates more truthful and informative answers on the TruthfulQA dataset, and shows improvements in appropriateness, obeying explicit constraints in the instruction, attempting the correct instruction, and not making up information on “closed-domain” tasks. However, this does not mean that the model is fully aligned or fully safe, as we detail in the next section.


## Limitations

### Model limitations

InstructGPT and our analysis of it have a number of limitations. Some of them are inherent to any model with machine learning (ML) components that can have high-bandwidth, open-ended interactions with people (e.g. via natural language): ML components have limited robustness; ML components are biased; open-ended systems have large surface areas for risk; and safety is a moving target for ML systems. Like any model with ML components, InstructGPT can only be expected to provide reasonable outputs for inputs similar to those in its training data.

We outline some further limitations below. These limitations are similar to those of the original GPT-3 model, though many of them may be mitigated by our InstructGPT training procedure.

* Repetition: GPT-3 samples sometimes repeat themselves semantically at the document level, and can lose coherence over long passages, contradict themselves, and occasionally contain non-sequitur sentences or paragraphs.

* Lack of real-world grounding: GPT-3, like other large pretrained language models, is not grounded in other modalities of experience, such as video, real-world physical interaction, or human feedback, and thus lacks a large amount of context about the world.

* Predominantly English: GPT-3 is trained largely on text in the English language, and is best suited for classifying, searching, summarizing, or generating such text. GPT-3 will by default perform worse on inputs that are different from the data distribution it is trained on, including non-English languages as well as specific dialects of English that are not as well-represented in  training data.

* Interpretability and predictability: the capacity to interpret or predict how GPT-3 will behave is very limited, a limitation common to most deep learning systems, especially in models of this scale.

* High variance on novel inputs: GPT-3 is not necessarily well-calibrated in its predictions on novel inputs. This can be observed in the much higher variance in its performance as compared to that of humans on standard benchmarks.

* Biases: GPT-3, like all large language models trained on internet corpora, will generate stereotyped or prejudiced content. The model has the propensity to retain and magnify biases it inherited from any part of its training, from the datasets we selected to the training techniques we chose. This is concerning, since model bias could harm people in the relevant groups in different ways by entrenching existing stereotypes and producing demeaning portrayals amongst other potential harms.

* Follow harmful instructions: Perhaps the greatest limitation of InstructGPT relative to GPT-3 is that, in most cases, they follow the user's instruction, even if that could lead to harm in the real world.  For example, when given a prompt instructing the models to be maximally biased, InstructGPT generates more toxic outputs than equivalently-sized GPT-3 models. We discuss potential mitigations in the following sections.


### Methodology limitations

The behavior of our InstructGPT models is determined in part by the human feedback obtained from our contractors. Some of the labeling tasks rely on value judgments that may be impacted by the identity of our contractors, their beliefs, cultural backgrounds, and personal history. We hired about 40 contractors, guided by their performance on a screening test meant to judge how well they could identify and respond to sensitive prompts, and their agreement rate with researchers on a labeling task with detailed instructions. We kept our team of contractors small because it's easier to have high-bandwidth communication with a smaller set of contractors who are doing the task full-time. However, this group is clearly not representative of the full spectrum of people who will use and be affected by our deployed models. As a simple example, our labelers are primarily English-speaking and our data consists almost entirely of English instructions.


[LINK_TO_PAPER]: https://www.openai.com
