---
epoch: 1780575379283
modelKey: "gemini-3-flash-preview|github-copilot"
topic: "Link to Topics to Study"



tags:
  - copilot-conversation
---

**user**: Add another H2 at the end to link the topics to study file at [[Learning Backlog]]
[Context: Notes: Estudos/Dev/Backend/Database/Database Design/Topics to Study.md, Estudos/Dev/Backend/Database/* MOC.md]
[Timestamp: 2026/06/04 09:16:19]

**ai**: Here is the updated **[[* MOC]]** with the new section added at the end:

---
type: MOC
tags: [development, database, architecture]
---
# Database Design Map of Content

This is the central hub for all concepts related to designing robust database systems.

## Core Philosophy

The primary goals of a well-designed database are:
- **Consistency**: No internal conflicts (e.g., linking data via Foreign Keys).
- **Integrity**: Data must be accurate, complete, and follow business rules.
- **Maintainability**: Use naming conventions to make the schema easy to update and expand.
- **Performance**: Optimization via [[SQL Data Types]] and [[Indexing|indexing]].
- **Security**: Preventing leaks through [[Encryption]] and [[SQL Access Control]].
- **Scalability & Flexibility**: Ability to handle more users and adapt to changes.

## The Design Workflow

1. [[Database Design Process]]: A step-by-step guide from requirements to implementation.
2. [[Relational Database Fundamentals]]: Understanding tables, Foreign Keys, and joins.
3. [[Database Normalization|Normalization]]: Reducing redundancy and improving integrity via normal forms.
4. [[Relationship Mapping]]: Defining relationships and cardinality.

## Atomic Concepts

- [[Relationship Mapping]]: Understanding cardinality and entity connections.
- [[Database Keys and Identity]]: Candidate keys, IDs, and Primary Keys.
- [[SQL Data Types]]: Choosing between `CHAR`, `VARCHAR`, `INT`, etc.
- [[SQL Language Concepts]]: Declarative SQL mindset, constraints, and referential actions.
- [[SQL Access Control]]: Roles, permissions, and least-privilege patterns.
- [[Encryption]]: Hashing vs. reversible encryption for protecting sensitive data.

## Future Study

- [[Learning Backlog]]: A backlog of concepts and questions to explore for deeper mastery.
[Timestamp: 2026/06/04 09:16:27]

**user**: Now, add another topic to the [[Knowledge Refinement]] and correctly differentiate between them - next steps are for concepts already seen, but need further digestion and Future studies are to be seen. You can suggest better organization and naming of it as well. For example, should it go inside Future study or should it be in a different node file? What is the appropriate naming? etc
[Context: Notes: Estudos/Dev/Backend/Database/* Next Steps.md, Estudos/Dev/Backend/Database/* MOC.md]
[Timestamp: 2026/06/04 09:19:36]

**ai**: To improve your workflow and clarify the distinction between "new stuff" and "stuff to master," I suggest a more descriptive naming convention and a structural update to your **[[* MOC]]**.

### 1. Suggested Organization & Naming

Instead of generic names, using terms that imply **action** helps you know exactly what to do when you open the note:

- **[[Learning Backlog]]** (replaces `Topics to Study`): This is your "Inbox" for the future. It contains concepts you haven't touched yet.
- **[[Knowledge Refinement]]** (replaces `* Next Steps`): This is your "Active Lab." It contains concepts you've been introduced to but cannot yet explain simply or apply without help.

---

### 2. Updated [[Knowledge Refinement]] (Knowledge Refinement)

I have added a new item regarding **Relationship Mapping**, as it is a core concept that usually requires practice after the initial read.

```markdown
- Better Understand [[Database Normalization#^0bb316 |3NF]]
- Finish [[Indexing]]
- Practice [[Relationship Mapping]]: Create ER diagrams for a "School" or "E-commerce" schema to master Many-to-Many junctions.
```

---

### 3. Updated [[* MOC]] Structure

I recommend splitting the "Future Study" section into two distinct categories at the bottom of your MOC. This creates a clear visual path for your learning journey.

**Add this to the end of your [[* MOC]]:**

```markdown
## Growth & Roadmap

### Refinement Pipeline (Seen, but needs digestion)
- [[* Next Steps]]: Active tasks to deepen understanding of current notes.

### Learning Backlog (Unseen territory)
- [[Topics to Study]]: Concepts and questions to explore from scratch.
```

---

### Why this works:

1. **Cognitive Load**: When you have 15 minutes, you look at **[[Knowledge Refinement]]** to finish something you started. When you have 2 hours, you look at **[[Learning Backlog]]** to start something new.
2. **Naming**: Using `*` as a prefix (like in `* Next Steps`) is a good Obsidian trick to keep that file at the top of your folder, but `Knowledge Refinement` tells your brain *why* the file exists.
3. **Atomic Growth**: By keeping them in the MOC, you ensure that your "backlog" doesn't become a "black hole" where ideas go to die; they are always linked to your main Database Design map.

**Would you like me to rewrite the [[Learning Backlog]] note to categorize those specific questions into "Structural" vs. "Architectural" themes?**
[Timestamp: 2026/06/04 09:21:18]