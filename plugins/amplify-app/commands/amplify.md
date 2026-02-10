---
description: Build fullstack applications with AWS Amplify Gen2 using prompt-driven development (plan first, then build)
---

# Amplify Workflow

Orchestrated workflow for AWS Amplify Gen 2 development using prompt-driven development.

## Approach: Plan First, Then Build

This workflow uses a two-phase approach:
1. **Planning Phase** - Retrieve SOPs and create a detailed implementation plan
2. **Building Phase** - Execute the plan precisely

## When to Use This Workflow

Use for any Amplify Gen 2 work:
- Building a new full-stack application
- Adding features to an existing backend
- Connecting frontend to backend
- Deploying to sandbox or production

---

## Critical Rules

1. **Always retrieve and follow SOPs completely** - Do not improvise or skip steps
2. **Never use Gen 1 patterns** - This is for Amplify Gen 2 only (TypeScript code-first, `defineAuth`/`defineData`/`defineStorage`/`defineFunction`)
3. **Plan before building** - Create a complete plan before writing any code
4. **Research before planning** - If unsure about Amplify capabilities, use documentation tools first
5. **Wait for confirmation** - Get user approval of the plan before building

---

## Step 1: Understand the Request

Read all necessary project files to understand the current state:
- `amplify/` directory (if exists)
- `package.json`
- Frontend code structure
- Any existing Amplify configuration

Determine which phases apply:

| Phase | Applies when |
|-------|--------------|
| Backend | User needs to create or modify Amplify backend resources |
| Deployment | Backend code needs deployment for testing or production |
| Frontend | Frontend needs to connect to Amplify backend |

---

## Step 2: Planning Phase

**Use the amplify-planner agent** to create a detailed implementation plan.

The planner will:
1. Retrieve relevant SOPs using the SOP retrieval tool:
   - **amplify-backend-implementation** - for auth, data, storage, functions
   - **amplify-deployment-guide** - for sandbox or production deployment
   - **amplify-frontend-integration** - for connecting frontend to backend

2. Analyze requirements against the SOPs

3. Create a detailed implementation plan specifying:
   - Exact files to create with their contents
   - Commands to run
   - Validation steps
   - Constraints from SOPs

Present the plan to the user:

```
## Implementation Plan

### What I understood
[Summary of requirements]

### Phases
[List phases that apply]

### Detailed Plan
[Full specification from planner agent]

---

Does this plan look correct? Ready to build?
```

**WAIT for user confirmation before proceeding.**

---

## Step 3: Building Phase

**Use the amplify-builder agent** to execute the plan.

The builder will:
1. Follow the plan exactly
2. Create files as specified
3. Run commands as specified
4. Validate each step
5. Report progress and any issues

Execute phases in sequence:

### Backend (if applicable)
- Create `amplify/` directory structure
- Create resource files (auth, data, storage, functions)
- Validate TypeScript syntax

**After completion, confirm with user before proceeding.**

### Deployment (if applicable)
- Run deployment commands (`npx ampx sandbox --once` or CI/CD setup)
- Validate `amplify_outputs.json` is generated
- Report deployment status

**After completion, confirm with user before proceeding.**

### Frontend (if applicable)
- Install dependencies
- Configure Amplify in entry point
- Implement integrations (auth, data, storage)
- Follow framework-specific patterns

**After completion, confirm with user.**

---

## Step 4: Verification

Present testing instructions:

```
## Ready to Test

### Start your dev server
[framework-specific command]

### Features to test
[list from plan]

Let me know how it goes!
```

---

## Troubleshooting

If issues occur:
1. Retrieve the relevant SOP again using the SOP retrieval tool
2. Check the SOP's troubleshooting section
3. Use read_documentation tool to search AWS Amplify docs for the error
4. Update the plan if needed and re-execute

---

## User Request

${ARGUMENTS}
