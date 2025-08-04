# 4.1 Domain-Specific Prompting (30 minutes)

## Core Concept

Different domains require specialized prompt engineering patterns that leverage domain-specific knowledge, terminology, and success criteria. Mastering these patterns allows you to create highly effective prompts for professional applications.

**Key Insight:** Generic prompting techniques become powerful when adapted to domain-specific contexts, terminology, and quality standards.

## Code Generation: Programming Task Patterns

### The Code Generation Framework

**Context → Specification → Implementation → Validation**

Each step requires domain-specific considerations:

### Context Patterns for Code

**Technical Environment Context:**
```
Programming context:
- Language: Python 3.9+
- Framework: FastAPI with SQLAlchemy
- Database: PostgreSQL
- Deployment: Docker containers on AWS
- Code style: PEP 8, type hints required
- Testing: pytest with 90%+ coverage requirement
```

**Functional Context:**
```
Business context:
- Purpose: User authentication microservice
- Scale: 10k+ concurrent users
- Security: OAuth 2.0 + JWT tokens
- Performance: <100ms response time
- Integration: Must work with existing user database
```

### Specification Patterns

**❌ Vague Specification:**
```
Write a function to handle user login.
```

**✅ Domain-Specific Specification:**
```
Create a FastAPI endpoint for user authentication with these requirements:

Function signature:
- POST /auth/login
- Input: LoginRequest (email: str, password: str)  
- Output: AuthResponse (access_token: str, user_id: int, expires_in: int)

Security requirements:
- Hash password verification using bcrypt
- Generate JWT token with 24-hour expiration
- Rate limiting: 5 attempts per minute per IP
- Input validation and sanitization

Error handling:
- Invalid credentials: 401 with generic message
- Rate limit exceeded: 429 with retry-after header
- Server errors: 500 with logging but no detail exposure

Code quality:
- Type hints for all parameters and returns
- Docstring with examples
- Unit tests with positive and negative cases
- Error logging for security events
```

### Implementation Patterns

**Structured Code Generation:**
```
Generate the code following this structure:

1. **Imports and Dependencies**
   - Standard library imports first
   - Third-party imports second  
   - Local imports last

2. **Data Models** (if needed)
   - Request/response models with validation
   - Type definitions and enums

3. **Core Function Implementation**
   - Main business logic
   - Error handling
   - Logging and monitoring

4. **API Endpoint** (if applicable)
   - Route definition
   - Request validation
   - Response formatting

5. **Tests**
   - Unit tests for core logic
   - Integration tests for endpoints
   - Edge cases and error conditions

Include detailed comments explaining security decisions and business logic.
```

### Code Review Integration

**Code Review Prompt Pattern:**
```
Review this code for a production authentication system:

[CODE HERE]

Evaluate for:

**Security:**
- Vulnerability assessment (OWASP Top 10)
- Credential handling and storage
- Input validation and sanitization
- Error message information disclosure

**Performance:**
- Time complexity analysis
- Database query optimization
- Caching opportunities
- Resource usage patterns

**Maintainability:**
- Code clarity and documentation
- Error handling completeness
- Testing coverage and quality
- Adherence to coding standards

**Production Readiness:**
- Logging and monitoring hooks
- Configuration management
- Deployment considerations
- Scalability implications

Provide specific recommendations with code examples where helpful.
```

## Analysis and Research: Information Processing Patterns

### Research Task Architecture

**Question → Investigation → Analysis → Synthesis → Recommendations**

### Structured Research Prompts

**Multi-Layered Research Pattern:**
```
Research task: [SPECIFIC RESEARCH QUESTION]

**Layer 1: Information Gathering**
Sources to investigate:
- Primary sources: [Company reports, official data, direct surveys]
- Secondary sources: [Industry reports, academic research, expert analysis]  
- Tertiary sources: [News articles, opinions, summaries]

**Layer 2: Information Validation**
Validation criteria:
- Source credibility and bias assessment
- Data currency and relevance
- Cross-reference verification
- Methodology evaluation

**Layer 3: Pattern Analysis**
Analytical frameworks:
- Trend identification and significance
- Causal relationship assessment
- Comparative analysis across categories
- Statistical significance evaluation

**Layer 4: Insight Synthesis**
Synthesis requirements:
- Key findings with confidence levels
- Strategic implications and opportunities
- Risk assessment and mitigation factors
- Actionable recommendations with priorities

Deliver results in executive summary format with supporting detail appendix.
```

### Domain-Specific Analysis Examples

**Market Research Pattern:**
```
Analyze the [SPECIFIC MARKET] using this framework:

**Market Structure Analysis:**
- Market size, growth rate, and maturity stage
- Key segments and their characteristics
- Entry barriers and competitive dynamics
- Value chain analysis and profit pools

**Competitive Landscape:**
- Market share distribution and trends
- Competitive positioning and differentiation
- Strengths/weaknesses of key players
- Emerging threats and opportunities

**Customer Analysis:**
- Customer segments and needs analysis
- Purchase decision processes and criteria
- Satisfaction levels and loyalty patterns
- Unmet needs and pain points

**Strategic Implications:**
- Market opportunities and threats
- Success factors for market participants
- Investment attractiveness assessment
- Strategic recommendations by stakeholder type

Include confidence levels for all major claims and identify information gaps.
```

**Financial Analysis Pattern:**
```
Perform financial analysis of [COMPANY/SECTOR] with focus on:

**Performance Analysis:**
- Revenue growth trends and drivers
- Profitability metrics and margin analysis
- Efficiency ratios and operational performance
- Cash flow generation and quality

**Financial Health Assessment:**
- Liquidity position and working capital management
- Leverage analysis and debt serviceability
- Capital allocation effectiveness
- Financial flexibility and stress testing

**Valuation Perspective:**
- Multiple-based valuation comparisons
- DCF analysis assumptions and sensitivity
- Asset-based valuation considerations
- Market sentiment and technical factors

**Investment Implications:**
- Risk-return profile assessment
- Investment thesis strengths and weaknesses
- Scenario analysis and key sensitivities
- Recommendation with target price/timeline

Structure findings for investment committee presentation.
```

## Creative Work: Balancing Creativity and Control

### The Creative Control Spectrum

Creative prompts must balance two competing objectives:
- **Creativity**: Original, engaging, unexpected outputs
- **Control**: Brand consistency, message alignment, quality standards

### Creative Constraint Patterns

**Bounded Creativity Framework:**
```
Creative brief: [CREATIVE OBJECTIVE]

**Creative Constraints (Non-Negotiable):**
- Brand guidelines: [Specific voice, tone, visual elements]
- Message requirements: [Key points that must be included]
- Format specifications: [Length, structure, medium requirements]
- Audience considerations: [Demographics, preferences, context]

**Creative Freedom Areas:**
- Narrative approach and storytelling methods
- Metaphors, analogies, and creative examples
- Emotional tone and engagement strategies
- Visual and linguistic style choices

**Quality Standards:**
- Originality: Avoid clichés and overused approaches
- Relevance: Direct connection to audience needs and interests
- Memorability: Elements that make content stick
- Actionability: Clear next steps or value delivery

Generate 3 distinct creative approaches, then select and develop the strongest.
```

### Content Creation Patterns

**Blog Post Creation Pattern:**
```
Create a blog post about [TOPIC] for [AUDIENCE]:

**Content Strategy:**
- Primary objective: [Educate/persuade/entertain/convert]
- Reader journey: [What should reader think/feel/do after reading]
- Content angle: [Unique perspective or approach]
- Success metrics: [How to measure effectiveness]

**Structure Template:**
- Hook: Compelling opening that promises value
- Context: Why this matters to the reader now
- Core content: 3-5 main points with supporting evidence
- Practical application: How to use this information
- Call to action: Specific next step for reader

**Style Guidelines:**
- Voice: [Professional/conversational/authoritative/friendly]
- Tone: [Optimistic/pragmatic/urgent/calm]
- Complexity: [Beginner/intermediate/advanced level]
- Length: [Optimal word count range]

**SEO Integration:**
- Primary keyword: [Target phrase] - integrate naturally
- Secondary keywords: [Supporting phrases] - use contextually
- Meta title and description: Compelling and keyword-optimized
- Internal linking: Connect to relevant existing content

Include headline variations and social media preview text.
```

**Marketing Copy Pattern:**
```
Create marketing copy for [PRODUCT/SERVICE]:

**Strategic Foundation:**
- Target audience: [Specific demographic and psychographic profile]
- Value proposition: [Primary benefit and differentiation]
- Positioning: [How product fits in market landscape]
- Competitive advantage: [What makes this better/different]

**Message Architecture:**
- Primary message: [Core benefit in one compelling sentence]
- Supporting messages: [3-4 proof points or secondary benefits]
- Emotional drivers: [Fear, desire, aspiration, urgency]
- Rational justifiers: [Logic, data, social proof]

**Copy Variations:**
- Headline options: 5 variations testing different approaches
- Body copy: Long and short versions
- Call-to-action: Multiple urgency and benefit variations
- Subject lines: For email campaigns (if applicable)

**Testing Framework:**
- A/B test variables: Which elements to test
- Success metrics: How to measure effectiveness
- Target improvement: Specific performance goals

Optimize for [SPECIFIC CHANNEL: email/web/social/print] requirements.
```

### Creative Quality Assurance

**Creative Review Checklist:**
```
Creative output evaluation:

**Brand Alignment:**
□ Voice and tone consistent with brand guidelines
□ Visual elements (if any) follow brand standards
□ Messaging supports overall brand positioning
□ No conflicts with brand values or promises

**Audience Relevance:**
□ Language appropriate for target audience
□ Content addresses audience needs and interests
□ Examples and references resonate with audience
□ Call-to-action matches audience readiness level

**Creative Effectiveness:**
□ Original approach that stands out from competition
□ Memorable elements that aid recall
□ Emotional engagement appropriate for objectives
□ Clear value proposition and benefits

**Technical Quality:**
□ Grammar, spelling, and syntax correct
□ Format requirements met
□ SEO optimization (if applicable) implemented naturally
□ Legal and compliance requirements addressed

**Performance Potential:**
□ Clear success metrics identified
□ A/B testing opportunities defined
□ Conversion optimization elements included
□ Measurement and iteration plan established
```

## Domain Pattern Adaptation

### Transferring Patterns Between Domains

The patterns from code, analysis, and creative work can be adapted to other domains:

**Customer Service → Code Pattern Adaptation:**
- Context: Customer situation and history
- Specification: Resolution requirements and constraints
- Implementation: Response strategy and actions
- Validation: Customer satisfaction and issue resolution

**Education → Analysis Pattern Adaptation:**
- Question: Learning objectives and student needs
- Investigation: Content research and pedagogical methods
- Analysis: Learning effectiveness and engagement factors
- Synthesis: Curriculum design and teaching strategies

**Sales → Creative Pattern Adaptation:**
- Creative brief: Prospect needs and sales objectives
- Constraints: Brand guidelines and compliance requirements
- Freedom areas: Approach, examples, and presentation style
- Quality standards: Relevance, persuasiveness, and professionalism

## Quick Practice Exercise

Choose one domain (code, analysis, or creative) and create a domain-specific prompt for a task in your field of work or interest.

**Your domain-specific prompt:**
_______________

**Evaluation checklist:**
□ Uses domain-appropriate terminology and concepts
□ Includes relevant context and constraints
□ Specifies quality standards and success criteria
□ Provides structured approach to the task
□ Addresses common domain-specific challenges

## Key Takeaways

1. **Domain expertise** enhances generic prompt techniques with specialized knowledge
2. **Context patterns** provide necessary technical and business background
3. **Specification structures** ensure comprehensive requirement coverage
4. **Quality frameworks** maintain professional standards across domains
5. **Creative constraints** balance originality with brand and message requirements
6. **Pattern adaptation** allows transfer of effective structures between domains

## Next Section

Now that you understand domain-specific applications, let's explore [Production Considerations](02-production.md) to learn how to deploy prompt-based systems safely and effectively in real-world environments.

---

**⏱️ Section Time: 30 minutes**  
**🎯 Key Concept: Domain expertise transforms generic techniques into powerful professional tools**  
**💡 Main Insight: Each domain requires specialized patterns but follows transferable structural principles**