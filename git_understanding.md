## Merge Conflicts & Conflict Resolution
1. What caused the conflict?
The conflict occurred because the same file, OHS-Laptop-Ergonomics.md, was modified in two different branches at the exact same location before being merged. First, I created a new branch named merge_conflict and made edits to the file. Then, I switched back to the main branch and made a different, conflicting change to the exact same lines of that file. When I attempted to merge the merge_conflict branch into main, Git could not automatically decide which version to keep, resulting in a merge conflict.

2. How did you resolve it?
I resolved the conflict using my Git desktop client. The client flagged the conflicted file OHS-Laptop-Ergonomics.md and highlighted the differences between the incoming changes from the merge_conflict branch and the current changes on the main branch. I carefully reviewed both versions, selected the correct blocks of text to keep (and cleaned up any unnecessary lines), saved the file, and then committed the resolved merge before pushing the final changes to GitHub.

3. What did you learn?
This experience taught me firsthand how Git tracks changes line by line and why merge conflicts happen when collaborative work overlaps. I learned how to use a Git desktop client to easily visualize and fix conflicts instead of panicking when things break. Most importantly, I realized that to avoid painful conflicts in real-world team projects, it is essential to communicate with teammates, keep branches short-lived, and pull the latest changes from main frequently.

## Git Concepts: Staging vs. Committing
1. What is the difference between staging and committing?
- Staging: Think of the staging area (also called the "index") as a loading dock or a rough draft workspace. When you stage a file, you tell Git, it marks the changes as ready, but nothing is permanent yet.
- Committing: Committing is like sealing the shipping container or saving a permanent checkpoint in a game. When you commit, Git packages all the changes currently sitting in your staging area, assigns a unique ID (SHA-1 hash), and permanently records that snapshot into the project history.

2. Why does Git separate these two steps?
Git separates staging and committing to give developers absolute control and precision over their project history. Instead of blindly forcing you to save every single edit you made on your computer all at once, the staging area acts as a buffer. It allows you to review, organize, and curate exactly what gets grouped into a single, clean commit. 

3. When would you want to stage changes without committing?
- Splitting Unrelated Work: If you worked on fixing a bug in auth.js but also cleaned up some formatting typos in styles.css, you don't want to lump them into one messy commit message. You can stage auth.js first, commit it with a clear message, and then stage/commit styles.css separately.
- Reviewing Code Line-by-Line: Staging lets you double-check your own diffs in the Git client before making them official. You can stage individual files as you confirm they work perfectly, leaving experimental changes unstaged.
- Saving Intermediate Progress Safely: If you are halfway through a complex feature and want to freeze a working state of a specific file while you continue messing with others, you can stage it to protect that milestone without polluting the main commit log.

## Git concept: staging vs committing

1. Why is pushing directly to main problematic?
Pushing directly to the `main` branch is highly problematic for several reasons:
- Breaking Production Code: The `main` branch represents the stable, working version of the application. Committing directly increases the risk of introducing untested bugs, syntax errors, or broken code that could bring down the entire system for users or block other developers.
- Lack of Isolation: Without branches, multiple developers working on completely different features will constantly overwrite or interfere with each other's code, leading to chaotic development tracks and frequent deployment failures.

2. How do branches help with reviewing code?
Branches act as isolated parallel universes or sandboxes. They benefit code reviews by:
- Enabling Pull Requests (PRs): By keeping changes contained within a specific branch, developers can open a Pull Request to show exactly what was modified, added, or deleted compared to the `main` branch.
- Facilitating Peer Feedback: Team members can easily leave comments on specific lines of code, test the branch locally without affecting their own work, and run automated testing pipelines (CI/CD) to ensure quality before the code ever touches the production environment.

3. What happens if two people edit the same file on different branches?
If two people edit the exact same lines of the same file on different branches, Git will allow them to work and commit in isolation without any issues. However, when the time comes to merge both branches back into `main`, Git will trigger a Merge Conflict. Because Git cannot automatically deduce which version is correct, it will pause the merge and flag the overlapping lines, requiring a developer to manually review both edits, choose the desired code, and commit the resolution.