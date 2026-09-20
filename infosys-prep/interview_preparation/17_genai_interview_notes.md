# GenAI Interview Notes

## Table of Contents
- [Generative AI](#generative-ai)
- [Traditional ML vs Generative AI](#traditional-ml-vs-generative-ai)
- [Foundation Models](#foundation-models)
- [Tokens](#tokens)
- [Embeddings](#embeddings)
- [Transformers](#transformers)
- [Attention](#attention)
- [LLMs](#llms)
- [Prompting](#prompting)
- [Temperature and Sampling](#temperature-and-sampling)
- [Context Window](#context-window)
- [Hallucination](#hallucination)
- [RAG](#rag)
- [RAG Pipeline](#rag-pipeline)
- [Vector Databases](#vector-databases)
- [Semantic Search](#semantic-search)
- [Fine Tuning vs RAG](#fine-tuning-vs-rag)
- [Function Calling and Tool Use](#function-calling-and-tool-use)
- [Agents](#agents)
- [Structured Output](#structured-output)
- [Inference Cost and Latency](#inference-cost-and-latency)
- [Evaluation](#evaluation)
- [AI Safety and Security Basics](#ai-safety-and-security-basics)
- [Important GenAI Interview Q&A](#important-genai-interview-qa)
- [SceneFlow Connection](#sceneflow-connection)
- [GenAI Interview Traps](#genai-interview-traps)
- [Final Checklist](#final-checklist)

<a id="table-of-contents"></a>

<a id="generative-ai"></a>
## Generative AI
[Back to Table of Contents](#table-of-contents)

Generative AI refers to models that generate new content such as text, images, audio, video or code.

Example:
A language model generates the next token based on the context.

<a id="traditional-ml-vs-generative-ai"></a>
## Traditional ML vs Generative AI
[Back to Table of Contents](#table-of-contents)

Traditional supervised ML commonly predicts a target from input features.

GenAI models learn patterns in large datasets and generate outputs based on learned representations and conditioning context.

<a id="foundation-models"></a>
## Foundation Models
[Back to Table of Contents](#table-of-contents)

A foundation model is trained on broad data and can be adapted to many downstream tasks.

Adaptation methods include prompting, retrieval augmentation, fine-tuning and tool use.

<a id="tokens"></a>
## Tokens
[Back to Table of Contents](#table-of-contents)

LLMs usually process text as tokens rather than raw characters or whole sentences.

Tokenization affects context length, latency and cost.

<a id="embeddings"></a>
## Embeddings
[Back to Table of Contents](#table-of-contents)

An embedding is a numerical vector representing learned semantic information.

Example:
"car" and "automobile" can produce vectors that are close in embedding space.

Used for:
- semantic search
- recommendations
- clustering
- RAG retrieval

In SceneFlow, `all-MiniLM-L6-v2` was used to produce compact embeddings for similarity workflows.

<a id="transformers"></a>
## Transformers
[Back to Table of Contents](#table-of-contents)

Transformers are neural-network architectures centered on attention, with feed-forward layers and modern normalization/residual components.

High-level LLM flow:

```text
text
 ↓
tokenization
 ↓
embeddings
 ↓
transformer layers
 ↓
output logits
 ↓
sampling/decoding
 ↓
generated tokens
```

<a id="attention"></a>
## Attention
[Back to Table of Contents](#table-of-contents)

Attention lets a token representation use information from other tokens.

Scaled dot-product attention:

```text
Attention(Q,K,V) = softmax(QK^T / sqrt(d_k)) V
```

Intuition:
For a sentence, attention helps a token use relevant context from other tokens.

<a id="llms"></a>
## LLMs
[Back to Table of Contents](#table-of-contents)

A Large Language Model is a large neural language model trained to model token sequences and generate text conditioned on context.

Many modern LLMs are transformer-based.

The model is not simply a normal database of exact answers; outputs depend on learned parameters plus current context.

<a id="prompting"></a>
## Prompting
[Back to Table of Contents](#table-of-contents)

A prompt provides task instructions and context.

Useful structure:

```text
Context
Task
Constraints
Input
Output format
Examples if useful
```

Example:

```text
Summarize this complaint in 3 bullets.
Return JSON with category, urgency and reason.
```

<a id="temperature-and-sampling"></a>
## Temperature and Sampling
[Back to Table of Contents](#table-of-contents)

Temperature changes the distribution used for sampling.

Lower temperature generally means less variation; higher temperature generally allows more variation.

Exact behavior depends on the decoding configuration.

<a id="context-window"></a>
## Context Window
[Back to Table of Contents](#table-of-contents)

The context window is the amount of tokenized information a model can process for a request, subject to model/provider limits.

A larger context window does not automatically mean better reasoning.

<a id="hallucination"></a>
## Hallucination
[Back to Table of Contents](#table-of-contents)

A hallucination is generated content that is unsupported, fabricated or incorrect.

Mitigations:
- retrieval/grounding
- structured outputs
- validation
- source-aware generation
- constrained tools
- evaluation
- fallback/abstention behavior

<a id="rag"></a>
## RAG
[Back to Table of Contents](#table-of-contents)

Retrieval-Augmented Generation combines retrieval with generation.

```text
question
  ↓
retrieve relevant knowledge
  ↓
provide context to LLM
  ↓
generate answer
```

Useful when knowledge is private, frequently changing, domain-specific or too large for a prompt.

<a id="rag-pipeline"></a>
## RAG Pipeline
[Back to Table of Contents](#table-of-contents)

Indexing:

```text
documents
 ↓
chunking
 ↓
embedding model
 ↓
vector store
```

Query:

```text
user query
 ↓
query embedding
 ↓
similarity search
 ↓
top-k chunks
 ↓
prompt construction
 ↓
LLM
 ↓
answer
```

Know:
- chunk size
- overlap
- top-k
- metadata filters
- reranking
- retrieval evaluation

<a id="vector-databases"></a>
## Vector Databases
[Back to Table of Contents](#table-of-contents)

A vector database stores vectors and metadata and supports similarity search.

Examples:
- Qdrant
- Pinecone
- Weaviate
- Milvus

Typical record:

```text
vector + document_id + metadata
```

<a id="semantic-search"></a>
## Semantic Search
[Back to Table of Contents](#table-of-contents)

Semantic search compares learned representations to retrieve conceptually related content.

Example:
"reduce server response time" can retrieve content about "latency optimization" even without exact word matches.

<a id="fine-tuning-vs-rag"></a>
## Fine Tuning vs RAG
[Back to Table of Contents](#table-of-contents)

RAG:
- changes runtime context
- useful for changing/private knowledge

Fine-tuning:
- changes model parameters
- useful for behavior, style, format or domain patterns

Fine-tuning alone is not a substitute for retrieval of frequently changing facts.

<a id="function-calling-and-tool-use"></a>
## Function Calling and Tool Use
[Back to Table of Contents](#table-of-contents)

Tool use lets a model request an external operation.

Example:

```text
User -> LLM
       -> get_order_status(order_id)
       -> backend/API
       -> result
       -> LLM
       -> response
```

The application should validate arguments and authorize the operation.

<a id="agents"></a>
## Agents
[Back to Table of Contents](#table-of-contents)

An agentic system commonly combines:
- model generation/reasoning
- tools
- state/context
- a control loop

```text
goal
 ↓
decide
 ↓
tool
 ↓
observe
 ↓
decide next step
 ↓
answer
```

A deterministic workflow can be simpler and more reliable when agent autonomy is unnecessary.

<a id="structured-output"></a>
## Structured Output
[Back to Table of Contents](#table-of-contents)

Structured output constrains model responses to a schema such as JSON.

```json
{
  "category": "billing",
  "priority": "high"
}
```

Validate returned data before using it in application logic.

<a id="inference-cost-and-latency"></a>
## Inference Cost and Latency
[Back to Table of Contents](#table-of-contents)

Important drivers:
- token count
- model size
- hardware
- concurrency
- network latency
- retrieval/tool calls

Optimization:
- reduce unnecessary context
- cache repeated work
- stream responses
- choose an appropriate model
- batch where suitable
- use smaller models for simple tasks

<a id="evaluation"></a>
## Evaluation
[Back to Table of Contents](#table-of-contents)

Evaluate:
- correctness
- relevance
- groundedness
- factuality
- format compliance
- latency
- cost
- safety

For RAG, evaluate retrieval quality separately from generation quality.

<a id="ai-safety-and-security-basics"></a>
## AI Safety and Security Basics
[Back to Table of Contents](#table-of-contents)

Important risks:
- prompt injection
- sensitive-data leakage
- insecure tool use
- malicious retrieved content
- excessive permissions
- weak output validation

Principles:
- least privilege
- validate tool inputs
- separate trusted instructions from untrusted content
- restrict dangerous actions
- log security-relevant events

<a id="important-genai-interview-qa"></a>
## Important GenAI Interview Q&A
[Back to Table of Contents](#table-of-contents)

### What is an LLM?

A large neural language model trained to model token sequences and generate text conditioned on context.

### What is an embedding?

A vector representation useful for measuring learned semantic relationships.

### Why do we need RAG?

To provide relevant external knowledge at inference time, especially for private or changing data.

### RAG vs fine-tuning?

RAG supplies retrieved context at runtime. Fine-tuning updates model parameters.

### What is a hallucination?

An unsupported or incorrect generated claim.

### What is a vector database?

A system optimized for vector storage and similarity retrieval.

### What is tool calling?

A structured mechanism where a model requests an external function/API and the application executes it.

### What is an agent?

A system where a model participates in a loop involving decisions, tools and observations to accomplish a goal.

<a id="sceneflow-connection"></a>
## SceneFlow Connection
[Back to Table of Contents](#table-of-contents)

SceneFlow combines several GenAI concepts:

```text
scene script
   ↓
Gemini prompt/query analysis
   ↓
search keywords
   ↓
embedding generation
   ↓
Qdrant similarity search
   ↓
image candidates
   ↓
metadata persistence
```

Interview explanation:
"The system uses an LLM for query analysis and an embedding model for similarity retrieval. Qdrant stores vectors and metadata for similarity search. The LLM is not the vector database."

<a id="genai-interview-traps"></a>
## GenAI Interview Traps
[Back to Table of Contents](#table-of-contents)

- LLM does not mean database.
- RAG is not fine-tuning.
- Embeddings are not plain keyword search.
- More context is not automatically better.
- Tool calling does not mean the model directly executes privileged actions.
- An agent is not required for every GenAI application.
- Temperature does not guarantee factuality.
- Vector similarity alone does not guarantee answer correctness.

<a id="final-checklist"></a>
## Final Checklist
[Back to Table of Contents](#table-of-contents)

Know:
- GenAI
- foundation models
- tokens
- embeddings
- transformers
- attention
- LLMs
- prompting
- temperature
- context window
- hallucination
- RAG
- chunking
- vector databases
- semantic search
- fine-tuning vs RAG
- tool calling
- agents
- structured output
- cost/latency
- evaluation
- prompt injection
- SceneFlow architecture
