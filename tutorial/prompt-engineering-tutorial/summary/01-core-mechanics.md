# Core Mechanics (20 minutes)

## The Fundamental Truth About LLMs

**LLMs are probability distribution machines.** They predict the next token based on patterns learned from training data. Your prompt shapes these probability distributions toward desired outcomes.

**Key Insight:** Prompts don't "tell" the AI what to do—they steer probability distributions toward specific patterns.

## How Prompts Actually Work

### Token Prediction Process
1. **Tokenization**: Your prompt is split into tokens (words/sub-words)
2. **Pattern Matching**: Model identifies relevant patterns from training
3. **Probability Calculation**: Each possible next token gets a probability score
4. **Selection**: Model samples from this distribution to choose the next token
5. **Repetition**: Process repeats until response is complete

### Why This Matters
- **Specificity works**: Narrow probability distributions produce better results
- **Context shapes everything**: All tokens in your prompt influence the output
- **Patterns matter**: Model completes patterns it recognizes from training

## The Four Foundational Principles

### 1. Clarity - Eliminate Guesswork
**Principle**: Be explicit about what you want, how you want it, and what success looks like.

**Why it works**: Clear instructions activate the right probability patterns while excluding wrong ones.

**Examples:**
- ❌ "Make this better" 
- ✅ "Rewrite this email to be more professional and reduce word count by 30%"

### 2. Context - Provide Relevant Background
**Principle**: Include necessary information while prioritizing what matters most.

**Why it works**: Context helps the model understand the situation and respond appropriately.

**Information Hierarchy**:
1. **Essential**: Task-critical information that affects the entire response
2. **Important**: Supporting details that improve quality
3. **Nice-to-have**: Background that adds flavor but isn't necessary

### 3. Structure - Organize Information Logically
**Principle**: Present information in a logical order that's easy for the model to process.

**Why it works**: Well-structured prompts help models process information efficiently and produce organized responses.

**Common Patterns**:
- **TASK**: Task → Audience → Specifications → Key constraints
- **CORE**: Context → Objective → Requirements → Examples
- **CLEAR**: Context → Length → Examples → Audience → Role

### 4. Examples - Show Rather Than Tell
**Principle**: Demonstrate desired outcomes with concrete examples.

**Why it works**: Examples provide specific patterns for the model to follow, which is more reliable than abstract descriptions.

**Types of Examples**:
- **Format examples**: Show the structure you want
- **Quality examples**: Demonstrate the level of detail or style
- **Content examples**: Provide similar but not identical cases

## Mental Models for Prompt Engineering

### Model 1: The Communication Protocol
Think of prompts as structured communication protocols, not just questions.

**Components**:
- **Role definition**: Who the AI should act as
- **Context setting**: Relevant background information
- **Task specification**: What exactly needs to be done
- **Format requirements**: How the response should be structured
- **Quality criteria**: What makes a good response

### Model 2: The Pattern Activation System
Your prompt activates specific knowledge patterns and response styles from the model's training.

**Strategic Questions**:
- What patterns do I want to activate?
- What patterns do I want to avoid?
- How can I make the desired pattern more probable?

### Model 3: The Probability Steering Mechanism
Every word in your prompt influences the model's probability distributions.

**Optimization Approach**:
- **Increase probability** of desired outcomes through specificity
- **Decrease probability** of unwanted outcomes through constraints
- **Balance** between control and creativity

## Context Windows: The Critical Constraint

### Understanding Limits
- **Context window**: Maximum tokens the model can process at once
- **Finite resource**: Must be managed strategically
- **Information hierarchy**: What to include first matters

### Strategic Management
**Priority Stack**:
1. **Essential information**: Always include
2. **Important details**: Include if space allows
3. **Nice-to-have context**: Only if plenty of space remains

**Compression Techniques**:
- Use structured formats (bullets, tables)
- Reference rather than repeat information
- Summarize instead of including full detail

## The Prompt-Response Loop

### Understanding the Interaction
**Traditional Q&A**: "What's the best way to learn Python?"
**Protocol Approach**: Role + Context + Task + Format + Success criteria

### Iterative Refinement
The loop enables improvement:
1. **Initial prompt**: Establish basic task
2. **Assess response**: Identify gaps or issues
3. **Refined prompt**: Add specificity based on results
4. **Better response**: More targeted to your needs

## Common Failure Modes and Why They Happen

### Ambiguity Failures
**Problem**: Vague prompts lead to responses that miss the mark
**Root cause**: Model has to guess your intentions
**Solution**: Apply the four principles systematically

### Context Confusion
**Problem**: Mixed signals or contradictory instructions
**Root cause**: Competing probability patterns activated simultaneously
**Solution**: Clear, consistent instruction hierarchy

### Format Failures
**Problem**: Output in wrong format or structure
**Root cause**: No clear format specification provided
**Solution**: Explicit format templates and examples

### Scope Creep
**Problem**: Too much or too little information
**Root cause**: No clear boundaries defined
**Solution**: Specific scope constraints and success criteria

## Practical Application Framework

### Before Writing Any Prompt
1. **Define success**: What does a good response look like?
2. **Identify context**: What background information is essential?
3. **Choose structure**: How should information be organized?
4. **Prepare examples**: What patterns should the model follow?

### Prompt Quality Checklist
- [ ] Task is specific and measurable
- [ ] Context is sufficient but not excessive
- [ ] Structure is logical and clear
- [ ] Examples demonstrate desired outcome
- [ ] Success criteria are explicit
- [ ] Constraints and limitations are defined

### When Prompts Fail
1. **Identify the failure type**: Ambiguity, context, format, or scope
2. **Apply appropriate principle**: Clarity, context, structure, or examples
3. **Test systematically**: One change at a time
4. **Iterate based on results**: Use the prompt-response loop

## Key Takeaways

**Fundamental Understanding**:
- LLMs predict tokens using probability distributions your prompts shape
- Specificity and structure consistently produce better results
- Context windows are finite resources requiring strategic management

**Practical Framework**:
- Apply four principles: Clarity, Context, Structure, Examples
- Use mental models: Communication protocol, pattern activation, probability steering
- Follow systematic approach: Define success → Provide context → Structure information → Show examples

**Optimization Approach**:
- Understand why techniques work, not just how to use them
- Iterate systematically using the prompt-response loop
- Prevent failures through understanding common failure modes

---

**Next: [Essential Toolkit](02-essential-toolkit.md) - The 5 techniques that solve 80% of prompting challenges**