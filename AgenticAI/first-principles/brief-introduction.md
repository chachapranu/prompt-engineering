## How Agents Structure Prompts for LLMs

### Basic Agent Prompt Structure

```
[SYSTEM PROMPT] - Agent's identity & capabilities
+
[CONTEXT] - Memory & conversation history  
+
[TOOLS] - Available functions with schemas
+
[USER INPUT] - Current request
+
[INSTRUCTIONS] - How to respond/format output
```

### Real Example Breakdown

**System Prompt:**
```
You are a helpful assistant that can use tools to help users.
You have access to: web_search, calculator, email_sender
```

**Tool Schemas:**
```json
{
  "name": "web_search",
  "description": "Search the internet",
  "parameters": {
    "query": {"type": "string", "description": "search terms"}
  }
}
```

**Context Window Management:**
- **Sliding window**: Keep recent conversation, drop old messages
- **Summarization**: Compress old context into summaries
- **Retrieval**: Pull relevant past info when needed

### Prompt Engineering Techniques Agents Use

**1. Chain of Thought Prompting:**
```
Think step by step:
1. What is the user asking?
2. What tools do I need?
3. What information do I have?
4. What's my plan?
```

**2. Few-Shot Examples:**
```
Example 1: User asks X → Agent thinks Y → Uses tool Z → Gets result
Example 2: User asks A → Agent thinks B → Uses tool C → Gets result
Now: User asks [current question]
```

**3. Structured Output:**
```
Respond in this format:
{
  "reasoning": "your thinking process",
  "tool_calls": [...],
  "response": "user-facing message"
}
```

### The Prompt Assembly Process

1. **Template loading** - Agent has base prompt templates
2. **Dynamic insertion** - Fills in current context, available tools
3. **Token counting** - Ensures it fits in context window
4. **Optimization** - Removes unnecessary details if too long

**Key insight**: Agents are sophisticated prompt engineers that dynamically build optimal prompts for each situation.

Want to explore how agents handle the LLM response parsing, or dive into context window management strategies?