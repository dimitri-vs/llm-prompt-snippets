<!-- Original FlashPaste name: Cursor: .cursorrules Template -->
<!-- FlashPaste ID: 193 -->

This project is an [business or industry]'s [project type] intended to [goal / problem to solve] for the [intended user].

**Tech Stack**

- Frontend: 
- Backend: 
- UI Components:
  - ...
- Hosting: 
- Database: 
- Authentication: 
- Core Third Party APIs:
  - ...

**Cursor Guidelines**

When writing out lists in .md files, I strongly prefer longer, multi-sentence bullet points with an emphasis on information density over grammar. I also like to mix in sentences and paragraphs to make the content more readable and engaging rather than just having lists of lists.

It's very important to preserve and include any nearby comments in the code edits in your responses, updating them as needed.
If the reference code contains or is near "TODO:", "NOTE:", or "IMPORTANT:" comments, always include them in your response code.
Example: Given code with `#NOTE: Business logic\n\n\ndef calc():...`, respond with updated code as `// ... #NOTE: Business logic {{ updated_code }} // ...`

Use functional programming patterns over object-oriented programming paradigms, where applicable.

When adding or inserting functions, use the "stepdown rule" approach, starting with the high-level business logic functions that tell the main story at the top, then progressing to lower-level details later.

When asked to do a database migration, write a migration function that can be run in the `main` block unless otherwise specified, including highly visible warnings about irreversible operations and concise safety recommendations for testing and rollback. For non-backwards compatible changes (e.g., dropping columns, changing nullability), add a very prominent "⚠️ BREAKING CHANGE" warning with rollout steps to prevent production downtime.

If the code you are writing or editing has functions that have many lines of complex code for calculations, data processing, external dependencies, or critical business rules in any non-trivial way, consider writing a test for it. Prefix this suggestion in your response with a "💡" emoji.

To minimize maintenance burden, when writing tests keep them small, simple and minimal unless specifically requested otherwise. Be sure to concisely document each test function with a single-sentence docstring explaining their testing intent.