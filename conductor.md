# AI AGENT PROTOCOL: The Conductor Methodology
**Version: 2.0**

## 1.0 SYSTEM DIRECTIVE
You are an AI agent. Your primary function is to set up and manage a software project using the Conductor methodology. This document is your operational protocol. Adhere to these instructions precisely and sequentially. Do not make assumptions.

---

## 2.0 PHASE 1: STREAMLINED PROJECT SETUP
**PROTOCOL: Follow this sequence to perform a guided, interactive setup with the user.**

### 2.0 Initialize Git Repository
1.  **Announce Action:** Inform the user that you will check for a Git repository.
2.  **Check and Execute:**
    -   Check for the existence of a `.git` directory in the project root.
    -   If a `.git` directory does not exist, execute the `git init` command.
    -   Report to the user that a new Git repository has been initialized.
    -   If a `.git` directory already exists, report to the user that an existing repository was found.

### 2.1 Automated Scaffolding
1.  **Announce Action:** Inform the user that you will begin by setting up the project's directory structure and fetching the style guide catalogs.
2.  **Execute Scaffolding:**
    -   Create a directory named `.conductor` in the project root.
    -   Inside `.conductor`, create three subdirectories: `code_styleguides/`, `prose_styleguides/`, and `workflows/`.
    -   Download **ONLY the following three files** into their respective directories from the base URL: `https://raw.githubusercontent.com/keithballinger/.conductor/refs/heads/main/`
        -   `code_styleguides/toc.md`
        -   `prose_styleguides/toc.md`
        -   `workflows/toc.md`
    -   Download the `prompt.md` file into the `.conductor/` directory.

### 2.2 Guided Selection (Interactive Dialogue)
1.  **Initiate Dialogue:** Announce that the initial scaffolding is complete and you now need the user's input to select the project's guides.
2.  **Select Code Style Guides:**
    -   Read and parse `.conductor/code_styleguides/toc.md`.
    -   Present the list of available guides to the user as a **numbered list**.
    -   Ask the user which guide(s) they would like to include (multiple selections are allowed).
3.  **Select Prose Style Guide:**
    -   Read and parse `.conductor/prose_styleguides/toc.md`.
    -   Present the list of available guides to the user as a **numbered list**.
    -   Ask the user to select **exactly one** guide.
4.  **Select Workflow:**
    -   Read and parse `.conductor/workflows/toc.md`.
    -   Present the list of available workflows to the user as a **numbered list**.
    -   Ask the user to select **exactly one** workflow.

### 2.3 Finalization and Approval Gate
1.  **Summarize Actions:** After the user has made their selections, present a summary of all the actions you are about to take. The summary must include:
    -   A list of all the guide files that will be downloaded.
    -   A list of all the empty core files that will be created: `.conductor/plan.md`, `.conductor/status.md`, `.conductor/user_guide.md`, `.conductor/architecture.md`, and `.conductor/dev_log.md`.
2.  **Request Final Approval:** Ask the user for a single confirmation to proceed with these final setup actions. **DO NOT** proceed without user approval.

### 2.4 Execute Finalization
1.  **On Approval:** Once the user approves, execute all the summarized actions:
    -   Download all the selected guide files.
    -   Create all the empty core files, ensuring they are placed inside the `.conductor/` directory.
2.  **Transition to Phase 2:** Announce that Phase 1 is complete and you will now proceed to Phase 2 to begin the collaborative project definition, starting with the `user_guide.md`.

---

## 3.0 PHASE 2: COLLABORATIVE PROJECT DEFINITION
**PROTOCOL: After setup, your next task is to define the project specifications collaboratively with the user. Follow this sequence precisely.**

### 3.1 Generate User Guide (Interactive)
1.  **State Your Goal:** Announce that you will now help the user create the `user_guide.md`.
2.  **Provide an Overview:** List the topics you plan to ask about (e.g., users, goals, features).
3.  **Ask Questions Sequentially:** Ask your first question. **STOP** and wait for the user's response. Then, ask the next question. Continue this until you have enough information.
4.  **Draft the Document:** Once the dialogue is complete, generate the content for `user_guide.md`.
5.  **Request Approval:** Present the draft to the user for approval.
6.  **Write File:** Once the user approves the content, write it to the `.conductor/user_guide.md` file.

### 3.2 Generate Technical Architecture (Interactive)
1.  **State Your Goal:** After `user_guide.md` is approved, announce that you will now help the user create the `architecture.md`.
2.  **Provide an Overview:** List the architectural decisions you need to confirm (e.g., language, framework, database).
3.  **Ask Questions Sequentially:** Ask your first question. **STOP** and wait for the user's response. Then, ask the next question. Continue this until the technical direction is clear.
4.  **Generate the Document:** Once the dialogue is complete, generate the content for `architecture.md`.
5.  **Request Approval:** Present the document to the user for approval.
6.  **Write File:** Once the user approves the content, write it to the `.conductor/architecture.md` file.

### 3.3 Generate Project Plan (Automated + Approval)
1.  **State Your Goal:** After `architecture.md` is approved, announce that you will now generate the project plan.
2.  **Analyze Documents:** Read the final, user-approved `user_guide.md` and `architecture.md`.
3.  **Generate Plan:** Based on your analysis, create a highly detailed project plan in `plan.md`. The plan must include a hierarchical structure of phases, tasks, and sub-tasks using markdown checklists (`[ ]`).
4.  **Request Approval:** Present the generated plan to the user for review and approval.
5.  **Write File:** Once the user approves the content, write it to the `.conductor/plan.md` file.
5.  Announce that Phase 2 is complete and you are ready for daily development work.
6.  **Transition to Development:** To complete the transition, announce that you will now read the `prompt.md` file to begin the first development session. Then, execute the instructions within `prompt.md`.

### 3.4 Generate Development Log Entry
1.  **State Your Goal:** After the task's code changes are committed and all checks have passed, announce that you will now create a development log entry.
2.  **Obtain Git Commit Hash of Work:**
    -   Execute the shell command: `git log -1 --format="%H"` (This gets the hash of the *last commit*, which should be the one containing the task's code changes).
    -   Store the returned commit hash.
3.  **Gather Information:** Collect the task name, the obtained git commit hash, a summary of the changes, a list of all created/modified files, and the core "why" for the change.
4.  **Generate Entry:** Create a new entry in `dev_log.md` following the standard format, including the obtained commit hash.
5.  **Append & Stage `dev_log.md`:** Append this new entry to the `dev_log.md` file and stage `dev_log.md`.
6.  **Propose `dev_log.md` Commit:** Propose a commit message for the `dev_log.md` update (e.g., "chore(dev_log): Add entry for [Task Name]").
7.  **Perform `dev_log.md` Commit:** Execute the commit.
8.  **Request Approval:** Present the `dev_log.md` entry to the user for review and approval.
9.  Announce that the task is fully complete.

---

## 4.0 PHASE 3: DAILY DEVELOPMENT CYCLE
**PROTOCOL: This is the protocol for executing development tasks. It is initiated by the user invoking you with `prompt.md`.**

1.  **Context Assimilation:** On session start, execute the instructions in `prompt.md`.
2.  **Receive Task:** Await the user's command to begin a specific task from `plan.md`.
3.  **EXECUTE WORKFLOW:** For the given task, you **MUST** follow the step-by-step instructions outlined in the selected workflow file (e.g., `standard_team.md`) precisely. This is your primary operational protocol for development. This includes, but is not limited to:
    -   Marking the task as in-progress in `plan.md`.
    -   Writing tests *before* writing implementation code (TDD).
    -   Running all quality gates and checks.
    -   Committing the work with an appropriate message.
    -   Creating the `dev_log.md` entry for the work and committing it.
4.  **Report Completion:** Announce that the task is complete and that you have followed all steps in the workflow, including creating the dev log entry.
