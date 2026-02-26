---
name: code-review-agent
description: Conduct thorough, constructive code reviews using team standards. Use when reviewing pull requests, code changes, or when asked to evaluate code quality.
---

# Code Review Agent

## Review Process

When conducting a code review:

1. **Load team standards**: Apply criteria from [code-review-standards](code-review-standards) skill
2. **Analyze the change context**: Understand what the code is trying to accomplish
3. **Systematic evaluation**: Check structure, standards compliance, and potential issues
4. **Constructive feedback**: Provide actionable suggestions using team feedback patterns

## Review Workflow

Copy this checklist and track progress:

Code Review Progress:
 Step 1: Read PR description and understand the intended change
 Step 2: Analyze code structure and organization
 Step 3: Apply team standards (from code-review-standards skill)
 Step 4: Check for potential bugs and edge cases
 Step 5: Provide constructive feedback following team patterns
 Step 6: Suggest specific improvements with examples

## Step-by-Step Process

**Step 1: Context Analysis**
- What feature/bug is being addressed?
- Does the approach align with existing architecture?
- Are there any breaking changes or migration considerations?

**Step 2: Structure Review** 
- Is the code organized logically?
- Are responsibilities clearly separated?
- Does it follow established project patterns?

**Step 3: Standards Application**
Use the evaluation criteria from code-review-standards skill:
- Variable naming and clarity
- Function size and single responsibility
- Error handling completeness
- Documentation adequacy

**Step 4: Issue Detection**
- Potential bugs or race conditions
- Performance implications
- Security considerations
- Test coverage gaps

**Step 5: Feedback Generation**
Follow the constructive feedback pattern from code-review-standards:
- Start with positive observations
- Explain reasoning behind suggestions
- Provide concrete code examples
- Offer alternatives when possible

## Review Templates

**For minor improvements:**
```
# Code Review: [Feature Name]

## What works well
- [Specific positive observations]

## Suggestions for improvement
- [Issue]: [Explanation of why it matters]
  ```[language]
  // Current approach
  [current code]
  
  // Suggested improvement
  [improved code]
  ```

## Additional considerations
- [Any architectural or future-proofing thoughts]
```

**For significant issues:**
```
# Code Review: [Feature Name]

## Overall approach
[Assessment of the general direction and architecture]

## Critical issues
- [Issue]: [Explanation and impact]
  - Suggested approach: [detailed guidance]
  - See: [reference to team guidelines if applicable]

## Standard compliance
[Results from applying code-review-standards checklist]

## Next steps
[Clear action items for the author]
```

## Advanced Review Scenarios

**Complex architectural changes**: See [ARCHITECTURE_REVIEW.md](ARCHITECTURE_REVIEW.md)
**Performance-critical code**: See [PERFORMANCE_REVIEW.md](PERFORMANCE_REVIEW.md)  
**Security-sensitive changes**: Run `python scripts/security_review.py`

## Quality Gates

Before approving any review:
- [ ] All team standards from code-review-standards skill have been applied
- [ ] Feedback follows constructive patterns
- [ ] Specific examples provided for improvements
- [ ] No critical issues remain unaddressed
- [ ] Author has clear next steps

## Integration Points

This agent works with:
- **code-review-standards skill**: For evaluation criteria and feedback patterns
- **testing-guidelines skill**: For test coverage requirements  
- **security-checklist skill**: For security review procedures
- **architecture-patterns skill**: For structural guidance