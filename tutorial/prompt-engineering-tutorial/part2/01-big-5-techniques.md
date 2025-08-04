# 2.1 The Big 5 Techniques (45 minutes)

## Overview

These five techniques solve 80% of prompt engineering challenges. Each technique leverages specific aspects of how LLMs process information and can be combined for even more powerful results.

**Key Insight:** Master these five techniques and you'll have the tools to handle most prompting tasks effectively.

---

## Technique 1: Few-Shot Prompting (10 minutes)

### What It Is
Few-shot prompting provides 2-4 examples of the desired input-output pattern before asking the model to perform the task on new input.

### Why It Works
- **Pattern Recognition:** LLMs excel at identifying and replicating patterns
- **Format Clarity:** Examples show exactly what the output should look like
- **Quality Consistency:** Examples establish the standard for response quality

### The Few-Shot Formula
```
Example 1: [Input] → [Desired Output]
Example 2: [Input] → [Desired Output]  
Example 3: [Input] → [Desired Output]

Now apply this pattern to: [New Input]
```

### Example 1: Sentiment Analysis

**❌ Zero-Shot (Less Reliable):**
```
Classify the sentiment of this review: "The service was okay but the food took forever."
```

**✅ Few-Shot (More Reliable):**
```
Classify customer review sentiment as Positive, Negative, or Neutral:

Review: "Amazing food and super friendly staff!"
Sentiment: Positive

Review: "Terrible experience, will never come back."
Sentiment: Negative

Review: "The place was decent, nothing special."
Sentiment: Neutral

Review: "The service was okay but the food took forever."
Sentiment: ?
```

### Example 2: Code Documentation

**❌ Zero-Shot:**
```
Document this function:
def calculate_discount(price, discount_rate):
    return price * (1 - discount_rate)
```

**✅ Few-Shot:**
```
Add documentation following this pattern:

def validate_email(email):
    """
    Validates email address format using regex.
    
    Args:
        email (str): Email address to validate
        
    Returns:
        bool: True if valid email format, False otherwise
        
    Example:
        >>> validate_email("user@example.com")
        True
    """
    return re.match(r'^[^@]+@[^@]+\.[^@]+$', email) is not None

def hash_password(password, salt):
    """
    Creates secure password hash using SHA-256.
    
    Args:
        password (str): Plain text password
        salt (str): Random salt string
        
    Returns:
        str: Hexadecimal hash string
        
    Example:
        >>> hash_password("mypass", "randomsalt")
        "a1b2c3d4e5f6..."
    """
    return hashlib.sha256((password + salt).encode()).hexdigest()

Now document this function:
def calculate_discount(price, discount_rate):
    return price * (1 - discount_rate)
```

### Common Few-Shot Mistakes

**❌ Too Many Examples** (Wastes context window)
- Use 2-4 examples max
- More examples don't always mean better results

**❌ Inconsistent Quality** (Confuses the pattern)
- All examples should match your desired quality level
- Don't mix good and bad examples

**❌ Irrelevant Examples** (Activates wrong patterns)
- Examples should match the new task closely
- Don't use email examples for code tasks

### Quick Practice

Create a few-shot prompt for extracting key information from job postings:

**Your few-shot prompt:**
_______________

---

## Technique 2: Chain-of-Thought (10 minutes)

### What It Is
Chain-of-thought prompting asks the model to show its reasoning process step-by-step before providing the final answer.

### Why It Works
- **Complex Reasoning:** Breaks down multi-step problems
- **Error Reduction:** Makes mistakes visible and correctable
- **Transparency:** Shows how the model reached its conclusion

### The Chain-of-Thought Formula
```
Think step by step:
1. [Step 1 reasoning]
2. [Step 2 reasoning]  
3. [Step 3 reasoning]

Therefore: [Final answer]
```

### Example 1: Problem Solving

**❌ Direct Answer:**
```
A company has 150 employees. 40% work remotely, 35% work in the office, and the rest work hybrid. If hybrid workers come to the office 3 days per week, what's the average office occupancy per day?
```

**✅ Chain-of-Thought:**
```
A company has 150 employees. 40% work remotely, 35% work in the office, and the rest work hybrid. If hybrid workers come to the office 3 days per week, what's the average office occupancy per day?

Think step by step:
1. First, calculate the number of employees in each category
2. Determine daily office presence for each group
3. Calculate total average daily occupancy
```

### Example 2: Technical Analysis

**❌ Direct Answer:**
```
Should we use React or Vue for our new dashboard project?
```

**✅ Chain-of-Thought:**
```
Should we use React or Vue for our new dashboard project?

Consider this step by step:
1. Analyze project requirements (performance, complexity, timeline)
2. Evaluate team expertise with each framework
3. Consider long-term maintenance and hiring
4. Compare ecosystem and community support
5. Make recommendation based on weighted factors
```

### Chain-of-Thought Variations

**Explicit Steps:**
```
Let's solve this step by step:
Step 1: [Do this]
Step 2: [Then this]
Step 3: [Finally this]
```

**Question-Based:**
```
To answer this, I need to consider:
- What are the key constraints?
- What options do we have?
- What are the trade-offs?
- What's the best choice given these factors?
```

**Process-Based:**
```
My reasoning process:
1. Understanding the problem
2. Gathering relevant information
3. Analyzing options
4. Making a recommendation
```

### Common Chain-of-Thought Mistakes

**❌ Skipping Steps** (Defeats the purpose)
- Don't rush to the conclusion
- Each step should build on the previous

**❌ Too Vague** (Not helpful for debugging)
- Make each step specific and clear
- Show actual reasoning, not just categories

**❌ Wrong Starting Point** (Garbage in, garbage out)
- Start with correct problem understanding
- Verify assumptions before reasoning

### Quick Practice

Create a chain-of-thought prompt for choosing a database technology:

**Your chain-of-thought prompt:**
_______________

---

## Technique 3: Role Prompting (10 minutes)

### What It Is
Role prompting instructs the model to adopt a specific persona, profession, or perspective when responding.

### Why It Works
- **Context Activation:** Triggers relevant knowledge patterns
- **Response Style:** Shapes tone and approach appropriately
- **Quality Filter:** Accesses higher-quality, specialized knowledge

### The Role Prompting Formula
```
You are a [specific role] with [relevant experience/expertise].
[Context about the situation]
[Task request with role-appropriate expectations]
```

### Example 1: Technical Explanation

**❌ Generic:**
```
Explain APIs to me.
```

**✅ Role-Based:**
```
You are a senior software engineer mentoring a junior developer who has never worked with APIs before.

The junior developer asks: "I keep hearing about APIs but I don't really understand what they are or why they're important. Can you explain them in a way that will help me understand how to use them in my projects?"

Provide a clear, practical explanation with simple examples.
```

### Example 2: Business Analysis

**❌ Generic:**
```
Analyze this marketing campaign performance data.
```

**✅ Role-Based:**
```
You are an experienced marketing analyst presenting findings to the VP of Marketing. 

Campaign data:
- Email open rate: 22% (industry avg: 18%)
- Click-through rate: 3.1% (industry avg: 2.6%)
- Conversion rate: 1.8% (target: 2.5%)
- Cost per acquisition: $45 (budget: $35)

Provide an executive summary with key insights and strategic recommendations.
```

### Effective Role Categories

**Professional Roles:**
- "You are a senior [job title] with 10 years of experience..."
- "As a [industry] consultant who has worked with Fortune 500 companies..."
- "Acting as a [specialist] who focuses on [specific area]..."

**Teaching Roles:**
- "You are a patient tutor helping someone learn..."
- "As an expert teacher who excels at making complex topics simple..."
- "You are mentoring a [skill level] who needs guidance on..."

**Advisory Roles:**
- "You are a trusted advisor helping with..."
- "As a strategic consultant brought in to..."
- "You are an expert reviewer evaluating..."

### Role Prompting Best Practices

**✅ Be Specific:**
```
"You are a cybersecurity specialist with expertise in cloud infrastructure"
```
**Not:**
```
"You are a computer expert"
```

**✅ Include Relevant Context:**
```
"You are a UX designer who has worked on mobile banking apps for 5 years"
```

**✅ Set Appropriate Expectations:**
```
"Provide advice at the level of detail a C-suite executive would need"
```

### Common Role Prompting Mistakes

**❌ Too Generic** (Doesn't activate specific knowledge)
- "You are an expert" vs. "You are a React developer with 5 years experience"

**❌ Mismatched Expectations** (Wrong level of detail)
- Don't ask a "beginner tutor" for advanced technical details

**❌ Unrealistic Roles** (Model can't actually fulfill)
- Avoid roles requiring real-time information or personal experience

### Quick Practice

Create a role prompt for getting help with investment decisions:

**Your role-based prompt:**
_______________

---

## Technique 4: Template Structures (10 minutes)

### What It Is
Template structures provide a consistent format that the model should follow in its response, ensuring organized and complete outputs.

### Why It Works
- **Completeness:** Ensures all important aspects are covered
- **Consistency:** Produces reliable, similarly structured outputs
- **Clarity:** Makes responses easy to scan and use

### The Template Formula
```
[Task description]

Please structure your response as follows:

**Section 1:** [What goes here]
**Section 2:** [What goes here]
**Section 3:** [What goes here]

[Additional formatting requirements]
```

### Example 1: Problem Analysis Template

**❌ Unstructured:**
```
Analyze why our mobile app's user retention is dropping.
```

**✅ Template-Structured:**
```
Analyze why our mobile app's user retention is dropping.

Structure your analysis as follows:

**Current Situation:**
- Key metrics and trends
- Timeline of changes

**Root Cause Analysis:**
- Primary factors (top 3)
- Supporting evidence

**Impact Assessment:**
- Business consequences
- User experience effects

**Recommendations:**
- Immediate actions (next 30 days)
- Long-term strategies (3-6 months)
- Success metrics to track
```

### Example 2: Code Review Template

**❌ Unstructured:**
```
Review this Python function for issues.
```

**✅ Template-Structured:**
```
Review this Python function for issues:

[paste code here]

Structure your review as follows:

**Code Quality:**
- Readability and style
- Documentation completeness

**Functionality:**
- Logic correctness
- Edge case handling

**Performance:**
- Efficiency concerns
- Optimization opportunities

**Security:**
- Potential vulnerabilities
- Best practice violations

**Recommendations:**
- Priority: High/Medium/Low
- Specific changes needed
- Code examples where helpful
```

### Template Categories

**Analysis Templates:**
- Problem → Root Causes → Solutions → Next Steps
- Current State → Desired State → Gap Analysis → Action Plan
- Strengths → Weaknesses → Opportunities → Threats

**Creative Templates:**
- Hook → Context → Main Content → Call to Action
- Problem → Agitation → Solution → Proof → Action
- Introduction → Body → Conclusion → Resources

**Technical Templates:**
- Requirements → Design → Implementation → Testing → Deployment
- Input → Processing → Output → Error Handling
- Problem → Approach → Code → Explanation → Usage

### Advanced Template Features

**Conditional Sections:**
```
**Risk Assessment:**
If high risk: Include mitigation strategies
If medium risk: Include monitoring plan
If low risk: Brief acknowledgment
```

**Dynamic Length:**
```
**Executive Summary:** 2-3 sentences
**Detailed Analysis:** 200-300 words per major point
**Action Items:** Bullet points, 1 sentence each
```

**Interactive Elements:**
```
**Decision Points:**
For each option, provide:
- Pros (3-5 bullets)
- Cons (3-5 bullets)  
- Recommendation (1 sentence)
```

### Common Template Mistakes

**❌ Too Rigid** (Stifles natural flow)
- Leave room for model creativity within structure
- Don't over-specify every detail

**❌ Too Complex** (Hard to follow)
- Keep templates simple and logical
- Usually 3-6 main sections work best

**❌ Wrong Granularity** (Mismatched detail level)
- Match template detail to task complexity
- Don't use detailed templates for simple tasks

### Quick Practice

Create a template for evaluating job candidates:

**Your template structure:**
_______________

---

## Technique 5: Constraint Setting (5 minutes)

### What It Is
Constraint setting explicitly defines limitations, boundaries, and requirements that the model must respect in its response.

### Why It Works
- **Focus:** Narrows the solution space to viable options
- **Quality Control:** Prevents common mistakes and oversights
- **Practical Utility:** Ensures outputs fit real-world requirements

### Constraint Categories

**Format Constraints:**
- Length limits: "Respond in exactly 3 bullet points"
- Style requirements: "Use only technical terminology"
- Structure rules: "No more than 2 levels of headers"

**Content Constraints:**
- Scope boundaries: "Focus only on mobile app features"
- Knowledge limits: "Use only information from the provided document"
- Accuracy requirements: "Include sources for all statistics"

**Practical Constraints:**
- Resource limits: "Solutions must cost under $10k"
- Timeline constraints: "Implementation within 30 days"
- Technical requirements: "Must work with our existing PHP codebase"

### Example 1: Constrained Analysis

**Without Constraints:**
```
Analyze our marketing strategy.
```

**With Strategic Constraints:**
```
Analyze our marketing strategy with these constraints:
- Focus only on digital channels (no traditional media)
- Budget limit: $50k quarterly
- Target audience: B2B decision makers in healthcare
- Must integrate with existing Salesforce CRM
- Measurable ROI required within 90 days
```

### Example 2: Constrained Code Generation

**Without Constraints:**
```
Write a function to process user data.
```

**With Technical Constraints:**
```
Write a Python function to process user data with these constraints:
- Input: List of user dictionaries
- Output: Pandas DataFrame
- Must handle missing data gracefully
- No external API calls
- Memory usage under 100MB for 10k users
- Include type hints and docstrings
- Compatible with Python 3.8+
```

### Constraint Setting Best Practices

**✅ Be Specific:**
```
"Word count: 200-250 words" (not "keep it short")
```

**✅ Prioritize Constraints:**
```
"Must have: Security compliance
Should have: Performance optimization  
Nice to have: Advanced features"
```

**✅ Explain Why When Helpful:**
```
"No technical jargon (audience is non-technical executives)"
```

### Quick Practice

Add appropriate constraints to this prompt:
"Create a training program for new employees."

**Your constrained version:**
_______________

---

## Combining the Big 5 Techniques

### Technique Synergy

The real power comes from combining techniques strategically:

**Few-Shot + Chain-of-Thought:**
```
Example 1: Problem: X → Reasoning: Y → Solution: Z
Example 2: Problem: A → Reasoning: B → Solution: C

Now for this problem, think step by step: [New Problem]
```

**Role + Template + Constraints:**
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
- Must integrate with existing user dashboard
```

### Selection Guide

**When to use each technique:**

| Task Type | Primary Technique | Why |
|-----------|------------------|-----|
| Pattern matching | Few-Shot | Shows exact desired format |
| Complex reasoning | Chain-of-Thought | Breaks down multi-step logic |
| Specialized knowledge | Role Prompting | Activates expert patterns |
| Consistent output | Templates | Ensures complete responses |
| Bounded problems | Constraints | Focuses on viable solutions |

## Key Takeaways

1. **Few-Shot Prompting** shows patterns through examples—use 2-4 quality examples
2. **Chain-of-Thought** breaks complex reasoning into visible steps
3. **Role Prompting** activates specific expertise and appropriate tone
4. **Template Structures** ensure complete, organized responses
5. **Constraint Setting** focuses outputs on practical, usable solutions
6. **Combination** of techniques creates more powerful and reliable prompts

## Next Section

Now that you've mastered the core techniques, let's learn [Context Management](02-context-management.md) to handle the practical challenges of working within context window limits and managing long conversations.

---

**⏱️ Section Time: 45 minutes**  
**🎯 Key Concept: Five techniques solve 80% of prompting challenges**  
**💡 Main Insight: Techniques work best when combined strategically**