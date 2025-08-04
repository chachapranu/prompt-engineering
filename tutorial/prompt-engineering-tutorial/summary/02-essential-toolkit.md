# Essential Toolkit (25 minutes)

## The Big 5 Techniques

These five techniques solve 80% of prompt engineering challenges. Master these and you'll handle most real-world prompting tasks effectively.

---

## 1. Few-Shot Prompting

**What it is**: Provide 2-4 examples of the desired input-output pattern before asking the model to perform the task.

**Why it works**: LLMs excel at pattern recognition and replication. Examples show exactly what success looks like.

**The Formula**:
```
Example 1: [Input] → [Desired Output]
Example 2: [Input] → [Desired Output]
Example 3: [Input] → [Desired Output]

Now apply this pattern to: [New Input]
```

**Quick Example**:
```
Classify review sentiment as Positive, Negative, or Neutral:

Review: "Amazing food and super friendly staff!"
Sentiment: Positive

Review: "Terrible experience, will never come back."
Sentiment: Negative

Review: "The place was decent, nothing special."
Sentiment: Neutral

Review: "The service was okay but the food took forever."
Sentiment: ?
```

**When to use**: Pattern-based tasks, formatting requirements, maintaining consistency across outputs.

**Pro tip**: Use 2-4 examples max. More doesn't always mean better.

---

## 2. Chain-of-Thought

**What it is**: Ask the model to show its reasoning process step-by-step before providing the final answer.

**Why it works**: Breaks down complex problems, makes mistakes visible, improves accuracy for multi-step reasoning.

**The Formula**:
```
Think step by step:
1. [Step 1 reasoning]
2. [Step 2 reasoning]
3. [Step 3 reasoning]

Therefore: [Final answer]
```

**Quick Example**:
```
Should we use React or Vue for our new dashboard project?

Consider this step by step:
1. Analyze project requirements (performance, complexity, timeline)
2. Evaluate team expertise with each framework
3. Consider long-term maintenance and hiring
4. Compare ecosystem and community support
5. Make recommendation based on weighted factors
```

**When to use**: Complex reasoning tasks, problem-solving, decision-making, mathematical calculations.

**Pro tip**: Each step should build logically on the previous one.

---

## 3. Role Prompting

**What it is**: Instruct the model to adopt a specific persona, profession, or perspective when responding.

**Why it works**: Activates relevant knowledge patterns and shapes response style appropriately.

**The Formula**:
```
You are a [specific role] with [relevant experience/expertise].
[Context about the situation]
[Task request with role-appropriate expectations]
```

**Quick Example**:
```
You are a senior software engineer mentoring a junior developer who has never worked with APIs before.

The junior developer asks: "I keep hearing about APIs but I don't really understand what they are or why they're important."

Provide a clear, practical explanation with simple examples.
```

**Effective Role Categories**:
- **Professional roles**: "You are a senior [job title] with 10 years of experience..."
- **Teaching roles**: "You are a patient tutor helping someone learn..."
- **Advisory roles**: "You are a trusted advisor helping with..."

**When to use**: Domain expertise needed, specific tone/style required, audience-appropriate responses.

**Pro tip**: Be specific about the role - "cybersecurity specialist" vs. "computer expert".

---

## 4. Template Structures

**What it is**: Provide a consistent format that the model should follow in its response.

**Why it works**: Ensures completeness, consistency, and makes responses easy to use.

**The Formula**:
```
[Task description]

Please structure your response as:

**Section 1:** [What goes here]
**Section 2:** [What goes here]
**Section 3:** [What goes here]
```

**Quick Example**:
```
Analyze why our mobile app's user retention is dropping.

Structure your analysis as:

**Current Situation:**
- Key metrics and trends
- Timeline of changes

**Root Cause Analysis:**
- Primary factors (top 3)
- Supporting evidence

**Recommendations:**
- Immediate actions (next 30 days)
- Long-term strategies (3-6 months)
- Success metrics to track
```

**Common Template Patterns**:
- **Analysis**: Problem → Root Causes → Solutions → Next Steps
- **Creative**: Hook → Context → Main Content → Call to Action
- **Technical**: Requirements → Design → Implementation → Testing

**When to use**: Need structured outputs, consistency across responses, complete coverage of topics.

**Pro tip**: Keep templates simple - usually 3-6 main sections work best.

---

## 5. Constraint Setting

**What it is**: Explicitly define limitations, boundaries, and requirements that the model must respect.

**Why it works**: Narrows the solution space to viable options, prevents common mistakes.

**Constraint Categories**:
- **Format**: "Respond in exactly 3 bullet points"
- **Content**: "Focus only on mobile app features"
- **Practical**: "Solutions must cost under $10k"

**Quick Example**:
```
Create a training program for new employees with these constraints:
- Duration: Maximum 2 weeks
- Budget: $5,000 per employee
- Remote delivery required
- Must cover: product knowledge, company culture, basic skills
- Target: Non-technical roles
- Success metric: 90% completion rate
```

**When to use**: Bounded problems, resource limitations, compliance requirements.

**Pro tip**: Prioritize constraints - "Must have" vs. "Should have" vs. "Nice to have".

---

## Combining Techniques for Maximum Impact

### Strategic Combinations

**Few-Shot + Chain-of-Thought**:
```
Example 1: Problem: X → Reasoning: Y → Solution: Z
Example 2: Problem: A → Reasoning: B → Solution: C

Now for this problem, think step by step: [New Problem]
```

**Role + Template + Constraints**:
```
You are a senior product manager at a SaaS company.

Analyze this feature request using this structure:
**User Need:** [What problem does this solve?]
**Business Impact:** [Revenue/retention effects]
**Technical Feasibility:** [Implementation complexity]
**Recommendation:** [Build/defer/reject with reasoning]

Constraints:
- Consider our current roadmap
- Development capacity: 2 engineers for 1 sprint
- Must integrate with existing dashboard
```

### Selection Guide

| Task Type | Primary Technique | Why |
|-----------|------------------|-----|
| Pattern matching | Few-Shot | Shows exact desired format |
| Complex reasoning | Chain-of-Thought | Breaks down multi-step logic |
| Domain expertise | Role Prompting | Activates expert knowledge |
| Consistent outputs | Templates | Ensures complete responses |
| Bounded problems | Constraints | Focuses on viable solutions |

## Context Management Essentials

### Working Within Token Limits

**Information Priority Stack**:
1. **Essential**: Task definition, critical constraints, key context
2. **Important**: Examples, quality guidelines, supporting details
3. **Optional**: Background info, additional examples, explanations

### Conversation Management

**Early Stage** (0-20% context full): Full detail and examples work well
**Active Working** (20-70% full): Focus on essential information, use compression
**Context Saturation** (70-90% full): Aggressive prioritization, consider reset
**Context Crisis** (90%+ full): Immediate reset or summarization needed

### Compression Techniques

**High Density Information**:
```
❌ Low Density:
"The customer said that they were not happy with the product. They mentioned that it was difficult to use and didn't work as expected."

✅ High Density:
"Customer complaints: Usability issues, functionality problems, poor UX"
```

**Reference vs. Repeat**:
```
❌ Repetitive:
"As mentioned in our earlier discussion about the marketing strategy..."

✅ Reference-Based:
"Per marketing strategy discussion (ref: earlier)..."
```

## Error Prevention Framework

### Common Failure Patterns

**Ambiguity Failures**: Vague prompts → Generic responses
**Context Confusion**: Mixed signals → Inconsistent outputs
**Format Failures**: No structure specified → Wrong format
**Scope Creep**: No boundaries → Too much/little information

### Built-in Validation

**Self-Correction Pattern**:
```
[Your main prompt]

After generating your response, review it against these criteria:
- Does it directly answer the question?
- Is the format correct?
- Is the tone appropriate?
- Are examples relevant and clear?

If any check fails, revise your response.
```

### Robust Prompt Architecture

**Defense-in-Depth Pattern**:
1. **Clear Task Definition**: Specific, measurable objective
2. **Context and Constraints**: Essential background + limitations
3. **Quality Assurance**: Success criteria + failure avoidance
4. **Self-Validation**: Built-in checking mechanisms

## Quick Application Guide

### For Any New Prompt

1. **Start with technique selection**: Which of the Big 5 fits best?
2. **Apply foundational principles**: Clarity, Context, Structure, Examples
3. **Add error prevention**: Common failure modes for this task type
4. **Test and iterate**: Use prompt-response loop for refinement

### Emergency Prompt Fixes

**Generic Response**: Add few-shot examples
**Confused Output**: Add role prompting and clearer context
**Wrong Format**: Add explicit template structure
**Too Broad/Narrow**: Add specific constraints
**Illogical Reasoning**: Add chain-of-thought requirement

### Quality Checklist

- [ ] Technique selection appropriate for task type
- [ ] Examples provided where helpful (few-shot)
- [ ] Step-by-step reasoning requested if needed (chain-of-thought)
- [ ] Appropriate expertise role defined (role prompting)
- [ ] Response structure specified (templates)
- [ ] Boundaries and limitations clear (constraints)
- [ ] Context window usage optimized
- [ ] Error prevention measures included

## Key Takeaways

**The Big 5 solve most challenges**:
- Few-shot: Show patterns through examples
- Chain-of-thought: Break down complex reasoning
- Role prompting: Activate expert knowledge
- Templates: Structure consistent outputs
- Constraints: Focus on viable solutions

**Strategic combination multiplies effectiveness**:
- Match techniques to task requirements
- Layer techniques for complex challenges
- Balance control with creativity

**Context management is critical**:
- Prioritize information strategically
- Use compression when needed
- Monitor context window usage

**Error prevention beats correction**:
- Understand common failure modes
- Build validation into prompts
- Use defensive architecture patterns

---

**Next: [Practical Application](03-practical-application.md) - Real-world implementation patterns and frameworks**