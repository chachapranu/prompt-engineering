## Response Parsing - The Critical Translation Step

### The Core Problem

LLMs output **unstructured text**, but agents need to execute **structured actions**.

```
LLM says: "I need to search for 'AI agents' and then calculate 2+3"
Agent needs: search("AI agents") → calculator(2, 3)
```

### Three Parsing Approaches

**1. Text Pattern Matching (Old Way)**
```python
if "search for" in response:
    query = extract_between_quotes(response)
    search(query)
```
**Problem**: Brittle, fails with slight variations

**2. Structured Prompting**
```
Always respond in this format:
ACTION: search
QUERY: "your search terms"
```
**Problem**: Still relies on LLM following format perfectly

**3. Function Calling (Modern Way)**
LLM trained to output valid JSON:
```json
{
  "function": "search",
  "arguments": {"query": "AI agents"}
}
```

### Function Calling Deep Dive

**How it works:**
1. Agent gives LLM function schemas in prompt
2. LLM decides which function(s) to call
3. LLM outputs structured JSON (not natural text)
4. Agent parses JSON → executes function → returns result to LLM

**Example Flow:**
```
User: "What's the weather in Paris?"

Agent → LLM: [prompt with weather_api schema]
LLM → Agent: {"function": "get_weather", "arguments": {"city": "Paris"}}
Agent: Executes get_weather("Paris") → "22°C, sunny"
Agent → LLM: "Weather result: 22°C, sunny"
LLM → User: "The weather in Paris is 22°C and sunny!"
```

### Error Handling in Parsing

**Common failures:**
- Invalid JSON syntax
- Function doesn't exist  
- Missing required parameters
- Parameters wrong type

**Agent strategies:**
- JSON validation before execution
- Retry with error message to LLM
- Fallback to text response if parsing fails repeatedly

**Key insight**: The agent acts as a "safety layer" between unpredictable LLM output and deterministic code execution.

Want to see how agents actually execute these parsed tool calls, or dive into specific error handling patterns?