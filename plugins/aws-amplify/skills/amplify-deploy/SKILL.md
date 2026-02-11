---
name: amplify-deploy
description: Deploy AWS Amplify Gen 2 applications to sandbox (development) or production environments. MUST be used when user wants to DEPLOY, RELEASE, PROMOTE, or PUBLISH an Amplify app. Handles both sandbox deployment for testing and production deployment for going live. This is the mandatory entry point for all Amplify deployment operations.
---

# Amplify Deploy

Deploy an AWS Amplify Gen 2 application to sandbox or production.

## When to Use This Skill

Use for any Amplify deployment:

- Deploy to sandbox for development/testing
- Deploy/promote to production
- Redeploy after code changes
- Any request involving "deploy my Amplify app"

---

## Invocation Context

This skill may be invoked standalone or from the `amplify-workflow` orchestrator.

- **From orchestrator:** The deployment type (sandbox or production) is specified
  by the caller. Do not re-ask the user. Prerequisites (Node.js, npm, AWS
  credentials) were already validated — skip the SOP's dependency verification step.
- **Standalone:** Determine deployment type from the user's request. Validate
  prerequisites per the SOP.

## Mapping Deployment Targets to SOP Parameters

The SOP uses the parameter name `deployment_type` with values `sandbox` or `cicd`.
Map user/caller intent as follows:

- "sandbox", "development", "testing" → SOP deployment_type: **sandbox**
- "production", "prod", "live", "release", "cicd" → SOP deployment_type: **cicd**

---

## Retrieve and Follow the SOP

The **"amplify-deployment-guide"** SOP must be retrieved **at least once**
during the conversation using the SOP retrieval tool from `aws-mcp`.

**All steps in the SOP must be followed** for any type of deployment
(sandbox or production). The SOP contains the latest and most accurate
deployment procedures. Do not improvise or skip steps.

### Critical Rules

1. **Follow the SOP completely** - Do not improvise or skip steps
2. **If you encounter an error:**
   - Fix the immediate issue
   - Return to the SOP and continue from where you left off
   - Do NOT abandon the SOP
3. **If you lose track of where you were:**
   - Retrieve the SOP again
   - Identify which step you completed last
   - Continue from the next step
