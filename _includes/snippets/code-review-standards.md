---
name: code-review-standards
description: Apply team code review standards focusing on readability, modularity, and error handling. Use when reviewing code or when the user asks about code quality.
---

# Code Review Standards

## Evaluation Criteria

When reviewing code, check against our team values:

**Understandable Code**
- Variable names follow our naming convention (camelCase for variables, PascalCase for classes)
- Functions have single responsibilities and descriptive names
- Complex logic includes explanatory comments about *why*, not just *what*

**Modular Structures**  
- Features are separated into distinct modules/packages
- Classes have focused, testable responsibilities
- Avoid monolithic classes exceeding 200 lines

**Error Handling**
- All external calls (API, database, file system) include error handling
- Errors include contextual information for debugging
- User-facing errors provide actionable messages

## Review Checklist

- [ ] Names clearly describe purpose and data
- [ ] Functions are under 50 lines and single-purpose  
- [ ] No deeply nested conditionals (refactor with guard clauses)
- [ ] External dependencies are mocked in tests
- [ ] Error cases are explicitly handled
- [ ] Documentation explains why the code exists