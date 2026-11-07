# Project 16: Your Own Skill (/viva)

A specialized AI Agent Skill built for technical oral viva examinations directly from syllabus study notes. Designed for turn-by-turn interactive assessment, dynamic answer evaluation, and structured diagnostic feedback.

---

## 📌 Project Overview
- **Project**: Week 2, Project 16 (Your Own Skill)[cite: 1, 19]
- **Section**: Section D (Video, skills and design)[cite: 1]
- **Skill Name**: `/viva`
- **Goal**: Convert repetitive instruction prompting into a reusable agent skill that initiates oral viva examinations one question at a time and scores the user accurately[cite: 19].

---

## 📂 Project Structure

```text
project-16-viva-skill/
│
├── .agent/
│   └── skills/
│       └── viva/
│           ├── skill.json          # Skill manifest, trigger syntax, and metadata
│           └── instructions.md     # Core prompt logic, tone enforcement, and grading rules
│
├── sample_notes/
│   ├── os_notes.txt                # Operating Systems (Deadlocks, Paging, Thrashing)
│   ├── dbms_notes.txt              # Database Management Systems (Normalization, ACID)
│   └── cn_notes.txt                # Computer Networks (OSI Layers, TCP/IP, Routing)
│
├── test_outputs/
│   ├── test1_transcript.md         # Full turn-by-turn viva transcript with final scorecard
│   └── test_without_skill.md       # Baseline comparison proving why the skill is necessary
│
├── prompts.md                      # Prompts and iterations used during skill creation
└── README.md                       # Documentation
