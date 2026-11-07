# Test Run: Without Custom Skill (/viva)

## Objective
Evaluate how baseline AI behaves when prompted to conduct an oral viva without the custom `/viva` skill instructions, contrasting it against the dedicated examiner agent.

---

## 1. Prompt Used (Raw / Unstructured)
```text
Take a viva from my OS notes:
Operating Systems Concepts:
1. Deadlock: A situation where a set of processes are blocked because each process is holding a resource and waiting for another resource held by another process...
[Full OS notes]```



### AI Response:
"I will now generate a viva-style assessment based on your Operating Systems notes covering deadlocks, memory management, and paging concepts."

Generated Output:

Operating Systems Viva Assessment (Widget / Google Sheets)

Format: 1 of 8 multiple-choice selector with Next/Back buttons and hints.

Metric|Without Skill (Default AI)|With Custom Skill (/viva)
Assessment Format|Degraded into a multiple-choice objective quiz (A/B/C/D) and spreadsheet generator.|Authentic oral viva examination requiring written/verbal analytical explanations.
Question Flow|Locked behind an 8-question static quiz UI widget.|Asks questions strictly one at a time directly in the chat session.
Evaluation Depth|Binary right/wrong click validation without conceptual depth.|"Deep technical feedback parsing nuances| control flow| and edge cases before advancing."
Grading & Diagnostics|Basic score tally (e.g. 0 wrong / 0 right).|Structured diagnostic rubric with concept-by-concept mastery levels and focused revision guidance.
Examiner Persona|Impersonal quiz generator.|Rigorous academic examiner conducting a real-time technical evaluation.


### Key Takeaway
Without the skill, the AI misinterpreted an oral "viva" as an objective multiple-choice test widget. The custom /viva skill successfully forces sequential conversation, conceptual answering, and strict examiner-style evaluation.

