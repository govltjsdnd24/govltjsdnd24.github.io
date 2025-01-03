---
categories: [ Study, Generative AI ]
tags: [ ai ] 
---


## Introduction

Firstly, what is a generative AI? Almost everyone nowadays is familiar with the concept--AI capable of creating original content while imitating human behavior. Copilot and Chat-GPT being two very famous examples of Gen-AI, there are multiple types of response that it can output:
- Natural Language Generation
- Image Generation
- Code Generation

## Language Models

A core element of Gen-AI is a language model, which is a machine learning model that performs NLP (Natural Language Processing) tasks. Then what are the contemporary language models based on? That is, a transformer model. Trained from a vast amount of text, transformer models comprehend the relationship between words and creates a "sequence of text" that is most likely to happen. Transformer model architecture is composed of the following two components:
- Encoder block that creates a sementic representation of training vocabularies
- Decoder block that creates a new language sequence

The process could be described as such:
1. Transformer model learns via a large quantity of NL text derived from various sources
2. Text sequence is tokenized (seperated into words) and the encoder uses attention technology to establish relationship between these tokens. For example, find out how much impact certain token makes within a sequence, or which tokens are generally used in the same context.
3. Encoder's output is a collection of vectors (array of multi-value numbers) where each element resembles the semantic property of a token. This kind of vector is called "embeddings".
4. The decoder block is executed in a new text token sequence and utilizes embeddings formulated by the encoder to create appropriate NL output.
5. For example, if a sequence such as "When my dog was a..." is given, the model uses attention to analyze the semantic property encoded in the embeddings and the input token to create the word "puppy"

However, not all transformer model architectures follow the same process. BERT(Bidirectional Encoder Representations from Transformers) model from Google uses only encoder blocks, but GPT only uses decoder blocks.

![image](https://github.com/user-attachments/assets/5e0ff877-6eae-4bc4-9ecc-aa7b93fd2026)


## Tokenization

The first process of traning a transformer model is seperating a training text into tokens, and in process identify each distinct textual values; each discontinuous word within a the training text can be regarded as a token (while in reality a part of word or a combination of words can be a token).

However, tokens are only used as a index for each word, and don't contain any semantic or relational information. This is where embeddings come in. Embeddings is a list of token vectors which represent the semantic properties of the specific token. Since vectors describe the direction and distance of a multi-level dimension, we can deduce how similar and asimiliar certain token is to another.

Let's take for example a 3d vector with the following words: dog, cat, puppy, and skateboard.
- 4("dog"): [10,3,2]
- 8(“cat“): [10,3,1]
- 9 ("puppy"): [5,2,1]
- 10 ("skateboard"): [-3,3,2]

Puppy and dog, while having different set of numbers, have a similar direction, and cat and dog has a similar positioning overall. However, skateboard is in a completely different position and direction, rendering it irrelevant.

![image](https://github.com/user-attachments/assets/d0bed15d-eaee-4193-9fe1-e53ab6dfe588)


## Attention

The encoder and decoder models are composed of several layers that make up the neural network. I'd like to cover an important layer among these--the attention layer. Attention is basically a technology to examine a text token sequence and quantify the intensity of the relationship between those tokens. Self attention also accounts for the impact that the surrounding tokens have on a certain token.

Each token is scrutinized carefully within the encoder block before the appropriate encoding for the vector is decided. The vetor value is based on the token itself and the relationship with other tokens it often appears with. This situational approach accounts for the circumstance where the same token have a different meaning based on the context.

Decoder block uses the attention layer to antipcate the following token in the sequence. For each token generated, the model has an attention layer that takes into account the sequence of tokens up to that point. The model considers which of the tokens are the most influential when considering what the next token should be. For example, "I" and "Heard" would be most important in "I heard a dog".

Attention layers express through numerical vectors rather than textx. In a decoder, the process starts with a sequence of token embeddings representing the text to be completed. The first task carried out is the addition of positional encoding layer in the very front.

The process of attention proceeds as follows:
1. A sequence of token embeddings is fed into the attention layer
2. The decoder's goal is to predict the next token in the sequence
3. The attention layer endows apropriate weight to each token in the sequence from the relative impact teach token makes on the prediction
4. New vector is calculated from the weight. Multi-head attention calculates several alternative tokens by using different elements in the embeddings
5. A fully connected neural network uses vector score to search the entire dictionary and predict the most likely token
6. Output joins the token sequence and the process repeats.

During training, we are provided with the actual sequence; we just mask the tokens so that it 'appears' unknown. Then, we compare the outcome with the actual sequence and calculate the loss.  Weights are adjusted so that loss is minimized.

## LLM vs SLM

- Large Language Model
    - LLM sources data available from internet and accessible media to train text representing a vastly general topic
    - Trained LLM has billions of parameters (weight applied on vector embeddings to calculate token sequence prediction)
    - Can provide Natural language response containing broad text generative feature
    - Too heavy to run on local device
    - Micro adjustments using additional data for specialization on a certain topic takes a longtime and additional training requires a lot of computational power.
- Small Language Model
    - SLM's training is based on a smaller yet specific data set
    - Has relatively fewer parameters
    - Is exceptional in a specific topic, but falls behind in general language response
    - The smaller it gets, the more on-premise-capable it beceomes with various deployment options and faster adjustment available
    - Micro adjustments take less time and resource


## Microsoft Copilot

There are various uses of Copilot:

- Web search using AI
- AI assistance for information workers
    - Summarize word document to 3 keypoints
    - Create entire presentation based on email
    - Find out my schedule based on the emails' content
- Business process aid with AI
    - Provide customer service with chatbot
    - Integrate CRM database to easily monitor customer data
    - Analyze risk and impact of a certain decision (prediction)
- AI assistance in data analysis
    - Create code to visualize, analyze data on Spark notebook
    - Create data visualization on Power BI
- Infrastructure and security
    - Find out and take care of security risks

## Prompt Engineering

Here are the steps to improve Copilot's reponses:
1. Start with the motive for the provided task
2. Provide source for the spcific range of data the response will be based on
3. Add context to maximize the appropriateness and relavance of the response
4. Set concrete expectation for the response
5. Materialize output by repeating query based on previous prompt and response

## Expanding Copilot

- Copilot Studio (SaaS)
- Azure AI Studio (PaaS)

## Reference

[https://learn.microsoft.com/en-us/training/modules/fundamentals-generative-ai/](https://learn.microsoft.com/en-us/training/modules/fundamentals-generative-ai/)

