
# MAMO Context Engineering Project

> **MAMO Context Engineering** คือ Framework สำหรับจัดการ Context ของ LLM และ AI Agent ตั้งแต่การรวบรวมข้อมูล การค้นหา การจัดลำดับ การกรอง การบีบอัด การส่ง Context เข้า Model ไปจนถึงการประเมินผลและอัปเดต Memory

---
# 🧠 MAMO Context Engineering

> **Memory • Awareness • Model Context • Orchestration**

![GitHub](https://img.shields.io/badge/GitHub-Repository-181717?style=for-the-badge&logo=github&logoColor=white)
![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Research%20Prototype-orange?style=for-the-badge)

## 🛠️ Software Tools

### 💻 Development

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![Git](https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)

### 🤖 AI & Agent

![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white)
![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=for-the-badge)
![LangGraph](https://img.shields.io/badge/LangGraph-1C3C3C?style=for-the-badge)

### 📚 RAG & Knowledge

![LlamaIndex](https://img.shields.io/badge/LlamaIndex-000000?style=for-the-badge)
![Qdrant](https://img.shields.io/badge/Qdrant-DC244C?style=for-the-badge)
![Neo4j](https://img.shields.io/badge/Neo4j-4581C3?style=for-the-badge&logo=neo4j&logoColor=white)

### 🗄️ Database & Memory

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white)

### 📊 Evaluation & Monitoring

![Ragas](https://img.shields.io/badge/Ragas-000000?style=for-the-badge)
![Langfuse](https://img.shields.io/badge/Langfuse-000000?style=for-the-badge)

## 🛠️ Software Tools

MAMO Context Engineering สามารถพัฒนาด้วย Software Tools ที่ครอบคลุมตั้งแต่
LLM, AI Agent, RAG, Memory, Vector Database, Knowledge Graph ไปจนถึง
Evaluation และ Monitoring

### 🧩 Technology Stack

| Layer | Software Tools | Purpose |
|---|---|---|
| 🧠 LLM | OpenAI, Claude, Gemini, Qwen | Reasoning และ Text Generation |
| 🤖 AI Agent | LangGraph, LangChain, CrewAI | Agent Workflow และ Orchestration |
| 📚 RAG | LlamaIndex, LangChain | Retrieval-Augmented Generation |
| 🔢 Embedding | Sentence Transformers, BGE, Qwen Embedding | สร้าง Vector Representation |
| 🎯 Reranker | BGE Reranker, Qwen Reranker | จัดอันดับ Context |
| 🗄️ Vector DB | Qdrant, Milvus, Weaviate, pgvector | Vector Search |
| 🕸️ Knowledge Graph | Neo4j | จัดการความสัมพันธ์ของข้อมูล |
| 🧠 Memory | Redis, PostgreSQL, Vector DB | Short-Term / Long-Term Memory |
| ⚡ Backend | Python, FastAPI | API และ Backend Services |
| 🎨 Frontend | Next.js, React | Web Application |
| 🔄 Workflow | n8n | Automation และ Workflow |
| 📊 Evaluation | Ragas, DeepEval | RAG และ Agent Evaluation |
| 🔍 Monitoring | Langfuse, LangSmith | Tracing, Debugging และ Monitoring |
| 📦 Container | Docker | Environment และ Deployment |
| 🗃️ Database | PostgreSQL | Application Data และ Metadata |
| 💻 Development | VS Code, Git, GitHub | Development และ Version Control |

---

# 2. ปัญหาที่ MAMO ต้องการแก้

LLM ไม่ควรได้รับข้อมูลทั้งหมดที่ระบบมี

ตัวอย่าง:

```text
100,000 Tokens
      ↓
ข้อมูลทั้งหมด
      ↓
LLM
```

อาจทำให้เกิดปัญหา:

* Context ยาวเกินไป
* Token Cost สูง
* Latency สูง
* ข้อมูลไม่เกี่ยวข้อง
* ข้อมูลเก่า
* ข้อมูลซ้ำ
* Context Conflict
* Model สับสน
* ความแม่นยำลดลง

MAMO จึงเปลี่ยนกระบวนการเป็น:

```mermaid
flowchart LR
    DATA["Raw Data"]
    DATA --> RETRIEVE["Retrieval"]
    RETRIEVE --> RANK["Ranking"]
    RANK --> FILTER["Filtering"]
    FILTER --> COMPRESS["Compression"]
    COMPRESS --> CONTEXT["Optimal Context"]
    CONTEXT --> LLM["LLM"]
```

---

# 3. M — Memory

**Memory** คือระบบจัดเก็บข้อมูลที่ Agent สามารถนำกลับมาใช้ในอนาคต

## 3.1 ประเภทของ Memory

```mermaid
mindmap
  root((Memory))
    Short-Term Memory
      Current Conversation
      Current Task
      Current State
    Long-Term Memory
      User Preferences
      User Profile
      Project Information
    Episodic Memory
      Past Events
      Previous Tasks
      Experiences
    Semantic Memory
      Facts
      Knowledge
      Concepts
```

---

## 3.2 Short-Term Memory

เก็บข้อมูลในบทสนทนาปัจจุบัน

```text
User:
ฉันกำลังสร้างระบบ RAG

User:
ช่วยออกแบบ Architecture ให้หน่อย
```

---

## 3.3 Long-Term Memory

เก็บข้อมูลที่สามารถนำกลับมาใช้ในอนาคต

```text
User Preferences

- สนใจ AI Agent
- สนใจ RAG
- ใช้ Python
- ต้องการคำอธิบายภาษาไทย
```

---

## 3.4 Episodic Memory

เก็บเหตุการณ์หรือประสบการณ์

```text
Project A
    ↓
Problem
    ↓
Solution
    ↓
Result
```

---

## 3.5 Semantic Memory

เก็บข้อเท็จจริงและความรู้

```text
RAG
├── Retrieval
├── Embedding
├── Vector Database
└── Reranking
```

---

# 4. Python: Memory Manager

ตัวอย่าง Memory แบบง่ายด้วย Python

```python
class MemoryManager:

    def __init__(self):
        self.short_term = []
        self.long_term = []

    def add_short_term(self, content):
        self.short_term.append(content)

    def add_long_term(self, content):
        self.long_term.append(content)

    def get_short_term(self):
        return self.short_term

    def get_long_term(self):
        return self.long_term

    def clear_short_term(self):
        self.short_term = []


memory = MemoryManager()

memory.add_short_term(
    "User กำลังพัฒนาระบบ RAG"
)

memory.add_long_term(
    "User สนใจ AI Agent และ Context Engineering"
)

print(memory.get_short_term())
print(memory.get_long_term())
```

---

# 5. A — Awareness

**Awareness** คือความสามารถของ Agent ในการเข้าใจ Context ปัจจุบัน

Agent ควรรู้:

```text
Who?
What?
When?
Where?
Why?
Goal?
Current State?
Constraints?
```

### Awareness Architecture

```mermaid
flowchart TD
    USER["User"]

    USER --> PROFILE["User Profile"]
    USER --> TASK["Current Task"]
    USER --> HISTORY["Conversation History"]
    USER --> STATE["Current State"]
    USER --> CONSTRAINT["Constraints"]

    PROFILE --> AWARENESS["Awareness Engine"]
    TASK --> AWARENESS
    HISTORY --> AWARENESS
    STATE --> AWARENESS
    CONSTRAINT --> AWARENESS

    AWARENESS --> CONTEXT["Current Context"]
```

---

# 6. Python: Awareness Engine

```python
class AwarenessEngine:

    def build_context(
        self,
        user,
        task,
        history,
        state,
        constraints
    ):
        return {
            "user": user,
            "task": task,
            "history": history,
            "state": state,
            "constraints": constraints
        }


awareness = AwarenessEngine()

context = awareness.build_context(
    user="Student",
    task="วิเคราะห์ระบบ RAG",
    history=["สร้าง RAG Architecture"],
    state="กำลังออกแบบระบบ",
    constraints=["ต้องใช้ Python"]
)

print(context)
```

---

# 7. M — Model Context

**Model Context** คือการเลือกข้อมูลที่เหมาะสมสำหรับส่งเข้า LLM

หลักการสำคัญ:

```text
Relevant
+
Recent
+
Reliable
+
Important
+
Task-specific
```

### Context Sources

```mermaid
flowchart TD
    SOURCES["Context Sources"]

    SOURCES --> CONVERSATION["Conversation"]
    SOURCES --> MEMORY["Memory"]
    SOURCES --> RAG["RAG"]
    SOURCES --> DOCS["Documents"]
    SOURCES --> GRAPH["Knowledge Graph"]
    SOURCES --> TOOLS["Tools"]
    SOURCES --> API["External APIs"]

    CONVERSATION --> SELECT["Context Selection"]
    MEMORY --> SELECT
    RAG --> SELECT
    DOCS --> SELECT
    GRAPH --> SELECT
    TOOLS --> SELECT
    API --> SELECT

    SELECT --> RANK["Ranking"]
    RANK --> COMPRESS["Compression"]
    COMPRESS --> MODEL["LLM Context"]
```

---

# 8. Context Retrieval

สมมติระบบมีข้อมูล 100 รายการ

```mermaid
flowchart LR
    QUERY["User Query"]

    QUERY --> RETRIEVAL["Retriever"]

    RETRIEVAL --> D100["100 Documents"]

    D100 --> D20["Top 20"]

    D20 --> RERANK["Reranker"]

    RERANK --> D8["Top 8"]

    D8 --> FILTER["Context Filter"]

    FILTER --> D5["Top 5"]

    D5 --> LLM["LLM"]
```

---

# 9. Python: Context Retriever

ตัวอย่างง่ายด้วย Keyword Matching

```python
documents = [
    "RAG ใช้ Retrieval เพื่อค้นหาข้อมูล",
    "Vector Database ใช้เก็บ Embedding",
    "Context Engineering จัดการ Context ของ LLM",
    "Python ใช้พัฒนา AI Agent",
    "Knowledge Graph ใช้แทนความสัมพันธ์ของข้อมูล"
]


def retrieve(query, documents, top_k=3):

    query_words = set(query.lower().split())

    scored = []

    for document in documents:

        words = set(document.lower().split())

        score = len(query_words & words)

        scored.append({
            "document": document,
            "score": score
        })

    scored.sort(
        key=lambda x: x["score"],
        reverse=True
    )

    return scored[:top_k]


results = retrieve(
    "Context LLM",
    documents
)

for result in results:
    print(result)
```

> ในระบบ Production สามารถเปลี่ยนเป็น Vector Search, BM25, Hybrid Search หรือ Reranker ได้

---

# 10. Context Ranking

Context แต่ละรายการควรได้รับคะแนน

สูตรตัวอย่าง:

```text
Context Score =
    Relevance
    +
    Recency
    +
    Importance
    +
    Reliability
```

สามารถกำหนด Weight:

```text
Score =
0.40(Relevance)
+
0.20(Recency)
+
0.20(Importance)
+
0.20(Reliability)
```

---

# 11. Python: Context Ranker

```python
def context_score(
    relevance,
    recency,
    importance,
    reliability
):
    return (
        0.40 * relevance +
        0.20 * recency +
        0.20 * importance +
        0.20 * reliability
    )


contexts = [
    {
        "name": "Document A",
        "relevance": 0.95,
        "recency": 0.90,
        "importance": 0.90,
        "reliability": 0.95
    },
    {
        "name": "Document B",
        "relevance": 0.80,
        "recency": 0.95,
        "importance": 0.70,
        "reliability": 0.80
    }
]


for item in contexts:

    item["score"] = context_score(
        item["relevance"],
        item["recency"],
        item["importance"],
        item["reliability"]
    )


contexts.sort(
    key=lambda x: x["score"],
    reverse=True
)

for item in contexts:

    print(
        item["name"],
        round(item["score"], 3)
    )
```

---

# 12. Context Compression

Context จำนวนมากไม่ควรถูกส่งเข้า LLM โดยตรง

```mermaid
flowchart LR
    A["100,000 Tokens"]
    B["20,000 Tokens"]
    C["10,000 Tokens"]
    D["4,000 Tokens"]

    A --> B
    B --> C
    C --> D

    D --> LLM["LLM"]
```

เป้าหมายคือ:

> ลดจำนวน Token แต่ยังคงรักษาข้อมูลที่จำเป็นต่อ Task

---

# 13. Python: Context Compressor

```python
def compress_context(
    contexts,
    max_items=5
):

    selected = contexts[:max_items]

    compressed = "\n".join(
        f"- {item}"
        for item in selected
    )

    return compressed


contexts = [
    "RAG ใช้ Retrieval",
    "Embedding ใช้แทนความหมายของข้อความ",
    "Vector Database ใช้ค้นหา Similarity",
    "Reranker ช่วยจัดอันดับผลลัพธ์",
    "Context Engineering จัดการ Context",
    "LLM ใช้สร้างคำตอบ"
]

compressed = compress_context(
    contexts,
    max_items=4
)

print(compressed)
```

ในระบบจริงสามารถใช้ LLM สำหรับ:

```text
Summarization
+
Deduplication
+
Information Extraction
+
Hierarchical Summarization
```

---

# 14. Context Injection

หลังจากผ่าน Retrieval และ Compression แล้ว ต้องสร้าง Context สำหรับ LLM

```mermaid
flowchart TD
    SYSTEM["System Context"]
    USER["User Context"]
    TASK["Task Context"]
    MEMORY["Memory Context"]
    KNOWLEDGE["Knowledge Context"]
    TOOLS["Tool Context"]
    CONSTRAINTS["Constraints"]

    SYSTEM --> BUILDER["Context Builder"]
    USER --> BUILDER
    TASK --> BUILDER
    MEMORY --> BUILDER
    KNOWLEDGE --> BUILDER
    TOOLS --> BUILDER
    CONSTRAINTS --> BUILDER

    BUILDER --> PROMPT["Final Context"]
    PROMPT --> LLM["LLM"]
```

---

# 15. Python: Context Builder

```python
def build_context(
    system,
    user,
    task,
    memory,
    knowledge,
    constraints
):

    return f"""
SYSTEM CONTEXT:
{system}

USER CONTEXT:
{user}

TASK CONTEXT:
{task}

MEMORY CONTEXT:
{memory}

KNOWLEDGE CONTEXT:
{knowledge}

CONSTRAINTS:
{constraints}
"""


context = build_context(
    system="You are an AI Agent.",
    user="นักพัฒนาระบบ AI",
    task="ออกแบบ RAG",
    memory="User สนใจ Context Engineering",
    knowledge="RAG ใช้ Retrieval-Augmented Generation",
    constraints="ตอบเป็นภาษาไทย"
)

print(context)
```

---

# 16. O — Orchestration

**Orchestration** เป็นส่วนควบคุม Workflow ทั้งหมด

```mermaid
flowchart TD
    USER["User Query"]

    USER --> UNDERSTAND["Understand Task"]
    UNDERSTAND --> MEMORY["Check Memory"]

    MEMORY --> RETRIEVE["Retrieve Knowledge"]

    RETRIEVE --> RANK["Rank Context"]

    RANK --> COMPRESS["Compress Context"]

    COMPRESS --> BUILD["Build Context"]

    BUILD --> LLM["LLM / Agent"]

    LLM --> DECISION{"Need Tool?"}

    DECISION -->|Yes| TOOL["Call Tool"]
    DECISION -->|No| RESPONSE["Generate Response"]

    TOOL --> OBSERVE["Observe Result"]

    OBSERVE --> LLM

    RESPONSE --> EVALUATE["Evaluate"]

    EVALUATE --> UPDATE["Update Memory"]

    UPDATE --> END["Final Response"]
```

---

# 17. Python: MAMO Orchestrator

```python
class MAMOAgent:

    def __init__(self):

        self.memory = MemoryManager()
        self.awareness = AwarenessEngine()

    def process(self, query):

        # 1. Awareness
        current_context = self.awareness.build_context(
            user="AI Developer",
            task=query,
            history=[],
            state="active",
            constraints=[]
        )

        # 2. Memory
        memories = self.memory.get_long_term()

        # 3. Context Collection
        contexts = [
            query,
            *memories
        ]

        # 4. Context Selection
        selected = contexts[:5]

        # 5. Context Compression
        compressed = compress_context(
            selected
        )

        # 6. Context Injection
        final_context = build_context(
            system="You are an AI Agent.",
            user=current_context["user"],
            task=query,
            memory=str(memories),
            knowledge=compressed,
            constraints="ตอบเป็นภาษาไทย"
        )

        return final_context


agent = MAMOAgent()

agent.memory.add_long_term(
    "User สนใจ RAG และ AI Agent"
)

result = agent.process(
    "ออกแบบระบบ Context Engineering"
)

print(result)
```

---

# 18. MAMO Full Pipeline

```mermaid
flowchart TD

    START(["User Request"])

    START --> UNDERSTANDING["Task Understanding"]

    UNDERSTANDING --> COLLECT["Context Collection"]

    COLLECT --> MEMORY["Memory"]
    COLLECT --> RAG["RAG"]
    COLLECT --> KNOWLEDGE["Knowledge"]
    COLLECT --> TOOLS["Tools"]

    MEMORY --> MERGE["Context Merge"]
    RAG --> MERGE
    KNOWLEDGE --> MERGE
    TOOLS --> MERGE

    MERGE --> RETRIEVE["Context Retrieval"]

    RETRIEVE --> RANK["Context Ranking"]

    RANK --> FILTER["Context Filtering"]

    FILTER --> COMPRESS["Context Compression"]

    COMPRESS --> INJECT["Context Injection"]

    INJECT --> AGENT["LLM / AI Agent"]

    AGENT --> DECISION{"Action Required?"}

    DECISION -->|Yes| EXECUTE["Tool Execution"]

    EXECUTE --> OBSERVE["Observe"]

    OBSERVE --> AGENT

    DECISION -->|No| EVALUATE["Evaluation"]

    EVALUATE --> UPDATE["Memory Update"]

    UPDATE --> RESPONSE(["Final Response"])
```

---

# 19. MAMO Context Loop

จุดเด่นของ MAMO คือ Context ไม่ได้จบเมื่อ LLM ตอบคำถาม

ผลลัพธ์สามารถกลับไปสร้าง Memory ใหม่ได้

```mermaid
flowchart LR

    USER["User"]
    CONTEXT["Context"]
    AGENT["AI Agent"]
    ACTION["Action"]
    RESULT["Result"]
    EVALUATION["Evaluation"]
    MEMORY["Memory"]

    USER --> CONTEXT
    CONTEXT --> AGENT
    AGENT --> ACTION
    ACTION --> RESULT
    RESULT --> EVALUATION
    EVALUATION --> MEMORY
    MEMORY --> CONTEXT
```

นี่คือ:

> **Context Engineering Feedback Loop**

---

# 20. MAMO + RAG

MAMO สามารถทำงานร่วมกับ RAG ได้

```mermaid
flowchart TD

    QUERY["User Query"]

    QUERY --> Q["Query Understanding"]

    Q --> VECTOR["Vector Search"]
    Q --> KEYWORD["Keyword Search"]
    Q --> GRAPH["Knowledge Graph"]

    VECTOR --> HYBRID["Hybrid Retrieval"]
    KEYWORD --> HYBRID
    GRAPH --> HYBRID

    HYBRID --> RERANK["Reranker"]

    RERANK --> CONTEXT["Context Selection"]

    CONTEXT --> COMPRESS["Context Compression"]

    COMPRESS --> MAMO["MAMO Context Engine"]

    MAMO --> LLM["LLM"]

    LLM --> RESPONSE["Response"]
```

---

# 21. MAMO + AI Agent

```mermaid
flowchart TD

    AGENT["AI Agent"]

    AGENT --> PLANNER["Planner"]
    AGENT --> MEMORY["Memory"]
    AGENT --> TOOLS["Tool Manager"]

    PLANNER --> MAMO["MAMO Context Engine"]
    MEMORY --> MAMO
    TOOLS --> MAMO

    MAMO --> RETRIEVAL["Retrieval"]
    RETRIEVAL --> RANKING["Ranking"]
    RANKING --> COMPRESSION["Compression"]

    COMPRESSION --> LLM["LLM Reasoning"]

    LLM --> ACTION["Action"]

    ACTION --> OBSERVATION["Observation"]

    OBSERVATION --> EVALUATION["Evaluation"]

    EVALUATION --> MEMORY
```

---

# 22. Project Structure

```text
mamo-context-engineering/
│
├── app/
│   ├── main.py
│   ├── agent.py
│   └── orchestrator.py
│
├── context/
│   ├── collector.py
│   ├── selector.py
│   ├── ranker.py
│   ├── compressor.py
│   └── injector.py
│
├── memory/
│   ├── short_term.py
│   ├── long_term.py
│   ├── episodic.py
│   └── semantic.py
│
├── retrieval/
│   ├── vector_search.py
│   ├── keyword_search.py
│   ├── hybrid_search.py
│   └── reranker.py
│
├── knowledge/
│   ├── documents/
│   ├── vector_db.py
│   └── knowledge_graph.py
│
├── agent/
│   ├── planner.py
│   ├── executor.py
│   ├── tool_manager.py
│   └── evaluator.py
│
├── evaluation/
│   ├── relevance.py
│   ├── accuracy.py
│   ├── faithfulness.py
│   ├── latency.py
│   └── cost.py
│
├── tests/
│
├── requirements.txt
│
└── README.md
```

---

# 23. MAMO Core Class

สามารถรวมองค์ประกอบทั้งหมดเป็น Core Engine

```python
class MAMO:

    def __init__(
        self,
        memory,
        retriever,
        ranker,
        compressor,
        llm
    ):
        self.memory = memory
        self.retriever = retriever
        self.ranker = ranker
        self.compressor = compressor
        self.llm = llm

    def run(self, query):

        # 1. Memory
        memories = self.memory.get_long_term()

        # 2. Retrieval
        retrieved = self.retriever(query)

        # 3. Merge Context
        contexts = memories + retrieved

        # 4. Ranking
        ranked = self.ranker(contexts)

        # 5. Compression
        context = self.compressor(ranked)

        # 6. LLM
        response = self.llm(
            query=query,
            context=context
        )

        # 7. Memory Update
        self.memory.add_short_term(
            response
        )

        return response
```

---

# 24. Prompt Engineering vs Context Engineering

| ประเด็น       | Prompt Engineering | Context Engineering |
| ------------- | ------------------ | ------------------- |
| Focus         | Prompt             | Context             |
| Data          | Static             | Dynamic             |
| Memory        | จำกัด              | มีระบบ Memory       |
| RAG           | Optional           | Core Component      |
| Retrieval     | จำกัด              | สำคัญ               |
| Ranking       | ไม่ใช่แกนหลัก      | สำคัญ               |
| Compression   | Optional           | สำคัญ               |
| Tools         | จำกัด              | Integrated          |
| Agent         | ไม่จำเป็น          | รองรับ              |
| Orchestration | ต่ำ                | สูง                 |
| Feedback Loop | จำกัด              | มี                  |
| Complexity    | ต่ำ                | สูง                 |

### สรุป

```text
Prompt Engineering
        ↓
"เขียนคำสั่งอย่างไรให้ AI ตอบดี?"

Context Engineering
        ↓
"AI ควรรู้อะไร?"
        ↓
"ข้อมูลไหนสำคัญ?"
        ↓
"ข้อมูลไหนควรตัด?"
        ↓
"ควรค้นหาอะไร?"
        ↓
"ควรจำอะไร?"
        ↓
"ควรเรียก Tool ไหน?"
        ↓
"ควรส่ง Context อะไรให้ LLM?"
```

---

# 25. MAMO Evaluation Framework

```mermaid
flowchart TD

    SYSTEM["MAMO System"]

    SYSTEM --> CQ["Context Quality"]
    SYSTEM --> AP["AI Performance"]
    SYSTEM --> SP["System Performance"]
    SYSTEM --> AG["Agent Performance"]

    CQ --> CR["Context Relevance"]
    CQ --> CP["Context Precision"]
    CQ --> CC["Context Recall"]
    CQ --> COM["Context Completeness"]

    AP --> ACC["Accuracy"]
    AP --> FAITH["Faithfulness"]
    AP --> REL["Answer Relevance"]

    SP --> TOKEN["Token Usage"]
    SP --> LAT["Latency"]
    SP --> COST["Cost"]

    AG --> TSR["Task Success Rate"]
    AG --> TOOL["Tool Success Rate"]
    AG --> ERR["Error Recovery"]
```

---

# 26. Experimental Design

สำหรับ Research สามารถเปรียบเทียบ:

```mermaid
flowchart LR

    BASE1["LLM"]
    BASE2["LLM + RAG"]
    BASE3["LLM + RAG + Memory"]
    BASE4["LLM + RAG + Memory + Reranking"]
    MAMO["MAMO Context Engineering"]

    BASE1 --> EVAL["Evaluation"]
    BASE2 --> EVAL
    BASE3 --> EVAL
    BASE4 --> EVAL
    MAMO --> EVAL
```

## Metrics

```text
Accuracy
Relevance
Faithfulness
Context Recall
Context Precision
Task Success Rate
Token Usage
Latency
Cost
```

---

# 27. Research Questions

### RQ1

> MAMO Context Engineering สามารถเพิ่ม Context Relevance ของ AI Agent ได้หรือไม่?

### RQ2

> Context Ranking มีผลต่อ Accuracy ของ AI Agent มากน้อยเพียงใด?

### RQ3

> Context Compression สามารถลด Token Usage โดยไม่ลด Task Performance ได้หรือไม่?

### RQ4

> Memory Architecture มีผลต่อ Long-term Task Completion หรือไม่?

### RQ5

> MAMO มีประสิทธิภาพเหนือกว่า RAG Architecture แบบทั่วไปหรือไม่?

---

# 28. MAMO Research Framework

```mermaid
flowchart TD

    CS["Context Sources"]

    CS --> MEMORY["Memory"]
    CS --> RAG["RAG"]
    CS --> KNOWLEDGE["Knowledge"]
    CS --> HISTORY["Conversation"]
    CS --> TOOLS["Tools"]

    MEMORY --> MAMO["MAMO Context Engineering"]
    RAG --> MAMO
    KNOWLEDGE --> MAMO
    HISTORY --> MAMO
    TOOLS --> MAMO

    MAMO --> SELECTION["Context Selection"]
    SELECTION --> RANKING["Context Ranking"]
    RANKING --> COMPRESSION["Context Compression"]
    COMPRESSION --> INJECTION["Context Injection"]

    INJECTION --> AGENT["AI Agent"]

    AGENT --> PERFORMANCE["Task Performance"]

    PERFORMANCE --> ACC["Accuracy"]
    PERFORMANCE --> REL["Relevance"]
    PERFORMANCE --> FAITH["Faithfulness"]
    PERFORMANCE --> COST["Token / Cost"]
    PERFORMANCE --> LAT["Latency"]
```

---

# 29. MAMO กับ AI Agent Architecture

```mermaid
flowchart TD

    DATA["Data"]
    KNOWLEDGE["Knowledge"]
    RAG["RAG"]
    MEMORY["Memory"]

    DATA --> KNOWLEDGE
    KNOWLEDGE --> RAG
    RAG --> MAMO["MAMO Context Engineering"]
    MEMORY --> MAMO

    MAMO --> RETRIEVE["Retrieval"]
    RETRIEVE --> RANK["Ranking"]
    RANK --> COMPRESS["Compression"]
    COMPRESS --> INJECT["Context Injection"]

    INJECT --> LLM["LLM"]

    LLM --> AGENT["AI Agent"]

    AGENT --> PLANNING["Planning"]
    AGENT --> TOOLS["Tools"]
    AGENT --> ACTION["Action"]

    ACTION --> EVALUATION["Evaluation"]

    EVALUATION --> MEMORY
```

---

# 30. MAMO Context Lifecycle

Context มีวงจรชีวิตตั้งแต่ต้นจนจบ

```mermaid
flowchart LR

    COLLECT["Collect"]
    STORE["Store"]
    RETRIEVE["Retrieve"]
    FILTER["Filter"]
    RANK["Rank"]
    COMPRESS["Compress"]
    INJECT["Inject"]
    REASON["Reason"]
    ACT["Act"]
    EVALUATE["Evaluate"]
    UPDATE["Update"]

    COLLECT --> STORE
    STORE --> RETRIEVE
    RETRIEVE --> FILTER
    FILTER --> RANK
    RANK --> COMPRESS
    COMPRESS --> INJECT
    INJECT --> REASON
    REASON --> ACT
    ACT --> EVALUATE
    EVALUATE --> UPDATE

    UPDATE --> COLLECT
```

---

# 31. MAMO Implementation Roadmap

```mermaid
flowchart LR

    P1["Phase 1<br/>Prototype"]
    P2["Phase 2<br/>RAG"]
    P3["Phase 3<br/>Memory"]
    P4["Phase 4<br/>Context Ranking"]
    P5["Phase 5<br/>Compression"]
    P6["Phase 6<br/>AI Agent"]
    P7["Phase 7<br/>Evaluation"]
    P8["Phase 8<br/>Research"]

    P1 --> P2
    P2 --> P3
    P3 --> P4
    P4 --> P5
    P5 --> P6
    P6 --> P7
    P7 --> P8
```

---

# 32. Technology Stack

ตัวอย่าง Technology Stack สำหรับพัฒนา MAMO

```text
Frontend
├── Next.js
├── React
└── Tailwind CSS

Backend
├── Python
├── FastAPI
└── Pydantic

AI
├── LLM
├── Embedding Model
├── Reranker
└── Agent Framework

RAG
├── Vector Search
├── Hybrid Search
└── Knowledge Graph

Memory
├── Short-Term Memory
├── Long-Term Memory
├── Episodic Memory
└── Semantic Memory

Database
├── PostgreSQL
├── Vector Database
└── Redis

Evaluation
├── Accuracy
├── Relevance
├── Faithfulness
├── Latency
├── Token Usage
└── Cost
```

---

# 33. MAMO Final Architecture

```mermaid
flowchart TB

    USER(["User"])

    subgraph SOURCES["Context Sources"]
        CONV["Conversation"]
        PROFILE["User Profile"]
        MEMORY["Memory"]
        DOCS["Documents"]
        RAG["RAG"]
        KG["Knowledge Graph"]
        TOOLS["Tools"]
    end

    subgraph MAMO["MAMO Context Engineering"]
        COLLECT["Context Collector"]
        SELECT["Context Selector"]
        RANK["Context Ranker"]
        COMPRESS["Context Compressor"]
        INJECT["Context Injector"]
    end

    subgraph AGENT["AI Agent"]
        PLAN["Planner"]
        REASON["LLM Reasoning"]
        EXECUTE["Executor"]
        OBSERVE["Observation"]
    end

    subgraph EVAL["Evaluation"]
        QUALITY["Context Quality"]
        TASK["Task Performance"]
        COST["Cost / Token"]
    end

    USER --> CONV
    USER --> PROFILE

    CONV --> COLLECT
    PROFILE --> COLLECT
    MEMORY --> COLLECT
    DOCS --> COLLECT
    RAG --> COLLECT
    KG --> COLLECT
    TOOLS --> COLLECT

    COLLECT --> SELECT
    SELECT --> RANK
    RANK --> COMPRESS
    COMPRESS --> INJECT

    INJECT --> PLAN
    PLAN --> REASON
    REASON --> EXECUTE
    EXECUTE --> OBSERVE
    OBSERVE --> REASON

    REASON --> QUALITY
    EXECUTE --> TASK
    REASON --> COST

    QUALITY --> MEMORY
    TASK --> MEMORY
```

---

# 34. สรุป

MAMO สามารถสรุปเป็น 4 องค์ประกอบหลัก:

```text
M — MEMORY
    จำข้อมูล ประสบการณ์ และ State

A — AWARENESS
    เข้าใจ User / Task / Environment

M — MODEL CONTEXT
    Retrieve / Select / Rank / Compress / Inject

O — ORCHESTRATION
    ควบคุม Agent / Tool / Workflow
```

กระบวนการหลัก:

```mermaid
flowchart LR

    COLLECT["Collect"]
    RETRIEVE["Retrieve"]
    SELECT["Select"]
    RANK["Rank"]
    COMPRESS["Compress"]
    INJECT["Inject"]
    REASON["Reason"]
    ACT["Act"]
    EVALUATE["Evaluate"]
    REMEMBER["Remember"]

    COLLECT --> RETRIEVE
    RETRIEVE --> SELECT
    SELECT --> RANK
    RANK --> COMPRESS
    COMPRESS --> INJECT
    INJECT --> REASON
    REASON --> ACT
    ACT --> EVALUATE
    EVALUATE --> REMEMBER

    REMEMBER -. Feedback .-> COLLECT
```

> **MAMO Context Engineering = การทำให้ AI Agent รู้ว่า “ควรรู้อะไร ควรรู้อย่างไร ควรใช้ข้อมูลไหน ควรจำอะไร และควรนำ Context ไปใช้เพื่อทำงานอย่างไร”**

---

# 35. แนวทางต่อยอดเป็นงานวิจัย

```mermaid
flowchart LR

    PROTOTYPE["MAMO Prototype"]
    RAG["RAG System"]
    MEMORY["Memory-Augmented Agent"]
    FRAMEWORK["MAMO Framework"]
    BENCHMARK["Benchmark"]
    EXPERIMENT["Experimental Framework"]
    PAPER["Research Paper"]

    PROTOTYPE --> RAG
    RAG --> MEMORY
    MEMORY --> FRAMEWORK
    FRAMEWORK --> BENCHMARK
    BENCHMARK --> EXPERIMENT
    EXPERIMENT --> PAPER
```

แนวทางการทดลองที่น่าสนใจ:

```text
LLM
    vs
LLM + RAG
    vs
LLM + RAG + Memory
    vs
LLM + RAG + Memory + Reranking
    vs
MAMO Context Engineering
```

โดยวัด:

```text
Accuracy
Context Relevance
Context Precision
Context Recall
Faithfulness
Task Success Rate
Token Usage
Latency
Cost
```

**Research Gap ที่น่าสนใจ:** การพัฒนา **Adaptive Context Engineering** ที่สามารถตัดสินใจแบบ Dynamic ว่าในแต่ละ Task ควรใช้ Memory, RAG, Knowledge Graph, Tool หรือ Context Compression ในระดับใด ก่อนส่ง Context ให้ LLM ซึ่งสามารถต่อยอด MAMO จาก Prototype ไปสู่ **Experimental Framework และ Benchmark สำหรับ AI Agent** ได้

```
```
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)
```
