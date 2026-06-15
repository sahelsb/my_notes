
### Language as a Bag-of-words

- **Tokenization**:
    - Process of splitting sentences into individual words or subwords (tokens).    
    - Most common method: splitting on whitespace.
        
- **Vocabulary creation**:
    - Combine all unique words from sentences to form a vocabulary.
        
- **Representation**:
    - Count how often each word appears in each sentence.
    - Produces a "bag of words" (numerical vector representation).
    - These vectors represent sentences/documents in numeric form.
        
- **Limitation**:
    - Bag-of-words captures word counts but does not capture **meaning** or **semantic relationships**.

![alt text](overview.png)

### Better representations

- **Embeddings**:
    - Vector representations of words that aim to capture **meaning**.
    - Word2vec was an early successful method (trained on large corpora like Wikipedia).
        
- **Training process**:
    - Every word in the vocabulary is initially assigned a vector embedding (e.g., 50 values, random initialization).
    - Training uses pairs of words from text and predicts whether they are likely to be neighbors in a sentence.
    - Model adjusts embeddings so that words with similar contexts have **closer embeddings**.
        
- **Semantic representation**:
    - Embeddings capture word properties (e.g., _baby_ → high on "newborn" & "human"; _apple_ → low on those).
    - These properties allow computers to understand and process meaning.
        
- **Applications**:
    - Enable measurement of **semantic similarity** between words using distance metrics.
    - Visualizing embeddings in 2D shows similar words clustering together.


![[embeddings.png]]

#### Comparison: Bag-of-Words vs. Word2Vec

- **Bag-of-Words**:
    - Embeddings at the **document/sentence level** (counts of words).
    - Captures frequency but not meaning.
        
- **Word2Vec**:
    - Embeddings at the **word level**.
    - Captures semantic similarity and contextual meaning.
    - Basis for more advanced embeddings (token embeddings, sentence embeddings, etc.).


### Encoding and Decoding Context with Attention

- **Limitation of Word2Vec**
    - Word2Vec creates **static embeddings**: each word has the same vector regardless of context.
    - Example: _bank_ → same embedding whether it means _financial institution_ or _river bank_.
    - Context is not captured.
        
### Recurrent Neural Networks (RNNs)

- Designed to handle **sequences** as input.
- Applied to **two tasks**:
    - **Encoding**: Representing an input sentence.
    - **Decoding**: Generating an output sentence.
- Example: Translating _“I love llamas”_ → Dutch _“Ik hou van lama’s”

- **Autoregressive nature**:
    - Each next word is generated using all previously generated words.
        
### Encoding Process with RNNs

- Input words are first represented using embeddings (e.g., word2vec).
- Processed **sequentially** (one word at a time).
- Generates a **context embedding** representing the entire input sequence.
- **Limitation**: A single context vector struggles with long sentences.

![[autoregressive.png]]
### Attention Mechanism (introduced 2014)

- Solves the problem of compressing long sentences into one embedding.
- **Key idea**: Model can **“attend”** to specific parts of the input sequence that are most relevant to the output.
    - Example: When translating _“llamas”_ → _“lama’s”_, attention between those words is high.
    - _“I”_ and _“lama’s”_ → low attention.
        
- **Effect**:
    - Decoder does not rely on one context embedding.
    - Instead, it uses the **hidden states of all input words** with attention weights.
    - Enables richer context representation during generation.

![[attention.png]]
### Example: Translation with Attention

- Step-by-step for _“Ik hou van lama’s”_:
    - After generating _“Ik”_, _“hou”_, and _“van”_, attention focuses strongly on _“llamas”_ before producing _“lama’s”_.
    - The decoder dynamically attends to relevant words in the source sentence.
        
### Benefits vs. Limitations

- **Benefits**:
    - Captures **sequential nature** of text.
    - Embeddings are **context-aware** through attention.
    - Improves translation and sequence modeling compared to word2vec.
        
- **Limitations**:
    - Sequential processing in RNNs prevents **parallelization** during training → slower than later architectures (e.g., Transformers).

![[attend.png]]


### Attention Is All You Need (2017)

- Introduced the **Transformer architecture** (no recurrence, only attention).
- Key advantage:
    - Unlike RNNs, Transformers can be **trained in parallel**, greatly speeding up training.
        
- Still **autoregressive**: generates one token at a time, each depending on previously generated tokens.
    

### Architecture Overview

- Transformer consists of **stacked Encoder and Decoder blocks** 
- Both encoder and decoder revolve around **attention**, not RNNs.

### Encoder Block

- Two main components :
    1. **Self-Attention**
        - Each token attends to all other tokens in the same sequence.
        - Captures relationships across the entire input 
        - Processes the **whole sequence at once** (not one token at a time).
            
    2. **Feedforward Neural Network**
        - Further processes intermediate representations from self-attention.

### Decoder Block

- Similar to the encoder but with an extra layer:
    1. **Self-Attention**
        - Masks **future positions** to avoid “looking ahead” 
        - Ensures autoregressive generation (only attends to earlier tokens).
            
    2. **Encoder-Decoder Attention**
        - Attends to the encoder’s output 
        - Selects relevant parts of the input sequence for generating each output token.
            
    3. **Feedforward Neural Network**
        - Same as in the encoder.

![[decoder.png]]

![[masked.png]]
        
### Key Features & Impact

- Transformer architecture = **self-attention + encoder-decoder attention + feedforward layers**.
- Foundation for major models in NLP: **BERT, GPT-1, GPT-2, GPT-3, GPT-4, etc.**
- Enables:
    - Better **contextual understanding**.
    - Much faster and more efficient training compared to RNNs.


### Representation Models: Encoder-Only Models

- **Background**
    - Original Transformer = **encoder-decoder architecture**, ideal for translation.
    - Limitation: Not as effective for other tasks (e.g., text classification).
        
### BERT (2018)

- **Name**: **Bidirectional Encoder Representations from Transformers**.
- **Architecture**:
    - **Encoder-only** (decoder removed).
    - Stack of encoder blocks (e.g., 12 in BERT base).
    - Each block = **self-attention + feedforward neural network**.
        
- **Special token**:
    - **[CLS] token** → added to input sequence.
    - Acts as the **representation of the entire input**.
    - Often used as the embedding for fine-tuning tasks (e.g., classification).

### Training BERT

- Uses **Masked Language Modeling (MLM)**:
    - Randomly mask parts of input and train model to predict them.
    - Encourages model to learn **contextual representations**.
- Produces **accurate, contextual embeddings**.

### Fine-Tuning and Transfer Learning

- Pretraining (e.g., on **Wikipedia**) → model learns semantics & context.
- Fine-tuning:
    - Apply pretrained BERT to a specific task (e.g., classification).
    - Requires **less compute & less data** than training from scratch.
- Benefit:
    - BERT generates embeddings at multiple layers.
    - Can be used for **feature extraction** without fine-tuning.

### Applications of Encoder-Only Models (BERT-like)

- **Classification** 
- **Clustering** 
- **Semantic search** 
- General role: **Representation models** (create embeddings, not generate text).
    
### Representation vs. Generative Models

- **Representation models (encoder-only, teal, vector icon)**:
    - Focus: Representing language → embeddings.
    - Do **not** generate text.
    - Example: BERT.
        
- **Generative models (decoder-only, pink, chat icon)**
    - Focus: **Text generation**.
    - Typically not designed to produce embeddings.
    - Example: GPT.

![[bert.png]]


### Generative Models: Decoder-Only (GPT Family)

- **Architecture**
    - Proposed in **2018**: **Generative Pre-trained Transformer (GPT-1)**.
    - **Decoder-only** → stacks decoder blocks (no encoder).
    - Designed for **generative tasks** (text generation, completion).

### GPT-1 (2018)

- Trained on:
    - **7,000 books**.
    - **Common Crawl** (large dataset of web pages).
- Size: **117 million parameters**
- Parameters = numerical values representing model’s language knowledge.

### Scaling Up GPT

- Growth trend: More parameters → better performance.
- **GPT-2 (2019)** → **1.5 billion parameters**.
- **GPT-3 (2020)** → **175 billion parameters**.
- Illustrated rapid growth in **LLMs (Large Language Models)**.

### LLMs (Large Language Models)

- **Definition**: Generative decoder-only models (but term _LLM_ also used for large encoder-only models).
- Core behavior: **sequence-to-sequence completion**.
    - Input some text → model predicts next words (autocomplete).
- Extended via fine-tuning:
    - From text completion → to **chatbots / instruction-following models**.
    - Can **answer questions, follow prompts, and generate coherent responses**.

### Completion Models

- Generative LLMs = **completion models**.
- Input = **prompt**, output = **completion** 
- Instruction-tuned versions → better at Q&A and following directions.

### Context Length / Context Window

- Definition: **Maximum number of tokens a model can process at once** 
- Importance:
    - Larger context windows → can process longer texts or even entire documents.
- Limitation:
    - Autoregressive nature → context length **grows with generated tokens**, increasing memory/computation needs.

![[Pasted image 20250823172704.png]]


### The Year of Generative AI

- **Impact of LLMs in 2023**
    - 2023 widely called _The Year of Generative AI_ due to release, adoption, and media coverage of **ChatGPT (GPT-3.5)**.
    - _ChatGPT_ refers to the **product**, not the underlying model.
    - Initially powered by **GPT-3.5**, later expanded to include more performant variants such as **GPT-4**.
        
- **Other LLMs in 2023**
    - Not only GPT-3.5, but also many **open source and proprietary LLMs** emerged rapidly.
    - Open-source base models = **foundation models**, often fine-tuned for tasks (e.g., instruction following).
    
- **Architectural Developments**
    - Besides Transformers, new architectures appeared:
        - **Mamba**
        - **RWKV**
    - Aim: Transformer-level performance with advantages such as
        - Larger context windows
        - Faster inference

### The Moving Definition of a “Large Language Model”

- **Current Understanding**
    - Typically refers to **generative decoder-only Transformer models**.
        
- **Issues with Definition**
    - Example: A GPT-3–level model, but **10× smaller** → excluded as “large”?
    - Example: A GPT-4–sized model doing **accurate text classification without generation** → does it qualify?
    - Problem: Definitions risk **excluding capable models**.
        
- **Evolving Definition**
    - “Large” is **arbitrary** — what is large today may be small tomorrow.
    - Multiple names exist for the same concept.
        - “Large language models” include models that **do not generate text**.
        - They can also run on **consumer hardware**.


![[Pasted image 20250823234106.png]]

### The Training Paradigm of Large Language Models

- **Traditional Machine Learning**
    - One-step process: train a model for a specific task (e.g., classification, regression).
        
- **LLM Training (Multistep Approach)**
    1. **Pretraining (Language Modeling)**
        - First and most resource-intensive step.
        - Train on a vast corpus of internet text.
        - Learns grammar, context, and patterns of language.
        - Goal: predict the next word.
        - Result: **foundation model / base model** (not instruction-following).
            
    2. **Fine-tuning (Post-training)**
        - Narrower training on specific tasks or behaviors.
        - Examples: classification, instruction-following.
        - Saves resources since only the base model needs costly pretraining.
        - Example: **Llama 2** → trained on **2 trillion tokens** (huge compute).
        - Fine-tuning allows customization for your dataset


### Large Language Model Applications: Why They’re Useful

- **Wide Range of Tasks**
    - Text generation + prompting → flexibility makes LLMs very powerful.
        
- **Examples of Applications**
    - **Sentiment Analysis (Supervised Classification)**
        - Detect if a customer review is positive/negative.
        - Can use encoder-only or decoder-only models.
        - Options: pretrained or fine-tuned models 
            
    - **Topic Modeling (Unsupervised Classification)**
        - Identify common themes in ticket issues (no predefined labels).
        - Encoder-only models → perform classification.
        - Decoder-only models → label the topics 
            
    - **Document Retrieval & Inspection**
        - Use semantic search to let LLMs access external information.
        - Can be improved by fine-tuning a custom embedding model 
            
    - **LLM Chatbot with External Resources**
        - Combines multiple techniques:
            - Prompt engineering 
            - Retrieval-Augmented Generation (RAG) 
            - Fine-tuning 
        - Example: chatbot that uses tools/documents.
            
    - **Multimodal LLMs (Text + Vision)**
        - Example: generate recipes from a fridge photo.
        - LLM processes both text and images 
        - Expands use cases into Vision and beyond.


### Limited Resources Are All You Need

- **Compute Resources & GPUs**
    - Training/using LLMs depends heavily on GPU availability.
    - Key factor: **VRAM (video memory)** → more is better.
    - Insufficient VRAM = some models can’t be run at all.
        
- **GPU-Poor vs. GPU-Rich**
    - Those without powerful GPUs are called the **GPU-poor**.
    - Training/fine-tuning LLMs is **expensive** in compute.
    - Example: Meta’s **Llama 2** trained on **A100-80GB GPUs**.
        - Renting one A100 GPU = ~$1.50/hr.
        - Total cost to train model = **$5M+**.
            
- **No Universal VRAM Requirement**
    - Depends on: model architecture, size, compression, context length, backend, etc.


### Interfacing with Large Language Models

- **Importance**
    - Interfacing = key for both **using LLMs** and **understanding inner workings**.
    - Many new **techniques, methods, and packages** for this.

#### Proprietary (Closed Source) Models

- **Definition**
    - Models with weights + architecture **not shared**.
    - Developed by companies, details kept secret.
    - Examples: **OpenAI’s GPT-4**, **Anthropic’s Claude**.
        
- **Access**
    - Through **API** (e.g., OpenAI Python package).
        
- **Advantages**
    - No need for strong GPU → provider hosts & runs model.
    - Easy to use (no setup expertise required).
    - Often **more performant** due to large commercial investment.
        
- **Disadvantages**
    - **Costly** (paid service).
    - Cannot fine-tune yourself.
    - Data shared with provider → privacy issues (e.g., patient data).
    
#### Open Models

- **Definition**
    - Models that share weights + architecture publicly.
    - Developed by organizations, code sometimes shared.
    - Examples: **Cohere Command R**, **Mistral**, **Microsoft Phi**, **Meta Llama**.
        
- **Licensing Issues**
    - Some have **restricted commercial use** → debate on what counts as “open source.”
    - Training data + full source code often **not shared**.
        
- **Usage**
    - Download + run locally
    - Requires **powerful GPU**.
        
- **Advantages**
    - Full **control** over model.
    - Can run sensitive data safely.
    - Can **fine-tune locally**.
    - **Transparent** process (weights + architecture visible).
    - Strong community support (e.g., Hugging Face).
        
- **Disadvantages**
    - Needs **powerful hardware** (especially for training).
    - Requires **technical knowledge** for setup + usage.



### Open vs Closed Source

- **Closed-source LLMs** (e.g., ChatGPT) → easy to use, minimal setup.
- **Open-source LLMs** → require packages/frameworks to run locally.
- Many new frameworks released in 2023
    

### Goal

- Goal: build **intuition + core knowledge** → easy to adopt any new framework.
- Focus: **backend frameworks (code, no GUI)** like:
    - `llama.cpp`
    - `LangChain`
    - `Hugging Face Transformers`

##### GUI Alternatives (local ChatGPT-like apps)

- **text-generation-webui**
- **KoboldCpp**
- **LM Studio**


### Hugging Face Hub

- Main source for open-source models.
- > 800,000 models (LLMs, vision, audio, tabular).
- Hugging Face = org behind **Transformers** library.

##### Example Model: Phi-3-mini

- **3.8B parameters**, small but performant.
- Runs on <8 GB VRAM (even <6 GB with quantization).
- **MIT license** → free for commercial use.



### Using an LLM – Two Components

1. **Model** (generative backbone).
2. **Tokenizer** (splits text into tokens & decodes output).



### In code : 
#### 1. Load model + tokenizer:

```python
from transformers import AutoModelForCausalLM, AutoTokenizer

model = AutoModelForCausalLM.from_pretrained(
    "microsoft/Phi-3-mini-4k-instruct",
    device_map="cuda",
    torch_dtype="auto",
    trust_remote_code=True
)
tokenizer = AutoTokenizer.from_pretrained("microsoft/Phi-3-mini-4k-instruct")

```

#### 2. Simplify with pipelines

```python
from transformers import pipeline

generator = pipeline(
    "text-generation",
    model=model,
    tokenizer=tokenizer,
    return_full_text=False,
    max_new_tokens=500,
    do_sample=False
)
messages = [{"role": "user", "content": "Create a funny joke about chickens."}]
output = generator(messages)
print(output[0]["generated_text"])
```

##### Important Parameters

- **return_full_text=False** → only model output, not prompt.
- **max_new_tokens=500** → limit length of generation.
- **do_sample=False** → deterministic (greedy decoding).
    - (If True → sampling adds randomness/creativity).



### LLM Tokenization

A model actually generates one token at a time. But tokens aren’t only the output of a model, they’re also the way in which the model sees its inputs. A text prompt sent to the model is first broken down into tokens through a tokenizer. 
You can find an example showing the tokenizer of GPT-4 on the [OpenAI Platform](https://platform.openai.com/tokenizer)


Here we’ll be downloading an LLM and seeing how to tokenize the input before
generating text with the LLM.

``` python
from transformers import AutoModelForCausalLM, AutoTokenizer
# Load model and tokenizer
model = AutoModelForCausalLM.from_pretrained(
"microsoft/Phi-3-mini-4k-instruct",
device_map="cuda",
torch_dtype="auto",
trust_remote_code=True,
)

tokenizer = AutoTokenizer.from_pretrained("microsoft/Phi-3-mini-
4k-instruct")
```

We can then proceed to the actual generation.

```python
prompt = "Write an email apologizing to Sarah for the tragic
gardening mishap. Explain how it happened.<|assistant|>"
# Tokenize the input prompt
input_ids = tokenizer(prompt,
return_tensors="pt").input_ids.to("cuda")
# Generate the text
generation_output = model.generate(
input_ids=input_ids,
max_new_tokens=20
)
# Print the output
print(tokenizer.decode(generation_output[0]))
```

Output:
```
<s> Write an email apologizing to Sarah for the tragic
gardening mishap. Explain how it happened.<|assistant|> Subject:
**My Sincere Apologies for the Gardening Mishap
Dear**
```

The text in ** ** is the 20 tokens generated by the model.
The code shows that the model doesn’t get the raw text prompt directly; instead, the tokenizer converts the prompt into `input_ids`, which the model then uses as input.

Let’s print **input_ids** :
```
tensor([[ 1, 14350, 385, 4876, 27746, 5281, 304, 19235, 363,
278, 25305, 293, 16423, 292, 286, 728, 481, 29889, 12027, 7420,
920, 372, 9559, 29889, 32001]], device='cuda:0')
```

This reveals the inputs that LLMs respond to, a series of integers as shown. Each one is the unique ID for a specific token (character, word, or part of a word).

![[tokenization.png]]

Notice the following:
- The first token is ID 1 (`<s>`), a special token indicating the beginning of the text.
- Some tokens are complete words (e.g., Write, an, email).
- Some tokens are parts of words (e.g., apolog, izing, trag, ic).
- Punctuation characters are their own token.

Notice how the space character does not have its own token. Instead, partial
tokens (like “izing” and “ic”) have a special hidden character at their
beginning that indicates that they’re connected with the token that precedes
them in the text.



