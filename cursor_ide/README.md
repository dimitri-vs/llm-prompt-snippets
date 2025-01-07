# Cursor IDE Best Practices

A guide for maximizing productivity with Cursor IDE and LLM-assisted development.

## Project Setup

Use the `.cursorrules` file as a global project directives that contain guidelines relevant to >90% of your Chat/Composer requests. See my [Cursor .cursorrules Template](cursor_cursorrules_template.md).

Use a `DEVELOPMENT.md` file to track high-level project progress and high-level business logic/decisions. See my [Cursor DEVELOPMENT.md](cursor_development_md_template.md) template.

Use a `temp/` folder as an additional context dump (meeting transcripts, specs/requirement docs, UI screenshots, etc.)

💡 Cursor makes it very easy to keep your README.md and DEVELOPMENT.md updated. For example, use the git diff to update it before a big commit or PR. Take a look at my [Cursor Commit Message (2 Part)](cursor_commit_message_2_part.md) template.

## Cursor Chat Best Practices

Check your Cursor Settings, specifically the "Model" setting. Models get updated frequently and you should try out the latest and most powerful coding model for a day or two to see if it's better for you. See https://livebench.ai/ and sort by "Coding Average" to find whats currently ranked best.

You can paste in a URL to an API docs page which will create an `@mention` that will pull in the API docs as a reference.

Avoid overly long chats (>3 requests), as these can dilute the models focus. Instead, generate a TL;DR of what you wanted what the LLM has done and then start in a new thread. See my [Cursor Summarize for New Chat Session](cursor_summarize_for_new_chat_sess.md) prompt template:

```
Generate a two-paragraph summary of our session:
1. First paragraph: Describe the original request/goal using "I wanted to..." (focus on technical objectives)
2. Second paragraph: Summarize progress made using "we" (e.g., "We implemented..."), emphasizing completed actions and key decisions
Keep it concise. Brevity is preferable over proper grammar.
```

As of 2024-12 I use `claude-3-5-sonnet-latest` (aka. `claude-3-5-sonnet-20241022`) for 80% of my chat, switching to `o1` when doing larger refactors or when `sonnet-latest` fails to resolve a bug after 2 attempts.

You should always review and edit the green diffs before applying, Cursor is very eager to remove your comments and delete functionality it deems "unnecessary" to the current task.

You can even get extra meta and use Ctrl+K to apply changes to green lines before accepting. 🤯

## When To Use Agentic Mode

The original Composer mode isn't anywhere reliable enough, but the Agentic mode is really great for when you need to do something that requires a lot of small changes across a lot of files or as a starting point for a refactoring when you don't really know what upstream/downstream changes are required.

## Debugging Workflow

1. Use sonnet, share relavant error message(s), if new thread explain what I was doing when I got the error message
2. Use sonnet again in same thread, most of the time it will figure it out on the second try
3. Switch to o1-preview on last message and resubmit, kind of like getting a second opinion
4. Switch back to sonnet ask it to add logging messages to help narrow down the source of the issue

## Cursor for Writing & Prompt Engineering

You can use Cursor for prompt engineering! Just include the prompt in the context, say that it's an LLM prompt, and you want to slightly adjust the instructions to make it do X or make it stop doing Y.

You can use Cursor for any kind of writing, writing emails, blog posts, legal documents, etc. But I would recommend doing this as a separate "writing" project where your Cursor instructions are modified to say something like this:

```
Your previous instructions apply to all forms of writing and content creation, not just code.
For this project, interpret code-specific guidance as applying to any written content including articles, documentation, marketing copy, creative writing, and other text.
```
