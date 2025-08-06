## Error Handling - Managing the Unpredictable

### The Error Reality

Agents face errors at **every layer**:
- LLM generates invalid JSON
- Tools fail/timeout 
- External APIs return errors
- Network issues
- Rate limits hit

### Error Categories & Strategies

### 1. Parsing Errors (LLM → Agent)

**Invalid JSON:**
```python
try:
    parsed = json.loads(llm_response)
except JSONDecodeError:
    # Strategy: Give LLM another chance
    retry_prompt = f"Your response wasn't valid JSON. Please fix: {llm_response}"
    # Try 2-3 times, then fallback to text mode
```

**Invalid Function Call:**
```python
if function_name not in available_tools:
    error_msg = f"Tool '{function_name}' doesn't exist. Available: {tool_list}"
    # Send back to LLM with error context
```

### 2. Tool Execution Errors

**Transient Errors (Retry):**
```python
def execute_with_retry(tool, args, max_retries=3):
    for attempt in range(max_retries):
        try:
            return tool.execute(args)
        except (NetworkTimeout, RateLimited) as e:
            if attempt == max_retries - 1:
                return f"Tool failed after {max_retries} attempts: {e}"
            time.sleep(2 ** attempt)  # Exponential backoff
```

**Permanent Errors (Fallback):**
```python
def execute_search(query):
    try:
        return primary_search_api(query)
    except APIKeyInvalid:
        try:
            return fallback_search_api(query)
        except Exception:
            return "Search unavailable, please try again later"
```

### 3. LLM Error Recovery Patterns

**Graceful Degradation:**
```
Agent: "Search API is down, but I can help with general knowledge about your topic"
```

**Error Context Injection:**
```
Previous attempt failed with: "Rate limit exceeded"
Please suggest alternative approach or wait before retrying.
```

**Partial Success Handling:**
```
"I successfully sent the email but couldn't update the calendar due to authentication issues. 
Would you like me to retry the calendar update?"
```

### 4. Advanced Error Strategies

**Circuit Breaker Pattern:**
```python
class ToolCircuitBreaker:
    def __init__(self, failure_threshold=5):
        self.failures = 0
        self.threshold = failure_threshold
        self.state = "CLOSED"  # CLOSED, OPEN, HALF_OPEN
    
    def call_tool(self, tool, args):
        if self.state == "OPEN":
            return "Tool temporarily disabled due to repeated failures"
        # Execute and track success/failure
```

**Error Context Memory:**
```python
# Agent remembers: "Gmail API failed 10 minutes ago, suggest alternative"
error_history = {
    "gmail_send": {"last_failure": timestamp, "failure_count": 3},
    "weather_api": {"status": "healthy"}
}
```

### 5. User Communication Strategies

**Transparent Errors:**
```
"I tried to search for that information, but the search service is currently unavailable. 
I can try again in a few minutes or help you with something else."
```

**Progressive Degradation:**
```
"I couldn't access the real-time data, but here's what I know from my training data..."
```

### Key Principles

1. **Fail Fast**: Don't waste time on obviously broken inputs
2. **Fail Gracefully**: Always give user something useful
3. **Learn from Failures**: Track patterns to improve
4. **Be Transparent**: Users appreciate honesty about limitations

**Critical insight**: Good error handling is what separates demo agents from production-ready systems.

Ready to move to context management, or want to explore specific error scenarios?