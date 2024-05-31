# Commands and Interfaces for the `fabric` Project

## Overview

The `fabric` project is an open-source framework for augmenting humans using AI. This document provides a comprehensive list of commands and interfaces available for users to interact with the `fabric` project.

## Quickstart

### Setting up the `fabric` Client

1. Navigate to where you want the Fabric project to live on your system.

```bash
cd /where/you/keep/code
```

2. Clone the project to your computer.

```bash
git clone https://github.com/danielmiessler/fabric.git
```

3. Enter Fabric's main directory

```bash
cd fabric
```

4. Install pipx:

macOS:

```bash
brew install pipx
```

Linux:

```bash
sudo apt install pipx
```

Windows:

Use WSL and follow the Linux instructions.

5. Install fabric

```bash
pipx install .
```

6. Run setup:

```bash
fabric --setup
```

7. Restart your shell to reload everything.

8. Test the installation:

```bash
fabric --help
```

## Using the `fabric` Client

### Environment Variables

Set up the following environment variables for OpenAI API compatible inference servers:

```bash
export OPENAI_BASE_URL=https://YOUR-SERVER:8000/v1/
export DEFAULT_MODEL="YOUR_MODEL"
export OPENAI_API_KEY="YOUR TOKEN"
```

### Command-Line Options

```bash
usage: fabric -h
usage: fabric [-h] [--text TEXT] [--copy] [--agents] [--output [OUTPUT]] [--session [SESSION]] [--gui] [--stream] [--list] [--temp TEMP] [--top_p TOP_P] [--frequency_penalty FREQUENCY_PENALTY]
              [--presence_penalty PRESENCE_PENALTY] [--update] [--pattern PATTERN] [--setup] [--changeDefaultModel CHANGEDEFAULTMODEL] [--model MODEL] [--listmodels]
              [--remoteOllamaServer REMOTEOLLAMASERVER] [--context]

An open source framework for augmenting humans using AI.

options:
  -h, --help            show this help message and exit
  --text TEXT, -t TEXT  Text to extract summary from
  --copy, -C            Copy the response to the clipboard
  --agents, -a          Use praisonAI to create an AI agent and then use it. ex: 'write me a movie script'
  --output [OUTPUT], -o [OUTPUT]
                        Save the response to a file
  --session [SESSION], -S [SESSION]
                        Continue your previous conversation. Default is your previous conversation
  --gui                 Use the GUI (Node and npm need to be installed)
  --stream, -s          Use this option if you want to see the results in realtime. NOTE: You will not be able to pipe the output into another command.
  --list, -l            List available patterns
  --temp TEMP           set the temperature for the model. Default is 0
  --top_p TOP_P         set the top_p for the model. Default is 1
  --frequency_penalty FREQUENCY_PENALTY
                        set the frequency penalty for the model. Default is 0.1
  --presence_penalty PRESENCE_PENALTY
                        set the presence penalty for the model. Default is 0.1
  --update, -u          Update patterns. NOTE: This will revert the default model to gpt4-turbo. please run --changeDefaultModel to once again set default model
  --pattern PATTERN, -p PATTERN
                        The pattern (prompt) to use
  --setup               Set up your fabric instance
  --changeDefaultModel CHANGEDEFAULTMODEL
                        Change the default model. For a list of available models, use the --listmodels flag.
  --model MODEL, -m MODEL
                        Select the model to use
  --listmodels          List all available models
  --remoteOllamaServer REMOTEOLLAMASERVER
                        The URL of the remote ollamaserver to use. ONLY USE THIS if you are using a local ollama server in an non-default location or port
  --context, -c         Use Context file (context.md) to add context to your pattern
```

### Example Commands

1. Run the `summarize` Pattern based on input from `stdin`.

```bash
pbpaste | fabric --pattern summarize
```

2. Run the `analyze_claims` Pattern with the `--stream` option.

```bash
pbpaste | fabric --stream --pattern analyze_claims
```

3. Run the `extract_wisdom` Pattern with the `--stream` option from a YouTube video.

```bash
yt --transcript https://youtube.com/watch?v=uXs-zPc63kM | fabric --stream --pattern extract_wisdom
```

4. Use aliases for patterns in the bash or zsh config file.

```bash
pbpaste | analyze_claims --stream
```

## Custom Patterns

Store custom patterns in `~/.config/custom-fabric-patterns` and copy them to `~/.config/fabric/patterns` when needed.

```bash
cp -a ~/.config/custom-fabric-patterns/* ~/.config/fabric/patterns/
```

Run custom patterns with:

```bash
pbpaste | fabric -p your_custom_pattern
```

## Agents

Create AI agents using PraisonAI.

```bash
echo "Search for recent articles about the future of AI and write me a 500-word essay on the findings" | fabric --agents
```

## Helper Apps

### yt (YouTube)

Use the `yt` command to interact with the YouTube API.

```bash
usage: yt [-h] [--duration] [--transcript] [url]

positional arguments:
  url           YouTube video URL

options:
  -h, --help    Show this help message and exit
  --duration    Output only the duration
  --transcript  Output only the transcript
  --comments    Output only the user comments
```

### ts (Audio transcriptions)

Use the `ts` command to transcribe audio files using the OpenAI Whisper API.

```bash
ts -h
usage: ts [-h] audio_file

Transcribe an audio file.

positional arguments:
  audio_file  The path to the audio file to be transcribed.

options:
  -h, --help  show this help message and exit
```

### Save

Use the `save` command to pipeline saving of content while keeping the output stream intact.

```bash
usage: save [-h] [-t, TAG] [-n] [-s] [stub]

positional arguments:
  stub                stub to describe your content. Use quotes if you have spaces. Resulting format is YYYY-MM-DD-stub.md by default

options:
  -h, --help          show this help message and exit
  -t, TAG, --tag TAG  add an additional frontmatter tag. Use this argument multiple times for multiple tags
  -n, --nofabric      don't use the fabric tags, only use tags from --tag
  -s, --silent        don't use STDOUT for output, only save to the file
```

Example:

```bash
echo test | save --tag extra-tag stub-for-name
test

$ cat ~/obsidian/Fabric/2024-03-02-stub-for-name.md
---
generation_date: 2024-03-02 10:43
tags: fabric-extraction stub-for-name extra-tag
---
test
```
