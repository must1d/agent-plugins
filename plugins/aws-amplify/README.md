# AWS Amplify Claude Plugin

Build full-stack applications with AWS Amplify Gen 2 using TypeScript code-first development.

## Overview

This plugin provides a workflow orchestrator for AWS Amplify Gen 2 development. It validates prerequisites, analyzes project state, retrieves official AWS SOPs via MCP, and guides you through backend creation, deployment, and frontend integration.

## Features

- **SOP-Driven**: Uses official AWS Amplify Standard Operating Procedures via MCP
- **Phased Workflow**: Backend → Sandbox → Frontend → Testing → Production
- **Framework Support**: React, Next.js, Vue, Angular, React Native, Flutter, Swift, Android
- **Gen 2 Only**: TypeScript code-first (`defineAuth`, `defineData`, `defineStorage`, `defineFunction`)

## Prerequisites

- Node.js 18.x or later
- AWS credentials configured (`aws configure` or `aws sso login`)
- `uv` package manager for MCP server: https://docs.astral.sh/uv/getting-started/installation/

## Installation

### Option 1: Marketplace (recommended)

```bash
/plugin marketplace add awslabs/agent-plugins
/plugin install aws-amplify@awslabs-agent-plugins
```

### Option 2: Load locally (for testing)

```bash
git clone https://github.com/awslabs/agent-plugins
claude --plugin-dir ./agent-plugins/plugins/aws-amplify
```

## Usage

### Slash Command

```
/aws-amplify:build I want to create a todo app with authentication
```

### Auto-Invoked Skill

The `amplify-workflow` skill is automatically invoked when you ask Claude to build, modify, or deploy an Amplify Gen 2 backend or full-stack app, for example:

- "Create a new Amplify backend with auth and a todo data model"
- "Add S3 storage and a Lambda function to my existing Amplify project"

The `amplify-deploy` skill is the mandatory entry point for all Amplify deployments (sandbox and production). It is automatically invoked for deployment requests, for example:

- "Deploy my Amplify sandbox environment"
- "Promote my sandbox to production"
- "Release my Amplify app"

When `amplify-workflow` reaches its deployment phases (Phase 2: Sandbox, Phase 5: Production), it delegates to `amplify-deploy` automatically.

These skills are **not** used for conceptual questions about Amplify, comparisons with other frameworks, or troubleshooting existing projects—ask those as normal questions without expecting the workflow to start. For build/create/deploy tasks, just describe what you want in natural language.

## Workflow Phases

| Phase      | Description                     | Handled By                            |
| ---------- | ------------------------------- | ------------------------------------- |
| Backend    | Create/modify Amplify resources | SOP: `amplify-backend-implementation` |
| Sandbox    | Deploy to sandbox for testing   | `amplify-deploy` skill                |
| Frontend   | Connect frontend to backend     | SOP: `amplify-frontend-integration`   |
| Testing    | Local verification              | Manual                                |
| Production | Deploy to production            | `amplify-deploy` skill                |

**Common Patterns:**

- New app: Backend → Sandbox → Frontend → Testing → Production
- Add feature: Backend → Sandbox
- Redeploy: Sandbox only
- Connect UI: Frontend → Testing
- Go live: Production only

## Plugin Structure

```
aws-amplify/
├── .claude-plugin/
│   └── plugin.json          # Plugin manifest
├── commands/
│   └── build.md             # /aws-amplify:build command
├── skills/
│   ├── amplify-deploy/
│   │   └── SKILL.md         # Deployment skill (sandbox & production)
│   └── amplify-workflow/
│       └── SKILL.md         # Auto-invoked orchestrator
├── .mcp.json                # AWS MCP server config
└── README.md
```

## AWS Credentials

Must be configured before use:

```bash
# Option 1: Access keys
aws configure

# Option 2: SSO
aws sso login

# Verify
aws sts get-caller-identity
```

## MCP Server

This plugin requires the AWS MCP server for SOP retrieval. It's automatically configured via `.mcp.json`.

Verify it's working:

```
/mcp
```

Should show `aws-mcp` as active.

**If MCP is unavailable**, the plugin will STOP and ask you to configure it. It will not proceed without MCP.

**Note:** The MCP endpoint (`us-east-1.api.aws`) is the API location for SOP
retrieval only. It does not affect which region your Amplify resources deploy
to — deployment region is controlled by your AWS credentials and CLI configuration.

## License

Apache-2.0

## Resources

- [AWS Amplify Docs](https://docs.amplify.aws/)
- [Amplify Gen 2 Guide](https://docs.amplify.aws/react/start/)
- [Claude Code Plugins](https://code.claude.com/docs/en/plugins)
- [Model Context Protocol](https://modelcontextprotocol.io/)
