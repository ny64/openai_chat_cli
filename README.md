# openai_chat_cli
Chat application in your terminal, built with OpenAI and Python 3

![openai_chat_cli screenshot](screenshot.png)

## Features

- Conversational history saved in Markdown files
- Multiple OpenAI model support (selectable at runtime)
- Attach files or code snippets to your prompt using `\att <filename> [from:to]` anywhere in your message
- Clean Tkinter-based text input interface
- **Quick-Reply Mode**: fire off a single prompt from your shell and get a one-off answer without opening the GUI or writing any history

## Setup

1. Install the dependencies:
   ```
   pip install -r requirements.txt
   ```
2. Set the `OPENAI_API_KEY` environment variable.
3. (Optional) Edit `occ` and adjust the `CONFIG_PATH` if you moved `config.json`.
4. Customize `config.json` (see below for key descriptions).

## Usage

### Full Conversational Mode

```bash
# Start a new conversation (auto-generated ID):
occ

# Or resume an existing conversation by ID:
occ my_conversation
```
- A Tkinter window will pop up for you to type and submit prompts.
- All prompts & replies are appended to `~/Conversations/<ID>.md`.

### Quick-Reply Mode

```bash
# Single-shot prompt, no GUI, no files:
occ -q "What’s the capital of France?"

# Or:
occ --quick How do I reverse a list in Python?
```
- Uses a dedicated `quick_model` and `quick_model_instruction` from your config.
- Prints the model’s answer to stdout and exits immediately.

### Attaching File Contents

Inside either mode you can inline file contents:

```
Here’s my code: \att path/to/script.py 5:10
```

- `\att <file>` inserts the entire file.
- `\att <file> from:to` inserts only lines `from` through `to` (1-based, inclusive).

## config.json

Below is a description of every key in your `config.json`:

```json
{
  "models": [ "...", "..." ],
  "system_message": "...",
  "quick_model": "...",
  "quick_model_instruction": "...",
  "conv_dir": null
}
```

- **models**  
  An array of model names you want available in the dropdown (e.g. `["gpt-4.1", "gpt-4.1-mini", "o1"]`).  
  The first entry is used as the default.

- **system_message**  
  The initial system prompt sent at the start of every conversation.  
  E.g. `"You are a helpful assistant."`

- **quick_model**  
  The model name to use in Quick-Reply Mode (e.g. `"gpt-4.1-mini"`).

- **quick_model_instruction**  
  An extra instruction string that is prepended *only* in Quick-Reply Mode.  
  Use this to force brevity or one-shot behavior (e.g. `"Give me a single-line answer."`).

- **conv_dir**  
  Where to store your conversation Markdown files.  
  If `null`, defaults to `~/Conversations`.
