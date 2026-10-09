---
name: github-copilot-chatgpt-access
description: Configure GitHub Copilot agent workflows with OpenAI integrations, inspect GitHub repository visibility, and safely guide permission changes.
---
# GitHub Copilot + ChatGPT Access Skill

## Purpose
Help configure GitHub Copilot instructions, optional OpenAI API or MCP integration, and GitHub repository permissions across personal and organization accounts.

## Activation
Use when asked to connect ChatGPT/OpenAI to GitHub Copilot, troubleshoot missing GitHub repositories, or change GitHub access permissions.

## Workflow
1. Identify account owner, repository owner, organization, repository, and requested integration. Distinguish ChatGPT GitHub connector, Copilot Chat, OpenAI API, and MCP server. Never claim these are interchangeable.
2. Inventory existing access using `gh auth status`, `gh repo view OWNER/REPO`, and `gh api repos/OWNER/REPO/collaborators/USERNAME/permission` where authorized. Do not print tokens.
3. For organization repos, inspect organization policies, installed GitHub App repository selection, SSO authorization, membership, and fine-grained token repository permissions. Explain that identical GitHub login does not guarantee connector access to all organizations.
4. Propose the minimum permission changes. Show current and proposed access, scope, and consequences; obtain explicit confirmation before mutations.
5. Guide owner/admin to GitHub Settings > Applications > Installed GitHub Apps or Authorized OAuth Apps (as appropriate), select the ChatGPT/OpenAI integration if present, and adjust repository selection and organization approval. UI names may vary; never assert an app is installed without verification.
6. For GitHub Copilot, install repository instructions in `.github/copilot-instructions.md` and this skill in `.github/skills/github-copilot-chatgpt-access/SKILL.md` if the installed Copilot agent supports repository skills. Verify the active agent's skill discovery behavior.
7. For OpenAI API integrations, use a server-side environment variable `OPENAI_API_KEY`, never commit secrets, and only configure an MCP server when its actual documented transport and authentication are known. Do not claim that a ChatGPT subscription supplies an API key.
8. Validate with read-only access tests, then recheck requested repositories through the actual ChatGPT GitHub connector. A successful `gh` CLI read alone does not prove connector access.
9. Record a concise audit: requested change, approval, affected repository, prior role, new role, validation, and rollback path. Never expose credentials.

## Permission rules
- Default to read-only and least privilege.
- Never escalate to organization owner or repository admin merely to solve visibility.
- Require explicit approval before collaborator invitations, permission upgrades, GitHub App installations, SSO authorization, or organization policy changes.
- Never bypass organization security policy.
- Distinguish GitHub App permissions from human collaborator roles and Copilot seat licensing.

## Troubleshooting checklist
- Correct GitHub account and organization?
- Organization has approved the GitHub App?
- App installed on all repositories or selected repositories?
- Repository newly created since authorization?
- Organization SAML SSO authorization required?
- Private repository access allowed by policy?
- Copilot seat/feature enabled separately?
- Connector refresh/reauthorization needed?

## Success criteria
Report exactly which repositories were tested and which integration could access them. If a check cannot be performed, label it unverified rather than successful.
