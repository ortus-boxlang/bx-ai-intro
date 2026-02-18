# ⚡︎ BoxLang AI Intro Examples

<img src="examples/assets/bxai-logo-full-light-L.svg" alt="bx-ai logo" width="500">

**Comprehensive Examples for the [bx-ai Module](https://github.com/ortus-boxlang/bx-ai)** – A progressive tutorial workspace showcasing everything from basic chat to advanced streaming, multimodal content, tool integration, and structured outputs.

<blockquote>
	<a href="https://ai.boxlang.io">ai.boxlang.io</a> |
	<a href="https://www.boxlang.io">www.boxlang.io</a> |
	<a href="https://boxlang.ortusbooks.com">Docs</a>
	<br>
	Copyright Since 2023 by <a href="https://www.ortussolutions.com">Ortus Solutions, Corp</a>
</blockquote>

---

## 📚 What is This?

This repository provides **progressive, hands-on examples** for learning the [bx-ai](https://github.com/ortus-boxlang/bx-ai) module — an enterprise-grade AI integration framework for BoxLang. Each example builds on previous concepts, from basic chat requests to advanced features like streaming, tool usage, and structured outputs.

**Perfect for:**

- Learning BoxLang AI capabilities incrementally
- Teaching AI integration patterns
- Prototyping AI features quickly
- Exploring different providers and models

---

## 🚀 Quick Start

### Prerequisites

- BoxLang CLI installed
  - We recommend using our BoxLang Version Manager (BVM) for easy setup: https://boxlang.ortusbooks.com/getting-started/installation/boxlang-version-manager-bvm
  - Alternatively, you can install BoxLang globally: https://boxlang.ortusbooks.com/getting-started/installation/boxlang-quick-installer
  - Or if you need a Windows installer: https://boxlang.io/download
- At least one AI provider API key (OpenAI, Claude, OpenRouter, Gemini, etc.), in the `.env` file (Make to create it from `.env.example`)

### Setup

```bash
# 1. Clone and enter the repo
git clone https://github.com/ortus-boxlang/bx-ai-intro.git
cd bx-ai-intro

#2a. Install BoxLang AI locally
install-bx-module bx-ai --local
#2b. Install BoxLang OS globally
install-bx-modules bx-ai

# 3. Create .env file with your API keys
cp .env.example .env
# Edit .env and add your API keys (e.g., OPENROUTER_API_KEY=sk-or-...)

# 4. Run any example
boxlang examples/01-basic-chat.bxs
```

---

## 📖 Progressive Examples

Each example demonstrates specific features. Run them in order to build understanding:

### Basic Chat Examples

| # | Example | Topics |
|---|---------|--------|
| 01 | [Basic Chat](examples/01-basic-chat.bxs) | Simple text prompts to AI |
| 02 | [Custom Provider](examples/02-basic-chat-custom-provider.bxs) | Override default provider/model |
| 03 | [Options & Formats](examples/03-basic-chat-options.bxs) | Logging, return formats, debugging |
| 04 | [Structured Output](examples/04-basic-chat-structured-output.bxs) | Typed responses with classes |

### Message & Conversation Examples

| # | Example | Topics |
|---|---------|--------|
| 05 | [Message Objects](examples/05-chat-with-messages.bxs) | Messages with metadata & roles |
| 06 | [Multimodal Content](examples/06-multimodal-messages.bxs) | Images, audio, and mixed content |
| 07 | [Multi-Turn Conversations](examples/07-chat-multi-turn.bxs) | Context-aware conversation loops |
| 08 | [Tool Usage](examples/08-chat-tools.bxs) | Function calling and tools |

### Streaming Examples

| # | Example | Topics |
|---|---------|--------|
| 09 | [Basic Streaming](examples/09-chat-stream.bxs) | Real-time response streaming |
| 10 | [Stream with UX](examples/10-chat-stream-ux.bxs) | Streaming with formatted output |
| 11 | [Reasoning Models](examples/11-chat-stream-with-reasoning.bxs) | Advanced reasoning with streaming |
| 12 | [Message Context](examples/12-message-context.bxs) | Managing complex conversation history |

### Pipeline Examples

| # | Example | Topics |
|---|---------|--------|
| 13 | [Basic Pipeline](examples/13-basic-pipeline.bxs) | Sequential AI operations ([Intro](examples/13-basic-pipeline.md)) |
| 14 | [Pipeline Streaming](examples/14-basic-pipeline-stream.bxs) | Pipelines with real-time output |
| 15 | [Pipeline Transformers](examples/15-pipeline-transform.bxs) | Custom and built-in transformers |
| 16 | [Pipeline Structured Output](examples/16-pipeline-structured-output.bxs) | Typed responses in pipelines |
| 17 | [Pipeline Tools](examples/17-pipeline-tools.bxs) | Function calling in pipelines |
| 18 | [Multi-Model Pipeline](examples/18-pipeline-multi-model.bxs) | Chain multiple AI models together |

### Agent Examples

| # | Example | Topics |
|---|---------|--------|
| 19 | [Basic Agent](examples/19-basic-agent.bxs) | Creating autonomous AI agents |
| 20 | [Agent Memories](examples/20-agent-memories.bxs) | Persistent memory and context recall |
| 21 | [Agent Tools](examples/21-agent-tools.bxs) | Tool-enabled agents and function execution |
| 22 | [Agent Subagents](examples/22-agent-subagents.bxs) | Delegation and multi-agent collaboration |
| 23 | [Agent Scheduler](examples/23-agent-scheduler.bx) | Scheduled and recurring agent tasks |


---

## ⚙️ Configuration

### Default Configuration (`config/boxlang.json`)

```json
{
    "modules": {
        "bxai": {
            "settings": {
                "provider": "openrouter",
                "defaultParams": {
                    "model": "stepfun/step-3.5-flash"
                },
                "timeout": 30,
                "logRequestToConsole": false,
                "returnFormat": "single"
            }
        }
    }
}
```

### API Keys (`.env`)

All providers use the pattern `<PROVIDER>_API_KEY`:

```bash
OPENAI_API_KEY=sk-...
CLAUDE_API_KEY=sk-ant-...
OPENROUTER_API_KEY=sk-or-...
GEMINI_API_KEY=...
```

See `.env.example` for all supported providers.

## 🐛 Debugging Tips

1. **Enable request logging** in `config/boxlang.json`:

   ```json
   "logRequestToConsole": true
   ```

2. **See the raw provider response**:

   ```javascript
   aiChat( "prompt", {}, { returnFormat: "raw" } )
   ```

3. **Check your API keys** - verify `.env` file has correct provider:

   ```bash
   # Common mistake: wrong provider name
   OPENROUTER_API_KEY=sk-or-...  # Exact case and spelling matters
   ```

4. **Use different return formats** for debugging:

   ```javascript
   { returnFormat: "all" }    // All messages
   { returnFormat: "json" }   // Parse as JSON
   ```

---

## 📚 Learn More

- **[bx-ai GitHub](https://github.com/ortus-boxlang/bx-ai)** – Main module repository
- **[BoxLang Docs](https://boxlang.ortusbooks.com)** – Language reference
- **[AI Module Docs](https://ai.ortusbooks.com)** – Detailed API documentation
- **[BoxLang MCP Server](https://boxlang.ortusbooks.com/~gitbook/mcp)** – Model Context Protocol integration

---

## 📝 License

Copyright Since 2023 by [Ortus Solutions, Corp](https://www.ortussolutions.com)
