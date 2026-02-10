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

This command delegates to the `amplify-workflow` skill which handles:

1. **Step 1: Validate Prerequisites** - Node.js, npm, AWS credentials
2. **Step 2: Handle Missing Credentials** - STOP if AWS credentials not configured
3. **Step 3: Execute Workflow** - Determine phases, present plan, execute

Follow the complete workflow defined in the skill.

**Key rules:**
- Gen 2 ONLY (`defineAuth`, `defineData`, `defineStorage`, `defineFunction`)
- NO Gen 1 patterns (`amplify init`, `amplify push`)
- Always follow SOPs completely
- STOP if MCP tools fail (do not improvise)
