# The Conductor Methodology: A Guide to Orchestrated Project Management

This document outlines the "Conductor" methodology, a structured system for managing complex projects with a focus on clarity, consistency, and quality. It's designed to keep projects on track, whether you're working solo, with a team, or directing an AI collaborator.

The core philosophy is simple: **A well-defined process frees you to focus on creative, high-quality work.**

Just like a conductor leads an orchestra, this system ensures every component of your project—from the grand vision to the tiniest code snippet—works in perfect harmony.

---

## The `.conductor` Directory: Your Project's Cockpit

At the heart of this methodology is a directory named `.conductor/`. This folder contains the "sheet music" for your project, defining the plan, the rules, and the workflow.

Here are the six essential files that make up the Conductor system:

### 1. `plan.md`: The Master Blueprint

This is the single source of truth for what the project aims to achieve. It's a living document that outlines the entire scope of work, broken down into phases and actionable tasks.

-   **Purpose:** To define the project's goals and provide a clear, hierarchical task list.
-   **Structure:** Use checklists (`[ ]`, `[~]`, `[x]`) to track the status of major phases and individual tasks. This makes it easy to see progress at a glance.
-   **Key Feature:** It's the "what" and the "why" of your project. Every major piece of work should be represented here before you begin.

> **For a New Project:** Start by outlining the major phases or features. You don't need every detail at first, but you need a clear roadmap.

### 2. `prose_styleguide.md`: Defining the Voice

This file establishes the personality and tone of all written content. It ensures that whether you're writing documentation, UI text, or commit messages, the voice remains consistent.

-   **Purpose:** To create a unified, intentional voice for the project.
-   **Structure:**
    -   Define a **Core Voice** or **Persona** (e.g., "The Accessible Expert").
    -   Provide guiding principles with clear "DO" and "DON'T" examples.
    -   Include sections on formatting, tone, and specific stylistic choices (like using analogies).
    -   Define callout boxes or special formatting to highlight information.
-   **Key Feature:** It turns writing from an arbitrary task into a systematic one, ensuring quality and consistency.

### 3. `code_styleguide.md`: Enforcing Code Consistency

This document is the PEP 8 for your project. It defines the rules for all code, ensuring it's readable, maintainable, and consistent, no matter who writes it.

-   **Purpose:** To ensure all code is clean, clear, and follows a single, predictable style.
-   **Structure:**
    -   State a **Core Principle** (e.g., "Clarity Over Cleverness").
    -   Link to base style guides (like PEP 8) and then add project-specific overrides or additions.
    -   Cover naming conventions, import order, comment style, and example structure.
-   **Key Feature:** It eliminates style debates and makes the codebase feel like it was written by a single, disciplined mind.

### 4. `workflow.md`: The Rules of Engagement

This is the most critical file for execution. It defines the step-by-step process for getting work done. It's the "how" that complements the "what" of the `plan.md`.

-   **Purpose:** To create a predictable, repeatable process for moving a task from "to-do" to "done."
-   **Structure:**
    -   Outline **Guiding Principles** for the workflow.
    -   Define a clear **Task Workflow** (e.g., Select Task -> Mark In Progress -> Revise -> Build -> Request Review -> Mark Done).
    -   Establish **Quality Gates**, such as requiring a peer or AI review before a task can be marked as complete.
    -   Specify a **Definition of Done**—a checklist that must be satisfied for a task to be considered truly finished.
-   **Key Feature:** It enforces discipline and ensures that every task meets the project's quality standards.

### 5. `status.md`: The Project Dashboard

This file provides a real-time snapshot of the project's status. It's designed to be updated at the end of every work session.

-   **Purpose:** To communicate the current state of the project quickly and efficiently.
-   **Structure:**
    -   **As of:** The date of the last update.
    -   **Project Status:** A high-level summary (e.g., "In Progress").
    -   **Current Phase:** The phase from `plan.md` that is currently active.
    -   **Current Task:** The specific task being worked on.
    -   **Next Action:** What needs to happen next (e.g., "Incorporate feedback," "Submit for review").
-   **Key Feature:** It prevents you from losing context between work sessions and keeps all stakeholders informed.

### 6. `prompt.md`: The Mission Briefing

This file is the starting point for any contributor, especially an AI. It sets the context, defines the persona, and points to the other Conductor files.

-   **Purpose:** To quickly orient anyone new to the project, ensuring they understand the goals and processes from the outset.
-   **Structure:**
    -   A clear mission statement.
    -   A **CRITICAL** section that instructs the user (or AI) to read the other Conductor files in a specific order.
    -   A summary of the **Persona** to be adopted.
    -   A "What I need help with today" section to frame the immediate task.
-   **Key Feature:** It's the ultimate "read me first" document that bootstraps the entire workflow.

### 7. `user_guide.md`: The What

A document outlining the user experience of what we are building. This should be highly detailed. As me questions to help you create this. You MUST ask at least 10 questions.

### 8. `architecture.md`: The How

This is a detailed technical spec. Ask me at least 5 questions to help you write this.

---

## How to Use the Conductor Methodology on Any Project

1.  **Create the `.conductor` Directory:** In your project's root, create a new folder named `.conductor`.

2.  **Create the Six Core Files:** Create empty markdown files for `plan.md`, `prose_styleguide.md`, `code_styleguide.md`, `workflow.md`, `status.md`, and `prompt.md`.

3.  **Start with the Plan and Prompt:**
    -   In `plan.md`, sketch out the high-level goals and phases of your project.
    -   In `prompt.md`, write a mission statement. What is this project trying to achieve?

4.  **Define Your Style and Workflow:**
    -   Flesh out the `prose_styleguide.md` and `code_styleguide.md`. Even a few simple rules are better than none.
    -   Define a simple `workflow.md`. It can be as easy as "Plan -> Do -> Review."

5.  **Follow the Process:**
    -   Before starting work, update your `status.md`.
    -   Consult your `plan.md` to choose a task.
    -   Follow your `workflow.md` to complete the task.
    -   Adhere to your style guides as you work.
    -   At the end of your session, update `status.md` again.

By following this orchestrated process, you ensure that every contribution is thoughtful, consistent, and high-quality, turning project chaos into a beautiful symphony.
