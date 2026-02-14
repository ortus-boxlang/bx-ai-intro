# BoxLang AI Module - Presentation Examples

## Project Purpose

This is a **presentation/demo workspace** showcasing the BoxLang AI Module (`bx-ai`). It contains progressive examples demonstrating key features of the module for teaching purposes.

**Important**: This is a **BoxLang project**, not CFML. BoxLang is a modern dynamic JVM language with CFML-like syntax but is a distinct runtime. While syntax may look familiar to CFML developers, BoxLang has its own runtime, module system, and features.

## Architecture Overview

```
bx-ai-intro/
├── config/boxlang.json      # Module configuration (provider, models, settings)
├── .env                      # API keys for providers (not committed)
├── examples/                 # Progressive tutorial scripts
│   ├── 01-basic-chat.bxs
│   ├── 02-basic-chat-custom-provider.bxs
│   ├── 03-basic-chat-options.bxs
│   ├── 04-baseic-chat-structured-output.bxs
│   └── models/              # BoxLang classes for structured output
│       └── Product.bx
└── boxlang_modules/bx-ai/   # The AI module (installed via box install)
```

## Running Examples

```bash
# Run any example script directly
boxlang examples/01-basic-chat.bxs

# Scripts are numbered progressively (01, 02, 03, 04...)
# Each builds on concepts from previous examples
```

## Configuration Workflow

### 1. Provider Configuration (`config/boxlang.json`)

```javascript
{
    "modules": {
        "bxai": {
            "settings": {
                "provider": "openrouter",           // Default provider
                "defaultParams": {
                    "model": "stepfun/step-3.5-flash"  // Default model
                },
                "timeout": 30,
                "logRequestToConsole": true,        // Enable for debugging
                "logResponseToConsole": false,      // Careful: can expose sensitive data
                "returnFormat": "single"            // Options: single, all, raw, json, xml
            }
        }
    }
}
```

### 2. API Keys (`.env`)

All provider API keys follow the pattern `<PROVIDER>_API_KEY`. The module auto-detects these:

```bash
OPENAI_API_KEY=sk-...
CLAUDE_API_KEY=sk-ant-...
OPENROUTER_API_KEY=sk-or-...
GEMINI_API_KEY=...
# See .env.example for complete list
```

## Example Patterns

### Pattern 1: Basic Chat (Example 01)
```javascript
results = aiChat( "What is ColdBox?" )
println( results )
```

### Pattern 2: Custom Provider (Example 02)
```javascript
// Override default provider from config
results = aiChat( "What is ColdBox?", {}, { provider: "claude" } )

// Override provider AND model
results = aiChat(
    "What is ColdBox?",
    { model: "claude-3-haiku-20240307" },
    { provider: "claude" }
)
```

### Pattern 3: Options & Return Formats (Example 03)
```javascript
// Debugging
aiChat( "prompt", {}, { logRequestToConsole: true } )
aiChat( "prompt", {}, { logResponseToConsole: true } )

// Different return formats
aiChat( "prompt", {}, { returnFormat: "all" } )   // All messages
aiChat( "prompt", {}, { returnFormat: "raw" } )   // Raw provider response
aiChat( "prompt", {}, { returnFormat: "json" } )  // Parse as JSON
```

### Pattern 4: Structured Output (Example 04)
```javascript
// Define a class in examples/models/
class Product {
    property name="title" type="string";
    property name="price" type="numeric";
    property name="inStock" type="boolean";
}

// AI returns typed object, not plain text
var product = aiChat(
    "Extract: Wireless Mouse - $29.99 - In Stock",
    returnFormat: new Product()
)
```

## Adding New Examples

1. **Create numbered script**: `examples/05-your-feature.bxs`
2. **Follow progressive pattern**: Build on previous examples
3. **Add clear comments**: Explain what's being demonstrated
4. **Include console output**: Use `println()` or `systemOutput()`
5. **Create models if needed**: Add classes to `examples/models/` for structured output

## BoxLang Syntax Quick Reference

```javascript
// String interpolation (two styles)
"Hello, ${name}!"
"Hello, #name#"

// Array operations (functional)
items.map( i => i.toUpper() ).filter( i => i.len() > 5 )

// Elvis operator (default values)
result = value ?: "default"

// Null-safe navigation
user?.address?.city

// Scripts (.bxs) don't need class wrapper
// Just write code directly (like Python)
```

## Key Conventions

### BIF Call Signature
```javascript
aiChat( 
    prompt,           // String or aiMessage() object
    params,           // Struct: { model, temperature, max_tokens, etc. }
    options           // Struct: { provider, returnFormat, timeout, logging }
)
```

### Parameters vs Options
- **params**: Sent to the AI provider API (model, temperature, max_tokens)
- **options**: Control module behavior (provider, returnFormat, logging)

### Common Mistakes to Avoid

❌ **Wrong**: Using wrong scope for API keys
```javascript
apiKey = "sk-..."  // Don't hardcode in scripts
```

✅ **Right**: Use .env file
```bash
OPENAI_API_KEY=sk-...  # In .env file
```

❌ **Wrong**: Confusing params vs options
```javascript
aiChat( "prompt", { provider: "claude" } )  // provider is an OPTION, not param
```

✅ **Right**: Options go in third argument
```javascript
aiChat( "prompt", {}, { provider: "claude" } )
```

## Debugging Tips

1. **Enable request logging** in config: `"logRequestToConsole": true`
2. **Check provider in console**: Request shows which provider/model is used
3. **Use returnFormat: "raw"**: See full provider response for debugging
4. **Verify API keys**: Check `.env` file matches provider name exactly

## Module Reference

For deep dives into the module itself (providers, agents, memory, tools, MCP):
- See: `boxlang_modules/bx-ai/.github/copilot-instructions.md`
- Module source: `boxlang_modules/bx-ai/`
- Full docs: https://github.com/ortus-boxlang/bx-ai

### MCP (Model Context Protocol) Documentation

- **BoxLang MCP Server**: https://boxlang.ortusbooks.com/~gitbook/mcp
- **BoxLang AI MCP Integration**: https://ai.ortusbooks.com/~gitbook/mcp

## Quick Start Checklist

- [ ] Copy `.env.example` to `.env`
- [ ] Add at least one provider API key (e.g., `OPENROUTER_API_KEY`)
- [ ] Run `boxlang examples/01-basic-chat.bxs` to verify setup
- [ ] Review `config/boxlang.json` to set default provider/model
- [ ] Try other examples progressively (02, 03, 04...)
