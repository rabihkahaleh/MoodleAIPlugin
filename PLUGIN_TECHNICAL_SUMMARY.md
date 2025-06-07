
# AI-Integrated Moodle Plugin: Technical Summary

## System Overview

This plugin integrates an AI-powered Socratic assistant into Moodle quizzes to support conceptual learning in Newtonian mechanics for secondary students.

---

### **System Configuration**

| Component        | Specification / Description                                  |
|------------------|-------------------------------------------------------------|
| Backend          | PHP 8                                                        |
| Frontend         | Vue 3                                                        |
| API Integration  | REST API to OpenAI GPT-3.5-turbo (0125)                      |
| Moodle Version   | 4.3+ (requires Quiz module & local plugin permissions)       |
| Server           | Ubuntu 22.04+ or equivalent, 4-core CPU, 16GB RAM, 100 Mbps, PHP `memory_limit` ≥ 512M, `max_execution_time` ≥ 120s |

---

### **Core Functional Modules**

- **Misconception Tagger:** Tags quiz items with JSON labels for targeted feedback.
- **Dialogue Thread Manager:** Maintains context across Socratic dialogue turns within a quiz attempt.
- **Branching Router:** Assigns users to AI chat or instructor/video resource by group.
- **Privacy Cleaner:** Removes all session data and AI threads after completion.

---

### **Instructional Grouping**

- **Experimental Group:**  
  Engages in 3–6-turn Socratic dialogue with the AI assistant for each quiz item.
- **Control Group:**  
  Accesses video resources, concept summary PDFs, and participates in instructor-led Q&A.

---

### **Assistant Model Configuration**

| Setting             | Value                  | Purpose                                                      |
|---------------------|------------------------|--------------------------------------------------------------|
| Model               | gpt-3.5-turbo-0125     | Fast, cost-effective dialogue generation                     |
| Temperature         | 0.5 – 0.7              | Balances deterministic reasoning and creativity              |
| Top-p               | 1.0                    | Full probability space for responses                         |
| Max tokens          | 400                    | Limits response length                                       |
| Frequency Penalty   | 0                      | Default setting                                              |
| Presence Penalty    | 0                      | Default setting                                              |
| Thread Context      | Enabled                | Maintains per-quiz-session memory (no cross-session memory)  |
| Memory              | Disabled               | Ensures privacy; session memory discarded after use          |
| Response Format     | Text                   | For seamless Moodle integration                              |
| Tools Enabled       | File Search, Code Interpreter | Internal context only; not visible to students         |

---

### **Dialogue Logic & Privacy**

- Plugin uses **thread-based OpenAI Assistant API** for continuity and pedagogical control.
- Persistent system prompts enforce Socratic scaffolding, affirmation, and misconception-sensitive questioning.
- Dialogue data is anonymized and erased after each quiz session to protect privacy.

---

### **Reference in Your Paper:**

> **Appendix A. Technical Summary of the AI Plugin**  
> A compact summary of the plugin’s architecture and model configuration is provided here. Complete implementation details, including instructional logic, system prompts, and full code, are available at [https://github.com/rabihkahaleh/MoodleAIPlugin](https://github.com/rabihkahaleh/MoodleAIPlugin).
