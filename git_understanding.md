1. What caused the conflict?
The conflict occurred because the same file, OHS-Laptop-Ergonomics.md, was modified in two different branches at the exact same location before being merged. First, I created a new branch named merge_conflict and made edits to the file. Then, I switched back to the main branch and made a different, conflicting change to the exact same lines of that file. When I attempted to merge the merge_conflict branch into main, Git could not automatically decide which version to keep, resulting in a merge conflict.

2. How did you resolve it?
I resolved the conflict using my Git desktop client. The client flagged the conflicted file OHS-Laptop-Ergonomics.md and highlighted the differences between the incoming changes from the merge_conflict branch and the current changes on the main branch. I carefully reviewed both versions, selected the correct blocks of text to keep (and cleaned up any unnecessary lines), saved the file, and then committed the resolved merge before pushing the final changes to GitHub.

3. What did you learn?
This experience taught me firsthand how Git tracks changes line by line and why merge conflicts happen when collaborative work overlaps. I learned how to use a Git desktop client to easily visualize and fix conflicts instead of panicking when things break. Most importantly, I realized that to avoid painful conflicts in real-world team projects, it is essential to communicate with teammates, keep branches short-lived, and pull the latest changes from main frequently.
