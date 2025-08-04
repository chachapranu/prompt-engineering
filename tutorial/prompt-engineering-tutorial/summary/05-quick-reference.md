# Quick Reference (10 minutes)

## Prompt Quality Checklist

### Before Sending Any Prompt
- [ ] **Task is specific and measurable** (not "help with" but "create," "analyze," "rewrite")
- [ ] **Success criteria are explicit** (length, format, quality standards)
- [ ] **Context is sufficient but not excessive** (essential background included)
- [ ] **Structure is logical and clear** (organized with headers, bullets, or sections)
- [ ] **Examples provided where helpful** (show desired outcome, not just describe)
- [ ] **Constraints and limitations defined** (what to avoid, resource limits)
- [ ] **Tone and audience specified** (professional, casual, technical level)

### The Big 5 Technique Quick Check
- [ ] **Few-shot**: Are examples provided for pattern-based tasks?
- [ ] **Chain-of-thought**: Is step-by-step reasoning requested for complex problems?
- [ ] **Role prompting**: Is appropriate expertise persona defined?
- [ ] **Templates**: Is response structure specified for consistency?
- [ ] **Constraints**: Are boundaries and requirements clearly stated?

---

## Common Failure Patterns and Fixes

### Problem: Generic, Unhelpful Responses
**Symptoms**: Response could apply to any situation, uses placeholder language
**Quick Fix**: Add specific context, constraints, and examples
```
❌ "Help me with marketing"
✅ "Create a 4-week email sequence for B2B SaaS targeting CTOs, focusing on security compliance pain points"
```

### Problem: Wrong Format or Structure
**Symptoms**: Output doesn't match intended use, hard to parse or apply
**Quick Fix**: Add explicit template structure
```
❌ "Analyze the data"
✅ "Analyze sales data using this format:
**Key Findings:** [Top 3 insights]
**Trends:** [What's changing]
**Recommendations:** [Specific actions with timelines]"
```

### Problem: Inconsistent Quality or Tone
**Symptoms**: Some parts excellent, others poor; tone shifts within response
**Quick Fix**: Add role prompting and quality standards
```
❌ "Write a proposal"
✅ "You are a senior consultant writing for C-suite executives. Create a proposal that's authoritative but accessible, with consistent executive-level detail throughout."
```

### Problem: Missing Critical Information
**Symptoms**: Response incomplete, doesn't address key requirements
**Quick Fix**: Add chain-of-thought and comprehensive templates
```
❌ "What should we do about this issue?"
✅ "Analyze this issue step by step:
1. Root cause identification
2. Impact assessment
3. Solution options with pros/cons
4. Recommended action with implementation plan"
```

### Problem: Context Window Overload
**Symptoms**: Model ignores early instructions, becomes repetitive or confused
**Quick Fix**: Prioritize information and compress context
```
❌ [Long conversation with full detail repeated]
✅ "Context summary: [Key decisions made]
Current focus: [Specific current need]
Question: [Targeted current request]"
```

---

## Template Library

### Business Analysis Template
```
Analyze [SUBJECT] for [AUDIENCE]:

**Current Situation:**
- Key metrics and performance indicators
- Recent changes and trends
- Competitive context

**Analysis:**
- Strengths and advantages
- Weaknesses and vulnerabilities
- Opportunities and threats

**Recommendations:**
- Priority 1: [High-impact action with timeline]
- Priority 2: [Medium-impact action with timeline]
- Priority 3: [Long-term strategic action]

**Success Metrics:**
- How to measure progress
- Key performance indicators
- Timeline for evaluation
```

### Code Generation Template
```
Create a [LANGUAGE] [COMPONENT TYPE] with these requirements:

**Functionality:**
- Input: [Parameter types and validation]
- Output: [Return type and format]
- Behavior: [What it should accomplish]

**Quality Requirements:**
- Error handling: [Specific scenarios to handle]
- Performance: [Speed/memory constraints]
- Security: [Authentication, validation, data protection]
- Testing: [Coverage requirements and test types]

**Integration:**
- Dependencies: [Required libraries/services]
- APIs: [Interface requirements]
- Documentation: [Comments and usage examples]

Include complete implementation with tests and documentation.
```

### Content Creation Template
```
Create [CONTENT TYPE] for [TARGET AUDIENCE]:

**Strategic Context:**
- Primary goal: [Educate/persuade/entertain/convert]
- Success metrics: [How to measure effectiveness]
- Key message: [Core takeaway for audience]

**Content Requirements:**
- Length: [Word count or time estimate]
- Tone: [Professional/conversational/authoritative]
- Format: [Structure and organization]
- Call-to-action: [Desired next step for reader]

**Optimization:**
- SEO considerations: [Keywords and searchability]
- Distribution channels: [Where this will be used]
- Engagement elements: [What makes it memorable/shareable]
```

### Research Template
```
Research [TOPIC] for [PURPOSE]:

**Research Scope:**
- Key questions to answer
- Information sources to prioritize
- Time frame and depth required

**Methodology:**
- Primary research approach
- Secondary source strategy
- Validation and cross-referencing plan

**Deliverable Format:**
**Executive Summary:** [Key findings in 2-3 paragraphs]
**Detailed Findings:** [Organized by research question]
**Sources and Methodology:** [Credibility and limitations]
**Recommendations:** [Actionable next steps]

Include confidence levels for major claims and identify information gaps.
```

---

## Context Management Quick Guide

### Information Priority Stack
1. **Essential (Always Include)**
   - Task definition and success criteria
   - Critical constraints and requirements
   - Key context that affects entire response

2. **Important (Include If Space Allows)**
   - Supporting examples and details
   - Quality guidelines and preferences
   - Relevant background information

3. **Optional (Space Permitting Only)**
   - Nice-to-have context
   - Additional examples
   - Explanatory content

### Context Compression Techniques
```
❌ Verbose: "The customer expressed dissatisfaction with the product because they found it difficult to use and it didn't work as they expected, and they also mentioned problems with documentation"

✅ Compressed: "Customer issues: Usability problems, functionality gaps, poor documentation"
```

### Conversation Reset Pattern
```
Session summary for context reset:

**Objective:** [Main goal we're working toward]
**Progress:** [What's been completed]
**Current Focus:** [Specific current task]
**Key Decisions:** [Important choices made]

Continuing with: [Current specific request]
```

---

## Troubleshooting Guide

### Step 1: Identify the Problem Type
- **Input Issues**: Ambiguous, contradictory, insufficient information
- **Context Problems**: Overload, poor prioritization, irrelevant information
- **Format Failures**: Unclear structure, inadequate examples
- **Quality Issues**: Wrong tone, inappropriate level, missing elements

### Step 2: Apply Targeted Solutions
**For Input Issues** → Apply Clarity Principle
- Make task more specific
- Add explicit success criteria
- Remove contradictory instructions

**For Context Problems** → Apply Context Management
- Prioritize essential information
- Compress supporting details
- Consider context reset

**For Format Failures** → Apply Structure Principle
- Add explicit templates
- Provide format examples
- Specify organization requirements

**For Quality Issues** → Apply Examples + Role Prompting
- Show desired quality level
- Define appropriate expertise persona
- Set clear quality standards

### Step 3: Test and Iterate
1. **Make one change at a time** (isolate what works)
2. **Test with similar inputs** (ensure consistency)
3. **Document what works** (build your pattern library)
4. **Monitor performance** (watch for degradation over time)

---

## Emergency Fixes

### When Prompts Completely Fail
```
Diagnostic prompt:
"The previous response didn't meet my needs. Let me be more specific:

What I need: [Clear, specific description]
Success looks like: [Concrete example of good output]
What was wrong with the previous response: [Specific issues]

Please address these requirements: [Numbered list of must-haves]"
```

### When Context Becomes Corrupted
```
Clean slate reset:
"Starting fresh with a clear request:

[Completely rewritten prompt using lessons learned]

Please respond only to this new request, ignoring previous exchanges."
```

### When Quality Suddenly Drops
```
Quality recovery prompt:
"Please improve your previous response by:
1. [Specific quality issue to fix]
2. [Another specific issue to address]
3. [Third improvement needed]

Maintain the good parts: [List what worked well]
Quality standard: [Reference to desired level]"
```

---

## Performance Optimization Quick Wins

### Token Efficiency
- **Remove filler words**: "Please" → direct instruction
- **Use bullet points**: More information per token
- **Compress examples**: Key elements only
- **Reference vs. repeat**: "As mentioned earlier" → "Per previous discussion"

### Response Speed
- **Precompute static prompts**: Template the unchanging parts
- **Parallel processing**: Independent tasks simultaneously
- **Strategic caching**: Store frequently used context
- **Smart defaults**: Reduce decision complexity

### Quality Consistency
- **Standard templates**: Consistent structure across uses
- **Quality checklists**: Built-in validation criteria
- **Version control**: Track what works
- **A/B testing**: Systematic improvement

---

## Domain-Specific Quick Patterns

### Code Tasks
```
Context: [Language, framework, environment, constraints]
Task: [Specific functionality needed]
Quality: [Testing, documentation, security requirements]
Integration: [Dependencies, APIs, deployment needs]
```

### Analysis Tasks
```
Question: [Specific question to answer]
Sources: [Where to find information]
Framework: [How to structure analysis]
Output: [Format and detail level for results]
```

### Creative Tasks
```
Objective: [What this content should accomplish]
Audience: [Who will consume this]
Constraints: [Brand, message, format requirements]
Freedom: [Areas for creative exploration]
Success: [How to measure effectiveness]
```

---

## Key Takeaways for Immediate Use

**Most Important Principles**:
1. **Be specific** - Vague prompts get vague results
2. **Show examples** - Demonstrate what you want
3. **Structure information** - Organize for easy processing
4. **Manage context** - Prioritize essential information
5. **Test systematically** - One change at a time

**Emergency Toolkit**:
- **Quality checklist** for all prompts
- **Template library** for common tasks
- **Troubleshooting guide** for systematic debugging
- **Context management** for complex conversations
- **Domain patterns** for specialized applications

**Performance Optimization**:
- Optimize for tokens, speed, and consistency
- Use templates and precomputed elements
- Implement testing and version control
- Monitor performance and iterate improvements

---

**🎉 Summary Complete: You now have both comprehensive understanding and practical tools for immediate application of prompt engineering principles.**