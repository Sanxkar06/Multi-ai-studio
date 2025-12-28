# Multi-AI-Studio

> **Multi-AI Consensus Tool**: Query multiple AI models in parallel, synthesize responses for better accuracy, and reduce AI bias through ensemble decision-making.

Multi-AI-Studio is a powerful MCP (Model Context Protocol) server that harnesses the "wisdom of crowds" by consulting multiple AI models simultaneously. Get more reliable, comprehensive answers by combining insights from OpenAI, Claude, Gemini, and any OpenAI-compatible API.

## ✨ What is Multi-ai-studio?

Multi-AI-Studio transforms how you interact with AI by:

- **🔄 Parallel Processing**: Queries multiple AI models simultaneously (not sequentially)
- **🎯 Bias Reduction**: Uses anonymous code names to prevent synthesis bias
- **⚡ Smart Synthesis**: One model synthesizes all responses into a comprehensive answer
- **🔧 Universal Compatibility**: Works with OpenAI, OpenRouter, and any OpenAI-compatible API
- **🛡️ Robust Error Handling**: Graceful degradation when individual models fail

**Perfect for**: Research questions, complex analysis, creative projects, technical decisions, and any task where multiple AI perspectives add value.

## 📋 Requirements
- Python 3.10+
- **uv** installed ([installation guide](https://docs.astral.sh/uv/getting-started/installation))
- alternatively:
  - **pipx** installed ([installation guide](https://pipx.pypa.io/stable/installation)), update config 
    ```json
      "command": "pipx",
      "args": ["run", "Multi-ai-studio"]
    ```
  - or manual install wiht `pip install ai-council`, and update config
      ```json
      "command": "Multi-ai-studio",
      "args": []
    ```

## 🚀 Quick Start

1. Get your [OpenRouter](https://openrouter.ai/) api key

### Cursor IDE Setup

2. Open Cursor Settings → MCP
3. Add new MCP server and set your api key:

```json
{
  "ai-council": {
    "command": "uvx",
    "args": ["Multi-ai-studio"],
    "env": {
      "OPENROUTER_API_KEY": "..."
    }
  }
}
```

### Claude Desktop Setup

2. Edit `~/.claude_desktop_config.json` and set your api key:

```json
{
  "mcpServers": {
    "ai-council": {
      "command": "uvx",
      "args": ["Multi-ai-studio"],
      "env": {
        "OPENROUTER_API_KEY": "..."
      }
    }
  }
}
```

**That's it!** Ask any complex question and the AI Council tool will automatically engage multiple models. 

By default it will use OpenRouter with Claude Sonnet 4, Gemini 2.5 Pro, and DeepSeek V3.

### CLI Arguments

Use command-line arguments for quick setup, add any of these to the `args` in you mcp config:

**Available CLI Arguments**:
- `--openai-api-key`: Your OpenAI API key
- `--openrouter-api-key`: Your OpenRouter API key  
- `--max-models`: Maximum models to query (default: 3)
- `--parallel-timeout`: Timeout in seconds (default: 60)
- `--log-level`: Logging level (DEBUG, INFO, WARNING, ERROR)
- `--config`: Path to custom config file

## ⚙️ Advanced Configuration

For advanced setups, create a `config.yaml` file and link to it with `--config path/to/config.yaml`:

```yaml
# config.yaml
openai_api_key: "your_openai_key_here"
openrouter_api_key: "your_openrouter_key_here"
max_models: 3
parallel_timeout: 90 # in seconds
synthesis_model_selection: "random"  # or "first"

models:
  # use OpenAI API
  - name: "GPT-4o"
    provider: "openai" 
    model_id: "gpt-4o"
    enabled: true # optional, defaults to true
    
  # use OpenRouter API
  - name: "Claude Sonnet"
    provider: "openrouter"
    model_id: "anthropic/claude-3.5-sonnet"
    code_name: "Bob" # optional, auto assigned otherwise
  
  # or any custom OpenAI compatible API
  - name: "Perplexity"
    provider: "custom"
    model_id: "llama-3.1-sonar-large-128k-online"
    base_url: "https://api.perplexity.ai"
    api_key: "your_perplexity_key_here"
    
  # Local LLM (Ollama)
  - name: "Local Llama"
    provider: "custom" 
    model_id: "llama-3b"
    base_url: "http://localhost:11434"
    api_key: "key-if-needed"
```

## 📖 How It Works

Multi-ai-studio uses a sophisticated three-phase approach:

### 1. **Parallel Consultation** 
- Simultaneously queries your configured AI models
- Maintains the same context and question for each model
- Handles failures gracefully (continues with successful responses)

### 2. **Anonymous Analysis**
- Assigns code names (Alpha, Beta, Gamma, etc.) to each model's response
- Prevents synthesis bias toward specific brands or providers
- Preserves response quality while removing model identity

### 3. **Smart Synthesis**
- Randomly selects one model to act as the synthesizer
- Synthesizer analyzes all anonymous responses
- Produces a comprehensive answer combining the best insights

## 🤝 Acknowledgments

This project was inspired by [Cognition Wheel](https://github.com/Hormold/cognition-wheel).

Multi-ai-studio extends these ideas with:
- Enhanced configuration flexibility  
- OpenRouter support for many model options with a single api key
- Support for custom API endpoints
- Improved error handling and logging
- Using Python

