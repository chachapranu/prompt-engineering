## Context Management - The Memory Challenge

### The Fundamental Problem

**LLMs have fixed context windows** (e.g., 8K, 32K, 128K tokens), but conversations can be unlimited length.

```
Token limits: GPT-4: ~8K tokens | Claude: ~200K tokens | Gemini: ~1M tokens
Real conversations: Can easily exceed any limit
```

### Core Strategies

### 1. Sliding Window (Simple)

**Keep recent, drop old:**
```python
def manage_context(messages, max_tokens=8000):
    current_tokens = count_tokens(messages)
    
    while current_tokens > max_tokens:
        messages.pop(1)  # Remove oldest (keep system prompt)
        current_tokens = count_tokens(messages)
    
    return messages
```

**Pros**: Simple, preserves recent context
**Cons**: Loses important early information

### 2. Summarization (Intelligent Compression)

**Compress old context:**
```python
def compress_context(old_messages):
    summary_prompt = """
    Summarize this conversation history in 200 tokens:
    Key decisions made, important facts established, user preferences.
    """
    
    summary = llm.generate(summary_prompt + old_messages)
    return summary  # Replace 50 messages with 1 summary
```

**Example:**
```
Original (1000 tokens): "User asked about AI agents... discussed tools... explained parsing..."
Summary (100 tokens): "User learning AI agents fundamentals. Covered: agents, tools, parsing, execution. Currently on: context management."
```

### 3. Retrieval-Based Memory

**Store & retrieve relevant context:**
```python
class ContextStore:
    def __init__(self):
        self.memories = []  # Vector database
    
    def store(self, content, metadata):
        embedding = get_embedding(content)
        self.memories.append({
            'content': content,
            'embedding': embedding,
            'timestamp': now(),
            'metadata': metadata
        })
    
    def retrieve_relevant(self, query, limit=5):
        query_embedding = get_embedding(query)
        # Find most similar memories by cosine similarity
        relevant = find_similar(query_embedding, self.memories, limit)
        return relevant
```

### 4. Hierarchical Memory

**Different memory types:**
```
Working Memory: Current conversation (high priority)
Episodic Memory: Past conversation summaries (medium priority)
Semantic Memory: Facts about user/domain (permanent)
Procedural Memory: How to use tools (permanent)
```

### 5. Smart Context Assembly

**Dynamic context building:**
```python
def build_context(user_query):
    context = []
    
    # Always include
    context.append(system_prompt)  # 200 tokens
    context.append(recent_messages)  # 2000 tokens
    
    # Conditionally include based on query
    if needs_user_history(user_query):
        context.append(get_user_summary())  # 300 tokens
    
    if needs_tool_context(user_query):
        context.append(recent_tool_results)  # 500 tokens
    
    # Fill remaining space with relevant memories
    remaining_tokens = max_tokens - count_tokens(context)
    relevant_memories = retrieve_memories(user_query, remaining_tokens)
    context.extend(relevant_memories)
    
    return context
```

### Real-World Challenges

**1. Token Counting Accuracy:**
```python
# Different models tokenize differently!
gpt4_tokens = len(gpt4_tokenizer.encode(text))
claude_tokens = len(claude_tokenizer.encode(text))  # Could be different!
```

**2. Context Boundary Problems:**
```
Middle of important conversation gets cut off
Tool result from 5 messages ago becomes irrelevant
User reference to "that thing we discussed earlier" breaks
```

**3. Multi-Turn Tool Usage:**
```
Turn 1: User asks complex question
Turn 2: Agent searches web
Turn 3: Agent processes results  
Turn 4: User asks follow-up referencing search results
# Context must preserve tool results for follow-up!
```

### Advanced Patterns

**Context Compression:**
```python
# Instead of dropping messages, compress them
compress_old_context() → 90% token reduction, keeps key info
```

**Context Routing:**
```python
# Different context for different tasks
if task == "coding":
    include_code_history()
elif task == "research":
    include_search_results()
```

**Key insight**: Context management is the bottleneck that determines how "intelligent" an agent appears over long conversations.

Ready for advanced orchestration patterns, or want to dive deeper into any specific context strategy?