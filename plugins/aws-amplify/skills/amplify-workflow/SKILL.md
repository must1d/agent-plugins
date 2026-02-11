---
name: amplify-workflow
description: Orchestrates AWS Amplify Gen 2 workflows for building full-stack apps with React, Next.js, Vue, Angular, React Native, Flutter, Swift, or Android. Use when user wants to BUILD or CREATE Amplify projects, add authentication, data models, storage, GraphQL APIs, or Lambda functions. Not for conceptual questions, comparisons, or troubleshooting unrelated to active development.
---

# Amplify Workflow

Orchestrated workflow for AWS Amplify Gen 2 development.

## Scope

This workflow covers building and creating Amplify Gen 2 projects through a phased
approach. Deployment phases delegate to the `amplify-deploy` skill automatically.

---

## Step 1: Validate Prerequisites

Run these checks before proceeding:

1. **Node.js 18.x or later**

   ```bash
   node --version
   ```

2. **npm available**

   ```bash
   npm --version
   ```

3. **AWS credentials configured** (CRITICAL)

   ```bash
   AWS_PAGER="" aws sts get-caller-identity
   ```

## Step 2: Handle Missing AWS Credentials

If the AWS credentials check fails, **STOP** and present this message to the user:

```
## AWS Credentials Required

I can't proceed without AWS credentials configured. Please set up your credentials first:

**Setup Guide:** https://docs.amplify.aws/react/start/account-setup/

**Quick options:**
- Run `aws configure` to set up access keys
- Run `aws sso login` if using AWS IAM Identity Center

Once your credentials are configured, **come back and start a new conversation** to continue building with Amplify.
```

**Do NOT proceed with Amplify work until credentials are configured.** The user must restart the conversation after setting up credentials.

## Step 3: Execute Workflow

Once all prerequisites pass, follow the workflow below.

---

## Critical Rules

1. **Always follow SOPs completely** - Do not improvise or skip steps
2. **Never use Gen 1 patterns** - This is for Amplify Gen 2 only (TypeScript code-first, `defineAuth`/`defineData`/`defineStorage`/`defineFunction`)
3. **Understand before planning** - Read all necessary project files (e.g., `amplify/`, `package.json`, existing code) to understand the current state BEFORE proposing a plan
4. **Research before planning** - If unsure about Amplify capabilities or best practices, use documentation tools to search and read AWS Amplify docs BEFORE presenting the plan
5. **Wait for confirmation after each phase** - After completing each phase, STOP and ask the user to confirm before proceeding to the next phase
6. **If you encounter an error or get sidetracked:**
   - Fix the immediate issue
   - Return to the SOP and continue from where you left off
   - Do NOT abandon the SOP or start improvising
7. **If you lose track of where you were in the SOP:**
   - Use the SOP retrieval tool to get the SOP again
   - Identify which step you completed last
   - Continue from the next step

---

## Determine Applicable Phases

Based on the user's request and project state, determine which phases apply:

| Phase         | Applies when                                               |
| ------------- | ---------------------------------------------------------- |
| 1: Backend    | User needs to create or modify Amplify backend resources   |
| 2: Sandbox    | Deploy to sandbox for testing (via `amplify-deploy` skill) |
| 3: Frontend   | Frontend needs to connect to Amplify backend               |
| 4: Testing    | App ready for local verification                           |
| 5: Production | Deploy to production (via `amplify-deploy` skill)          |

Common patterns:

- **New full-stack app:** 1 → 2 → 3 → 4 → 5
- **Backend only (no frontend):** 1 → 2
- **Add feature to existing backend:** 1 → 2
- **Redeploy after changes:** 2 only
- **Connect existing frontend:** 3 → 4
- **Deploy to production:** 5 only

**IMPORTANT: Only include phases that the user actually needs.** If the user asks for backend work only (e.g., "add auth", "create a data model", "add storage"), do NOT include Phase 3 (Frontend Integration) or Phase 4 (Local Testing). Frontend phases should only be included when the user explicitly asks for frontend work, a full-stack app, or to connect a frontend to Amplify.

---

## Present Plan and Confirm

Present to the user:

```
## Plan

### What I understood
- [Brief summary of what the user wants]

### Features
[list features if applicable]

### Framework
[framework if known]

### Phases I'll execute
1. [Phase name] - [one-line description] → SOP: [sop-name]
2. [Phase name] - [one-line description] → SOP: [sop-name]
...
(Include SOP name for phases 1 and 3. Phases 2 and 5 use the `amplify-deploy` skill. Phase 4 has no SOP.)

Ready to get started?
```

**WAIT for user confirmation before proceeding.**

**Once the user approves the plan, you MUST stick to it. Do not deviate from the planned phases or SOPs unless the user explicitly asks for changes.**

---

## Execute Phases

Execute each applicable phase IN SEQUENCE.

**When starting a phase, announce it as a header:**

```
## Phase 1: Backend (SOP: amplify-backend-implementation)
[Next: Phase 2: Sandbox Deployment]

## Phase 2: Sandbox Deployment (via amplify-deploy skill)
[Next: Phase 3: Frontend Integration]

## Phase 3: Frontend Integration (SOP: amplify-frontend-integration)
[Next: Phase 4: Local Testing]

## Phase 4: Local Testing
[Next: Phase 5: Production Deployment]

## Phase 5: Production Deployment (via amplify-deploy skill)
```

Omit "[Next: ...]" if it's the last phase in your plan.

---

### Phase 1: Backend

**CRITICAL: Do NOT create frontend scaffolding or templates during this phase.** Do not run `create-next-app`, `create-react-app`, `create-vite`, `npm create`, or any frontend project generators. Phase 1 is strictly for Amplify backend resources (the `amplify/` directory). If a frontend project already exists, leave it untouched. If no frontend project exists and the user only asked for backend work, do NOT create one.

Before creating any files, ensure `.gitignore` exists in the project root and includes:
`node_modules/`, `.env*`, `amplify_outputs.json`, `.amplify/`, `dist/`, `build/`.
Create or update it if these entries are missing.

**Do NOT write any code until you have retrieved and read the SOP.**

Use the SOP retrieval tool to get **"amplify-backend-implementation"** and follow it completely.

**SOP overrides for orchestrator context:**

- **Skip the SOP's Step 12** ("Determine Next SOP Requirements") — phase sequencing is controlled by this workflow, not the SOP.
- **Prerequisites were already validated** in Step 1 of this workflow. The SOP's dependency verification (Step 1) can be skipped.

**After completion:**

- Summarize what was created
- **STOP and ask:** "Phase 1 complete. Ready to proceed to Phase 2: Sandbox Deployment?"
- **WAIT for user confirmation before proceeding.**

---

### Phase 2: Sandbox Deployment

**Delegate to the `amplify-deploy` skill** for sandbox deployment.

When invoking, indicate that the deployment target is **sandbox (development)**.
Also indicate that prerequisites (Node.js, npm, AWS credentials) were already
validated in Step 1 of this workflow so the deploy skill can skip re-verification.

**After completion:**

- Confirm deployment succeeded and `amplify_outputs.json` exists
- **STOP and ask:** "Phase 2 complete. Ready to proceed to Phase 3: Frontend Integration?"
- **WAIT for user confirmation before proceeding.**

---

### Phase 3: Frontend Integration

**Prerequisite:** `amplify_outputs.json` must exist. If not, run Phase 2 first.

**Do NOT write any code until you have retrieved and read the SOP.**

Use the SOP retrieval tool to get **"amplify-frontend-integration"** and follow it completely.

**SOP overrides for orchestrator context:**

- **Skip the SOP's Step 12** ("Determine Next SOP Requirements") — phase sequencing is controlled by this workflow, not the SOP.
- **Prerequisites were already validated** in Step 1 of this workflow.

**After completion:**

- Summarize integration work
- **STOP and ask:** "Phase 3 complete. Ready to proceed to Phase 4: Local Testing?"
- **WAIT for user confirmation before proceeding.**

---

### Phase 4: Local Testing

Present to the user:

```
## Time to test

### Start your dev server
[framework-specific command]

### Try out these features
[list features implemented]

Let me know how it goes!
```

**After user confirms testing is successful:**

- **STOP and ask:** "Phase 4 complete. Ready to proceed to Phase 5: Production Deployment?"
- **WAIT for user confirmation before proceeding.**

---

### Phase 5: Production Deployment

**Delegate to the `amplify-deploy` skill** for production deployment.

When invoking, indicate that the deployment target is **production** (maps to
`cicd` deployment type in the SOP). Also indicate that prerequisites were
already validated in Step 1 of this workflow.

**After completion:**

```
## You're live!

### Production URL
[url]

### Amplify Console
https://console.aws.amazon.com/amplify/home

Your app is now deployed! Future updates: just push to your repo for auto-deploys.
```

---

## Troubleshooting

If issues occur during any phase:

1. Check the SOP's troubleshooting section first
2. Use documentation tools to search AWS Amplify docs for the error message
3. Read the relevant documentation page

**After resolving the issue, immediately return to the SOP and continue from where you left off. Do not abandon the workflow.**
