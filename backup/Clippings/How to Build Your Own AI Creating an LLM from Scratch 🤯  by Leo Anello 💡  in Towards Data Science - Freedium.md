---
title: "How to Build Your Own AI: Creating an LLM from Scratch 🤯 | by Leo Anello 💡 | in Towards Data Science - Freedium"
source: "https://freedium.cfd/https://towardsdatascience.com/how-to-build-your-own-ai-creating-an-llm-from-scratch-3b26b9a84b10"
author:
published:
created: 2025-01-25
description: "Understanding and building AI for natural language processing"
tags:
  - "clippings"
---
🚨 **[For Non-Members — Friend Link](https://medium.com/towards-data-science/how-to-build-your-own-ai-creating-an-llm-from-scratch-3b26b9a84b10?sk=05a090d087525aac90de033bd9fcf1a0)**: Thank you for your support, and please don't hold back on the claps! 👏

In my [previous tutorial](https://medium.com/towards-data-science/satellite-image-classification-with-deep-learning-complete-project-e4cb44337393), I introduced **Deep Learning for Computer Vision**, an essential area of research and application in artificial intelligence.

Now, let's shift our focus to a different domain: ***Natural Language Processing*** *(NLP)*. No other field has been as profoundly transformed by AI in recent years as NLP.

From the early approaches in NLP to today's state-of-the-art technologies — **Large Language Models (LLMs)** — the progress is simply extraordinary.

These LLMs, the cutting-edge tools in this domain, are what I will explore with you in this project. Once again, I'll break the tutorial into two parts, focusing on **Deep Learning for Natural Language Processing**.

This field is creating significant societal and business impacts, enabling applications capable of **generating** text, **translating** it, **creating** text from images, and **producing** human-level responses — with exceptional quality.

It's important to remember that this evolution is continuous and **challenging to keep up with**. New models, architectures, and tools are emerging at an incredible pace.

In this tutorial, we will build an **LLM architecture from scratch.**

While the resulting performance won't match that of commercially available models — due to the limited data we'll use — the goal is to thoroughly explain the architecture's construction.

### **2\. Overview**

I'll guide you step by step to **build and train an LLM from scratch**.

We'll design its framework, construct the architecture, train the model, and test its functionality — all using a **simple dataset of just 10 lines**.

The goal isn't to create a commercial-grade model but to help you **understand how LLMs work**. In the next tutorial, we'll dive into **fine-tuning pre-trained LLMs**, one of the most advanced AI techniques.

Traditional techniques like **LSTMs** and embedding models were innovative in their time but often failed to capture *context*.

For example: *"The bat is in the room."* Is it about a **flying mammal** or a **baseball bat**? Without context, the meaning is unclear.

LLMs excel at understanding **context**, thanks to the revolutionary **attention mechanism** introduced in 2017 as part of the **transformer architecture**.

Initially, LLMs were tools reserved for experts. However, the release of **ChatGPT in late 2022** transformed **public access to AI**. Suddenly, anyone could interact with an LLM through a simple interface.

This sparked a **rapid expansion in LLM development**, making it easier than ever to access models capable of near-human precision. Let's get started!

### 3\. **Python Packages Used**

First, we'll install the necessary packages. For this project, we'll use the `watermark` package to generate a watermark, which allows us to document the versions of the packages used in this notebook.

Here's the command to install it:

```python
# 1. Install the watermark package.
# This package is used to record the versions of other packages used in this Jupyter notebook.
!pip install -q -U watermark
```

I'll set the **random seed** so you can always reproduce the same results:

```python
# 2. Set the random seed
import random
random.seed(10)
```

We'll use a very small dataset here.

The goal is not to create any kind of commercial application but to show you the architecture.

It wouldn't make sense to wait 15 days to complete the training. Training an LLM can easily take 1, 2, or even 3 weeks. Some of the larger LLMs are trained in 90 days — yes, **90 days** to train a massive LLM.

So, it's impractical to wait 90 days just to see results. Besides, you'd need hardware that would likely cost thousands of dollars. Nowadays, training an LLM from scratch is rarely justified.

What truly matters today is using a **pre-trained LLM** and fine-tuning it with your own data, which is exactly what I'll demonstrate in the next tutorial.

For now, the goal is purely didactic: to help you understand how an LLM works internally. Since the dataset is very small, I'll set a **random seed** to ensure you can reproduce the same results as I do.

With this setup, all we need to construct the architecture is:

```python
# 3. Imports
import re
import math
import torch
import numpy as np
import torch.nn as nn
import torch.nn.functional as F
import torch.optim as optim
from random import *
```

We'll use **PyTorch**, the Python framework for working with Deep Learning, along with several functions to prepare the data in **NumPy array** format. Then, we'll build the architecture and train the model.

Additionally, I'm using the `re` package for regular expressions, as we'll be working with text data. What do we need to do with text data? It needs to be cleaned and processed, and regular expressions will help with that.

We'll also use the `math` package for mathematical operations in Python, and **NumPy** to prepare the data. All other components will come from PyTorch, enabling you to create the model's architecture.

So, load all of this into your session, and activate the `watermark` package:

```perl
# 4. Versions of the packages used in this Jupyter notebook
%reload_ext watermark
%watermark -a "Your_Name_Here"
```

Then, we can load the data in text format, apply the cleaning process, and pre-process the data. From there, we'll construct the architecture module by module, as planned. Once the architecture is complete, we'll train the **LLM** and test it at the end of the project.

### **4\. Loading Text Data**

The next step is to load the dataset that will be used to train the **LLM** from scratch. Follow the reasoning here, as there are some important points to consider.

```ini
# 5. Load the text data
text_data = open('text.txt', 'r').read()
```

Again, our goal is purely **didactic —** We're not building a commercial application with the LLM.

The focus is for you to understand the structure and architecture of an LLM and the components that make up this type of model.

```bash
# 6. Check the type of the text data
type(text_data)

# -----> str

# 7. Print the text data
print(text_data)
```

For our example, a dataset with **11 lines** is more than sufficient:

```
01. "Hello, how are you? I am Carol.\n"
02. "Hello, Carol, my name is Frank. Nice to meet you.\n"
03. "Nice to meet you too. How are you today?\n"
04. "Great. My football team won the competition.\n"
05. "Wow, congratulations Frank!\n"
06. "Thank you Carol.\n"
07. "Shall we have a pizza later to celebrate?\n"
08. "Sure. Do you recommend any restaurant, Carol?\n"
09. "Yes, a new restaurant opened, and they say the banana pizza is phenomenal.\n"
10. "Okay. Let's meet at the restaurant at seven PM, is that okay?\n"
11. "That's fine. See you later then."
```

Our dataset is small — just **11 lines** — but sufficient to create a functional model. This simplicity showcases how much more could be achieved with massive datasets.

To work with text data, we'll first **preprocess** it: clean the text, adjust it, and add **special tokens** like padding. For businesses, this step is crucial when evaluating whether training an LLM from scratch is worthwhile.

### ☝️ **Is It Worth Training an LLM from Scratch?**

In **95% of cases, the answer is no**. Training an LLM from scratch requires:

**Massive datasets** — not just a few lines but petabytes of data.

**Time and resources** — data extraction and preprocessing can take weeks, and model training even longer.

**High-cost hardware** — GPUs capable of handling this scale can cost thousands of dollars.

For perspective, training a commercial LLM from scratch can take **90 days or more**.

### 👉 **A Better Alternative**

Instead of building an LLM from the ground up, **fine-tuning pre-trained LLMs** is a faster, more cost-effective solution.

**Pre-trained models**: Already available, open-source, and powerful.

**Fine-tuning**: Requires smaller datasets and modest hardware.

**Time-efficient**: A few hours is enough to customize the model.

In the next tutorial, I'll guide you through this fine-tuning process step.

### **5\. Pre-Processing Text Data and Building the Vocabulary**

Now we have the data, but it's still in its raw format. So, what's the next step? Processing the data. After that, we'll build the vocabulary that will be used to train the **LLM**.

First, I'll filter out special characters, specifically **periods**, **commas**, **question marks**, and **exclamation points**. To achieve this, I'll use the `re` package (regular expressions in Python) to create a rule or pattern that scans the text data and removes those characters:

```python
# 8. Filter special characters: '.', ',', '?', '!'
sentences = re.sub("[.,!?\\-]", '', text_data.lower()).split('\n')
```

Let's enhance the procedure to handle all special characters by replacing them with an empty string.

I'll also convert all words to lowercase and split the text using the **`\n`** newline character. This ensures each sentence is properly separated:

```bash
# 9. Print the sentences
print(sentences)
['"hello how are you i am carol\\n"', 
'"hello carol my name is frank nice to meet you\\n"', 
'"nice to meet you too how are you today\\n"', 
'"great my football team won the competition\\n"', 
'"wow congratulations frank\\n"', 
'"thank you carol\\n"', 
'"shall we have a pizza later to celebrate\\n"', 
'"sure do you recommend any restaurant carol\\n"', 
'"yes a new restaurant opened and they say the banana pizza is phenomenal\\n"', 
'"okay let\'s meet at the restaurant at seven pm is that okay\\n"', 
'"that\'s fine see you later then"']
```

Observe, the special characters within each sentence are gone.

The comma you see here is separating one sentence from another because this is a **Python list**.

Just as a reminder, the square brackets indicate a list in Python. So, the commas are simply used to separate each element of the list, which in this case, is a list of sentences.

Now, notice that everything is in lowercase, and special characters have been removed. Let's proceed to the next step: splitting the sentences into words and creating a list of words:

```bash
# 10. Split the sentences into words and create a word list
word_list = list(set(" ".join(sentences).split()))
```

The `split()` function, when used with empty parentheses, splits the text by **spaces**. This means every time it encounters a space, it breaks the sentence into words. By applying this method to each sentence, we can create a list of words.

```bash
# 11. Print the word list
print(word_list)
['a', 'later', 'carol', 'frank\\n"', 'any', 'okay\\n"', 'i', '"shall', 'the', '
have', 'banana', 'you', 'say', 'pizza', 'that', 'fine', '"hello', 'too', 'won',
'am', 'to', 'new', 'carol\\n"', 'team', 'competition\\n"', 'then"', '"great', 
'"thank', '"yes', 'opened', 'we', 'they', 'is', 'do', '"that\'s', 'and', 'how',
'restaurant', '"okay', 'see', 'football', 'at', 'today\\n"', '"wow','celebrate\\n"', 'seven', '"nice', 'pm', 'nice', '"sure', 'my', 'you\\n"', 
'congratulations', 'meet', 'name', 'recommend', 'are', 'phenomenal\\n"', 'frank', "let's"]
```

We are creating a **list of words** as part of the data processing workflow. Now, imagine doing this on **petabytes of data** — a necessary step when training a large **LLM**, which demands enormous computational power.

Next, I'll initialize the **dictionary** with the special tokens used in **BERT**. These tokens are essential for properly handling sequences during training. Here's how we do it:

```python
# 12. Initialize the word dictionary with BERT's special tokens
word_dict = {'[PAD]': 0, '[CLS]': 1, '[SEP]': 2, '[MASK]': 3}
```

**BERT** is the architecture of the **LLM** we'll use. It is essentially **state-of-the-art** in transformer architectures, introduced in 2017.

While the **Transformer architecture** itself was created in 2017, the **BERT model** was introduced in 2018.

To this day, it is considered the gold standard for LLMs. Everything that came after BERT uses it as a reference.

Now, we'll define the **special tokens**: `[PAD]`, `[CLS]`, `[SEP]`, and `[MASK]`. Each of these tokens is assigned a specific number.

```bash
# 13. Print the word dictionary
print(word_dict)
```

![None](https://miro.medium.com/v2/resize:fit:700/1*s4kVb1SsIpQZlsa2buUVdw.png)

1. `[PAD]`: Used to pad sequences to a fixed length.
2. `[UNK]`: Represents unknown words not in the vocabulary.
3. `[CLS]`: Added to the beginning of the sequence for classification tasks.
4. `[SEP]`: Marks the end of a sentence or separates sentences in a sequence.
5. `[MASK]`: Used for masking tokens in **masked language modeling** tasks.

Here it is. Now, what will I do?

I'll iterate through the `word_list` that I created earlier to store this list of words in my `word_dict`, the dictionary I just initialized:

```python
# 14. Add the words to the dictionary and create indices
for i, w in enumerate(word_list):
    word_dict[w] = i + 4
```

And now, observe the result.

```bash
# 15. Print the updated word dictionary
print(word_dict)
{'[PAD]': 0, '[CLS]': 1, '[SEP]': 2, '[MASK]': 3, 'a': 4, 'later': 5, 
'carol': 6, 'frank\\n"': 7, 'any': 8, 'okay\\n"': 9, 'i': 10, '"shall': 11,
 'the': 12, 'have': 13, 'banana': 14, 'you': 15, 'say': 16, 'pizza': 17, 
'that': 18, 'fine': 19, '"hello': 20, 'too': 21, 'won': 22, 'am': 23, 'to': 24, 
'new': 25, 'carol\\n"': 26, 'team': 27, 'competition\\n"': 28, 'then"': 29, 
'"great': 30, '"thank': 31, '"yes': 32, 'opened': 33, 'we': 34, 'they': 35, 
'is': 36, 'do': 37, '"that\'s': 38, 'and': 39, 'how': 40, 'restaurant': 41, 
'"okay': 42, 'see': 43, 'football': 44, 'at': 45, 'today\\n"': 46, '"wow': 47, 
'celebrate\\n"': 48, 'seven': 49, '"nice': 50, 'pm': 51, 'nice': 52, '"sure': 53, 
'my': 54, 'you\\n"': 55, 'congratulations': 56, 'meet': 57, 'name': 58, 
'recommend': 59, 'are': 60, 'phenomenal\\n"': 61, 'frank': 62, "let's": 63}
```

This first token is assigned the code **0**. The second token has the code **1**, the third **2**, and so on. The first word receives the code **4**, the next **5**, and so forth, successively.

Why did we encode it this way — assigning a number to each token or word in our dataset? Because AI, as you know, is **mathematics**, right?

You won't work with data in text form; you'll always work with numerical formats. That's how the model processes data: it receives numerical input, performs mathematical operations, generates numerical output, and then you decode it back into text format.

This is the foundation of constructing the dictionary. Next, we'll reverse the order, setting the indices as keys and the words as values in the dictionary:

```python
# 16. Reverse the order and make the indices the key and the words the value in the dictionary
number_dict = {i: w for i, w in enumerate(word_dict)}
```

Essentially, I'm using a **Dict Comprehension**. I'm iterating through the entire dictionary to simply reverse the order. Here's how it looks:

```bash
# 17. Print the number dictionary
print(number_dict)
```

Now I have an **index**, and for each numerical value, I have the corresponding term.

```css
{0: '[PAD]', 1: '[CLS]', 2: '[SEP]', 3: '[MASK]', 4: 'a', 5: 'later', 
6: 'carol', 7: 'frank\\n"', 8: 'any', 9: 'okay\\n"', 10: 'i', 
11: '"shall', 12: 'the', 13: 'have', 14: 'banana', 15: 'you', 
16: 'say', 17: 'pizza', 18: 'that', 19: 'fine', 20: '"hello', 
21: 'too', 22: 'won', 23: 'am', 24: 'to', 25: 'new', 
26: 'carol\\n"', 27: 'team', 28: 'competition\\n"', 29: 'then"', 30: '"great',
 31: '"thank', 32: '"yes', 33: 'opened', 34: 'we', 35: 'they', 
36: 'is', 37: 'do', 38: '"that\'s', 39: 'and', 40: 'how', 
41: 'restaurant', 42: '"okay', 43: 'see', 44: 'football', 45: 'at', 
46: 'today\\n"', 47: '"wow', 48: 'celebrate\\n"', 49: 'seven', 50: 
'"nice', 51: 'pm', 52: 'nice', 53: '"sure', 54: 'my', 55: 'you\\n"', 
56: 'congratulations', 57: 'meet', 58: 'name', 59: 'recommend', 60: 'are', 
61: 'phenomenal\\n"', 62: 'frank', 63: "let's"}
```

It's coming together nicely. We're preparing the vocabulary.

Now, let's check the size of this vocabulary:

```python
# 18. Vocabulary size
vocab_size = len(word_dict)
print(vocab_size)

# -----> 64
```

The vocabulary size is **64**. Clearly, this is a very small vocabulary. For a large-scale **LLM**, we'd need data on the scale of petabytes. That's the core secret of any **LLM**.

Take **ChatGPT** as an example. Remember, ChatGPT is not an **LLM** itself; it's a **web interface** for an LLM — either **GPT-3** or **GPT-4**, depending on whether you're using the free or paid version.

Why does ChatGPT perform so well? Because its underlying LLM, **GPT**, was trained on a **massive dataset**. This resulted in an enormous vocabulary, which gives the impression of human-like intelligence in text generation. But this capability stems from the vast amount of training data fed into the model, leading to a rich vocabulary.

Now that we understand this, let's prepare a **list of tokens**:

```ini
# 19. Create a list for the tokens
token_list = list()
```

I'll now loop through the sentences to create the list by splitting them.

```perl
# 20. Loop through the sentences to create the token list
for sentence in sentences:
    arr = [word_dict[s] for s in sentence.split()]
    token_list.append(arr)
```

This output is a **list of tokens:**

```
[[20, 40, 60, 15, 10, 23, 26], 
[20, 6, 54, 58, 36, 62, 52, 24, 57, 55], 
[50, 24, 57, 15, 21, 40, 60, 15, 46], 
[30, 54, 44, 27, 22, 12, 28], 
[47, 56, 7], 
[31, 15, 26], 
[11, 34, 13, 4, 17, 5, 24, 48], 
[53, 37, 15, 59, 8, 41, 26], 
[32, 4, 25, 41, 33, 39, 35, 16, 12, 14, 17, 36, 61], 
[42, 63, 57, 45, 12, 41, 45, 49, 51, 36, 18, 9], 
[38, 19, 43, 15, 5, 29]]
```

What are these tokens here? Let's follow along together.

I'll print the sentence to show the tokens:

```makefile
# 22. First sentence
text_data[0:31]

# -----> "Hello, how are you? I am Carol
```

And now, I'll print the **list of tokens**:

```bash
# 23. First sentence in token format (what will be used to train the BERT model)
token_list[0]

# -----> [20, 19, 12, 5, 49, 23, 33]
```

This is the first sentence from my dataset. This is the first list of tokens. What does this mean? What did we just do? We assigned a code, a number, to each element in the sentence.

And where does this number 20 come from? No, it comes from up there.

```makefile
20: '"hello', 
19: 'how', 
12: 'are', 
5: 'you',  
49: 'i', 
23: 'am', 
33: 'carol
```

Where is the **20**? Let's search for it together. It's the word **Hello**, you can check it successively. We've just created a vocabulary.

The difference from a commercial **LLM** is that this would be scaled up to **petabytes of data**. But the vocabulary is created in exactly the same way: you assign a numerical value to each word, building a vocabulary.

The larger the dataset, the bigger the vocabulary will be. Naturally, with more words, the vocabulary becomes enormous. Then, you link your text data to this numerical representation of the vocabulary.

This is what feeds the model.

```css
[[20, 40, 60, 15, 10, 23, 26], 
[20, 6, 54, 58, 36, 62, 52, 24, 57, 55], 
[50, 24, 57, 15, 21, 40, 60, 15, 46], 
[30, 54, 44, 27, 22, 12, 28], 
[47, 56, 7], 
[31, 15, 26], 
[11, 34, 13, 4, 17, 5, 24, 48], 
[53, 37, 15, 59, 8, 41, 26], 
[32, 4, 25, 41, 33, 39, 35, 16, 12, 14, 17, 36, 61], 
[42, 63, 57, 45, 12, 41, 45, 49, 51, 36, 18, 9], 
[38, 19, 43, 15, 5, 29]]
```

So, in practice, the model doesn't actually know what the words **Olá**, **Como vai**, or others mean. It only works with numbers. Later, when I provide it with new text data, I'll convert that data into numerical format using the same vocabulary.

The model will then generate output in numerical format, and I'll decode it using my vocabulary. The result will be delivered to you as text, just like ChatGPT does.

But hold on — **GPT is fast**, isn't it? It's fast because it runs on **thousands of GPUs** that power a system where the GPT model operates. For an **LLM** to deliver results at high speed, you obviously need the appropriate hardware.

What we've done here is create a **vocabulary** to associate each word with a number. This is what we'll provide to the model. Instead of delivering this list of sentences, as we have up there:

```swift
01. "Hello, how are you? I am Carol.\n"
02. "Hello, Carol, my name is Frank. Nice to meet you.\n"
03. "Nice to meet you too. How are you today?\n"
04. "Great. My football team won the competition.\n"
05. "Wow, congratulations Frank!\n"
06. "Thank you Carol.\n"
07. "Shall we have a pizza later to celebrate?\n"
08. "Sure. Do you recommend any restaurant, Carol?\n"
09. "Yes, a new restaurant opened, and they say the banana pizza is phenomenal.\n"
10. "Okay. Let's meet at the restaurant at seven PM, is that okay?\n"
11."That's fine. See you later then."
```

We will indeed deliver the list of sentences, but in **numerical format**:

```css
[[20, 40, 60, 15, 10, 23, 26], 
[20, 6, 54, 58, 36, 62, 52, 24, 57, 55], 
[50, 24, 57, 15, 21, 40, 60, 15, 46], 
[30, 54, 44, 27, 22, 12, 28], 
[47, 56, 7], 
[31, 15, 26], 
[11, 34, 13, 4, 17, 5, 24, 48], 
[53, 37, 15, 59, 8, 41, 26], 
[32, 4, 25, 41, 33, 39, 35, 16, 12, 14, 17, 36, 61], 
[42, 63, 57, 45, 12, 41, 45, 49, 51, 36, 18, 9], 
[38, 19, 43, 15, 5, 29]]
```

And with an **order** and a **context**, exactly what we have in the vocabulary.

### 6\. Defining Hyperparameters

The next step is defining the hyperparameters. These parameters control the training process. **Who defines the hyperparameters?**

That's right — you, the AI engineer, are responsible for this definition. These settings dictate how the training will proceed.

In the end, many will admire the functioning AI, saying, *"Wow, it works automatically, what a marvel!"* True, but a human has to define the hyperparameters at some point — at least for now.

Perhaps in the future, AI will handle everything autonomously, creating, redefining, and setting its own hyperparameters. But for now, this isn't the case. **Humans are still essential to the process.**

```python
# 24. Hyperparameters
batch_size = 6
n_segments = 2
dropout = 0.2

# Maximum length
maxlen = 100

# Maximum number of tokens to be predicted
max_pred = 7

# Number of layers
n_layers = 6

# Number of heads in multi-head attention
n_heads = 12

# Embedding size
d_model = 768

# Feedforward dimension size: 4 * d_model
d_ff = d_model * 4

# Dimension of K(=Q)V
d_k = d_v = 64

# Epochs
NUM_EPOCHS = 50
```

For instance, you need to set values for parameters such as **batch size**, **number of segments**, and **dropout** — which, as we've studied, is a regularization strategy. Other key hyperparameters include:

- **Maximum sequence length**: Defines the maximum number of tokens in the input.
- **Number of tokens to predict**: Specifies how many tokens the model should generate.
- **Number of layers**: Determines the depth of the model architecture.
- **Number of heads in multi-head attention**: Controls how many attention mechanisms work in parallel.
- **Embedding size**: Represents the numerical matrix for text data representation.
- **Feedforward dimension size**: Typically set as `4 * d_model`, where `d_model` is the embedding size.
- **Key dimension size (****`k`****)**: Part of the attention module.
- **Number of training epochs**: Defines how many times the model will iterate over the training dataset.

I'll be using these hyperparameters throughout the various blocks of the implementation. For didactic purposes, they are initially consolidated in one place for better organization. As the architecture evolves, these hyperparameters will be distributed across different sections.

Feel free to adjust these values later. For example, you might want to test a different `dropout` rate, modify the number of layers in the model, or change the number of heads in the multi-head attention mechanism. However, **here's a key tip**: Avoid making multiple changes simultaneously.

Instead:

1. Adjust one parameter.
2. Train the model.
3. Document the results.
4. Return, tweak another parameter, and repeat the process.

This approach allows you to clearly track which changes led to the desired outcome and which did not. By documenting each step, you'll gain a deeper understanding of the model's behavior and its responses to specific hyperparameter adjustments.

### 7\. Creating Data Batches & Applying Special Tokens

The next step is one that might make you burn a few neurons. Not the artificial neural network's neurons, but your own, okay?

So, follow along carefully. This is not trivial, it's not simple — it requires a level of abstraction.

I will explain this to you using images. There is complementary text in the notebook, and shortly, the Python code will follow. I want you to understand, in general terms, the entire procedure.

Let's take a look at these images, which will explain exactly what we need for creating the data batches and applying the special tokens.

Take a moment to observe the image carefully:

![None](https://miro.medium.com/v2/resize:fit:700/1*IHe_ldq-58PTuHtMXezbUQ.png)

High-level architecture of the Transformer encoder used in the BERT model. Source: [BERT: Pre-training of DeepBidirectional Transformers for Language Understanding](https://arxiv.org/pdf/1810.04805), arXiv:1810.04805.

On the left side, you'll notice that we have `CLS`, which is a token. Then, we have a sentence—for instance, the first sentence. After that, there's another token, a separator, and then a second sentence, okay? It's already clear what `CLS` and `SEP` are, as we defined them earlier when building the vocabulary. They are just separator tokens.

*What's their purpose?* Simply to tell the LLM when a sentence starts and ends. That's right — there's no intelligence here; it's just math. So, we need to explicitly indicate, *"Hey, this is the beginning of a sentence."* And, *"This is the end of the sentence; now the next one starts,"* and so on. That's what those tokens are for.

In the middle, you'll see the stack of encoders, which are the exact structure of the Transformer architecture. These encoders are small blocks performing mathematical operations.

On the right side, you'll notice the output matrix. In this case, it has a dimension of **768**, a hyperparameter we defined earlier in the notebook under **#24** in the hyperparameter section.

```ini
# Embedding size
d_model = 768
```

This Is Embedding. In practice, what we'll do is take the input text, pass it through the red encoders, and they will generate the matrices.

These matrices will then be used throughout the entire training process of the model.

*But how does this happen?* This other image helps illustrate the process clearly:

![None](https://miro.medium.com/v2/resize:fit:700/1*_-fJmVdQDQYBgVB5NeWmUA.png)

Diagram representing the embedding, multi-head attention, and normalization steps in the BERT model. Source: [BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding](https://arxiv.org/pdf/1810.04805), arXiv:1810.04805

#### Let's Go From Bottom to Top

At the bottom, you'll notice the `CLS` token, which, as you already know, marks the beginning of the sequence.

Then, we have several values representing the sentences. You'll also see the `MASK` token—I'll explain it shortly.

Next comes the `SEP`token, which marks the end of the first sentence, such as Sentence A. After that, we move to Sentence B, where each yellow block represents a word in the sentence—a token.

*What's the purpose of* *`MASK`**?* It's for masking. In this specific architecture, BERT, masking is used to hide certain words in a sentence so the model can predict them. For instance:

1. One word in a sentence is masked.
2. Later, another word is masked.
3. Then another word is masked.

In each case, the original word is replaced with a `MASK` token. The model sees the sentence, notices the `MASK`, and realizes that a word is missing. It then tries to predict what the missing word should be.

Instead of providing the full sentence, we feed the model sentences with *gaps*, represented by `MASK`. By doing this, the model learns to predict the missing words. This approach works very well, as the architecture gradually learns these words while processing the entire dataset.

We then take this entire structure:

![None](https://miro.medium.com/v2/resize:fit:700/1*YsRAFPa60hfsIxErN7SxhA.png)

Diagram representing the embedding, multi-head attention, and normalization steps in the BERT model. Source: [BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding](https://arxiv.org/pdf/1810.04805), arXiv:1810.04805

#### And Build the Embedding Layer

This is where the embedding layer comes into play. The embedding layer converts text representation into a numerical representation. Each token is assigned a number based on our vocabulary.

- The `CLS` token receives its own numerical value.
- The `SEP` token is assigned a value.
- The `MASK` token has its unique value.
- Each word in the sentence also gets a corresponding number.

That's why we added these special tokens to our vocabulary in the first place. They play a crucial role in mapping text data into a numerical format that the model can process.

![None](https://miro.medium.com/v2/resize:fit:700/1*ewEDlEo5Afbi5h_QlUc9rg.png)

Diagram representing the embedding, multi-head attention, and normalization steps in the BERT model. Source: [BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding](https://arxiv.org/pdf/1810.04805), arXiv:1810.04805

This Embedding Feeds the BERT Architecture. The embedding will serve as input to the BERT architecture, which, in turn, will make predictions. But it's not just any prediction — BERT uses **Fully Connected Layers (FFNN)** at the end to perform the prediction.

The goal is to predict precisely the next word, which in this case, is the masked word. By leveraging these fully connected layers, the model refines its understanding and predicts the missing tokens with high accuracy.

![None](https://miro.medium.com/v2/resize:fit:700/1*aOEf9RiEE-_VFskzkqk5TQ.png)

Diagram representing the embedding, multi-head attention, and normalization steps in the BERT model. Source: [BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding](https://arxiv.org/pdf/1810.04805), arXiv:1810.04805

### The MASK and How the Model Learns

The masked word — the one replaced by `MASK`—is exactly what the model learns to predict. This is just one part of BERT, by the way. Soon, I'll bring the full architecture and explain all its components. For now, we're focusing on this specific section.

The reason I've explained all this is to prepare you for the next step: **creating the data batches.** In other words, considering that BERT expects the data in this specific format, *how do we prepare it?*

That's the question we'll address next, ensuring the data is ready to be fed into the model in the correct structure.

```python
# 25. Define the function to create data batches
def make_batch():

    # Initialize the batch as an empty list
    batch = []

    # Initialize counters for positive and negative examples
    positive = negative = 0

    # Continue until half of the batch is positive examples and the other half is negative examples
    while positive != batch_size / 2 or negative != batch_size / 2:

        # Randomly select indices for two sentences
        tokens_a_index, tokens_b_index = randrange(len(sentences)), randrange(len(sentences))

        # Retrieve the tokens corresponding to the indices
        tokens_a, tokens_b = token_list[tokens_a_index], token_list[tokens_b_index]

        # Prepare the input ids by adding special tokens [CLS] and [SEP]
        input_ids = [word_dict['[CLS]']] + tokens_a + [word_dict['[SEP]']] + tokens_b + [word_dict['[SEP]']]

        # Define the segment ids to differentiate the two sentences
        segment_ids = [0] * (1 + len(tokens_a) + 1) + [1] * (len(tokens_b) + 1)

        # Calculate the number of predictions to be made (15% of tokens)
        n_pred = min(max_pred, max(1, int(round(len(input_ids) * 0.15))))

        # Identify candidate positions for masking that are not [CLS] or [SEP]
        cand_masked_pos = [i for i, token in enumerate(input_ids) if token != word_dict['[CLS]'] and token != word_dict['[SEP]']]

        # Shuffle the candidate positions
        shuffle(cand_masked_pos)

        # Initialize lists for masked tokens and their positions
        masked_tokens, masked_pos = [], []

        # Mask tokens until the desired number of predictions is reached
        for pos in cand_masked_pos[:n_pred]:
            masked_pos.append(pos)
            masked_tokens.append(input_ids[pos])

            # Random mask
            if random() < 0.8:
                input_ids[pos] = word_dict['[MASK]']

            # Replace with another token 10% of the time (20% of the remaining time)
            elif random() < 0.5:
                index = randint(0, vocab_size - 1)
                input_ids[pos] = word_dict[number_dict[index]]

        # Add zero padding to the input ids and segment ids to reach the maximum length
        n_pad = maxlen - len(input_ids)
        input_ids.extend([0] * n_pad)
        segment_ids.extend([0] * n_pad)

        # Add zero padding to the masked tokens and their positions if needed
        if max_pred > n_pred:
            n_pad = max_pred - n_pred
            masked_tokens.extend([0] * n_pad)
            masked_pos.extend([0] * n_pad)

        # Add to the batch as a positive example if the sentences are consecutive
        if tokens_a_index + 1 == tokens_b_index and positive < batch_size / 2:
            batch.append([input_ids, segment_ids, masked_tokens, masked_pos, True])
            positive += 1

        # Add to the batch as a negative example if the sentences are not consecutive
        elif tokens_a_index + 1 != tokens_b_index and negative < batch_size / 2:
            batch.append([input_ids, segment_ids, masked_tokens, masked_pos, False])
            negative += 1

    # Return the complete batch
    return batch
```

### We Have the Function `make_batch`

The `make_batch` is responsible for generating data batches to train BERT.

This function prepares the correct input structure needed for model training.

This includes input tokens, masked tokens, positions of masked tokens, segment IDs, and a label indicating whether the second sentence immediately follows the first, if there's a sequence.

#### So, what does it involve?

We have **initialization**, **sentence pair generation**, **segment IDs**, and **MLM** (Masked Language Model), which is the BERT component responsible for language masking.

In this case, the function randomly selects **15% of the tokens** to mask for the MLM task, ensuring that the `[CLS]` and `[SEP]` tokens are **never masked**. Why is this important? If we mask `[CLS]` and `[SEP]`, it would cause issues. Why? Because the model wouldn't know where each sentence starts and ends.

So, when applying the masking, which is done randomly, we need to ensure that `[CLS]` and `[SEP]` are preserved. Otherwise, we'd lose the boundaries indicating where each sentence begins and ends. These are the **building blocks** for the `make_batch` function.

And where did we derive these rules applied to the `make_batch` function? From the **research paper**:

Reading This Takes You to Another Level. Diving into the source material and research paper takes you to the next level. It's directly available from the source and provides detailed descriptions of each architecture.

This is your **best reference**. Based on this knowledge, you can then use your programming skills to build a function like the one in **Command #25**.

#### What Does the Function Do?

It's a Python function that:

1. **Initializes** the batch as an empty list.
2. **Initializes counters** for positive and negative examples.
3. **Creates a loop** where:

- Random indices for two sentences are chosen.
- Corresponding tokens for these indices are retrieved.
- Input IDs are prepared.

And where do these IDs (tokens) come from? Believe it or not, **from the dictionary we created earlier**! That's why we built the dictionary in the first place.

#### Key Steps in the Function

- **Segment IDs**: Segment IDs are defined to differentiate sentences.
- **Masking**: The function calculates 15% of the tokens to be masked, as this is what BERT will predict during training.
- **Candidate Positions**: It identifies candidate positions for masking, ensuring that `[CLS]` and `[SEP]` are never masked (as explained before).
- **Shuffling**: Candidate positions are shuffled.
- **Masked Tokens**: Initializes lists for masked tokens and masks them.

#### Why Do This?

Yes, we have to do this because we're building the architecture **from scratch**. This isn't a pre-trained model. We're implementing it step by step. To achieve this, you need to refer to the **research paper**, understand how the researchers designed the model structure, and translate that into Python code. That's exactly what we're doing here.

#### How Does Masking Work?

- **80% of the time**, the selected token is replaced with `[MASK]`.
- **10% of the time**, the token is replaced with another random token.
- **10% of the time**, the token remains unchanged.

#### Padding

Padding is crucial for building the input matrix. Why? Because sentences have different lengths. However, when feeding data into the model, it must receive a **uniform matrix**. This means each sequence needs to be padded with a special token (`[PAD]`) to match the required length.

This padding ensures all input sequences are of equal length, making it possible to build the input matrix. This was the **final piece of the puzzle** that needed explaining.

By following this process, you're not just using a pre-trained model; you're learning how to construct it step by step, directly inspired by the research paper. Isn't that amazing? It truly is!

```python
# Add zero padding to the input ids and segment ids to reach the maximum length
        n_pad = maxlen - len(input_ids)
        input_ids.extend([0] * n_pad)
        segment_ids.extend([0] * n_pad)

        # Add zero padding to the masked tokens and their positions if needed
        if max_pred > n_pred:
            n_pad = max_pred - n_pred
            masked_tokens.extend([0] * n_pad)
            masked_pos.extend([0] * n_pad)

        # Add to the batch as a positive example if the sentences are consecutive
        if tokens_a_index + 1 == tokens_b_index and positive < batch_size / 2:
            batch.append([input_ids, segment_ids, masked_tokens, masked_pos, True])
            positive += 1

        # Add to the batch as a negative example if the sentences are not consecutive
        elif tokens_a_index + 1 != tokens_b_index and negative < batch_size / 2:
            batch.append([input_ids, segment_ids, masked_tokens, masked_pos, False])
            negative += 1

    # Return the complete batch
    return batch
```

So, even if the sentence has only one word, I will pad the rest with Padding tokens until it reaches the length of 100, which is the `MaxLen`.

What we are doing here in the code is exactly subtracting `MaxLen` from the length of the `input_ids`, which are the IDs for each sentence. The difference is what I will use to fill with Padding.

Then, I add zero padding to the masked tokens and their positions, if necessary, and proceed to work with positive and negative examples:

```python
# Add to the batch as a positive example if the sentences are consecutive
        if tokens_a_index + 1 == tokens_b_index and positive < batch_size / 2:
            batch.append([input_ids, segment_ids, masked_tokens, masked_pos, True])
            positive += 1

# Add to the batch as a negative example if the sentences are not consecutive
        elif tokens_a_index + 1 != tokens_b_index and negative < batch_size / 2:
            batch.append([input_ids, segment_ids, masked_tokens, masked_pos, False])
            negative += 1
```

#### What Are Positive and Negative Examples Here?

Positive and negative examples have nothing to do with sentiment or good vs. bad connotation. Positive and negative refer to the **sequence of sentences**. This is how BERT learns.

I will always provide **pairs of sentences** to the model. For example: "BERT, look, this is the first sentence — it's the positive one. The next sentence is the negative one — it's part of the sequence."

BERT will always receive pairs to help it learn **context**.

During training, I'll provide sentence pairs, and for each sentence, I'll make sure they are padded to the same length (`maxlen`) using the padding token.

- The **first sentence** in the pair is the positive one.
- The **second sentence** is the negative one.

This sequence of pairs is what the model will process during training. And that's exactly what I'm preparing in this `make_batch` function.

#### Preparing the Padding Function

The padding function will handle adding the special padding token to fill sequences up to the required length. Here's the function:

```python
# 26. Function for padding
def get_attn_pad_masked(seq_q, seq_k):

    batch_size, len_q = seq_q.size()

    batch_size, len_k = seq_k.size()

    pad_attn_masked = seq_k.data.eq(0).unsqueeze(1)

    return pad_attn_masked.expand(batch_size, len_q, len_k)
```

I have the operations according to the batch size, and in the notebook, once again, I've provided a description of everything this function does.

Make sure to read the description later, and now I want to show it to you so you can understand how the data will be delivered to the model.

Just a reminder: **we haven't created the model yet**. At this stage, we are only preparing the data. I'll start creating the model shortly. For now, what I'm focusing on is still data preparation.

### Running Padding

Now, I will apply `get_attn_pad_masked` so you can see the output.

This will help close the understanding. First, I'll create the batch by calling the function and generating the data batch:

```ini
# 27. Create a batch
batch = make_batch()
```

I will then pass the batch through the `map` function to apply it to all the batches, which will generate this output:

```python
# 28. Extract the elements from the batch
input_ids, segment_ids, masked_tokens, masked_pos, isNext = map(torch.LongTensor, zip(*batch))
```

It will generate the `input_ids`, `segment_ids`, `masked_tokens`, `masked_pos`, and whether it's the next sentence or not (`isNext`).

I'll print each of these elements for you. We already have the elements, right? I'm just printing the `input_ids`for now. Here's the result:

```bash
# 29. Sentence IDs
input_ids
```

![None](https://miro.medium.com/v2/resize:fit:700/1*Z0qRS6FGIu3W_iGjU2jTpQ.png)

input\_ids

Now that you have the `input_ids` for all the sentences and have created the complete data batch, you can retrieve the `input_ids` for just the first sentence.

Since indexing starts from 0 in Python, here's how you can access the `input_ids` for the first sentence:

```python
# 29. Input IDs of the first sentence
input_ids[0]
```

![None](https://miro.medium.com/v2/resize:fit:700/1*7Uvk9pMkdC34oSL-16wgXA.png)

input\_ids\[0\]

#### What is the Number 0?

The number `0` is exactly the **padding token**. So, if you count the tokens, the maximum length will be **100**. Considering this maximum length, the sentence will end at a certain point, and from there, it will be padded.

To reinforce: **I can't leave it empty**.

It must be filled with the padding token `0`, which corresponds to the padding token in our vocabulary. So, here you have the `input_ids` for the first sentence, where the padding is applied to fill up the sequence.

Now, Let's Look at the Segment IDs for the First Sentence. The `segment_ids` for the first sentence are:

```bash
# 30. Segment IDs of the first sentence
segment_ids[0]
```

![None](https://miro.medium.com/v2/resize:fit:700/1*-6TEVdLhr4HFYEyw4CjCLw.png)

segment\_ids\[0\]

I have the masked tokens:

```bash
# 31. Masked tokens of the first sentence
masked_tokens[0]
```

![None](https://miro.medium.com/v2/resize:fit:700/1*G0-DKk1zTVLSQZs2IzAEcA.png)

masked\_tokens\[0\]

I have the position of the tokens:

```bash
# 32. Masked positions of the first sentence
masked_pos[0]
```

![None](https://miro.medium.com/v2/resize:fit:700/1*a4GEdBL6uqDx21Ut7jxkgA.png)

masked\_pos\[0\]

And then I have this, `isNext`:

```python
# 33. "isNext" label of the first sentence
isNext[0]

# ----> tensor(0)
```

What is `isNext`? The `isNext` flag indicates whether the current sentence is the next one in the sequence or not. I took sentence 0, so it's the first one. Will it be the next sentence? No. Therefore, `isNext` will have a value of `0`.

In other words, it's the first sentence, not the second one. This is the information we're obtaining here.

A lot of details, right? Now, you can apply the masking function to prepare everything for the first sentence, which will be delivered to the model.

```python
# 34. Apply the padding function
get_attn_pad_masked(input_ids, input_ids)[0][0], input_ids[0]
```

![None](https://miro.medium.com/v2/resize:fit:700/1*7qFbEVQT6g8-FlPkkDYqXg.png)

get\_attn\_pad\_masked

Now, you can see that the masking is correctly set up. The `false` values indicate valid tokens—meaning **these are not padding**. In other words, it's **false**, so it's not padding. Everything else marked as `true` is padding.

To confirm this, I've printed the `input_ids` for you. What we've done with padding is exactly this: marked the positions as **true or false**, indicating whether it's padding or not. This will be used alongside the **embedding matrix** to train the model.

We now need to build the architecture. A lot of work, right? And we haven't even started building the model yet; this is all just **data preparation**.

If you were using a pre-trained model and only needed to fine-tune it with your own data, you could do that in just **two lines of code**. However, what we've done here is the foundation for training the model from scratch.

### **8\. Model Construction**

I'm going to show you something now. Don't get terrified — at least not yet! We're going to build a model from scratch, right? That's the purpose; everything is deliberate.

Here, I'll present the **model architecture**, and then we'll create it block by block. We'll start with:

1. The **embedding module**,
2. Then the **attention module**,
3. After that, the **multi-head attention**,
4. Next, the **positional feedforward module**,
5. Followed by the **encoder layer**,
6. And finally, the **complete architecture**.

Once we've done that, we'll have built the model. Yes, we're starting from scratch, so we'll create everything. Afterward, we'll move on to training and evaluation.

So, relax — there's no need to feel overwhelmed. I'll explain everything to you step by step. There's plenty of reading material in the notebook, along with references and images to guide you.

Let's start constructing the model! Below is a high-level description of the **Transformer Encoder**:

![None](https://miro.medium.com/v2/resize:fit:700/1*TWrv6sBGc6OhSZPIuDW6Rw.png)

Detailed visualization of data flow in BERT for masked token prediction, using the GELU activation function. Source: [BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding](https://arxiv.org/pdf/1810.04805), arXiv:1810.04805.

The **input** is a sequence of tokens, which are first embedded into vectors and then processed through the neural network.

The **output** is a sequence of vectors of size `H`, where each vector corresponds to an input token at the same index.

Predicting the output words involves:

1. Adding a **classification layer** on top of the encoder's output.
2. Multiplying the output vectors by the **embedding matrix** to match the vocabulary dimensions.
3. Calculating the probability of each word in the vocabulary using `softmax`.

The `softmax` function is commonly used in deep learning models for classification. In **BERT**, the **loss function** only considers the predictions of *masked tokens*, ignoring non-masked words.

This means **BERT** predicts the *masked words*. For example, in the sentence: *"The batter held the bat tightly,"* if the word *bat* is masked, the model processes the input as: *"The batter held the \[MASK\] tightly."*

The model then predicts the missing word, learning whether it's *bat* (a baseball bat) or something else during training.

**BERT** converges more slowly than directional models, but this is offset by its higher ability to understand **context**. Context is crucial — it's the foundation of **LLMs**.

The larger the context, the better the LLM performs. This approach originated with **BERT**, which emphasized the importance of *context* for learning and generating meaningful outputs.

*Context is key* for humans too. For instance:*"The batter held the bat tightly"* requires **context** to determine whether *bat* refers to a **baseball bat** or a **flying mammal**.

**LLMs** need this same contextual understanding to function effectively.

Let's now examine the **architecture** and see how the **embeddings** are loaded.

![None](https://miro.medium.com/v2/resize:fit:700/1*EkwF2MBcaFY5BIsHLa4w0A.png)

Detailed visualization of data flow in BERT for masked token prediction, using the GELU activation function. Source: [BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding](https://arxiv.org/pdf/1810.04805), arXiv:1810.04805.

Within these **embeddings**, I'll have the numerical representation of the words, including the **masked tokens**.

These embeddings will pass through the **encoder**, which will generate an output. This output will then feed into a **fully connected layer**, using, for example, **GELU** as the activation function, along with **normalization**.

This process will generate an output, which we'll multiply by the vocabulary embeddings and apply **Softmax**. Softmax will produce the probability for each word, allowing us to predict which word it is.

For instance, let's say we have words **W1**, **W2**, **W3**, and **W4**. Word **W4** is masked, so the model won't see it. We know what it is — you and I do — because we have the real data. The model, however, won't have access to this word.

This is how we'll perform the evaluation. The model will predict the word, and we'll compare it with the real value we have. This allows us to assess the model's performance.

How will it make the prediction? By generating a **probability distribution** using **Softmax**. This is a common approach in deep learning, particularly for **classification tasks**.

![None](https://miro.medium.com/v2/resize:fit:700/1*4u_wpb9NMYtPn5Ake8W1eA.png)

Representation of token, sentence, and positional embeddings in the BERT model. Source: [BERT: Pre-training of DeepBidirectional Transformers for Language Understanding](https://arxiv.org/pdf/1810.04805), arXiv:1810.04805.

We start with the **input**, which includes `[CLS]` to mark the beginning of the sequence, `[SEP]` as a separator, masks for hidden words, and paddings to ensure all sentences have the same length.

These padding tokens help standardize sentence sizes. This input will be converted into numerical representation during tokenization.

Beyond word tokenization, we also tokenize sentences, specifying which ones are positive or negative.

The input includes `[CLS]` at the start, followed by the words, the `[SEP]` token as a divider, and the masked words. After word tokenization, sentence tokenization follows, marking sentences as positive or negative.

Finally, **Positional Encoding** assigns a position to each word within the sentences, allowing the model to understand the order of words and perform its learning process effectively.

All these steps are managed within the batch creation function, preparing the input with both sentences and their positions for the model to learn and predict probabilities.

### **9\. Embedding Module**

We start with the **Embedding module**, which is responsible for converting text data into numerical representations.

To achieve this, we create a Python class named `Embedding`, which inherits features from the `Module` class in `torch.nn:`

```python
# 36. Embedding Class
class Embedding(nn.Module):

    # Constructor method
    def __init__(self):

        super(Embedding, self).__init__()

        # Token embedding
        self.tok_embed = nn.Embedding(vocab_size, d_model)

        # Position embedding
        self.pos_embed = nn.Embedding(maxlen, d_model)

        # Segment (token type) embedding
        self.seg_embed = nn.Embedding(n_segments, d_model)

        # Layer normalization
        self.norm = nn.LayerNorm(d_model)

    # Forward method
    def forward(self, x, seg):

        seq_len = x.size(1)

        pos = torch.arange(seq_len, dtype=torch.long)

        # (seq_len,) -> (batch_size, seq_len)
        pos = pos.unsqueeze(0).expand_as(x)

        embedding = self.tok_embed(x) + self.pos_embed(pos) + self.seg_embed(seg)

        return self.norm(embedding)
```

**Who is NN?** It refers to **PyTorch**, specifically the `neural network` module (`torch.nn`). You don't need to create the entire class from scratch.

Instead, you create the class and define only what is required for your architecture. Every class in Python typically includes a constructor method (`__init__`), and in this case, we also have the `forward` method.

The constructor (`__init__`) is used to initialize methods and attributes of the class. Here, we first initialize the **super constructor**:

```python
super(Embedding, self).__init__()
```

**What is** `super`**?** It refers to the **constructor of the parent class**. In this case, the `Embedding` class is the child of `nn.Module`.

Essentially, we're telling PyTorch: *"Hey, I'm creating a child class, but before proceeding, please initialize the parent class constructor as well."* This is precisely what the `super()` function does in the line of code.

After initializing the parent constructor, we prepare the **token embedding**. This is done by calling the `Embedding` function from the `neural network` module, where we define the `vocab_size` (the size of the vocabulary) and `d_model` (the embedding dimension, defined earlier as a hyperparameter).

**What is this for?** The token embedding maps each token (word, subword, or character) in the vocabulary to a vector of size `d_model`. These vectors are used as input for further processing in the neural network.

```ini
# Token embedding
self.tok_embed = nn.Embedding(vocab_size, d_model)
```

It's simply to **define the size of the matrix** that will hold the data in its numerical representation.

Following that, we prepare the **Positional Embedding:**

```ini
# Position embedding
self.pos_embed = nn.Embedding(maxlen, d_model)
```

This one will handle the position of the words in the sentences. It's part of the **Transformer architecture**, where we specify the position of the elements in the input data.

In this case, we are creating the **Positional Embedding**, which is the positioning matrix. Following that, we set up the **Segment Embedding**.

```ini
# Segment (token type) embedding
self.seg_embed = nn.Embedding(n_segments, d_model)
```

Remember that we created the `Segment_IDs`?

![None](https://miro.medium.com/v2/resize:fit:700/1*jrhbVD7eLI2_ceYHB1FqZA.png)

This is to indicate what is here:

![None](https://miro.medium.com/v2/resize:fit:700/1*UPRzu_dYcphJmektwL5N8A.png)

Representation of token, sentence, and positional embeddings in the BERT model. Source: [BERT: Pre-training of DeepBidirectional Transformers for Language Understanding](https://arxiv.org/pdf/1810.04805), arXiv:1810.04805.

In BERT, I need to provide the sentences in a specific order. So, I specify: this is the first sentence, this is the next one. This way, it understands the context.

Therefore, I need to create one more embedding: an embedding for the actual data itself, an embedding for the positions, and an embedding for the segments.

```ini
# Token embedding
self.tok_embed = nn.Embedding(vocab_size, d_model)

# Position embedding
self.pos_embed = nn.Embedding(maxlen, d_model)

# Segment (token type) embedding
self.seg_embed = nn.Embedding(n_segments, d_model)
```

And then, the layer normalization with `LayerNorm`:

```ini
# Layer normalization
self.norm = nn.LayerNorm(d_model)
```

Here, it's just to initialize each element.

In the `forward` method, that's where I provide the sequence:

```python
# Forward method
    def forward(self, x, seg):

        seq_len = x.size(1)

        pos = torch.arange(seq_len, dtype=torch.long)

        # (seq_len,) -> (batch_size, seq_len)
        pos = pos.unsqueeze(0).expand_as(x)

        embedding = self.tok_embed(x) + self.pos_embed(pos) + self.seg_embed(seg)

        return self.norm(embedding)
```

So, I will receive `X` and the segment. I will calculate the sequence length, then use that to create `pos`, which represents the positions.

I will then use `pos.unsqueeze` to adjust the shape accordingly. After that, I combine all of this.

When the model is ready for training, I will provide **one single embedding**—a **super matrix** that includes the embeddings of the data, the positions, and the sentences.

It's as if I'm merging all these components into a single matrix. Actually, it's not "as if"; this is exactly what we're doing. This is precisely the **embedding module** for our model.

### **10\. Scaled Dot Product Attention Module**

Here, we implement the **Dot Product Attention**, specifically the scaled version, which is normalized. Following this, we create the **Multi-Head Attention**, with multiple attention layers.

Take a look at the **definition of the Scaled Dot Product Attention Module** directly in the notebook, where all the details are provided. Notice that the code is relatively straightforward:

```ruby
# 37. Define the class to perform Scaled Dot-Product Attention
class ScaledDotProductAttention(nn.Module):

    # Initialization method for the class
    def __init__(self):

        # Initialize the base class
        super(ScaledDotProductAttention, self).__init__()

    # Forward method to define the data pass through
    def forward(self, Q, K, V, attn_mask):

        # Calculate the attention scores as the dot product of Q and K, and normalize by the key size
        scores = torch.matmul(Q, K.transpose(-1, -2)) / np.sqrt(d_k)

        # Apply the attention mask to prevent attention to certain tokens
        scores.masked_fill_(attn_mask, -1e9)

        # Apply softmax to get normalized attention weights
        attn = nn.Softmax(dim=-1)(scores)

        # Multiply the attention weights by V to get the context
        context = torch.matmul(attn, V)

        # Return the context and the attention weights
        return context, attn
```

We create our class, which also inherits directly from the **Module**. I define the constructor, initializing the parent class constructor. After that, I create the **forward method**, which will take these three elements as inputs:

```ruby
# Forward method to define the data pass through
    def forward(self, Q, K, V, attn_mask):
```

**Q, K, and V** are precisely the vectors used to learn the attention weights during Transformer model training. Notice that I am passing these elements along with the attention mask (`attn_mask`).

And the rest? Those are the well-known **matrix operations**.

```makefile
# Calculate the attention scores as the dot product of Q and K, and normalize by the key size
scores = torch.matmul(Q, K.transpose(-1, -2)) / np.sqrt(d_k)

# Apply the attention mask to prevent attention to certain tokens
scores.masked_fill_(attn_mask, -1e9)

# Apply softmax to get normalized attention weights
attn = nn.Softmax(dim=-1)(scores)

# Multiply the attention weights by V to get the context
context = torch.matmul(attn, V)

# Return the context and the attention weights
return context, attn
```

I am combining the elements precisely to deliver the result of a single attention head. Here, I am defining one attention head, but in practice, I will use several, right? This is because I will create a **Multihead Attention**.

This process defines the calculation for one attention head, which is the heart of the Transformer architecture. It is this component that truly makes the Transformer architecture work.

This approach is essentially the same used in **BERT** and in almost any LLM architecture available on the market.

Nearly all rely on the **Basic Transformer Module** because, at present, there is no significantly better alternative for enabling a model to learn effectively from text.

And with that, we have successfully defined yet another class.

### **11\. Multi-Head Attention Module**

The **Multi-Head Attention** is the implementation of multi-head attention, a key component of the Transformer architecture, which is used in **BERT** and almost any LLM.

The concept behind multi-head attention is to apply the **scaled dot-product attention**, which we just created, multiple times in parallel, each with different learned weights.

This allows the model to focus on different positions and capture various types of information. In essence, researchers discovered that applying the dot-product attention multiple times, specifically in the attention layer, significantly enhanced learning effectiveness.

Now, let's create the **Multi-Head Attention** module. Refer to the detailed description in the notebook, and here is the complete code for you.

```ruby
# 38. Define the class to perform multi-head attention
class MultiHeadAttention(nn.Module):

    def __init__(self) -> None:

        # Initialize the base class
        super(MultiHeadAttention, self).__init__()

        # Define the weight matrix for the queries Q
        self.W_Q = nn.Linear(d_model, d_k * n_heads)

        # Define the weight matrix for the keys K
        self.W_K = nn.Linear(d_model, d_k * n_heads)

        # Define the weight matrix for the values V
        self.W_V = nn.Linear(d_model, d_v * n_heads)

    # Forward method to define the data pass through
    def forward(self, Q, K, V, attn_mask):

        # Save the input Q for the residual and get the batch size
        residual, batch_size = Q, Q.size(0)

        # Process Q through W_Q and reshape the result to have [n_heads] in the second dimension
        q_s = self.W_Q(Q).view(batch_size, -1, n_heads, d_k).transpose(1, 2)

        # Process K through W_K and reshape the result to have [n_heads] in the second dimension
        k_s = self.W_K(K).view(batch_size, -1, n_heads, d_k).transpose(1, 2)

        # Process V through W_V and reshape the result to have [n_heads] in the second dimension
        v_s = self.W_V(V).view(batch_size, -1, n_heads, d_v).transpose(1, 2)

        # Adapt attn_mask to be compatible with the dimensions of q_s, k_s, v_s
        attn_mask = attn_mask.unsqueeze(1).repeat(1, n_heads, 1, 1)

        # Calculate the scaled dot-product attention and context for each attention head
        context, attn = ScaledDotProductAttention()(q_s, k_s, v_s, attn_mask)

        # Reshape the context to combine the attention heads and return to the original format
        context = context.transpose(1, 2).contiguous().view(batch_size, -1, n_heads * d_v)

        # Apply a linear transformation to the combined context
        output = nn.Linear(n_heads * d_v, d_model)(context)

        # Normalize the output layer and add the residual
        return nn.LayerNorm(d_model)(output + residual), attn
```

Take another look at the **MultiHeadAttention** class, which inherits from `nn.Module`.

I use a constructor here to initialize the parent class constructor. Within this class, I define the three matrices: **Q**, **K**, and **V**.

```ruby
def __init__(self) -> None:

        # Initialize the base class
        super(MultiHeadAttention, self).__init__()

        # Define the weight matrix for the queries Q
        self.W_Q = nn.Linear(d_model, d_k * n_heads)

        # Define the weight matrix for the keys K
        self.W_K = nn.Linear(d_model, d_k * n_heads)

        # Define the weight matrix for the values V
        self.W_V = nn.Linear(d_model, d_v * n_heads)
```

The query matrix **Q**, the key matrix **K**, and the value matrix **V** form the core of what we do in the Transformer. Each of these matrices is essentially a **linear layer** in a neural network.

In other words, a simple linear layer — a basic matrix — that you will feed data into during the training process. Notice that we multiply this by the number of heads, `n_heads`, which is a hyperparameter we defined earlier. Next, I prepare the **forward** method.

```ruby
# Forward method to define the data pass through
    def forward(self, Q, K, V, attn_mask):
```

I will first retrieve the size of **Q**, which is my query matrix:

```bash
# Save the input Q for the residual and get the batch size
residual, batch_size = Q, Q.size(0)
```

After that, I will process **Q** through **WQ**, which then organizes the result to have **n\_heads**, the number of heads, in the second dimension:

```python
# Process Q through W_Q and reshape the result to have [n_heads] in the second dimension
q_s = self.W_Q(Q).view(batch_size, -1, n_heads, d_k).transpose(1, 2)

# Process K through W_K and reshape the result to have [n_heads] in the second dimension
k_s = self.W_K(K).view(batch_size, -1, n_heads, d_k).transpose(1, 2)

# Process V through W_V and reshape the result to have [n_heads] in the second dimension
v_s = self.W_V(V).view(batch_size, -1, n_heads, d_v).transpose(1, 2)
```

I then repeat the operations to process **K**, followed by **V**. All of this is simply matrix operations.

Next, I adapt the mask to make it compatible with the dimensions:

```ini
# Adapt attn_mask to be compatible with the dimensions of q_s, k_s, v_s
attn_mask = attn_mask.unsqueeze(1).repeat(1, n_heads, 1, 1)
```

I calculate the scaled dot product of the attention:

```bash
# Calculate the scaled dot-product attention and context for each attention head
context, attn = ScaledDotProductAttention()(q_s, k_s, v_s, attn_mask)
```

Exactly the attention head we created earlier. Then, we reorganize the context to combine the attention heads back into the original format.

```ini
# Reshape the context to combine the attention heads and return to the original format
context = context.transpose(1, 2).contiguous().view(batch_size, -1, n_heads * d_v)
```

We apply the linear transformation and normalize the layer.

```bash
# Apply a linear transformation to the combined context
output = nn.Linear(n_heads * d_v, d_model)(context)

# Normalize the output layer and add the residual
return nn.LayerNorm(d_model)(output + residual), attn
```

All of this takes place within the `MultiHeadAttention`. In the end, it all boils down to matrix operations. I'm not joking when I say this, alright?

Let's create the embedding object using the first module we built.

```ini
# 39. Create the Embedding object
emb = Embedding()
```

Let's generate the embeddings:

```ini
# 40. Generate the Embeddings
embeds = emb(input_ids, segment_ids)
```

I'll generate the attention mask:

```ini
# 41. Generate the attention mask
attenM = get_attn_pad_masked(input_ids, input_ids)
```

I'll generate the `MultiHeadAttention` object.

```ini
# 42. Generate the MultiHeadAttention
MHA = MultiHeadAttention()(embeds, embeds, embeds, attenM)
```

Then generate an output using the `MultiHeadAttention` object and print it:

```bash
# 43. Output
output, A = MHA

# 44. First element of the attention matrix
A[0][0]
```

![None](https://miro.medium.com/v2/resize:fit:700/1*0sYz2uPkM4s4tVwFESD53A.png)

This is the output up to the `MultiHeadAttention`, which means matrices representing the model's learning.

However, to effectively train and learn from this, we still need a few more components. We need to add the **positional feedforward layer**.

After that, we incorporate the **encoder layer**, which essentially combines all these elements. Finally, we assemble the **complete architecture**.

### 12\. Positional Feedforward Module

The next module is the **Positional Feedforward**. Module, which enables us to indicate the position of tokens within the embedding that will feed the model.

Now, we will build the class as `PoswiseFeedForward` for this module.

Once again, the notebook contains a complete description of the module, and here is the class for you:

```python
# 45. Define the class for the Positional Feed Forward Network
class PoswiseFeedForward(nn.Module):

    def __init__(self) -> None:

        # Initialize the base class
        super(PoswiseFeedForward, self).__init__()

        # First linear layer that increases the data dimension from d_model to d_ff
        self.fc1 = nn.Linear(d_model, d_ff)

        # Second linear layer that reduces the dimension back from d_ff to d_model
        self.fc2 = nn.Linear(d_ff, d_model)

    # Forward method to define the data pass through
    def forward(self, x):

        # Apply the first linear transformation, followed by the GELU activation function,
        # and then the second linear transformation
        return self.fc2(gelu(self.fc1(x)))
```

By the way, notice how another module was created using a Python class. Why? Because we usually build algorithms using the concept of **Object-Oriented Programming (OOP)**.

You first create a class, then instantiate the class as an object, and finally use its methods and attributes. This is practically a standard approach when working with machine learning, especially in Python.

Once again, we define the constructor:

```ruby
def __init__(self) -> None:
```

So, we follow the same pattern here, starting with the constructor and then initializing the base class or parent class:

```python
# Initialize the base class
super(PoswiseFeedForward, self).__init__()
```

Next, we create the first linear layer, which increases the dimension of the data:

```ini
# First linear layer that increases the data dimension from d_model to d_ff
self.fc1 = nn.Linear(d_model, d_ff)
```

Then, we create the second linear layer, which reduces the dimension back:

```ini
# Second linear layer that reduces the dimension back from d_ff to d_model
self.fc2 = nn.Linear(d_ff, d_model)
```

And all of this is to initialize the constructor. Then, we prepare the forward method to define the forward pass of the data:

```ruby
# Forward method to define the data pass through
    def forward(self, x):

# Apply the first linear transformation, followed by the GELU activation function,
# and then the second linear transformation
        return self.fc2(gelu(self.fc1(x)))
```

In this case, we use `gelu` as the activation function. Note that it takes `FC1` as input, which we defined earlier.

The `FC1`layer receives `X`, passes it through the activation function, and then feeds it into `FC2`. Finally, it returns the result to whoever calls this class. This process allows us to precisely define the positioning of the tokens within the embedding that will feed our model during training.

### **13\. Encoder Layer Module**

The **Encoder Layer module** is relatively simple because, in practice, it combines two components that we have already created: the `MultiHeadAttention` layer and the `PoswiseFeedForward`.

Below is the implementation:

```python
# 46. Define the class for the encoder layer
class EncoderLayer(nn.Module):

    def __init__(self) -> None:

        # Initialize the base class
        super(EncoderLayer, self).__init__()

        # Instantiate multi-head attention for the encoder self-attention
        self.enc_self_attn = MultiHeadAttention()

        # Instantiate the Positional Feed Forward network to use after self-attention
        self.pos_ffn = PoswiseFeedForward()

    # Forward method to define the data pass through
    def forward(self, enc_inputs, enc_self_attn_mask):

        # Apply self-attention to the input data
        enc_inputs, atnn = self.enc_self_attn(enc_inputs, enc_inputs, enc_inputs, enc_self_attn_mask)

        # After self-attention, pass the result through the Positional Feed Forward network
        enc_inputs = self.pos_ffn(enc_inputs)

        # Return the encoder output and attention weights
        return enc_inputs, atnn
```

As you can see, we have another class, the `EncoderLayer` class. It includes a constructor that first initializes the base class constructor.

Then, it initializes the `MultiHeadAttention` and the `PoswiseFeedForward`. These are objects from the respective classes, and they are being set up within the `EncoderLayer` constructor.

Now, we define the `forward` method:

```ruby
# Forward method to define the data pass through
def forward(self, enc_inputs, enc_self_attn_mask):
```

It will receive the arguments as input, including the attention module and the mask `enc_self_attn_mask`.

I will pass all of this through the first object, `enc_self_attn`, which is the `MultiHeadAttention`. This will generate the output, and this output will be fed into the positional module, `self.pos_ffn`, precisely to produce the final result.

This completes the `EncoderLayer`, which is essentially the last component of this architecture, considering the Batch architecture.

### 14\. Final Architecture of the LLM

We have reached the sixth and final module, which is the actual final architecture of the LLM, in this case, using the BERT model.

Below is the class for it:

```python
# 47. Define the BERT Model
class BERT(nn.Module):  

    def __init__(self) -> None:
        # Initialize the base class nn.Module
        super(BERT, self).__init__()

        # Embedding module for tokens, positions, and segments
        self.embedding = Embedding()

        # Encoder layers using the EncoderLayer class
        self.layers = nn.ModuleList([EncoderLayer() for _ in range(n_layers)])

        # Fully connected layer for linear transformation
        self.fc = nn.Linear(d_model, d_model)

        # Activation function Tanh
        self.activ1 = nn.Tanh()

        # Additional linear layer
        self.linear = nn.Linear(d_model, d_model)

        # Activation function GeLU
        self.activ2 = gelu

        # Layer normalization
        self.norm = nn.LayerNorm(d_model)

        # Final classification layer
        self.classifier = nn.Linear(d_model, 2)

        # Initialize the decoder and share weights with token embeddings
        embed_weight = self.embedding.tok_embed.weight
        n_vocab, n_dim = embed_weight.size()
        self.decoder = nn.Linear(n_dim, n_vocab, bias=False)
        self.decoder.weight = embed_weight

        # Initialize decoder bias
        self.decoder_bias = nn.Parameter(torch.zeros(n_vocab))

    def forward(self, input_ids, segment_ids, masked_pos):
        # Generate embeddings for input tokens and segments
        output = self.embedding(input_ids, segment_ids)

        # Generate attention mask to handle padding tokens
        enc_self_attn_mask = get_attn_pad_masked(input_ids, input_ids)

        # Pass embeddings through encoder layers
        for layer in self.layers:
            output, enc_self_attn = layer(output, enc_self_attn_mask)

        # Apply pooling to the [CLS] token representation
        h_pooled = self.activ1(self.fc(output[:, 0]))

        # Generate classification logits
        logits_clsf = self.classifier(h_pooled)

        # Expand masked positions for attention
        masked_pos = masked_pos[:, :, None].expand(-1, -1, output.size(-1))

        # Gather masked token representations
        h_masked = torch.gather(output, 1, masked_pos)

        # Apply activation and normalization to the masked tokens
        h_masked = self.norm(self.activ2(self.linear(h_masked)))

        # Decode masked token representations to logits
        logits_lm = self.decoder(h_masked) + self.decoder_bias

        # Return logits for masked language modeling and classification
        return logits_lm, logits_clsf
```

We create the class, which inherits from the `nn.Module` module in PyTorch. Then, we have the constructor method and the `forward` method defined below.

Once again, what is the purpose of the constructor? To initialize methods and attributes. I start by initializing the constructor of the base class, the parent class:

```python
def __init__(self) -> None:
        # Initialize the base class nn.Module
        super(BERT, self).__init__()
```

After that, I initialize the `Embedding` module.

Next, I create a list comprehension to generate a list of modules. For each of the layers—we'll have six—I initialize the encoder layer.

```ini
# Encoder layers using the EncoderLayer class
 self.layers = nn.ModuleList([EncoderLayer() for _ in range(n_layers)])
```

The underscore (`_`) appears because I am not interested in the return value from `n_layers`; I only need the loop.

For each value in the range, which in this case is six (as defined by the hyperparameter), I create an `EncoderLayer`. Each `EncoderLayer` combines multi-head attention with positional feedforward.

I then define the layers, following the BERT architecture: a linear layer, Tanh activation, another linear layer with GELU activation, layer normalization (`LayerNorm`), and a linear classification layer.

Afterward, I retrieve the embedding weights, vocabulary size, and dimensionality, set up the decoding linear layer with the weights, and prepare the decoder bias.

All of this initializes the constructor, which is then executed in the `forward` method:

```ruby
def forward(self, input_ids, segment_ids, masked_pos):
```

Take a look at what the `forward` method receives as input: the data, right? Specifically, `input_ids`, `segment_ids`, and `masked_pos`.

The `input_ids` represent the words, the `segment_ids` indicate the sentences or segments, and the `masked_pos` provides the positions of the masks.

All of this is provided when you feed the data batch through the embedding creation function. Then, in the `forward` method, the first step is to create the embedding using the input and segment IDs:

```ini
# Generate embeddings for input tokens and segments
output = self.embedding(input_ids, segment_ids)
```

I will then create an `output` object. For the `input_ids`, I will pass them through the function that generates the attention mask.

This will produce the output.

```ini
 # Generate attention mask to handle padding tokens
enc_self_attn_mask = get_attn_pad_masked(input_ids, input_ids)
```

I then create a loop through the layers:

```python
# Pass embeddings through encoder layers
for layer in self.layers:
    output, enc_self_attn = layer(output, enc_self_attn_mask)
```

The `layers` object represents the encoder layers, iterated through a loop six times. Each layer processes the `output`(embedding) and the attention mask with padding, generating outputs.

The result is passed through the activation function and classification module. Using the mask positions, the logits are calculated, representing predictions. These logits indicate the masked word's identity and generate the output text.

Logits, interpreted as probabilities, allow the model to predict the most likely word during text generation. **This completes the LLM architecture, demonstrating the process of building it from scratch**.

### **15\. Training and Evaluation of the LLM**

We can now train the model. Next, we instantiate the class and create an object called `model`:

```ini
# 48. Create the model
model = BERT()
```

Everything so far has relied on the `forward` method, which handles the forward pass in a neural network. Now, we need to define the backward pass, or backpropagation, to enable learning.

The `forward` method doesn't involve learning—it only executes operations to produce an output. This is simply output generation, not training.

After obtaining the model's output, we calculate the error based on the actual sentences. The model predicts by identifying the value of the masked word.

We then compute the error using a loss function, such as **Cross Entropy Loss**, commonly used in natural language processing tasks.

```ini
# 49. Loss function
criterion = nn.CrossEntropyLoss()
```

This model error is then utilized by the optimizer. Here, we are using the **ADAM** algorithm, which applies backpropagation.

This is where the actual learning occurs.

```ini
# 50. Optimizer
optimizer = optim.Adam(model.parameters(), lr=0.001)
```

Here, I am simply assembling the components. **ADAM** is the backpropagation algorithm, one of many options available, and it is responsible for enabling learning. The optimizer calculates the partial derivatives for each weight, referred to as `gradients`, which are then used to adjust the weights during the next forward pass.

Initially, in the first forward pass, random initialization is used. The model generates a prediction, the error is calculated, and the optimizer adjusts the weights for the subsequent forward pass.

In the next pass, the model produces a new prediction, ideally with reduced error. This process repeats: calculating the error, applying the optimizer, and adjusting the weights — continuing for the entire training cycle.

This method is fundamental to any artificial neural network. **LLMs** are no exception — they are artificial neural networks. The primary distinction lies in their training on enormous datasets, requiring vast amounts of data and computational resources.

This process does not produce *intelligence*; it generates outputs at high speed. While it mimics *intelligence* and aids in problem-solving, it remains a tool designed for tasks like **generating text, translating, comparing, answering questions, and so on**. Now, let's create the `optimizer`:

```ini
# 50. Optimizer
optimizer = optim.Adam(model.parameters(), lr=0.001)
```

We prepare the `data batch`:

```ini
# 51. Create a batch
batch = make_batch()
```

And here is the `data batch` that I will soon use to feed the model:

```python
# 52. Extract elements from the batch
input_ids, segment_ids, masked_tokens, masked_pos, isNext = map(torch.LongTensor, zip(*batch))
```

In the notebook, you'll find a description of each of these elements. And here, I have a training loop for you:

```python
%%time

# Start the training loop for a defined number of epochs
for epoch in range(NUM_EPOCHS):

    # Zero the gradients of the optimizer to avoid accumulation from previous epochs
    optimizer.zero_grad()

    # Pass the input data through the model and get the logits for language masking
    # and next sentence classification
    logits_lm, logits_clsf = model(input_ids, segment_ids, masked_pos)

    # Calculate the loss for the language modeling task by comparing the predicted logits
    # with the true tokens
    loss_lm = criterion(logits_lm.transpose(1,2), masked_tokens)

    # Compute the mean of the loss for normalization
    loss_lm = (loss_lm.float()).mean()

    # Calculate the loss for the next sentence classification task
    loss_clsf = criterion(logits_clsf, isNext)

    # Sum the losses from both tasks to get the total loss
    loss = loss_lm + loss_clsf

    # Display the current epoch and total loss
    print(f'Epoch: {epoch + 1} | Loss {loss:.4f}')

    # Perform backpropagation to compute the gradients
    loss.backward()

    # Update the model parameters based on the calculated gradients
    optimizer.step()
```

I will create a loop based on the number of epochs.

How many epochs did we configure? **50**. I will reset the gradients, execute the model, and feed it the data we generated earlier from the data batch.

```python
# 52. Extract elements from the batch
input_ids, segment_ids, masked_tokens, masked_pos, isNext = map(torch.LongTensor, zip(*batch))
```

I will then pass this data to the model. It will return the **logits:**

```bash
# Pass the input data through the model and get the logits for language masking
    # and next sentence classification
    logits_lm, logits_clsf = model(input_ids, segment_ids, masked_pos)
```

I will then take these **logits**, which are the model's predictions, and compare them with the actual values by calculating the loss function.

Notice that I have the masked tokens:

```ini
# Calculate the loss for the language modeling task by comparing the predicted 
# logits with the true tokens
    loss_lm = criterion(logits_lm.transpose(1,2), masked_tokens)
```

I will compare these masked tokens with the **logits**, which are the model's predictions. This means comparing the actual values with the predictions. This process generates the error, and I calculate the average error.

Next, I compute the loss for the next sentence classification task and then sum up the losses.

```ini
# Sum the losses from both tasks to get the total loss
    loss = loss_lm + loss_clsf
```

And I will display the loss for each epoch.

Once the error has been calculated, you simply call the `backward` method, which initiates the **backpropagation** process.

```bash
# Perform backpropagation to compute the gradients
loss.backward()
```

This allows you to optimize each step by updating the weights based on the model's error. This is where **backpropagation** performs its learning task.

From everything we've built so far, the actual learning happens right here at the very end.

```bash
# Perform backpropagation to compute the gradients
loss.backward()

# Update the model parameters based on the calculated gradients
optimizer.step()
```

This is where **machine learning** truly takes place. Everything we've done so far has been to enable the model to make predictions, calculate the error, and feed it back into **backpropagation** for weight adjustments.

Now, I'll start the training process, which will run for 50 epochs in total. Don't expect a highly accurate model — we're working with only 10 input sentences. As a result, you'll notice the model starts with a high error rate.

![None](https://miro.medium.com/v2/resize:fit:700/1*mATClyDjYkb-zum_15w_GA.png)

Then, the error might even increase at times. However, over time, it decreases and stabilizes. This stability happens because the dataset is very small.

Overall, the model is reducing the error, which is exactly what we aim for. Despite fluctuations, the model is following the learning process — learning how to generate text based on its training and predictions of masked words.

This is the core functionality of the **BERT architecture**.

### 16\. Extracting Predictions from the Trained LLM

Initially, the error started high, at **92**, increased slightly, and then began to decrease steadily until it reached **13**. The lower the error, the better.

This clearly demonstrates that the model is learning, meaning the architecture works. The model manages to learn patterns in the data sufficiently to predict the next token.

Of course, don't expect exceptional precision — this isn't what you'll achieve here. After all, we only have **10 input sentences**.

However, the model was successfully trained. I've also gone ahead and executed the final cells. At this point, I'm extracting the batch of data:

```python
# 53. Extract the batch
input_ids, segment_ids, masked_tokens, masked_pos, isNext = map(torch.LongTensor, zip(batch[0]))
print(text_data)
print([number_dict[w.item()] for w in input_ids[0] if number_dict[w.item()] != '[PAD]'])
```

![None](https://miro.medium.com/v2/resize:fit:700/1*KWKxNWMq6nmdMDNfZcl4RQ.png)

The dataset is small, so I will extract only the batch of data here. We extract the **predictions** for the tokens:

```perl
# 54. Extract predictions of the tokens
logits_lm, logits_clsf = model(input_ids, segment_ids, masked_pos)
logits_lm = logits_lm.data.max(2)[1][0].data.numpy()
print('List of Real Masked Tokens: ', [pos.item() for pos in masked_tokens[0] if pos.item() != 0])
print('List of Predicted Masked Tokens: ', [pos for pos in logits_lm if pos != 0])
```

![None](https://miro.medium.com/v2/resize:fit:700/1*h-ZNJsiZDjndnhKl3S34-w.png)

So, observe the list of **real tokens**. In this case, these are the values corresponding to the vocabulary. Our model predicted empty results.

The actual values were `10`, `39`, `31`, and `56`. Naturally, our model made mistakes—don't expect high accuracy.

Now, regarding the **token prediction**:

```python
# 55. Extract predictions of the next token
logits_clsf = logits_clsf.data.max(1)[1].data.numpy()[0]
print('isNext (True Value): ', True if isNext else False)
print('isNext (Predicted Value): ', True if logits_clsf else False)
```

![None](https://miro.medium.com/v2/resize:fit:700/1*v5vqvyogyGy8fMtDQPw46A.png)

The actual value was **true**, but the model predicted **false**. Once again, the model made a mistake.

If you run this process multiple times, the model will eventually get the token right at some point and make mistakes at others. It fails more often than it succeeds, primarily due to the extremely low data volume.

Our goal here was not to create a highly accurate model. Instead, the focus was on **building the architecture of an LLM from scratch**, and that goal was successfully achieved.

### **Conclusion**

How many people in the world have the technical knowledge to create an LLM architecture from scratch? *Very few*, right? Well, now you are one of them. You've become someone capable of designing an entire LLM, from concept to practical implementation.

In this journey, I've shown you the entire process. You've learned the foundational structure behind most models: **the Transformer architecture**.

We covered how to build the embedding module, encoder layer, decoder, attention module, and even multiple attention heads. Combining these components is like solving a puzzle that forms the core of an LLM.

However, *the architecture is just the shell*: the true power of an LLM lies in training it with massive, well-prepared datasets, transforming its potential into **real generative intelligence**.

Together, we went through every step:

1. We loaded the data and performed preprocessing.
2. Defined hyperparameters and created functions to handle batches.
3. Built each module of the architecture, with clear explanations and commented code.
4. Assembled the complete LLM architecture, integrating all components.
5. Ran the training loop, validated predictions, and evaluated the model's performance.

Although the limited data volume didn't allow for high performance, the focus was entirely didactic: *to demonstrate how everything connects*. With this knowledge, you can now consult papers like **BERT's** and easily understand the described operations, recognizing them directly in the code.

Training an LLM from scratch is a fantastic way to learn, but it's rarely a practical necessity. With so many **open-source**options available, it's often more efficient to use them for commercial applications. However, you now have the tools to go beyond: create, adapt, and refine models to meet your specific needs.

In the next tutorial, we'll explore how to integrate a pre-trained LLM into real-world applications. Thank you for following along! 🐼❤️

All images, content, and text by **Leo Anello.**

#### Bibliography & Useful Links

1. [Project Repository](https://github.com/Anello92/LLM-From-Scratch/tree/main)
2. [BERT Research Paper](https://arxiv.org/abs/1810.04805)
3. [PyTorch Documentation](https://pytorch.org/docs/)
4. [Hugging Face Transformers](https://huggingface.co/transformers/)