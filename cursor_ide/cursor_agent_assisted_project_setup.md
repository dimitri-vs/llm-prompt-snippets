<!-- Original FlashPaste name: Cursor: Agent Assisted Project Setup -->
<!-- FlashPaste ID: 207 -->

<!-- Okay, let's get this project set up. Please refer to the project-setup.md document throughout this process, and then any time you see the "🛑" or references like "@Cursor agent", please follow those instructions. You don't need to include emojis in your response. -->

1. **Create a .cursorrules file**

```
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
```

2. **🛑 @Cursor agent: Stop here and ask the user to review and update the .cursorrules file. Remind the user how important it is that their .cursorrules file is accurate to their needs and reviewed frequently as the project evolves. Use gratuitous emojis here (just here).**

3. **Review the updated project info and tech stack outlined in the .cursorrules file, create an appropriate requirements.txt file**

Example for a python Streamlit project. Note how required packages are uncommented and suggested/optional packages are commented out.
```
# for adding new packages, add a locked version here and then run `uv pip install -r requirements.txt`
python-dotenv==1.0.0
streamlit==1.42.2
pandas==2.2.3
requests==2.31.0
authlib==1.3.2  # Needed for Streamlit OAuth 2.0

# Database
sqlalchemy==2.0.35
psycopg2-binary==2.9.9  # to connect to postgres

# AI API clients
litellm==1.55.3 # for easy model-provider switching
# openai==1.30.1
# anthropic==0.42.0
# google-cloud-aiplatform==1.42.1

# Utilities/Services
slack_sdk==3.34.0 # for sending messages as a slack bot
```

4. **🛑 @Cursor agent: Stop here and allow for the user to review the requirements.txt file**

5. **Create a .env file with placeholder variable names that might be appropriate for the project**

```
OPENAI_API_KEY=
ANTHROPIC_API_KEY=
```

6. **Create an appropriate README.md file, one that contains somethign like this (project dependant):**

```
# [project name]

[project description]

## Project Structure

[recommended minimal project structure, example below]

```
[project name]/
├── tasks/              # Background and scheduled tasks
│   ├── scheduler.py    # APScheduler configuration
│   ├── processor.py
│   └── health_monitor.py
├── db/                 # Database layer
│   ├── ...
│   └── ...
├── services/           # External API clients
│   ├── ...
│   └── ...
├── utils/             # Shared utilities
│   ├── ...
│   └── ...
├── frontend/          # Streamlit frontend
│   └── app.py
├── tests/             # Test suite
├── requirements.txt
├── .env
├── .gitignore
├── .cursorrules
└── README.md
```

## Running & Developing the Project Locally

[@Cursor agent: Keep this section minimal, compact, but junior-dev-friendly - very similar to how it's shown here.]

### Initial Setup
Requires Python 3.9 or higher (check with `python --version`)
Requires `uv` CLI tool (https://docs.astral.sh/uv/getting-started/#installation)
- Create a virtual environment using `uv venv --python ">=3.9"`
- Always run `.venv\Scripts\activate` to activate the virtual environment (setup your IDE to do it automatically)
- Run `uv pip install -r requirements.txt` to install all dependencies
- Run `streamlit run frontend/app.py` to start the server

### Ongoing Development
- Run `.venv\Scripts\activate` to activate the virtual environment
- ⚠️ Always activate the virtual environment before running any commands
- Run `streamlit run frontend/app.py` to start the server
- To check for package updates, run `pip list --outdated`
- To add new packages, first add it to `requirements.txt` then run `uv pip install -r requirements.txt`

### Database Management
- The application uses SQLAlchemy with PostgreSQL
- Database migrations are handled through custom migration scripts in the `db/migrations` directory
```

7. **🛑 @Cursor agent: Stop here and allow for the user to review and update the README.md file**

8. **Create a .gitignore file with the appropriate contents**

Example for style and formatting:

```
<{When using this template, make sure not to create too many new top-level categories.}>
########################################################################
# Project Specific
########################################################################

# Add your local project specific .gitignore rules here

# === Temporary Files ===
temp/ # <Always add this folder to the .gitignore file>


########################################################################
# Environment, System, IDE Files
########################################################################

# === Environment files ===
.env
.env.*
!.env.example
env/
venv/

# === IDE and Editor files ===
.vscode
*.suo
*.ntvs*
*.njsproj
*.sln
*.sw?
.idea/

# === Mac system files ===
.DS_Store

# === Common Windows Files ===
Thumbs.db
Desktop.ini

########################################################################
# <Framework-Specific>
########################################################################

; ...


########################################################################
# <Language-Specific>
########################################################################

; ...
```

9. **Using the updated README.md file's content for guidance, assist the user with the initial setup of the project and directory creation, but do not create the files yet**

10. **Initialize the git repository**

11. **Verify everything above has been completed correctly**