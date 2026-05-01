# 🌉 EduBridge: Multi-Agent AI Tutor for Under-Resourced Education

![Status](https://img.shields.io/badge/Status-Architecture_Phase-orange)
![Focus](https://img.shields.io/badge/Focus-Multi--Agent_System-blue)
![Mission](https://img.shields.io/badge/Mission-Tech_For_Good-green)

## 📖 The Vision

Generic Large Language Models (LLMs) are powerful, but they often fail students in rural or under-resourced areas. These students require strict alignment with local curriculums, culturally relatable examples, and step-by-step pedagogical patience.

**EduBridge** is not just a wrapper around an API. It is a sophisticated, localized, multi-agent reasoning system designed to bridge the educational gap. By simulating a team of specialized educators, EduBridge ensures that every answer is factually accurate, curriculum-aligned, and culturally nuanced.

*Current Status: We are currently in the deep architectural design and prompt-engineering phase, preparing for core implementation.*

---

## 🏗️ System Architecture

To achieve high-fidelity teaching without human intervention, EduBridge employs a multi-agent debate and consensus workflow.
```mermaid
graph TD
    User((Student)) -->|Raw Query| InputMod[Input Moderation/Safety]
    InputMod -->|Clean Query| Orch[Orchestrator Agent]
    
    subgraph Memory & Context Layer
        Orch <-->|Read/Update| SessionMem[(Short-term Session Memory)]
        Orch <-->|Fetch| ProfileMem[(Long-term Learner Profile)]
    end
    
    subgraph Multi-Agent Reasoning Core
        Orch -->|Query Decomposition| TaskPlan[Task Planner]
        TaskPlan -->|Sub-task 1: Fetch| RAG[Curriculum RAG Agent]
        
        subgraph Dense Retrieval Pipeline
            RAG -->|Semantic Search| VectorDB[(Pinecone: Textbook Embeddings)]
            RAG -->|Graph Traversal| GraphDB[(Curriculum Knowledge Graph)]
            VectorDB -->|Chunked Context| RAG
            GraphDB -->|Entity Relations| RAG
        end
        
        TaskPlan -->|Sub-task 2: Analyze| Ped[Pedagogical Agent]
        ProfileMem -->|Identify Weaknesses| Ped
        
        RAG -->|Raw Academic Context| Synthesis[Reasoning & Synthesis]
        Ped -->|Teaching Strategy| Synthesis
        
        Synthesis -->|Academic Draft| Loc[Localization Agent]
        Loc <-->|Fetch Local Idioms| LocalDB[(Cultural Nuance DB)]
        Loc -->|Relatable Draft| Ver[Verification Agent]
    end
    
    subgraph Alignment & Hallucination Defense
        Ver -->|Cross-reference Context| RAG
        Ver -->|Check Factual Accuracy| Eval{Strict Constraints Met?}
        Eval -.->|Fails: Inject Critique| Synthesis
        Eval -.->|Fails: Simplify Language| Loc
        Eval -->|Passes| OutputGen[Final Output Formatter]
    end
    
    OutputGen -->|Update State| SessionMem
    OutputGen --> FinalResponse((Final Output))
