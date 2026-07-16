
### ML Fundamentals
 * **The Paradigm Shift:**
   * Software 1.0 (Rules + Data -> Answers) vs. Software 2.0 (Data + Answers -> Rules).
 * **Fundamental Rule:**
   * Input \rightarrow numbers.
   * Output \rightarrow numbers.
   * *The "What is a network?" Slide:* A neuron is just a vector; a layer is a matrix; a deep neural network is a massive set of matrices (weights/parameters).
 * **The Hardware:**
   * GPU cores are massive parallel processing units optimized heavily for one math operation: matrix multiplication.
 * **The Main Training Steps:**
   * Forward pass (predict) \rightarrow Loss (error check) \rightarrow Backward pass (Gradients via Chain Rule) \rightarrow Update weights (Optimization).
 * **Standard Datasets:**
   * Train Set (updates weights) \rightarrow Val Set (tunes hyperparameters) \rightarrow Test Set (final grade).
 * **Transfer Learning:**
   * Pre-train on massive, raw unlabeled datasets \rightarrow Fine-tune on tiny, custom-labeled datasets.
### The Decoder-Only Transformer Block
 * **The Original Transformer (2017):**
   * *Slide visual:* Shows the original paper's diagram with Encoder (left) and Decoder (right) halves.
   * *Modern LLM standard:* We discard the left (Encoder) half entirely and focus **strictly on the Decoder-only** architecture.
 * **Inputs & Tokenization:**
   * Computers process text by assigning IDs in a vocabulary (e.g., the = 383).
   * *Slide hint:* LLMs split words into sub-word tokens using Byte Pair Encoding (BPE) rather than parsing raw characters or entire words.
 * **Embeddings & Positional Encoding:**
   * *One-hot vector:* Sparse representation of a token ID (a vector of mostly zeros with a single 1).
   * *Dense embedding:* Converts one-hot vectors into dense, continuous vectors in semantic space.
   * *Positional Encoding:* Injected directly because self-attention processes all tokens in parallel and has no built-in sense of text order.
 * **Self-Attention (Q, K, V):**
   *    * Q (Query), K (Key), V (Value) are linear projections of the input token vector.
   * QK^T measures semantic similarity (which words relate to each other).
 * **Masking (Causal Attention):**
   * Multiplies future-token weights by 0 (via -\infty inside the softmax) to prevent the decoder from looking at tokens that occur after the current step.
 * **The Feed-Forward Network (FFN):**
   * Standard Multi-Layer Perceptron (MLP) applied to each token vector individually.
   * *Key slide takeaway:* This is where the model stores its factual, permanent database of patterns/knowledge.
 * **Normalization & Residuals:**
   * Skip connections (residual links) bypass layers to prevent vanishing gradients.
   * LayerNorm is a normalization step used to keep vectors mathematically stable (mean 0, variance 1) across deep layers.
### Notable LLMs & Scale
 * **The Architectural Tree:**
   * *Encoder-only (BERT):* Bidirectional, mask-prediction (best for extraction and search).
   * *Encoder-Decoder (T5):* Seq-to-seq (best for translation).
   * *Decoder-only (GPT):* Autoregressive, next-token prediction.
 * **GPT-3 Milestone:**
   * 175B parameters.
   * *Slide takeaway:* Proved that sheer scale unlocks "In-Context Learning" (zero-shot, few-shot prompting works out-of-the-box).
 * **Chinchilla Scaling Laws (DeepMind):**
   * Prior LLMs were starved of data.
   * *The rule:* Parameters (N) and data tokens (D) should scale equally under a fixed compute budget.
 * **LLaMA Strategy (Meta):**
   * Consciously over-trained a smaller model on far more data than the Chinchilla optimal limit.
   * *The goal:* Create a fast, lightweight model that is cheap to run during inference while maintaining massive performance.
### Alignment & Code
 * **The Base Model Limit:**
   * Raw base models are document completers, not helpful assistants.
 * **The Alignment Pipeline:**
   * Pre-training (Predict next token from internet) \rightarrow Supervised Fine-Tuning (SFT, follow prompt-response formats) \rightarrow Preference Tuning (RLHF/DPO, reinforce helpful, polite answers over harmful ones).
 * **The Code Superpower:**
   * *Key slide takeaway:* Training models on programming code (like GitHub data) makes them drastically better at multi-step logical reasoning on regular, non-coding English tasks.
