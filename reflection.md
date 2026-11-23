\# CSC 299 Final Project Reflection



1. In Round 2, I decided that the totals summary should only appear when analyzing two or more file paths. However, in Round 4, a fresh Claude session asked me again whether a single file should display a summary. This decision was already documented in `docs/handoffs/round-2.md` (lines 31-34) and `spec.md` (line 202). The Round 4 handoff shows the repeated question in `docs/handoffs/round-4.md` (lines 38-53). Nothing broke because I gave the same answer, but the repository could have prevented the repeated question by keeping a centralized list of finalized decisions and instructing new sessions to review it before asking questions.
2. In Round 2, I decided that the totals summary should only appear when analyzing two or more file paths. However, in Round 4, a fresh Claude session asked me again whether a single file should display a summary. This decision was already documented in `docs/handoffs/round-2.md` (lines 31-34) and `spec.md` (line 202). The Round 4 handoff shows the repeated question in `docs/handoffs/round-4.md` (lines 38-53). Nothing broke because I gave the same answer, but the repository could have prevented the repeated question by keeping a centralized list of finalized decisions and instructing new sessions to review it before asking questions.
3. In Round 3, Claude wrote a test that did not correctly check whether the longest word kept its original capitalization. The test used `self.assert\_longest(b"tiny HUGE Word", "HUGE")`, but all three words have four characters. Since R15 requires choosing the first word when lengths are tied, the correct answer would have been "tiny". Claude fixed the test in commit `1dbf9f1` by changing the input to `b"big HUGE Word"`, making "HUGE" the first longest word. This showed me why tests need to be checked carefully, because even AI-generated tests can contain mistakes.

File: `tests/test\_file\_analyzer.py`, lines 637–638.

Original test commit: `f7c7fbe`

Correction commit: `1dbf9f1`
4. I would rewrite commit `f7c7fbe`, which added the Round 3 longest-word tests. Instead of committing a test with an incorrect expectation, I would check the test inputs against the requirements first. The original test used words of equal length, which conflicted with the tie-breaking rule. I would use the corrected example from commit `1dbf9f1` and make the commit message more specific about what the tests verify.
5. \*\*Function:\*\* `list\_text\_files()` in `file\_analyzer.py`, lines 64–87.

\*\*My explanation before asking Claude:\*\*
I think the `list\_text\_files()` function finds and returns the paths of `.txt` files directly inside a directory. I'm not completely sure how it checks which files qualify or how it organizes the results.

\*\*After asking Claude:\*\*

Claude confirmed that I correctly understood the function's main purpose. What I missed was that it checks filenames without considering capitalization, makes sure each entry is a file, and sorts the results alphabetically before returning them. I also learned that it uses `os.scandir()` to look through the directory and raises an error if the directory cannot be read.





