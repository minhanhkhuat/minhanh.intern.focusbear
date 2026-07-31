# Merge Conflicts & Conflict Resolution
1. What caused the conflict?
The conflict occurred because the same file, OHS-Laptop-Ergonomics.md, was modified in two different branches at the exact same location before being merged. First, I created a new branch named merge_conflict and made edits to the file. Then, I switched back to the main branch and made a different, conflicting change to the exact same lines of that file. When I attempted to merge the merge_conflict branch into main, Git could not automatically decide which version to keep, resulting in a merge conflict.

2. How did you resolve it?
I resolved the conflict using my Git desktop client. The client flagged the conflicted file OHS-Laptop-Ergonomics.md and highlighted the differences between the incoming changes from the merge_conflict branch and the current changes on the main branch. I carefully reviewed both versions, selected the correct blocks of text to keep (and cleaned up any unnecessary lines), saved the file, and then committed the resolved merge before pushing the final changes to GitHub.

3. What did you learn?
This experience taught me firsthand how Git tracks changes line by line and why merge conflicts happen when collaborative work overlaps. I learned how to use a Git desktop client to easily visualize and fix conflicts instead of panicking when things break. Most importantly, I realized that to avoid painful conflicts in real-world team projects, it is essential to communicate with teammates, keep branches short-lived, and pull the latest changes from main frequently.

# Git Concepts: Staging vs. Committing
1. What is the difference between staging and committing?
- Staging: Think of the staging area (also called the "index") as a loading dock or a rough draft workspace. When you stage a file, you tell Git, it marks the changes as ready, but nothing is permanent yet.
- Committing: Committing is like sealing the shipping container or saving a permanent checkpoint in a game. When you commit, Git packages all the changes currently sitting in your staging area, assigns a unique ID (SHA-1 hash), and permanently records that snapshot into the project history.

2. Why does Git separate these two steps?
Git separates staging and committing to give developers absolute control and precision over their project history. Instead of blindly forcing you to save every single edit you made on your computer all at once, the staging area acts as a buffer. It allows you to review, organize, and curate exactly what gets grouped into a single, clean commit. 

3. When would you want to stage changes without committing?
- Splitting Unrelated Work: If you worked on fixing a bug in auth.js but also cleaned up some formatting typos in styles.css, you don't want to lump them into one messy commit message. You can stage auth.js first, commit it with a clear message, and then stage/commit styles.css separately.
- Reviewing Code Line-by-Line: Staging lets you double-check your own diffs in the Git client before making them official. You can stage individual files as you confirm they work perfectly, leaving experimental changes unstaged.
- Saving Intermediate Progress Safely: If you are halfway through a complex feature and want to freeze a working state of a specific file while you continue messing with others, you can stage it to protect that milestone without polluting the main commit log.

# Branching & Team Collaboration

1. Why is pushing directly to main problematic?
Pushing directly to the main branch is highly problematic for several reasons:
- Breaking Production Code: The main branch represents the stable, working version of the application. Committing directly increases the risk of introducing untested bugs, syntax errors, or broken code that could bring down the entire system for users or block other developers.
- Lack of Isolation: Without branches, multiple developers working on completely different features will constantly overwrite or interfere with each other's code, leading to chaotic development tracks and frequent deployment failures.

2. How do branches help with reviewing code?
Branches act as isolated parallel universes or sandboxes. They benefit code reviews by:
- Enabling Pull Requests (PRs): By keeping changes contained within a specific branch, developers can open a Pull Request to show exactly what was modified, added, or deleted compared to the `main` branch.
- Facilitating Peer Feedback: Team members can easily leave comments on specific lines of code, test the branch locally without affecting their own work, and run automated testing pipelines (CI/CD) to ensure quality before the code ever touches the production environment.

3. What happens if two people edit the same file on different branches?
If two people edit the exact same lines of the same file on different branches, Git will allow them to work and commit in isolation without any issues. However, when the time comes to merge both branches back into `main`, Git will trigger a Merge Conflict. Because Git cannot automatically deduce which version is correct, it will pause the merge and flag the overlapping lines, requiring a developer to manually review both edits, choose the desired code, and commit the resolution.

# Advanced Git Commands & When to Use Them

1. `git checkout main -- <file>`
- What it does: Restores a specific file from the `main` branch to your current working directory, completely overwriting any uncommitted local changes you made to that file without touching the rest of your project.
- Real-world use case: You are experimenting with code variations in a local file and it completely breaks. Instead of wasting time manually undoing your mistakes line-by-line, you use this command to instantly pull the clean, working version of that specific file straight from `main`.
- What surprised me: I was surprised by how surgical it is. It instantly wipes away local mistakes in one specific file while leaving all other modified files in my working tree completely untouched.

2. `git cherry-pick <commit-hash>`
- What it does: Applies the exact changes from a single, specific commit belonging to another branch directly onto your current active branch. It copies the change without merging the entire branch history.
- Real-world use case: A teammate fixes a critical production bug on a feature branch, but the rest of their feature isn't ready to go live yet. Instead of waiting for their entire branch to be merged, you can "cherry-pick" just the bug-fix commit and apply it straight to `main` immediately.
- What surprised me: It feels like a copy-paste tool for commits. It duplicates the exact contents and message of the chosen commit and drops it onto my active branch with a brand new commit hash.

3. `git log`
- What it does: Displays the chronological history of commits made in the repository, showing the unique commit hash, author details, date, and commit messages.
- Real-world use case: When trying to figure out when a bug was introduced or tracking the evolution of a feature, running `git log` helps you trace the project's timeline to understand the context behind past architectural decisions.
- What surprised me: The sheer amount of detail it tracks. Combining it with flags like `git log --oneline --graph` turns the chaotic terminal output into a beautiful, easy-to-read roadmap of the project's entire history.

4. `git blame <file>`
- What it does: Shows a line-by-line breakdown of a specific file, annotating every single line with the author who last modified it, the commit hash, and the timestamp.
- Real-world use case: You run into a confusing, undocumented block of code or an edge-case bug. Instead of guessing why it's there, you use `git blame` to find out exactly who wrote it and when, so you can reach out to them for context or check the original commit message.
- What surprised me: Despite the slightly aggressive name, it isn't actually about pointing fingers. It is incredibly satisfying to see exactly how a single file is a living tapestry woven by different developers over weeks or months.

# Debugging with git bisect

1. What does git bisect do?

`git bisect` uses a binary search algorithm to systematically narrow down the exact commit that introduced a bug or regression in your project history. 
- You start the process by giving Git a "bad" checkpoint (usually your current broken state) and a known "good" checkpoint (a point in the past where you are 100% sure the feature worked perfectly).
- Git then automatically splits the commit history in half and checks out a commit right in the middle. 
- You test the code at that middle commit and tell Git whether it is `good` or `bad`. Git repeats this splitting process until it isolates the exact, single commit that broke the code.

2. When would you use it in a real-world debugging situation?

You would use `git bisect` in situations where:
- The Bug Origin is Unknown: A feature that worked perfectly a few weeks ago is suddenly broken today, but nobody knows exactly when or how it happened because hundreds of commits have been merged since then.
- Complex Regressions: The codebase is massive, and tracing the source code manually or looking at standard error logs isn't immediately revealing where the structural logic broke down.

3. How does it compare to manually reviewing commits?

- Efficiency O(log n) vs O(n): Manually checking out commits one-by-line or scrolling through endless code diffs is a linear process ($O(n)$). If there are 100 commits to check, it could take hours. `git bisect` uses binary search O(log n), meaning it will pinpoint the exact broken commit out of 100 possibilities in roughly 7 steps or fewer.
- Reduces Human Error: Instead of guessing which developer's commit might have caused the issue based on vague commit messages, `git bisect` forces you to strictly rely on the physical state of the code at that exact snapshot, removing guesswork from the equation.