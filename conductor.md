
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
