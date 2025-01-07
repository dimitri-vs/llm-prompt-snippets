# Cursor IDE Best Practices

A guide for maximizing productivity with Cursor IDE and LLM-assisted development.

## Project Setup

Use the `.cursorrules` file as global project directives that contain guidelines applicable to >90% of your Chat/Composer requests. See my [Cursor .cursorrules Template](cursor_cursorrules_template.md).

Use a `DEVELOPMENT.md` file to track high-level project progress and high-level business logic/decisions. See my [Cursor DEVELOPMENT.md](cursor_development_md_template.md) template.

Use a `temp/` folder as an additional context dump (meeting transcripts, specs/requirement docs, UI screenshots, etc.)

💡 Cursor makes it very easy to keep your README.md and DEVELOPMENT.md updated. For example, use the git diff to update it before a big commit or PR. Take a look at my [Cursor Commit Message (2 Part)](cursor_commit_message_2_part.md) template.

## Cursor Chat Best Practices

Check your Cursor Settings, specifically the "Model" setting. Models are updated frequently, so try out the latest and most powerful coding model for a few days to evaluate if it improves your workflow. See https://livebench.ai/ and sort by "Coding Average" to find the current top-ranked models.

You can paste in a URL to an API docs page which will create an `@mention` that will pull in the API docs as a reference.

Avoid overly long chats (>3 requests), as these can dilute the models focus. Instead, generate a TL;DR of what you wanted what the LLM has done and then start in a new thread. See my [Cursor Summarize for New Chat Session](cursor_summarize_for_new_chat_sess.md) prompt template:

```
Generate a two-paragraph summary of our session:
1. First paragraph: Describe the original request/goal using "I wanted to..." (focus on technical objectives)
2. Second paragraph: Summarize progress made using "we" (e.g., "We implemented..."), emphasizing completed actions and key decisions
Keep it concise. Brevity is preferable over proper grammar.
```

As of 2025-01 I use `claude-3-5-sonnet-latest` (aka. `claude-3-5-sonnet-20241022`) for 80% of my chat, switching to `o1` (points to `o1-preview`) when doing larger refactors or when `sonnet-latest` fails to resolve a bug after 2 attempts.

You should always review and edit the green diffs before applying, Cursor is very eager to remove your comments and delete functionality it deems "unnecessary" to the current task.

You can even get extra meta and use Ctrl+K to apply changes to green lines before accepting. 🤯

## When To Use Agentic Mode

While the original Composer mode lacks reliability, Agentic mode excels at tasks requiring multiple small changes across files or when initiating refactoring without full knowledge of required upstream/downstream changes.

⚠️ You should already be doiing this, but if you are going to use Agentic mode, make sure that you keep your code file under 500 lines. As of 2025-01, this is the maximum range that Cursor Agent can read in two attempts.

## Debugging Workflow

1. Start with sonnet and share relevant error message(s). For new threads, explain the context of when the error occurred
2. If the error persists, switch to o1-preview and resubmit your last message (like getting a second opinion)
3. Return to sonnet and request additional logging messages to help identify the error source
4. Create a new chat thread focused specifically on the error message

## Cursor for Writing & Prompt Engineering

You can use Cursor for prompt engineering! Just include the prompt in the context, say that it's an LLM prompt, and you want to slightly adjust the instructions to make it do X or make it stop doing Y.

You can use Cursor for any kind of writing, writing emails, blog posts, legal documents, etc. But I would recommend doing this as a separate "writing" project where your Cursor instructions are modified to say something like this:

```
Your previous instructions apply to all forms of writing and content creation, not just code.
For this project, interpret code-specific guidance as applying to any written content including articles, documentation, marketing copy, creative writing, and other text.
```
