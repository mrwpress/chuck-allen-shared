---
name: Git Workflow & Autonomy
description: Never push to main directly — always branch → PR → merge. Claude has full autonomy within this project.
type: feedback
---

**Never push directly to main.** All changes go through: branch → PR → approve and merge.

**Full autonomy granted** within /Users/batman/Sites/chuck-allen/ and all subfolders. No need to ask permission for:
- Creating/editing/deleting files
- Creating branches, commits, PRs
- Running builds, installs, dev servers
- Any operation within this project directory

**Only ask** when an action touches the file system outside of this project.

**Why:** GitHub provides full version history, branches, and reverts — the safety net is already in place. Asking for confirmation on routine operations slows things down unnecessarily.

**How to apply:** Work confidently and move fast. Always create a feature branch, commit there, push, and open a PR. Never `git push origin main`.
