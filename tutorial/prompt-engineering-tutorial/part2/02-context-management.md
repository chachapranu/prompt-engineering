# 2.2 Context Management (25 minutes)

## Core Concept

Context management is the art of working effectively within the constraints of LLM context windows while maintaining conversation coherence and maximizing the utility of available tokens.

**Key Insight:** Context windows are finite resources that require strategic management—what you include is as important as what you exclude.

## Understanding Context Window Limitations

### Context Window Sizes (as of 2024)

| Model | Context Window | Approximate Words |
|-------|----------------|-------------------|
| GPT-3.5-turbo | 4,096 tokens | ~3,000 words |
| GPT-4 | 8,192 tokens | ~6,000 words |
| GPT-4-32k | 32,768 tokens | ~24,000 words |
| Claude-3 | 100,000 tokens | ~75,000 words |
| Claude-3.5 | 200,000 tokens | ~150,000 words |

### What Consumes Context

**System Messages:** Model instructions and role definitions
**Conversation History:** All previous messages in the session
**Current Prompt:** Your new input
**Response Space:** Tokens reserved for the model's output

**Example Context Breakdown:**
```
System message: 150 tokens
Previous conversation: 2,000 tokens  
Current prompt: 500 tokens
Reserved for response: 1,000 tokens
------------------
Total used: 3,650 / 4,096 tokens (89% full)
```

## Information Hierarchy: What to Include First

### The Priority Stack

**Tier 1: Essential (Always Include)**
- Core task definition
- Critical constraints and requirements
- Key context that affects the entire response

**Tier 2: Important (Include If Space Allows)**
- Supporting examples
- Detailed specifications
- Quality guidelines

**Tier 3: Nice-to-Have (Include Only If Plenty of Space)**
- Background information
- Additional examples
- Detailed explanations

### Practical Example: Project Brief

**❌ Poor Hierarchy (Nice-to-have first):**
```
Our company was founded in 2019 and has grown from 5 to 50 employees. We focus on sustainable business practices and have won several awards for innovation. Our culture emphasizes work-life balance and we offer flexible remote work options. We recently moved to a new office space with modern amenities.

We need help creating a project management system for our software development team. The team has 8 developers working on 3 different products. We use Agile methodology and have 2-week sprints. The system should track tasks, deadlines, and team member assignments.

Requirements:
- Must integrate with our existing Git repositories
- Should support Kanban boards
- Needs reporting capabilities for management
- Budget limit: $15,000
- Implementation deadline: 6 weeks
```

**✅ Good Hierarchy (Essential first):**
```
Task: Design a project management system for an 8-person software development team

Critical Requirements:
- 3 products, 2-week Agile sprints
- Git integration (essential)
- Kanban board support
- Management reporting
- Budget: $15,000, Timeline: 6 weeks

Team Context:
- 8 developers, Agile methodology
- Currently using [existing tools]
- Need task tracking, deadlines, assignments

Company Background (if relevant):
- 50-person company, founded 2019
- Focus on sustainable practices
- Flexible/remote work culture
```

## Context Compression Techniques

### 1. Information Density

**❌ Low Density:**
```
The customer said that they were not happy with the product. They mentioned that it was difficult to use and didn't work as expected. They also said the documentation was poor and they couldn't figure out how to set it up properly. The customer service experience was also bad according to them.
```

**✅ High Density:**
```
Customer complaints:
- Usability: Difficult to use, doesn't work as expected
- Documentation: Poor quality, unclear setup instructions  
- Support: Bad customer service experience
```

### 2. Structured Compression

**Original (150 words):**
```
We conducted user interviews with 20 participants between ages 25-45. The interviews were conducted over video calls lasting 30-45 minutes each. We asked questions about their current workflow, pain points, and desired features. The main findings were that users spend too much time on manual data entry, they find the current interface confusing, and they want better integration with their existing tools. Users also mentioned wanting mobile access and better reporting capabilities. The majority of users (18 out of 20) expressed willingness to pay for improvements.
```

**Compressed (45 words):**
```
User Research (n=20, ages 25-45):
Key findings:
- Pain: Manual data entry, confusing interface
- Wants: Tool integration, mobile access, better reporting
- Willingness to pay: 90% (18/20)
Method: 30-45min video interviews
```

### 3. Reference Compression

Instead of repeating information, reference it:

**❌ Repetitive:**
```
In the marketing meeting on Monday, we discussed Q3 campaigns. Sarah mentioned the social media strategy needs updating. The social media strategy includes Facebook, Instagram, and LinkedIn campaigns. Facebook campaigns focus on brand awareness. Instagram campaigns focus on product showcases. LinkedIn campaigns focus on B2B lead generation.

In the follow-up meeting on Wednesday, we revisited the social media strategy Sarah mentioned on Monday...
```

**✅ Reference-Based:**
```
Monday Marketing Meeting:
- Q3 campaigns discussed
- Social media strategy needs updating (Sarah)
  - Facebook: Brand awareness
  - Instagram: Product showcases  
  - LinkedIn: B2B leads

Wednesday Follow-up:
- Revisited social media strategy (ref: Monday meeting)
```

## Managing Long Conversations

### The Conversation Lifecycle

**Phase 1: Fresh Context (0-20% full)**
- Full detail and examples work well
- Can include extensive background
- Exploratory and broad approaches effective

**Phase 2: Active Working (20-70% full)**
- Focus on essential information
- Use compression techniques
- Reference previous exchanges rather than repeating

**Phase 3: Context Saturation (70-90% full)**
- Aggressive prioritization required
- Consider conversation reset
- Focus only on current task needs

**Phase 4: Context Crisis (90%+ full)**
- Immediate reset or summarization needed
- Risk of lost context and degraded performance

### Conversation Reset Strategies

**Strategy 1: Summary Reset**
```
Let me summarize our conversation so far to reset context:

Original Goal: [Main objective]
Key Decisions Made: [Important conclusions]
Current Status: [Where we are now]
Next Steps: [What we're working on now]

Continuing from here: [Current task]
```

**Strategy 2: Focused Reset**
```
Based on our previous discussion, I'm now focusing specifically on:
[Current narrow task]

Previous context that's still relevant:
- [Key point 1]
- [Key point 2]
- [Key point 3]

Let's proceed with: [Specific current request]
```

### Context Window Early Warning Signs

**Watch for these indicators:**
- Responses becoming less specific or relevant
- Model ignoring earlier instructions
- Repetitive or circular responses
- Sudden topic shifts
- Generic rather than contextual responses

## Practical Context Management Examples

### Example 1: Code Review Conversation

**Initial State (Context: 20%):**
```
Please review this 200-line Python class for a user authentication system. Look for security issues, performance problems, and code quality concerns.

[Full code included]

Context: This is part of a web application that handles 10k+ daily users.
```

**Mid-Conversation (Context: 60%):**
```
Thanks for the security feedback. Now let's focus on the performance issues you identified.

Reference: Lines 45-67 (password hashing function you mentioned earlier)
Specific question: Is bcrypt the best choice here, or should we consider Argon2?
```

**Near Context Limit (Context: 85%):**
```
Summary reset:

Code review progress:
✓ Security issues identified and solutions provided
✓ Performance bottlenecks found (lines 45-67, 120-135)  
Current focus: Implementing Argon2 password hashing

Question: Show me the specific Argon2 implementation for lines 45-67.
```

### Example 2: Strategic Planning Session

**Early Stage:**
```
Help me develop a comprehensive go-to-market strategy for our new B2B SaaS product.

Product details: [Full description]
Market analysis: [Complete research]
Competitive landscape: [Detailed comparison]
Team capabilities: [Full breakdown]
```

**Context-Aware Later Stage:**
```
Continuing our GTM strategy discussion:

Reference: Pricing strategy we developed (tier-based, $49-$299)
Current focus: Distribution channel selection

Specific decision needed: Direct sales vs. partner channel for enterprise segment (>100 employees)

Key factors from earlier discussion:
- Sales team capacity: 3 people
- Average deal size target: $5k annually
- 6-month sales cycle expected
```

## Tools and Techniques for Context Tracking

### Manual Tracking Methods

**Context Budget Worksheet:**
```
Total context: 8,192 tokens
System message: ~200 tokens  
Conversation history: ~3,500 tokens
Current prompt: ~800 tokens
Response buffer: ~1,500 tokens
Remaining: ~2,192 tokens (27%)
```

**Information Priority Checklist:**
```
Essential (must include):
□ Core task definition
□ Critical constraints  
□ Key context

Important (include if space):
□ Examples
□ Quality guidelines
□ Supporting details

Optional (space permitting):  
□ Background information
□ Additional examples
□ Explanatory content
```

### Strategic Context Management

**The "Context Constitution":**
Define upfront what information is essential vs. optional:

```
Context Management Rules for This Session:
1. Always include: Project requirements, technical constraints, deadline
2. Compress when needed: Examples (reference vs. full text)
3. Drop first: Background info, detailed explanations
4. Reset trigger: When response quality degrades
```

## Common Context Management Mistakes

### ❌ Context Hoarding
**Problem:** Trying to keep everything in context indefinitely
**Solution:** Actively manage and remove outdated information

### ❌ Information Obesity  
**Problem:** Including too much detail when brevity would work
**Solution:** Use compression techniques and prioritization

### ❌ No Context Strategy
**Problem:** Not planning how to use limited context space
**Solution:** Define information hierarchy upfront

### ❌ Reset Paralysis
**Problem:** Afraid to reset context when it becomes cluttered
**Solution:** Regular "context hygiene" with strategic resets

## Quick Practice Exercise

You're having a conversation about redesigning a company website. The context is 75% full. Write a context-conscious prompt that:
1. References previous decisions without repeating them
2. Focuses on the current specific need
3. Uses compressed information format

**Your context-aware prompt:**
_______________

**Sample Solution:**
```
Website redesign progress check:

Decisions made: Modern design, mobile-first, integrated blog (per earlier discussion)
Current focus: Navigation structure

Specific need: Header navigation layout for 7 main sections + search
Constraint: Max 2 navigation levels, mobile hamburger menu

Question: Show 3 navigation pattern options with pros/cons for our B2B audience.
```

## Key Takeaways

1. **Context windows are limited resources** requiring strategic management
2. **Information hierarchy** determines what to include first (essential → important → nice-to-have) 
3. **Compression techniques** maximize information density without losing meaning
4. **Conversation resets** prevent context saturation and maintain response quality
5. **Early warning signs** help identify when context management is needed
6. **Strategic planning** prevents context crises through proactive management

## Next Section

With context management mastered, let's explore [Error Prevention and Recovery](03-error-prevention.md) to learn how to avoid common prompt failures and recover when things go wrong.

---

**⏱️ Section Time: 25 minutes**  
**🎯 Key Concept: Context is a finite resource requiring strategic management**  
**💡 Main Insight: What you exclude is as important as what you include**