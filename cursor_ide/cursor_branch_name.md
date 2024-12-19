<!-- Original FlashPaste name: Cursor: Branch Name -->
<!-- FlashPaste ID: 196 -->

git add . && git diff --staged > temp/git_diff.diff
git diff --staged > temp/git_diff_staged.diff

@🔴git_diff.diff
Analyze the git diff and generate a branch name following these guidelines:
- Use kebab-case (lowercase with hyphens)
- Start with a type prefix (feat/fix/refactor/chore/docs/test)
- Add a scope in brackets if changes are isolated to one component
- Keep the total length under 50 characters
- Make it descriptive but concise
- Use only alphanumeric characters and hyphens
- Format: <type>/<scope>-<description>