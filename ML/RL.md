## Representation Learning Fundamentals

is a process that simplifies raw data into understandable patterns for machine learning. It enhances interpretability, uncovers hidden features, and aids in transfer learning. Data in its raw form (words and letters in text, pixels in images) is too complex for machines to process directly. Representation learning transforms the data into a representation that machines can use for classification or predictions.

## History of Representation Learning

Representation Learning has evolved significantly over time. Breakthroughs such as Hinton et al.'s work in 2006 propelled the field towards deep learning architectures, replacing traditional manual feature engineering with automated feature extraction methods.

- **Traditional Techniques (Pre-2000):**
  - **Linear Methods**\
  Principal Component Analysis (PCA): Focuses on capturing overall data variance for dimensionality reduction.\
   Linear Discriminant Analysis (LDA): Emphasizes maximizing separation between classes in the low-dimensional space.

  - **Kernel Methods**\
   Kernel PCA for nonlinear data projection: Researchers created techniques like Kernel PCA to manage non-linear data by projecting it into a higher-dimensional space before applying linear methods.

- **Manifold Learning (2000’s):**
  - Emerged to discover intrinsic low-dimensional structures within high-dimensional data.

- **Deep Learning Era (2006 onwards):**
  - Introduction of deep neural networks enabled hierarchical representation learning.
  - Models like CNNs, RNNs, Autoencoders, and Transformers exemplify deep learning's impact.

## Characteristics of a Good Representation

A good representation:
- **Information:** Encodes important features compactly.
- **Compactness:** Efficient storage with essential information preserved.
- **Generalization (Transfer Learning):** The aim is to learn versatile representations for transfer learning, starting with a pre-trained model (computer vision models are often trained on ImageNet first) and then fine-tuning it for specific tasks requiring less data.

## Deep Learning Models for Representation Learning
**Deep Neural Networks are representation learning models.** They encode the input information into hierarchical representations and project it into various subspaces. These subspaces then go through a linear classifier that performs classification operations.

### Supervised Learning 
You can think of supervised learning as a classroom where a student is taught by a teacher with many examples (annotated/ labeled data). For e.g. object classification.

### Unsupervised Learning
used to find implicit patterns in the data without being explicitly trained on labeled data. Unlike supervised learning, it does not require annotations.

### Semi-supervised Learning
we have input data, and a fraction of input data is labeled as the output. Semi-supervised learning can be useful in cases where we have a small number of labeled data points to train the model. The training process can use a small chunk of labeled data and pseudo-label the rest of the dataset.

### Reinforcement Learning
Reinforcement learning is a method used to train AI agents to learn environment behavior in specific contexts using reward feedback policy.
For example: Think of it as a child who is trying to win a stage in a game.

### Self-supervised Learning
the model trains itself to learn one part of the input from another part of the input. It is also known as predictive or pretext learning. 

In this process, the unsupervised problem is transformed into a supervised problem by auto-generating the labels. To make use of the huge quantity of unlabeled data, it is crucial to set the right learning objectives to get supervision from the data itself.

The process of the self-supervised learning method is to identify any hidden part of the input from any unhidden part of the input.

For example, in natural language processing, if we have a few words, using self-supervised learning we can complete the rest of the sentence. Similarly, in a video, we can predict past or future frames based on available video data. **Self-supervised learning uses the structure of the data to make use of a variety of supervisory signals across large data sets** – all without relying on labels.

- Self-supervised is related to transfer learning. Suppose we are interested in training an image classifier to classify bird species. In transfer learning we would pretrain a convolutional neural network on ImageNet. After pretraining on the general ImageNet dataset, we would take the pretrained model and train it on the smaller, more specific target dataset that contains the bird species of interest.

	![](./images/self-supervised-transfer.png)

- Self-supervised learning is an alternative approach to transfer learning where we don’t pretrain the model on labeled but _unlabeled_ data. We consider an unlabeled dataset for which we do not have label information. We then find a way to obtain labels from the dataset’s structure to formulate a prediction task for the neural network. These self-supervised training tasks are also called _pretext tasks_.
	Such a self-supervised learning task could be a “missing-word” prediction in a natural language processing context. For example, given the sentence “It is beautiful and sunny outside,” we can mask out the word “sunny,” feed the network the input It is beautiful and [MASK] outside,” and have the network predict the missing word in the “[MASK]” location. Similarly, we could remove image patches in a computer vision context and have the neural network fill in the blanks. Note that these are just two examples of self-supervised learning tasks. Many more methods and paradigms for self-supervised learning exist.

	![](./images/self-supervised-1.png)

	**In sum, we can think of self-supervised learning on the pretext task as representation learning. We can then take the pretrained model to finetune it on the target task (also known as the _downstream_ task).**
	self-supervised learning is likely useful if we work with large neural networks and we only have a limited amount of labeled training data.
	
An easier way to put it is that the ‘unsupervised’ learning technique focuses a lot on the model and not on the data whereas the ‘self-supervised learning’ technique works the other way around. However, unsupervised learning methods are good at clustering, and dimensionality reduction, while self-supervised learning is a pretext method for regression and classification tasks.

### Knowledge Distillation


### Supervised Learning

- **Convolutional Neural Networks (CNNs)**:
	a class of supervised learning models that are highly effective in processing grid-like structured data (images). A CNN captures the spatial and temporal dependencies in an image through the application of learnable filters or kernels. The key components of CNNs include: 
	**Convolutional Layers**: These layers apply filters to the input to create feature maps, highlighting important features like edges and shapes. 
	**Pooling Layers**: Follow convolutional layers to reduce the dimensionality of the feature maps, making the model more efficient by retaining only the most essential information.
	**Fully Connected Layers**: At the end of the network, these layers classify the image based on the features extracted by the convolutional and pooling layers.  
	CNNs are good at learning hierarchical feature representations in images. **Lower layers learn to detect edges, colors, and textures, while deeper layers identify more complex structures like parts of objects or entire objects themselves.** This hierarchical learning approach is highly effective for tasks requiring the recognition of complex patterns and objects within images.
	**CNNs provide translation invariance.** This means, that even if an object moves around in an image, or the image is rotated, or skewed, it can still recognize the image. Moreover, the learned filters incorporate large number parameter sharing, allowing for dense and reduced size representation.

- **Recurrent Neural Networks (RNNs):**
	Recurrent Neural Networks (RNNs) and their variants, including Long Short-Term Memory (LSTM) networks and Gated Recurrent Units (GRUs), **specialize in processing sequential data**, making them highly suitable for tasks in natural language processing and time series analysis.
	**core idea behind RNNs is their ability to maintain a memory of previous inputs in their internal state, which influences the processing of current and future inputs, allowing them to capture temporal dependencies.** 
	**RNNs** possess a simple structure where the output from the previous step is fed back into the network as input for the current step, creating a loop that allows information to persist. **However, they suffer from exploding and vanishing gradients.** 
	**LSTMs** are an advanced variant of RNN. They introduce a complex architecture with a memory cell and three gates (input, forget, and output gates). **These components work together to regulate the flow of information, deciding what to retain in memory, what to discard, and what to output.** **Which solves the exploding and vanishing gradients problem.**
	**GRUs simplify the LSTM design by combining the input and forget gates into a single “update gate” and merging the cell state and hidden state.** 
	**However, RNNs, LSTMs, and GRUs learn to capture temporal dependencies by adjusting their weights by backpropagation through time (BPTT)**, a variant of the standard backpropagation algorithm adapted for sequential data. By doing so, these networks learn complex patterns in the data, such as the grammatical structure in a sentence or trends in a time series, effectively capturing both short-term and long-term dependencies.  

### Unsupervised Learning

- **Autoencoders:**
	**Learn compressed representations of data without labels, useful for dimensionality reduction and feature learning**.
	as unsupervised feature learning models, **learn encodings of unlabeled data**, usually for dimensionality reduction or feature learning. Essentially, **they aim to reconstruct input data from the constructed representation.**
	Autoencoders have two parts, encoder and decoder. 
    **Encoder**: The encoder compresses the input into a latent-space representation. It learns to reduce the dimensionality of the input data, **capturing its most important features in a compressed form.**
	**Decoder**: The decoder takes the encoded data and tries to recreate the original input. The reconstruction might not be perfect but with training, **the decoder learns to produce output significantly similar to the input.**  
	
	Auto-encoders learn to create dense and useful representations of data by **forcing the network to prioritize important aspects of the input data**. These learned representations can be later used for various other tasks.


- **Variational Autoencoders (VAEs):**
	**Probabilistic approach to autoencoders**, capturing data distribution in latent space.
    They are a unique kind of autoencoder that compresses data probabilistically, unlike regular autoencoders. **Instead of converting an input (e.g. an image) into a single compressed form, VAEs transform it into a spectrum of possibilities within the latent space,** often **represented by a multivariate Gaussian distribution.**


- **Generative Adversarial Networks (GANs):**
	introduced by Ian Goodfellow and colleagues in 2014, are a type of artificial intelligence algorithm used in unsupervised machine learning. **They involve two neural networks**: 
	**the generator, which aims to create data resembling real data**, **and the discriminator, which tries to differentiate between real and generated data**. These networks are trained together in a competitive game-like process. 
	Generator: **The generator network takes random noise as input and generates samples that resemble the distribution of the real data**. **Its goal is to produce data so convincing that the discriminator cannot tell it apart from actual data**. 
	Discriminator: **The discriminator network is a classifier that tries to distinguish between real data and fake data produced by the generator**. **It is trained on a mixture of real data and the fake data generated by the generator, learning to make this distinction**.

- **Transformers:**
	Transformers have revolutionized natural language processing (NLP), offering significant improvements over previous models like RNNs and LSTMs for tasks like text translation, sentiment analysis, and question-answering. 
	**The core innovation of the Transformer is the self-attention mechanism**, **which allows the model to weigh the importance of different parts of the input data differently, enabling it to learn complex representations of sequential data.** 
	A Transformer model is composed of an encoder and a decoder, each consisting of a stack of identical layers. 
	Encoder: Processes the input data (e.g., a sentence) and transforms it into a continuous representation that holds the learned information of that input. 
	Decoder: Takes the encoder’s output and generates the final output sequence, step by step, using the encoder’s representation and what it has produced so far. Both the encoder and decoder are made up of multiple layers that include self-attention mechanisms. 
	**Self-Attention is the ability of the model to associate each word in the input sequence with every other word to better understand the context and relationships within the data.** **It calculates the attention scores, indicating how much focus to put on other parts of the input sequence when processing a specific part.** 
	**Unlike sequential models like RNNs, the Transformer treats input data as a whole, allowing it to capture context from both directions** (left and right of each word in NLP tasks) simultaneously. This leads to more nuanced and contextually rich representations.

- **Graph Neural Networks (GNNs):**
    Learn node and edge representations in graph data, incorporating both local and global structural information.

- **Transfer Learning** :
	**In transfer learning, you first train a model on a very large and comprehensive dataset**. This initial training **allows the model to learn a rich representation of features, weights, and biases.** **Then, you use this learned representation as a starting point for a second model, which may not have as much training data available.** 
	For instance, in the field of computer vision, **models often undergo pre-training on the ImageNet dataset, which includes over a million annotated images. This process helps the model to learn rich features.** 
	Furthermore, **after this pre-training phase, you can fine-tune the model on a smaller, task-specific dataset.** **During this fine-tuning phase, the model adapts the general features it learned during pre-training to the specifics of the new task.**


- **Zero-Shot Learning** (ZSL):

- ZSL involves training AI models to recognize and categorize objects or concepts **without prior exposure to examples** of those categories during training.
- **Unlike traditional supervised learning, where models rely on labeled data for training**, **ZSL leverages auxiliary information to make predictions for unseen classes.**
- **This auxiliary information can include textual descriptions, attributes, embedded representations, or semantic information relevant to the task at hand**.
- ZSL methods typically **output a probability vector representing the likelihood that a given input belongs to certain classes**, rather than directly modeling decision boundaries between classes.
- One significant advantage of ZSL is its ability to generalize quickly to a large number of semantic categories with minimal training overhead, making it suitable for scenarios with limited labeled data.

- **Example** -> For a simple analogy, imagine a child wants to learn what a bird looks like. In a process resembling supervised learning or FSL, the child learns by looking at images labeled “bird” in a book of animal pictures. Moving forward, she’ll recognize a bird because it resembles the bird images she’s already seen. But in a ZSL scenario, no such labeled examples are available. Instead, the child might read an encyclopedia entry on birds and learn that they are small- or medium-sized animals with feathers, beaks and wings that can fly through the air. She’ll then be able to recognize a bird in the real world, even though she has never seen one before, because she has learned the concept of a bird.
  
**Generalized Zero-Shot Learning (GSZL):** 

- GSZL extends the concept of ZSL by considering scenarios **where new examples may belong to either unseen classes or classes that the model has already learned from labeled examples.**
- In GSZL, models must overcome the challenge of bias towards predicting classes seen during training over unseen classes.
	Techniques to mitigate bias in GSZL may include additional discrimination mechanisms or adjustments to the learning process.

	- Transfer Learning:
	- **Transfer learning plays a crucial role in ZSL by enabling models to leverage pre-trained knowledge for new tasks and classes.**
	- **Instead of training models from scratch, transfer learning allows models to repurpose knowledge learned from large datasets for specific tasks with limited labeled data.**
		For example, pre-trained language models like BERT or pre-trained convolutional neural networks (CNNs) can be fine-tuned for zero-shot text or image classification tasks, respectively.
	- **Transfer learning is particularly beneficial for GSZL, where knowledge of seen classes can serve as auxiliary information for predicting unseen classes.**
  
  Overall, zero-shot learning and its variants offer efficient solutions for tasks with limited labeled data, leveraging auxiliary information and pre-trained knowledge to make accurate predictions for unseen classes. 
  

#### Zero-shot learning methods:

#### Attribute-based 

- Train classifiers on features like color and shape instead of data classes.
- Infer unseen classes based on learned attributes.
- Example -> Recognize a bee as a "yellow, striped flying insect" without seeing a bee image.
- Useful when labeled examples of target classes are unavailable, but labeled examples of characteristics are available.
- Drawbacks ->
Assumes each class can be described by a single vector of attributes, which is not always true.
Annotating attributes can be costly and time-consuming.
Cannot generalize to classes with unknown or absent attributes.

#### Embedding-based methods:

- Represent classes and samples as semantic embeddings (vector representations).
- Classify based on similarity between embeddings.
  
###### Embeddings can be generated using:
- Pre-trained models (e.g., BERT for words, ResNet for images).
- Autoencoders that learn compressed representations.
- Models trained from scratch on relevant data.
###### Classification is determined by measuring proximity between sample and class embeddings.
- Require normalization and projection of embeddings into a shared high-dimensional space for consistent comparison.
- Use contrastive learning to align embeddings by minimizing distances between matching pairs and maximizing distances between non-matching pairs.
- Joint end-to-end training, like OpenAI’s CLIP, trains models together to ensure alignment, enabling zero-shot classification.
  
#### Generative-based methods:

- Use auxiliary information to generate synthetic data samples, converting zero-shot problems into standard supervised learning.
###### Techniques include:
- Variational autoencoders (VAEs) that learn latent representations as distributions of variables.
Conditional VAEs (CVAEs) that constrain properties of synthesized samples.
- Generative adversarial networks (GANs) that use a generator and discriminator in an adversarial setup.
- VAEGANs that combine VAEs' stability and GANs' image quality.

