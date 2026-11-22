# rag-course

A Go command-line chat client for OpenAI-compatible APIs. It's the starting point for a course on Retrieval-Augmented Generation (RAG). Replies stream to the terminal as they're generated.

> **Status:** work in progress. The chat REPL (`chat` package) isn't written yet, and the project doesn't build right now.

## Requirements

- Go 1.27+
- An API key for OpenAI, or for any server that speaks the OpenAI Chat Completions API (for example a local model server)

## Configuration

Settings come from environment variables. A `.env` file in the working directory is loaded automatically, if one exists.

| Variable                    | Required | Default                     | Description                                   |
|-----------------------------|----------|-----------------------------|-----------------------------------------------|
| `OPENAI_API_KEY`            | yes*     | —                           | API key sent with each request                |
| `OPENAI_BASE_URL`           | no       | `https://api.openai.com/v1` | Base URL of the OpenAI-compatible API         |
| `OPENAI_MODEL`              | no       | `gpt-5-nano`                | Model name used for chat completions          |
| `OPENAI_SYSTEM_PROMPT_FILE` | no       | —                           | Path to a file with the system prompt         |

\* Local servers that don't check authentication can run without it.

Example `.env`:

```env
OPENAI_API_KEY=sk-...
OPENAI_MODEL=gpt-5-nano
OPENAI_SYSTEM_PROMPT_FILE=prompts/system.txt
```

Don't commit `.env`, since it holds your API key.

## Running

```sh
go run ./cmd/rag
```

Or build a binary:

```sh
go build -o rag ./cmd/rag
./rag
```

Press `Ctrl+C` to exit. The app shuts down cleanly on `SIGINT`/`SIGTERM`.

## Project layout

```
cmd/rag/      entry point: sets up signal handling, loads config, starts the app
app/          wires the config, LLM client and chat REPL together
config/       reads settings from the environment / .env
llm/          streaming chat-completions client built on openai-go
chat/         interactive REPL (not written yet)
```
