<!-- Original FlashPaste name: Cursor: Commit Message (2 Part) -->
<!-- FlashPaste ID: 168 -->

git add . && git diff --staged > temp/git_diff.diff  # stage all + diff
git diff --staged > temp/git_diff_staged.diff        # diff staged only

[🔴run of one of above; replace this and above with empty space; drag&drop git_diff file here🔴] 
Summarize the diff into a concise commit message of ~40 words or fewer, favoring brevity over proper grammar. Use imperative mood and Conventional Commits format (`<type>[scope]: <description>`). Include scope only if changes are limited to one file or a specific component/module (auth/db/api). Write as a single line, separating multiple items with ";".

Then, looking at the diff, can you infer if there is anything that needs to be updated in the DEVELOPMENT|README|OTHER_MD🔴  file(s)? There might not be, and any additions or changes we should make should be minimal - I don't want to unecessarily bloat this file.