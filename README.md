# openai_chat_cli
Chat application in your terminal build with OpenAI and python3

## Setup

1. Set <code>OPENAI_API_KEY</code> env variable.
2. Set _conversation directory_, _model_ and _model cost_ in the <code>occ</code> script.
3. Install [<code>glow</code> command line app](https://github.com/charmbracelet/glow) for markdown formatting or replace each <code>subprocess.run(["glow", response_file])</code> line with <code>print(response_file)</code>.
