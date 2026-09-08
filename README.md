# 🚀 Self-Improving Multi-Agent Research System (MAS vs. Baseline Benchmark)

> An autonomous, self-improving research framework built with **LangGraph** and the **Google Gemini API**. By leveraging automated feedback loops, the system evaluates and iteratively enhances large language model (LLM) outputs with minimal human intervention.

---

## 📌 1. Executive Summary

This project evaluates the performance of a **Multi-Agent System (MAS)** against a **Single-Pass Baseline** across complex technical, regulatory, and industrial research topics. By decoupling research generation from quality auditing, the system achieves significant improvements in factual accuracy, source grounding, and comprehensive coverage.

* **Core Frameworks**: LangGraph, LangChain, Google Gemini API (`gemini-flash-latest`), Tavily Web Search API
* **Key Capabilities**:
  * Automated quality auditing using Pydantic-based **Structured Output** schema
  * Dynamic **Critic-Researcher feedback loops** that extract missing context and auto-generate targeted re-search queries
  * Quantitative reliability analysis using tracked `score_history` metrics
  * Automated batch execution, Markdown report exports, and visualization pipelines

---

## 💡 2. Background & Motivation

### 2.1. Limitations of Single-Agent Architectures
* **Hallucinations & Unverified Claims**: Standard single-pass search agents often generate unverified statements or fail to attach precise markdown source URLs for critical metrics.
* **Lack of Self-Correction**: Single agents cannot independently audit their outputs to identify missing subtopics or temporal inaccuracies.

### 2.2. The Multi-Agent Advantage
* **Decoupled Quality Auditing**: Separating the research generation role (**Researcher**) from the quality assurance role (**Critic**) enforces strict verification standards.
* **Iterative Self-Improvement**: Automated feedback loops ensure that research reports are refined until they meet a pre-defined quality threshold (Critic Score ≥ 8/10).

---

## 🛠️ 3. System Methodology

### 3.1. Agent Architecture & Node Roles

The system architecture comprises three specialized nodes interacting within a stateful graph:

[START] ──> Senior Researcher ──> Quality Critic ──(Score < 8)──> [Feedback Loop (Re-Search)]
│
(Score >= 8)
│
▼
Technical Writer ──> [Export .md] ──> [END]

* **Senior Researcher Node**:
  * Executes web searches via Tavily based on initial queries or refined feedback from the Critic.
  * Synthesizes newly retrieved facts into past research frameworks.
* **Quality Critic Node**:
  * Evaluates synthesized research against three criteria using Pydantic structure (`QualificationScore`): **Accuracy & Grounding**, **Data Sufficiency**, and **Relevance**.
  * Outputs an integer score (0–10) and structured feedback (`[CRITIC_FEEDBACK]`) if the score is below 8.
* **Technical Writer Node**:
  * Compiles the final, verified research into a clean Markdown document.
  * Calculates the **Reliability Index Metric** and **Iterative Improvement Index** via Pydantic output when operating in Multi-Agent mode.

### 3.2. Experimental Design (Benchmark Setup)
1. **Benchmark Topics**: 10 high-complexity topics covering A2A vs. MCP protocols, HBM3e/HBM4 packaging roadmaps, EU AI Act compliance timelines, and SMR economics.
2. **Comparative Control Groups**:
   * **Baseline**: `Researcher ➔ Writer` (Single-pass generation without feedback loops)
   * **MAS**: `Researcher ➔ Critic ➔ (Loop) ➔ Writer` (Iterative feedback-driven refinement)

---

## 📊 4. Results & Evaluation

### 4.1. Quantitative Performance Improvement

* **Overall Reliability Gain**:
  * The Multi-Agent System achieved a statistically significant increase in mean Critic Scores compared to the Single-Pass Baseline across all benchmark topics.

[Figure 1: Mean Critic Score Comparison Bar Chart (Baseline vs. MAS)]
*(Description: Bar chart illustrating the average Critic Score and percentage reliability gain of MAS over Baseline)*

* **Iterative Score Progression**:
  * Initial research outputs scoring between 5–6 points due to missing URLs or missing subtopics consistently improved to **8–10 points** after 1–3 feedback iterations.

[Graph 1: Reliability Growth Trend across Feedback Iterations]
*(Description: Line graph showing score progression across iteration steps per research topic)*

### 4.2. Architecture Diagrams & Visualizations

The node interaction flow, input/output schemas, and conditional feedback branch structure are automatically exported as presentation slides for architectural audits.

[Figure 2: LangGraph Architecture Diagram (Baseline vs. MAS Workflow)]
*(Description: Exported PowerPoint diagram mapping node inputs, outputs, and feedback loops)*

---

## 📁 5. Repository Structure

```text
.
├── topics.txt                        # Benchmark research topics (10 complex queries)
├── mas_reports/                      # Generated MAS research reports (.md)
├── baseline_reports/                 # Generated Baseline research reports (.md)
├── mas-research-project.ipynb               # Execution notebook & control loops
└── README.md                         # Project documentation