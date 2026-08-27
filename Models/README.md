# LLM Model

**LLM (Large Language Model)** คือโมเดล AI ที่ถูกฝึกด้วยข้อมูลข้อความจำนวนมหาศาล เพื่อเรียนรู้รูปแบบของภาษา ความสัมพันธ์ระหว่างคำ และบริบท แล้วนำความรู้นั้นมาใช้ในการ **เข้าใจ วิเคราะห์ สร้าง และแปลงข้อความ**

## 1. LLM Model Architecture

```mermaid
flowchart TD
    INPUT["User Input"]
    TOKEN["Tokenization"]
    EMB["Token Embedding"]
    POS["Positional Information"]
    TRANS["Transformer"]
    
    INPUT --> TOKEN
    TOKEN --> EMB
    EMB --> POS
    POS --> TRANS

    TRANS --> ATT["Self-Attention"]
    ATT --> FFN["Feed Forward Network"]
    FFN --> NORM["Normalization"]
    NORM --> TRANS

    TRANS --> HEAD["Output / LM Head"]
    HEAD --> LOGITS["Logits"]
    LOGITS --> SOFTMAX["Probability"]
    SOFTMAX --> NEXT["Next Token"]

    NEXT --> OUTPUT["Generated Response"]
```

---

# 2. Core Components ของ LLM

```mermaid
mindmap
  root((LLM Model))
    Tokenization
      Token
      Vocabulary
      Token ID
    Embedding
      Token Embedding
      Positional Embedding
    Transformer
      Self Attention
      Multi Head Attention
      Feed Forward
      Layer Normalization
      Residual Connection
    Output
      Logits
      Probability
      Next Token
    Training
      Pretraining
      Instruction Tuning
      Alignment
      RLHF
      DPO
    Inference
      Prompt
      Context
      Sampling
      Decoding
```

---

# 3. LLM Processing Pipeline

```mermaid
flowchart LR
    A["Text"] --> B["Tokenizer"]
    B --> C["Token IDs"]
    C --> D["Embedding"]
    D --> E["Transformer Layers"]
    E --> F["Logits"]
    F --> G["Probability"]
    G --> H["Token Selection"]
    H --> I["Next Token"]
    I --> J["Generated Text"]
```

---

# 4. Transformer Architecture

LLM สมัยใหม่จำนวนมากมีพื้นฐานจาก **Transformer Architecture**

```mermaid
flowchart TD
    INPUT["Input Tokens"]
    --> EMB["Embedding"]

    EMB --> ATT["Multi-Head Self-Attention"]
    ATT --> ADD1["Residual Connection"]
    ADD1 --> NORM1["LayerNorm"]

    NORM1 --> FFN["Feed Forward Network"]
    FFN --> ADD2["Residual Connection"]
    ADD2 --> NORM2["LayerNorm"]

    NORM2 --> NEXT["Next Transformer Layer"]

    NEXT --> OUTPUT["Output Representation"]
```

---

# 5. Self-Attention

Self-Attention ช่วยให้โมเดลพิจารณาความสัมพันธ์ระหว่าง Token ต่าง ๆ ใน Context

```mermaid
flowchart LR
    X["Input Tokens"]

    X --> Q["Query"]
    X --> K["Key"]
    X --> V["Value"]

    Q --> SCORE["Attention Score"]
    K --> SCORE

    SCORE --> SOFT["Softmax"]
    SOFT --> WEIGHT["Attention Weights"]

    WEIGHT --> OUT["Weighted Value"]
    V --> OUT

    OUT --> RESULT["Attention Output"]
```

แนวคิดหลักสามารถเขียนเป็น

$$
Attention(Q,K,V)
=
softmax
\left(
\frac{QK^T}{\sqrt{d_k}}
\right)V
$$

---

# 6. LLM Training

การสร้าง LLM โดยทั่วไปมีหลายขั้นตอน

```mermaid
flowchart TD
    DATA["Large Dataset"]
    --> CLEAN["Data Cleaning"]
    --> TOKEN["Tokenization"]
    --> PRE["Pretraining"]
    --> SFT["Supervised Fine-Tuning"]
    --> ALIGN["Alignment"]
    --> EVAL["Evaluation"]
    --> MODEL["LLM Model"]
```

## Pretraining

โมเดลเรียนรู้จากข้อมูลจำนวนมาก โดยภารกิจพื้นฐานของ Decoder-based LLM คือการคาดการณ์ Token ถัดไป

```mermaid
flowchart LR
    A["The cat is"]
    --> B["sitting"]
    --> C["on"]
    --> D["the"]
    --> E["mat"]
```

---

# 7. LLM Inference

เมื่อผู้ใช้ส่ง Prompt ให้ LLM

```mermaid
flowchart TD
    USER["User Prompt"]
    --> TOKEN["Tokenization"]
    --> CONTEXT["Context"]
    --> LLM["LLM"]

    LLM --> LOGITS["Logits"]
    LOGITS --> PROB["Token Probabilities"]
    PROB --> SAMPLE["Sampling / Decoding"]
    SAMPLE --> TOKEN2["Next Token"]

    TOKEN2 --> CONTEXT
    CONTEXT --> LLM

    LLM --> OUTPUT["Final Response"]
```

จุดสำคัญคือ LLM ไม่ได้สร้างคำตอบทั้งหมดในครั้งเดียว แต่โดยทั่วไปจะ **สร้าง Token ต่อ Token**

---

# 8. LLM Model Types

```mermaid
flowchart TD
    LLM["LLM"]
    
    LLM --> DEC["Decoder-only"]
    LLM --> ENCDEC["Encoder-Decoder"]
    LLM --> ENC["Encoder-only"]

    DEC --> GPT["GPT-style Models"]
    DEC --> QWEN["Qwen-style Models"]
    DEC --> LLAMA["Llama-style Models"]

    ENCDEC --> T5["T5-style Models"]

    ENC --> BERT["BERT-style Models"]
```

### Decoder-only

เหมาะกับ

* Text Generation
* Chatbot
* Coding
* Reasoning
* AI Agent

### Encoder-Decoder

เหมาะกับ

* Translation
* Summarization
* Text-to-Text Tasks

### Encoder-only

เหมาะกับ

* Classification
* Semantic Representation
* Embedding
* Information Retrieval

---

# 9. LLM Model Lifecycle

```mermaid
flowchart LR
    DATA["Data"]
    --> PRE["Pretraining"]
    --> FT["Fine-Tuning"]
    --> ALIGN["Alignment"]
    --> EVAL["Evaluation"]
    --> DEPLOY["Deployment"]
    --> INFER["Inference"]
    --> FEEDBACK["Feedback"]

    FEEDBACK --> FT
```

---

# 10. LLM + RAG

LLM สามารถทำงานร่วมกับ **RAG (Retrieval-Augmented Generation)** เพื่อดึง Knowledge ภายนอกเข้ามาประกอบการตอบคำถาม

```mermaid
flowchart TD
    Q["User Question"]

    Q --> EMB["Question Embedding"]
    EMB --> RET["Retriever"]
    RET --> DB["Vector Database"]
    DB --> DOC["Relevant Documents"]

    Q --> PROMPT["Prompt"]
    DOC --> PROMPT

    PROMPT --> LLM["LLM"]
    LLM --> ANSWER["Generated Answer"]
```

แนวคิดสำคัญคือ

```text
Question
   ↓
Retrieve Knowledge
   ↓
Build Context
   ↓
LLM
   ↓
Answer
```

---

# 11. LLM + AI Agent

LLM สามารถเป็น **Reasoning Engine** ของ AI Agent

```mermaid
flowchart TD
    USER["User"]

    USER --> AGENT["AI Agent"]
    AGENT --> LLM["LLM"]

    LLM --> PLAN["Planning"]
    LLM --> REASON["Reasoning"]
    LLM --> TOOL["Tool Selection"]

    TOOL --> SEARCH["Search"]
    TOOL --> API["API"]
    TOOL --> DB["Database"]
    TOOL --> CODE["Code Execution"]

    SEARCH --> OBS["Observation"]
    API --> OBS
    DB --> OBS
    CODE --> OBS

    OBS --> LLM

    LLM --> RESPONSE["Final Response"]
```

---

# 12. LLM Model ในระบบ AI สมัยใหม่

```mermaid
flowchart TD
    USER["Human"]

    USER --> APP["AI Application"]

    APP --> ROUTER["Model Router"]

    ROUTER --> LLM1["General LLM"]
    ROUTER --> LLM2["Reasoning Model"]
    ROUTER --> LLM3["Coding Model"]
    ROUTER --> LLM4["Vision-Language Model"]

    APP --> RAG["RAG"]
    APP --> MEMORY["Memory"]
    APP --> TOOLS["Tools"]
    APP --> AGENT["AI Agent"]

    RAG --> APP
    MEMORY --> APP
    TOOLS --> APP
    AGENT --> APP
```

---

# 13. LLM Model Stack

```mermaid
flowchart TD
    APP["AI Application"]
    --> AGENT["Agent Layer"]
    --> ORCH["Orchestration Layer"]
    --> LLM["LLM Layer"]
    --> INFER["Inference Engine"]
    --> GPU["GPU / Accelerator"]
```

ตัวอย่าง Stack

```text
Application
     ↓
AI Agent
     ↓
RAG / Memory / Tools
     ↓
LLM
     ↓
Inference Engine
     ↓
GPU
```

---

# 14. LLM Model กับ Software Engineering

LLM สามารถเข้ามาช่วยในหลายขั้นตอนของ Software Engineering

```mermaid
flowchart TD
    REQ["Requirement"]
    --> ANALYSIS["Analysis"]
    --> DESIGN["Design"]
    --> CODE["Code Generation"]
    --> TEST["Testing"]
    --> REVIEW["Code Review"]
    --> DEPLOY["Deployment"]
    --> MAINT["Maintenance"]

    LLM["LLM"]

    LLM -.-> REQ
    LLM -.-> ANALYSIS
    LLM -.-> DESIGN
    LLM -.-> CODE
    LLM -.-> TEST
    LLM -.-> REVIEW
    LLM -.-> MAINT
```

---

# 15. สรุป LLM Model

```mermaid
flowchart LR
    DATA["Data"]
    --> TOKEN["Tokens"]
    --> EMB["Embedding"]
    --> TRANS["Transformer"]
    --> ATT["Attention"]
    --> FFN["FFN"]
    --> LOGITS["Logits"]
    --> PROB["Probability"]
    --> TOKEN2["Next Token"]
    --> TEXT["Generated Text"]
```

**สรุปสั้น ๆ**

> **LLM = Tokenization + Embedding + Transformer + Attention + Feed Forward + Training + Inference + Decoding**

และเมื่อ LLM ถูกนำมารวมกับ

```text
LLM
 +
RAG
 +
Memory
 +
Tools
 +
Planning
 +
Reasoning
 +
Workflow
```

จะกลายเป็นพื้นฐานสำคัญของ **AI Agent / Agentic AI System** ในยุคปัจจุบัน
