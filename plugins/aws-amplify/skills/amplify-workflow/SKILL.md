---
name: amplify-workflow
description: Orchestrates AWS Amplify Gen 2 workflows for building full-stack apps with React, Next.js, Vue, Angular, Flutter, or Swift. Use when user wants to BUILD, CREATE, or DEPLOY Amplify projects, add authentication, data models, storage, GraphQL APIs, Lambda functions, or deploy to sandbox/production. Do NOT invoke for conceptual questions, comparisons, or troubleshooting unrelated to active development.
---

# Amplify Workflow

Orchestrated workflow for AWS Amplify Gen 2 development.

## When to Use This Workflow

Use for any Amplify Gen 2 work:
- Building a new full-stack application
- Adding features to an existing backend
- Connecting frontend to backend
- Deploying to sandbox or production

The workflow determines which phases apply based on your request.

**DO NOT invoke when:**
- User asks conceptual questions ("What is Amplify?", "How does defineData work?")
- User asks for comparisons ("Gen 1 vs Gen 2")
- User is troubleshooting existing issues unrelated to building
- User just wants information, not action

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
## ⚠️ AWS Credentials Required

I can't proceed without AWS credentials configured. Please set up your credentials first:

**📚 Setup Guide:** https://docs.amplify.aws/react/start/account-setup/

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

| Phase | Applies when |
|-------|--------------|
| 1: Backend | User needs to create or modify Amplify backend resources |
| 2: Sandbox | Backend code needs deployment for testing |
| 3: Frontend | Frontend needs to connect to Amplify backend |
| 4: Testing | App ready for local verification |
| 5: Production | User wants to deploy to production |

Common patterns:
- **New full-stack app:** 1 → 2 → 3 → 4 → 5
- **Add feature to existing backend:** 1 → 2
- **Redeploy after changes:** 2 only
- **Connect existing frontend:** 3 → 4
- **Deploy to production:** 5 only

---

## Present Plan and Confirm

Present to the user:

```
## 📋 Plan

### What I understood
- [Brief summary of what the user wants]

### 🛠️ Features
[list features if applicable]

### ⚛️ Framework
[framework if known]

### 📦 Phases I'll execute
1. [Phase name] - [one-line description] → SOP: [sop-name]
2. [Phase name] - [one-line description] → SOP: [sop-name]
...
(Include SOP name for phases 1, 2, 3, and 5. Phase 4 has no SOP.)

Ready to get started? ✨
```

**WAIT for user confirmation before proceeding.**

⚠️ **Once the user approves the plan, you MUST stick to it. Do not deviate from the planned phases or SOPs unless the user explicitly asks for changes.**

---

## Execute Phases

Execute each applicable phase IN SEQUENCE.

**When starting a phase, announce it as a header:**
```
## ⚙️ Phase 1: Backend (SOP: amplify-backend-implementation)
[Next: Phase 2: Sandbox Deployment]

## 🚀 Phase 2: Sandbox Deployment (SOP: amplify-deployment-guide)
[Next: Phase 3: Frontend Integration]

## 🎨 Phase 3: Frontend Integration (SOP: amplify-frontend-integration)
[Next: Phase 4: Local Testing]

## 🧪 Phase 4: Local Testing
[Next: Phase 5: Production Deployment]

## 🌐 Phase 5: Production Deployment (SOP: amplify-deployment-guide)
```
Omit "[Next: ...]" if it's the last phase in your plan.

---

### Phase 1: Backend

⚠️ **Do NOT write any code until you have retrieved and read the SOP.**

Use the SOP retrieval tool to get **"amplify-backend-implementation"** and follow it completely.

**After completion:**
- Summarize what was created
- **STOP and ask:** "Phase 1 complete. Ready to proceed to Phase 2: Sandbox Deployment? 🚀"
- **WAIT for user confirmation before proceeding.**

---

### Phase 2: Sandbox Deployment

⚠️ **Do NOT run any commands until you have retrieved and read the SOP.**

Use the SOP retrieval tool to get **"amplify-deployment-guide"** and follow it for SANDBOX deployment.

**After completion:**
- Confirm deployment succeeded and `amplify_outputs.json` exists
- **STOP and ask:** "Phase 2 complete. Ready to proceed to Phase 3: Frontend Integration? 🎨"
- **WAIT for user confirmation before proceeding.**

---

### Phase 3: Frontend Integration

**Prerequisite:** `amplify_outputs.json` must exist. If not, run Phase 2 first.

⚠️ **Do NOT write any code until you have retrieved and read the SOP.**

Use the SOP retrieval tool to get **"amplify-frontend-integration"** and follow it completely.

**After completion:**
- Summarize integration work
- **STOP and ask:** "Phase 3 complete. Ready to proceed to Phase 4: Local Testing? 🧪"
- **WAIT for user confirmation before proceeding.**

---

### Phase 4: Local Testing

Present to the user:

```
## 🧪 Time to test!

### Start your dev server
[framework-specific command]

### Try out these features
[list features implemented]

Let me know how it goes! 🤞
```

**After user confirms testing is successful:**
- **STOP and ask:** "Phase 4 complete. Ready to proceed to Phase 5: Production Deployment? 🌐"
- **WAIT for user confirmation before proceeding.**

---

### Phase 5: Production Deployment

⚠️ **Do NOT run any commands until you have retrieved and read the SOP.**

Use the SOP retrieval tool to get **"amplify-deployment-guide"** and follow it for PRODUCTION deployment.

**After completion:**

```
## 🎉 You're live!

### 🌐 Production URL
[url]

### 🔧 Amplify Console
https://console.aws.amazon.com/amplify/home

Your app is now deployed! Future updates: just push to your repo → auto-deploys ✨
```

---

## Troubleshooting

If issues occur during any phase:
1. Check the SOP's troubleshooting section first
2. Use documentation tools to search AWS Amplify docs for the error message
3. Read the relevant documentation page

**After resolving the issue, immediately return to the SOP and continue from where you left off. Do not abandon the workflow.**
