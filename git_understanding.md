1. What is the difference between staging and committing?
- Staging: Think of the staging area (also called the "index") as a loading dock or a rough draft workspace. When you stage a file, you tell Git, it marks the changes as ready, but nothing is permanent yet.
- Committing: Committing is like sealing the shipping container or saving a permanent checkpoint in a game. When you commit, Git packages all the changes currently sitting in your staging area, assigns a unique ID (SHA-1 hash), and permanently records that snapshot into the project history.

2. Why does Git separate these two steps?
Git separates staging and committing to give developers absolute control and precision over their project history. Instead of blindly forcing you to save every single edit you made on your computer all at once, the staging area acts as a buffer. It allows you to review, organize, and curate exactly what gets grouped into a single, clean commit. 

3. When would you want to stage changes without committing?
- Splitting Unrelated Work: If you worked on fixing a bug in auth.js but also cleaned up some formatting typos in styles.css, you don't want to lump them into one messy commit message. You can stage auth.js first, commit it with a clear message, and then stage/commit styles.css separately.
- Reviewing Code Line-by-Line: Staging lets you double-check your own diffs in the Git client before making them official. You can stage individual files as you confirm they work perfectly, leaving experimental changes unstaged.
- Saving Intermediate Progress Safely: If you are halfway through a complex feature and want to freeze a working state of a specific file while you continue messing with others, you can stage it to protect that milestone without polluting the main commit log.