# Analysis Question

**Analysis Question** คือกระบวนการที่ AI Agent นำคำถามดิบของผู้ใช้มาวิเคราะห์ เพื่อทำความเข้าใจว่า **ผู้ใช้ต้องการอะไร มีข้อมูลสำคัญอะไร มีเงื่อนไขอะไร และข้อมูลส่วนใดไม่เกี่ยวข้อง** ก่อนสร้าง `Clean Question` และส่งต่อไปยัง RAG, Tool หรือ LLM

พูดง่าย ๆ:

> **Analysis Question = ขั้นตอนทำความเข้าใจคำถามก่อนลงมือค้นหา คิด หรือทำงาน**

---

## 1. Question Analysis Pipeline

```mermaid
flowchart LR
    A["Raw Question"] --> B["Question Analysis"]
    B --> C["Intent"]
    B --> D["Entity"]
    B --> E["Context"]
    B --> F["Constraint"]
    B --> G["Relevance"]
    
    C --> H["Clean Question"]
    D --> H
    E --> H
    F --> H
    G --> H
    
    H --> I["RAG / AI Agent / LLM"]
```

---

# 2. สิ่งที่ Analysis Question ต้องวิเคราะห์

สามารถแบ่งเป็น 6 ส่วนหลัก:

```text
Question Analysis
│
├── Intent
├── Entity
├── Context
├── Constraint
├── Relevance
└── Expected Output
```

### 1. Intent

ผู้ใช้ต้องการอะไร?

```text
Explain
Compare
Search
Create
Analyze
Summarize
Translate
Solve
Generate
```

### 2. Entity

กำลังพูดถึงอะไร?

```text
Python
MySQL
RAG
LLM
Software Architecture
```

### 3. Context

มีบริบทอะไรที่ช่วยให้ตอบได้ดีขึ้น?

```text
ผู้เริ่มต้น
ระดับมหาวิทยาลัย
ใช้สำหรับโปรเจกต์
ต้องการตัวอย่าง
```

### 4. Constraint

มีข้อจำกัดอะไร?

```text
Python 3.12
ใช้ MySQL
เขียนเป็น Markdown
ไม่เกิน 1,000 คำ
```

### 5. Relevance

ข้อมูลไหนเกี่ยวข้องหรือไม่เกี่ยวข้อง?

```text
CORE
CONTEXT
NOISE
```

### 6. Expected Output

ผู้ใช้ต้องการผลลัพธ์แบบไหน?

```text
บทความ
โค้ด
ตาราง
Diagram
Markdown
JSON
```

---

# 3. ตัวอย่าง Analysis Question

### Raw Question

```text
ผมกำลังเรียน Software Engineering อยู่ครับ
ตอนนี้ทำโปรเจกต์ Python และอยากทำระบบ AI Agent
แต่ยังไม่ค่อยเข้าใจว่า RAG กับ GraphRAG ต่างกันอย่างไร
อาจารย์อยากให้ทำเป็นบทความ Markdown พร้อม Diagram
และขอให้ยกตัวอย่างง่าย ๆ สำหรับนักศึกษา
```

Analysis:

```json
{
  "intent": "compare",
  "entities": [
    "RAG",
    "GraphRAG",
    "AI Agent"
  ],
  "context": [
    "นักศึกษา",
    "ผู้เริ่มต้น"
  ],
  "constraints": [
    "Markdown",
    "มี Diagram",
    "มีตัวอย่าง"
  ],
  "noise": [
    "กำลังทำโปรเจกต์ Python"
  ],
  "expected_output": [
    "บทความ",
    "Comparison",
    "Diagram",
    "Example"
  ]
}
```

---

# 4. Analysis → Clean Question

หลังจากวิเคราะห์แล้ว Agent จึงสร้าง `Clean Question`

```mermaid
flowchart TD
    RAW["Raw Question"]

    RAW --> ANALYSIS["Question Analysis"]

    ANALYSIS --> INTENT["Intent"]
    ANALYSIS --> ENTITY["Entity"]
    ANALYSIS --> CONTEXT["Context"]
    ANALYSIS --> CONSTRAINT["Constraint"]

    INTENT --> CLEAN["Clean Question"]
    ENTITY --> CLEAN
    CONTEXT --> CLEAN
    CONSTRAINT --> CLEAN
```

ผลลัพธ์:

```text
เปรียบเทียบ RAG และ GraphRAG
อธิบายความแตกต่าง ข้อดี ข้อเสีย
พร้อมตัวอย่างง่าย ๆ สำหรับนักศึกษา
เขียนในรูปแบบ Markdown และมี Diagram
```

---

# 5. Analysis Question กับ Question Relevance Filter

สองส่วนนี้ทำงานต่อเนื่องกัน:

```text
Raw Question
      ↓
Question Analysis
      ↓
Question Relevance Filter
      ↓
Clean Question
```

หรือ:

```mermaid
flowchart LR
    RAW["Raw Question"]
    RAW --> ANALYSIS["Analysis"]

    ANALYSIS --> FILTER["Relevance Filter"]

    FILTER --> CLEAN["Clean Question"]
```

**Analysis** = ทำความเข้าใจข้อมูล

**Filter** = ตัดข้อมูลที่ไม่เกี่ยวข้อง

**Clean Question** = สร้างคำถามที่ผ่านการคัดกรองแล้ว

---

# 6. Analysis Question กับ AI Agent

ใน AI Agent ขั้นตอนนี้สำคัญมาก เพราะ Agent ไม่ควรรีบเรียก Tool ทันที

```mermaid
flowchart TD
    USER["User"]

    USER --> ANALYSIS["Question Analysis"]

    ANALYSIS --> INTENT["Intent Detection"]

    INTENT --> DECISION{"What does user need?"}

    DECISION -->|Search| RAG["RAG / Search"]
    DECISION -->|Calculate| CALC["Calculator"]
    DECISION -->|Code| CODE["Code Tool"]
    DECISION -->|Create| GENERATE["Generation"]
    DECISION -->|Explain| LLM["LLM"]
```

ดังนั้น:

> **Question Analysis เป็นตัวช่วยให้ Agent เลือก “จะทำอะไรต่อ”**

---

# 7. Analysis Question + RAG

```mermaid
flowchart LR
    USER["User"]

    USER --> ANALYSIS["Question Analysis"]

    ANALYSIS --> QUERY["Optimized Query"]

    QUERY --> RETRIEVER["Retriever"]

    RETRIEVER --> RERANK["Reranker"]

    RERANK --> CONTEXT["Relevant Context"]

    CONTEXT --> LLM["LLM"]

    LLM --> ANSWER["Answer"]
```

ถ้าไม่วิเคราะห์คำถามก่อน:

```text
Raw Question
 ↓
Retriever
 ↓
Noise
 ↓
Wrong Context
 ↓
LLM
 ↓
Poor Answer
```

แต่ถ้าวิเคราะห์ก่อน:

```text
Raw Question
 ↓
Analysis
 ↓
Clean Question
 ↓
Optimized Query
 ↓
Relevant Retrieval
 ↓
LLM
 ↓
Better Answer
```

---

# 8. Analysis Question + MAMO

สำหรับ **MAMO Context Engineering** สามารถกำหนดเป็น Layer แรก:

```mermaid
flowchart TD
    USER["User"]

    USER --> ANALYSIS["Question Analysis"]

    ANALYSIS --> INTENT["Intent"]
    ANALYSIS --> ENTITY["Entity"]
    ANALYSIS --> CONTEXT["Context"]
    ANALYSIS --> CONSTRAINT["Constraint"]
    ANALYSIS --> RELEVANCE["Relevance"]

    INTENT --> MAMO["MAMO Context Engine"]
    ENTITY --> MAMO
    CONTEXT --> MAMO
    CONSTRAINT --> MAMO
    RELEVANCE --> MAMO

    MAMO --> MEMORY["Memory"]

    MAMO --> RAG["RAG"]

    MAMO --> GRAPH["GraphRAG"]

    MEMORY --> ASSEMBLY["Context Assembly"]
    RAG --> ASSEMBLY
    GRAPH --> ASSEMBLY

    ASSEMBLY --> LLM["LLM"]

    LLM --> ANSWER["Answer"]
```

---

# 9. Python Prototype

```python
class QuestionAnalyzer:

    def analyze(self, question):

        result = {
            "raw_question": question,
            "intent": None,
            "entities": [],
            "context": [],
            "constraints": [],
            "expected_output": []
        }

        text = question.lower()

        # Intent
        if "เปรียบเทียบ" in question:
            result["intent"] = "compare"
        elif "คืออะไร" in question:
            result["intent"] = "explain"
        elif "สร้าง" in question:
            result["intent"] = "create"
        else:
            result["intent"] = "unknown"

        # Entities
        entities = [
            "RAG",
            "GraphRAG",
            "AI Agent",
            "Python",
            "MySQL"
        ]

        for entity in entities:
            if entity.lower() in text:
                result["entities"].append(entity)

        # Output format
        if "Markdown" in question:
            result["expected_output"].append("Markdown")

        if "Diagram" in question:
            result["expected_output"].append("Diagram")

        if "ตัวอย่าง" in question:
            result["expected_output"].append("Example")

        return result
```

---

# 10. Agent State

ในระบบจริงควรเก็บผล Analysis เป็น State:

```json
{
  "raw_question": "...",

  "analysis": {
    "intent": "compare",

    "entities": [
      "RAG",
      "GraphRAG"
    ],

    "context": [
      "beginner",
      "student"
    ],

    "constraints": [
      "Markdown",
      "Diagram"
    ],

    "relevance": {
      "core": [],
      "context": [],
      "noise": []
    },

    "expected_output": [
      "article",
      "diagram",
      "example"
    ]
  }
}
```

---

# 11. Complete Question Understanding Architecture

```mermaid
flowchart TD
    USER["User"]

    USER --> RAW["Raw Question"]

    RAW --> ANALYSIS["Question Analysis"]

    ANALYSIS --> INTENT["Intent Detection"]

    ANALYSIS --> ENTITY["Entity Extraction"]

    ANALYSIS --> CONTEXT["Context Extraction"]

    ANALYSIS --> CONSTRAINT["Constraint Extraction"]

    ANALYSIS --> OUTPUT["Output Requirement"]

    ANALYSIS --> RELEVANCE["Relevance Analysis"]

    INTENT --> FILTER["Question Relevance Filter"]
    ENTITY --> FILTER
    CONTEXT --> FILTER
    CONSTRAINT --> FILTER
    RELEVANCE --> FILTER
    OUTPUT --> FILTER

    FILTER --> CLEAN["Clean Question"]

    CLEAN --> OPT["Query Optimization"]

    OPT --> ROUTER["AI Agent Router"]

    ROUTER --> RAG["RAG"]
    ROUTER --> TOOL["Tools"]
    ROUTER --> MEMORY["Memory"]
    ROUTER --> LLM["LLM"]

    RAG --> VERIFY["Verification"]
    TOOL --> VERIFY
    MEMORY --> VERIFY
    LLM --> VERIFY

    VERIFY --> ANSWER["Final Answer"]
```

---

# 12. สรุปความสัมพันธ์

```text
Raw Question
      ↓
Question Analysis
      ↓
┌───────────────────────┐
│ Intent                │
│ Entity                │
│ Context               │
│ Constraint            │
│ Relevance             │
│ Expected Output       │
└───────────────────────┘
      ↓
Question Relevance Filter
      ↓
Clean Question
      ↓
Query Optimization
      ↓
AI Agent Router
      ↓
RAG / Memory / Tools / LLM
      ↓
Verification
      ↓
Final Answer
```

### แนวคิดสำคัญ

| Component              | หน้าที่                                  |
| ---------------------- | ---------------------------------------- |
| **Analysis Question**  | ทำความเข้าใจคำถาม                        |
| **Relevance Filter**   | คัดกรองข้อมูล                            |
| **Clean Question**     | คำถามที่สะอาดและครบ                      |
| **Query Optimization** | ปรับคำถามให้เหมาะกับ Retrieval           |
| **Router**             | เลือกว่าจะใช้ RAG, Tool, Memory หรือ LLM |
| **Verification**       | ตรวจสอบผลลัพธ์                           |

> **Analysis Question คือสมองส่วนแรกของ Pipeline** ที่ช่วยให้ AI Agent เข้าใจว่า *“ผู้ใช้กำลังถามอะไร ต้องใช้อะไร และควรทำอะไรต่อ”* ก่อนเข้าสู่ Context Engineering, RAG และ LLM.
