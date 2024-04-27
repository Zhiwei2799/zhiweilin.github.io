---
layout: post
math: true
toc: true
---
Some notes for transformer architecture
![image](https://github.com/zhiweilin27/zhiweilin27.github.io/assets/111717798/f68f846c-f661-486f-9cfe-f6fc71a0725c)

## Self-Attention
The self-attention mechanism uses three matrices - query (Q), key (K), and value (V) - to help the system understand and process the relationships between words in a sentence. 

Let’s say we have an input sequence of length N, represented as a matrix X of shape (N, d), where d is the dimension of the input embedding vector. We can calculate the query, key, and value vectors as follows:

- Query: We multiply the input embedding matrix X with a learned weight matrix Wq of shape (d, h), where h is the number of attention heads. This produces a matrix Q of shape (N, h), where each row corresponds to the query vector for the corresponding token in the input sequence.Q = XWq
- Key: We multiply the input embedding matrix X with a learned weight matrix Wk of shape (d, h). This produces a matrix K of shape (N, h), where each row corresponds to the key vector for the corresponding token in the input sequence.K = XWk
- Value: We multiply the input embedding matrix X with a learned weight matrix Wv of shape (d, h). This produces a matrix V of shape (N, h), where each row corresponds to the value vector for the corresponding
  token in the input sequence.V = XWv
  Once we have calculated the query, key, and value vectors, we can use them to compute the attention scores between all pairs of tokens in the input sequence.
  The attention scores are then used to weight the corresponding value vectors, which are summed to produce the final output of the self-attention mechanism.
![image](https://github.com/zhiweilin27/zhiweilin27.github.io/assets/111717798/8b1af8b3-57a7-4823-9b28-88a6d265811d)


## Word and Positional Embeddings
A typical word embedding is a dense vector that represents the meaning and semantic information of a word in a continuous space. The dimension of the embeddings depends on the specific model and configuration. Let's assume we have a 3-dimensional embedding space for simplicity. An example of embeddings for the tokens in the input sentence "The cat sat on the mat" could look like this:
- The: [0.21, -0.15, 0.32]
- cat: [0.85, 0.29, -0.61]
- sat: [-0.37, 0.72, 0.45]
- on: [0.12, -0.64, 0.27]
- the: [0.21, -0.15, 0.32] (Note: Same as 'The' embedding, as word embeddings are usually case-insensitive)
- mat: [-0.53, 0.31, 0.81]
These are just example values and not real embeddings. In practice, the embeddings are learned by the model during training, and the dimensionality is usually much larger, such as 128, 256, 512, or even larger.
In addition to the word embeddings, we also need to add positional encoding to these vectors to preserve the order of the words in the input sentence.
Positional encodings is sinusoidal functions
-  the output of sine and cosine is in [-1, 1], which is normalized. It won’t grow to an unmanageable size like integers would.
-  no additional training has to be done since unique representations are generated for each position.
![image](https://github.com/zhiweilin27/zhiweilin27.github.io/assets/111717798/3c446378-f354-4d49-a8ad-9af6cce197b4) where k is position, i is dimensional index 

Assuming we have a simple learned positional encoding, the final input embeddings might look like this:
- The (word + position): [0.21, -0.15, 0.32] + [0.01, 0.02, 0.03] = [0.22, -0.13, 0.35]
- cat (word + position): [0.85, 0.29, -0.61] + [0.04, 0.05, 0.06] = [0.89, 0.34, -0.55]
- sat (word + position): [-0.37, 0.72, 0.45] + [0.07, 0.08, 0.09] = [-0.30, 0.80, 0.54]
- on (word + position): [0.12, -0.64, 0.27] + [0.10, 0.11, 0.12] = [0.22, -0.53, 0.39]
- the (word + position): [0.21, -0.15, 0.32] + [0.13, 0.14, 0.15] = [0.34, -0.01, 0.47]
- mat (word + position): [-0.53, 0.31, 0.81] + [0.16, 0.17, 0.18] = [-0.37, 0.48, 0.99]

## Multi-headed attention
In the multi-head attention layer, the self-attention mechanism is applied multiple times in parallel, each with different sets of learned weights. This allows the model to capture various aspects of the context and focus on different relationships among words simultaneously.
Here's a step-by-step explanation of the multi-head attention layer:

- Determine the number of attention heads. Let's say we have H heads.
- For each attention head h (where h = 1, 2, ..., H), initialize separate sets of weight matrices WQ_h, WK_h, and WV_h.
- Perform self-attention H times in parallel, using the different sets of weight matrices for each head. This involves calculating the Q, K, and V matrices, computing the attention scores and weights, and obtaining the context-aware representations. 
- Multiply the concatenated matrix by another learned weight matrix, WO (output matrix), to produce the final output of the multi-head attention layer.
The multi-head attention layer allows the model to capture different contextual aspects and relationships among words simultaneously. For example, one attention head might focus on syntactic relationships, while another could focus on semantic relationships. Combining the results from multiple attention heads enables the transformer to build a richer understanding of the input text.
The output of the multi-head attention layer is then passed through the remaining layers of the transformer, such as position-wise feedforward layers, layer normalization, and residual connections, before producing the final output.

## FFNS
In a transformer architecture, after the multi-head attention layer, the output goes through a position-wise feedforward layer. This layer applies a feedforward neural network (FFNN) independently to each position in the input sequence. The purpose of this layer is to process and combine the features learned by the multi-head attention layer for each token while maintaining their positions.
Here's an overview of what happens in the position-wise feedforward layer:

- For each position (i.e., each token) in the input sequence, apply a feedforward neural network. This FFNN has the same architecture and weights across all positions, but it operates independently on each token.
- The FFNN typically consists of two linear layers (i.e., fully connected layers) with a non-linear activation function, such as ReLU (Rectified Linear Unit), applied in between. This structure allows the model to learn more complex relationships and features within the input data.
- The first linear layer expands the dimension of the input, which helps the model capture more complex patterns. The dimension is then reduced back to the original size by the second linear layer.
- The output of the position-wise feedforward layer for each token is then combined with its corresponding input through a **residual connection (addition)** and passed through a layer normalization step.
  
In summary, the position-wise feedforward layer applies a feedforward neural network independently to each token in the input sequence. This helps process and combine the features learned by the multi-head attention layer while maintaining the positional information of the tokens.
The layer enhances the expressive power of the transformer model, allowing it to capture more complex patterns and relationships within the input data.

## Layer Normalization
Normalization is a process that standardizes the input layer by adjusting and scaling the activations. Specifically, Transformers use Layer Normalization (LN). Unlike other normalization methods that operate over the batch dimension, LN operates over the feature dimension (across all channels).
The mathematical representation of Layer Normalization is:

$$ LN(x) = gamma * (x — mean(x)) / sqrt(var(x) + epsilon) + beta $$

Reference：
https://towardsdatascience.com/into-the-transformer-5ad892e0cee 
https://www.linkedin.com/pulse/gpt-4-explaining-self-attention-mechanism-fatos-ismali/
https://www.linkedin.com/pulse/clear-explanation-transformer-neural-networks-ebin-babu-thomas/

## Bert Implementation
https://readmedium.com/en/https:/towardsdatascience.com/masked-language-modelling-with-bert-7d49793e5d2c

## Generative Language Modeling (Greedy, Beam Search, Random Walk)
###  Greedy Decoding
- It is one of the simplest and fastest methods for generating text and involves selecting the most likely next word at each step in the sequence.
### Beam Search
- The fundamental idea of beam search is exploring multiple paths instead of just single one.: Unlike greedy decoding, which only keeps the single best path (the most probable next word) at each step, beam search keeps track of the k most probable paths at each step. This means at every step in the sequence,
- it doesn’t just consider the single most likely next word, but the k most likely next words.
### Random Walk 
method where the selection of each next word in a sequence is based on some level of randomness rather than deterministic rules or purely greedy choices.
- Stochastic Sampling: In language generation, a random walk can be analogous to sampling methods where each word is chosen based on a probability distribution over the vocabulary. The model computes probabilities for the next word based on the context provided by previous words, and then a word is randomly selected based on this distribution.
- Temperature Adjusted Sampling: This is a refinement where the "temperature" parameter is used to control the randomness of the word selection:
   - A high temperature results in more uniform distributions (higher randomness), making the generation process more exploratory and diverse, akin to a random walk with many possible paths.
   - A low temperature results in sharper distributions (less randomness), making the generation more conservative, focusing on more likely words.
- Top-k and Top-p Sampling: These are methods to constrain the randomness to the most likely next words:
   - Top-k Sampling: Top-k sampling refines the selection process by limiting the pool of potential next tokens to the top-k most likely candidates. Among these top-k tokens, the next token is chosen based on its probability, maintaining a degree of randomness while focusing on more likely options.
   - Top-p (Nucleus) Sampling: In top-p sampling or nucleus sampling, the selection pool for the next token is determined by the cumulative probability of the most probable tokens. When you set a threshold p, the model includes just enough of the most probable tokens so that their combined probability reaches or exceeds this threshold

https://medium.com/@pashashaik/natural-language-generation-from-scratch-in-large-language-models-with-pytorch-4d9379635316

![image](https://github.com/zhiweilin27/zhiweilin27.github.io/assets/111717798/bc9ad6f1-514f-4222-9a00-a05b74d4eb36)
![image](https://github.com/zhiweilin27/zhiweilin27.github.io/assets/111717798/4480c6aa-ba6e-426b-b08d-a696340ffd22)

## Pre-training
Pre-training is a foundational step in the LLM training process, where the model gains a general understanding of language by exposure to vast amounts of text data. 

Think of it as the model's introduction to the world of words, phrases, and ideas. During this phase, the LLM learns grammar rules, linguistic patterns, factual information, and reasoning abilities. 

To achieve this, the model is fed an extensive dataset containing diverse texts from books, articles, websites, and more. Take the example of GPT-3, with its immense parameter count. It ingested around 570 GB of text data during pre-training. This is like reading hundreds of thousands of books in multiple languages, giving the model a rich tapestry of language to draw from. 

## fine-tuning
After the initial pre-training phase, like primary and secondary education where the LLM gets its general language skills, fine-tuning is like giving it on-the-job training. It's honing its abilities for particular tasks or domains, transforming it from a language learner into a task-specific expert. 

For instance, scientists might fine-tune a model with a dataset of medical texts, making it exceptional at understanding medical jargon and answering health-related questions. 

Similarly, you can train a model on legal documents, turning it into a whizz at summarizing contracts and legal discussions. 

During fine-tuning, the parameters of the pre-trained model are updated (fine-tuned) using task-specific data, typically with a smaller learning rate than during pre-training.

### task fine-tuning
This method allows the model to adapt its parameters to the nuances and requirements of the targeted task, thereby enhancing its performance and relevance to that particular domain. Task-specific fine-tuning is particularly valuable when you want to optimize the model's performance for a single, well-defined task, ensuring that the model excels in generating task-specific content with precision and accuracy.

Task-specific fine-tuning is closely related to transfer learning, but transfer learning is more about leveraging the general features learned by the model, whereas task-specific fine-tuning is about 
adapting the model to the specific requirements of the new task.

### Instruction fine-tuning
Whereas supervised fine-tuning consists in training models on example inputs and the results derived from them (output), instruction tuning fleshes out input-output examples with another component: instructions.

This is precisely what enables instruction-tuned models to generalize more easily to new tasks. As a result, LLMs tuned in this way become much more versatile and useful.

input examples and their corresponding outputs, instruction tuning augments input-output examples with instructions, which enables instruction-tuned models to generalize more easily to new tasks.

### Contextual Embeddings
Both embedding techniques, traditional word embedding (e.g. word2vec, Glove) and contextual embedding (e.g. ELMo, BERT), aim to learn a continuous (vector) representation for each word in the documents. Continuous representations can be used in downstream machine learning tasks.

Traditional word embedding techniques learn a global word embedding. They first build a global vocabulary using unique words in the documents by ignoring the meaning of words in different context. Then, similar representations are learnt for the words appeared more frequently close each other in the documents. The problem is that in such word representations the words' contextual meaning (the meaning derived from the words' surroundings), is ignored. For example, only one representation is learnt for "left" in sentence "I left my phone on the left side of the table." However, "left" has two different meanings in the sentence, and needs to have two different representations in the embedding space.

On the other hand, contextual embedding methods are used to learn sequence-level semantics by considering the sequence of all words in the documents. Thus, such techniques learn different representations for polysemous words, e.g. "left" in example above, based on their context.

### RAG
Retrieval-augmented generation is a technique used in natural language processing that combines the power of both retrieval-based models and generative models to enhance the quality and relevance of generated text.
https://webcache.googleusercontent.com/search?q=cache:https://colabdoge.medium.com/what-is-rag-retrieval-augmented-generation-b0afc5dd5e79&strip=0&vwsrc=1&referer=medium-parser

## Few short, Zero-shot
- Zero-shot learning — a technique whereby we prompt an LLM without any examples, attempting to take advantage of the reasoning patterns it has gleaned (i.e. a generalist LLM)
- Few-shot learning — a technique whereby we prompt an LLM with several concrete examples of task performance
   -  Fine tuning - When you already have a model trained to perform the task you want but on a different dataset, you initialise using the pre-trained weights and train it on target (usually smaller) dataset (usually with a smaller learning rate).
   - Few shot learning - When you want to train a model on any task using very few samples. e.g., you have a model trained on different but related task and you (optionally) modify it and train for target task using small number of examples.
    For example: Fine tuning - Training a model for intent classification and then fine tuning it on a different dataset. Few shot learning - Training a language model on large text dataset and modifying it (usually last (few) layer) to classify intents by training on small labelled dataset.
