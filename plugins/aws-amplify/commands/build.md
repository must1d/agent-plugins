---
description: Build full-stack apps with AWS Amplify Gen 2 - describe what you want to build
argument-hint: "[description of what to build]"
---

# Build with AWS Amplify Gen 2

**Request:** $ARGUMENTS

## Input Validation

If `$ARGUMENTS` is empty or unclear, ask:

```
What would you like to build? For example:
- "A todo app with user authentication"
- "Add a GraphQL API to my existing Next.js app"
- "Deploy my app to production"
```

## Execution

Delegate to the `amplify-workflow` skill and follow its complete workflow.
The skill handles prerequisite validation, phase planning, SOP retrieval,
and user confirmation gates.

Gen 2 ONLY — no Gen 1 patterns (`amplify init`, `amplify push`).
