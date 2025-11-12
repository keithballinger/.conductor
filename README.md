# .conductor: An AI-Driven Project Management Framework

Welcome to Conductor, a structured system for managing software projects with an AI agent like the Gemini CLI.

The core philosophy is to provide the AI with a clear, unambiguous **protocol** to follow, turning it from a simple coding assistant into a proactive project manager. This system ensures a consistent, high-quality development process from initial setup to daily work.

## How It Works

The Conductor methodology is divided into two main phases:

1.  **Phase 1: Guided Setup:** A one-time, interactive process where the AI acts as a setup wizard. It scaffolds the project structure, helps you select the appropriate style guides and workflows, and creates the core project management files.
2.  **Phase 2: Daily Development:** For all subsequent interactions, the AI uses the `.conductor/prompt.md` file to re-assimilate the project's context and rules, ensuring it always adheres to the established workflow for every task.

---

## Getting Started

To use the Conductor methodology, you will use one of the two prompts below, depending on your project's state.

### Initial Project Setup

To be used **once** in a new, empty project directory. This prompt instructs the AI to fetch the master protocol and begin the guided setup wizard.

**Launch the Gemini CLI with the following command:**

```bash
gemini -i "I want to set up this project using the Conductor methodology. Your instructions are in the protocol file located at https://raw.githubusercontent.com/keithballinger/.conductor/refs/heads/main/conductor.md. Please begin the setup process." --yolo
```

### Daily Development Workflow

After the initial setup is complete, use this prompt **every time** you start a new work session. It directs the AI to read the local `prompt.md` file, understand the project's context, and prepare for the day's tasks.

**Launch the Gemini CLI with the following command:**

```bash
gemini -i "Start my development session by following the instructions in .conductor/prompt.md." --yolo
```

---

## Core Files

-   **`conductor.md`**: The master protocol file used only for the initial project setup.
-   **`prompt.md`**: The entry point for all daily development sessions.
-   **`plan.md`**: The AI-generated, human-approved project plan with phases and tasks.
-   **`dev_log.md`**: A detailed, chronological log of all changes made to the codebase.
-   **`code_styleguides/`**: Contains the selected code style guides for the project.
-   **`prose_styleguides/`**: Contains the selected prose style guide for all written content.
-   **`workflows/`**: Contains the selected workflow protocol that the AI must follow for all tasks.