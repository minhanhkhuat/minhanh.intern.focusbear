# Research Best Debugging Techniques for Python



1. Most Common Debugging Techniques
- `print()` / `display()`: Fast and zero-setup, but clutters output and requires manual cleanup after debugging.
- `%debug` (Post-mortem): Drops into an interactive IPdb console immediately after an exception occurs, allowing inspection of the stack trace without re-running the cell.
- JupyterLab Visual Debugger: Provides a full IDE experience with visual breakpoints in the gutter, variable inspectors, and call stacks—ideal for stepping through execution lines visually without CLI commands.
- `icecream` (`ic()`) & `snoop`: Modern logging libraries. `icecream` formats variable names and values cleanly without verbose print statements, while `@snoop` traces line-by-line function execution automatically.

2. Effective Tools for Typical Notebook Workflows
- Out-of-Order & Stale State: Use `%reset -f` to clear workspace variables or regularly run
Kernel -> Restart & Run All to ensure reproducible, sequential execution.
- Interactive Step-by-Step Debugging: Use `%pdb on` to auto-trigger the debugger upon every exception, or `%%debug` at the top of a cell to step through line-by-line.
- Performance & Memory Profiling:**
    - `%time` and `%timeit`: Measure single-line and averaged execution time.
    -  `%prun`: Profile function execution times using `cProfile`.
    -  `%lprun` & `%memit`: Track line-by-line execution speed (`line_profiler`) and peak RAM usage (`memory_profiler`).

3. Debugging Advanced & Harder Notebook Issues
- Hidden State from Re-running Cells: Check execution order counters (`In[n]`). Avoid relying on global variables defined in out-of-order cells.
- Kernel Hangs: Interrupt the kernel (`Esc + I + I`). If unresponsible, force restart (`Esc + 0 + 0`) and check for infinite loops or unclosed IO streams.
- Memory Leaks Across Cells: Large DataFrames remain retained in GPU/RAM across execution sessions. Clear references using `del df` followed by explicit garbage collection (`import gc; gc.collect()`).
- External `.py` Modules Integration: Use `IPython` autoreload magics so external module changes load instantly without restarting the kernel:
  ```python
  %load_ext autoreload
  %autoreload 2