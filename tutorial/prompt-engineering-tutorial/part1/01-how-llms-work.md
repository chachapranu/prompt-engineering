# 1.1 How LLMs Actually Work (20 minutes)

## Core Concept

Large Language Models (LLMs) are sophisticated next-token prediction systems. Every time you send a prompt, the model calculates probability distributions over its entire vocabulary to determine what word (token) should come next, then repeats this process to generate a complete response.

**Key Insight:** LLMs don't "understand" in the human sense—they predict what text should follow based on patterns learned from training data.

## How Prompts Shift Probability Distributions

### The Prediction Process

When you provide a prompt, the LLM:

1. **Tokenizes** your input (splits text into tokens)
2. **Calculates probabilities** for every possible next token
3. **Samples** from this distribution (usually with some randomness)
4. **Repeats** until it generates a complete response

### Example: Probability Shifting in Action

**Prompt:** "The capital of France is"

Without context, the model might assign probabilities like:
- "Paris" (85%)
- "located" (10%)
- "a" (3%)
- Other tokens (2%)

**Prompt:** "In the 1800s, the capital of France was"

Now the probabilities shift:
- "Paris" (70%)
- "still" (15%)
- "already" (10%)
- Other tokens (5%)

**Why This Matters:** Your prompt literally shapes what the model considers probable. This is why prompt engineering works—you're steering the probability distributions toward your desired outcomes.

## Context Windows: The Foundation of Prompt Design

### What Are Context Windows?

The context window is the maximum amount of text (measured in tokens) that an LLM can process at once. Common context windows:

- GPT-3.5: 4,096 tokens (~3,000 words)
- GPT-4: 8,192 tokens (~6,000 words) or 32,768 tokens (~24,000 words)
- Claude: 100,000+ tokens (~75,000+ words)

### Why Context Windows Matter

1. **Memory Limitation**: The model can't remember anything outside its context window
2. **Information Hierarchy**: Earlier content has less influence on later predictions
3. **Strategic Placement**: Important information should be placed strategically within the window

### Practical Implications

**❌ Poor Approach:**
```
Write a story about a detective solving a murder case in Victorian London. Make it dark and atmospheric. The detective should be methodical and intelligent. Include period-appropriate details about technology and society. The victim should be a wealthy merchant. The killer's motive should be revenge for a past injustice. Write in third person. Make it about 1000 words.
```

**✅ Better Approach:**
```
Write a 1000-word Victorian London murder mystery. 

Setting: 1880s London
Protagonist: Methodical, intelligent detective  
Victim: Wealthy merchant
Motive: Revenge for past injustice
Style: Dark, atmospheric, third person

Include period details about technology and society.
```

**Why the second works better:** Structured information is easier for the model to reference throughout generation.

## The Token Economy

### Understanding Tokens

Tokens aren't always whole words:
- "hello" = 1 token
- "ChatGPT" = 2 tokens ("Chat" + "GPT")  
- "don't" = 2 tokens ("don" + "'t")

### Cost and Performance Implications

1. **API Costs**: You pay per token (input + output)
2. **Processing Speed**: More tokens = slower response
3. **Context Limits**: Efficient token usage extends your effective context

### Practical Token Management

**Token-Heavy Prompt:**
```
Please provide me with a comprehensive and detailed explanation of the various different methods and approaches that can be utilized and implemented for the purpose of optimizing and improving the performance and effectiveness of machine learning models.
```
(~40 tokens)

**Token-Efficient Prompt:**
```
Explain methods for optimizing machine learning model performance.
```
(~10 tokens)

Both prompts request similar information, but the second is 75% more efficient.

## Why This Understanding Matters

### Pattern Completion vs. Understanding

LLMs excel at pattern completion. They've learned that:
- After "The capital of France is" comes "Paris"
- After "Dear [Name]," comes formal language
- After "```python" comes Python code

**Strategic Implication:** Structure your prompts to trigger the right patterns.

### Probability Steering

Every word in your prompt influences the probability distribution. Consider:

**Prompt A:** "Write a story"
**Prompt B:** "Write a thrilling mystery story"  
**Prompt C:** "Write a thrilling mystery story with unexpected plot twists"

Each addition narrows the probability space toward more specific outcomes.

## Common Misconceptions

### ❌ "LLMs Think Like Humans"
**Reality:** They predict tokens based on statistical patterns

### ❌ "More Detailed Prompts Are Always Better"  
**Reality:** Relevant detail helps; irrelevant detail hurts

### ❌ "LLMs Have Perfect Memory"
**Reality:** They forget information outside the context window

## Quick Practice Exercise

Transform this ineffective prompt using your understanding of how LLMs work:

**Original:** "Make it good and interesting"

**Your improved version:** _______________

**Suggested improvement:** "Write an engaging short story with compelling characters and an unexpected ending"

**Why it's better:** Provides specific patterns for the model to follow rather than vague qualitative instructions.

## Key Takeaways

1. **LLMs predict next tokens** based on probability distributions your prompt shapes
2. **Context windows limit memory**—structure information strategically  
3. **Token efficiency** affects cost, speed, and context usage
4. **Pattern completion** is the core mechanism—trigger the right patterns
5. **Specificity** narrows probability distributions toward desired outcomes

## Next Section

Now that you understand the mechanical foundation, let's explore [The Prompt-Response Loop](02-prompt-response-loop.md) to understand how this prediction process creates the interactive experience of working with LLMs.

---

**⏱️ Section Time: 20 minutes**  
**🎯 Key Concept: LLMs are probability distribution machines**  
**💡 Main Insight: Your prompts steer these distributions toward desired outcomes**