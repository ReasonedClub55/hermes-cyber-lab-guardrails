# Hermes Cyber Lab Guardrails

Give a local research agent useful freedom inside an authorized lab while protecting the workstation, hypervisor, and home network.

Designed for Hermes Desktop on Windows 11, a locally hosted model, and Kali on a separate Proxmox server. All repository files are Markdown. No paid model API, cloud inference, or model API key is required by this repository. SSH keys are still credentials and must be protected.

**This repository is a behavioral policy, not a sandbox.** Reading these files cannot restrict a process, guarantee model compliance, configure a firewall, or make downloaded code safe. Use the enforcement and acceptance steps before enabling research tools.

## Start here

1. Read [the design and its limits](docs/DESIGN.md).
2. Follow [network isolation](docs/NETWORK.md) and [SSH setup](docs/SSH.md) as the human administrator. Changes to Windows, Proxmox, SSH, or firewall configuration need your approval.
3. Follow [Hermes integration](docs/HERMES-SETUP.md). Use a dedicated research profile and Windows standard account. Confirm every enabled tool's execution location.
4. Copy [the scope template](templates/SCOPE.example.md) to a **private directory outside this public checkout**, fill it in, and approve it. An empty or example scope authorizes no testing.
5. Load [AGENTS.md](AGENTS.md) as persistent project instructions and [SOUL.md](SOUL.md) into the research profile only. Keep the private scope accessible in the verified execution environment. Use [the bootstrap prompt](templates/BOOTSTRAP.md) for the first session.
6. Run [acceptance scenarios](tests/ACCEPTANCE.md), record actual results privately, and complete [the go-live checklist](docs/GO-LIVE.md).

## What the agent may do

Within a current, human-approved scope: investigate lab findings, run bounded tests, download tools from checked sources, install reviewed user-level dependencies, and iterate inside Kali. Internet access for documentation and downloads is distinct from permission to test an Internet target.

It must ask before adding a target, changing either physical host or lab infrastructure, escalating privileges outside a specific grant, performing a destructive test, or publishing artifacts. It must stop when identity, scope, containment, or execution location is uncertain. Unanswered approval requests remain pending; elapsed time is never permission.

## Files

| File | Purpose |
| --- | --- |
| [AGENTS.md](AGENTS.md) | Compact always-loaded operational rules |
| [SOUL.md](SOUL.md) | Research-profile identity and durable safety boundaries |
| [SECURITY.md](SECURITY.md) | Policy authority, threat model, disclosure, limitations |
| [docs/DESIGN.md](docs/DESIGN.md) | Why each boundary exists and what enforces it |
| [docs/HERMES-SETUP.md](docs/HERMES-SETUP.md) | Verified integration points and version-sensitive checks |
| [docs/NETWORK.md](docs/NETWORK.md) | Proxmox lab separation and firewall requirements |
| [docs/SSH.md](docs/SSH.md) | Least-privilege access to Kali |
| [docs/TOOLS.md](docs/TOOLS.md) | Download, dependency, installation, and execution policy |
| [docs/OPERATIONS.md](docs/OPERATIONS.md) | Autonomous research loop and approval decisions |
| [docs/RECOVERY.md](docs/RECOVERY.md) | Stop, contain, recover, and resume |
| [docs/LOCAL-MODEL.md](docs/LOCAL-MODEL.md) | Local inference without paid model calls |
| [docs/GO-LIVE.md](docs/GO-LIVE.md) | Deployment gates |
| [docs/SOURCES.md](docs/SOURCES.md) | Primary references and verification limits |
| [templates/SCOPE.example.md](templates/SCOPE.example.md) | Private scope and capability grants |
| [templates/BOOTSTRAP.md](templates/BOOTSTRAP.md) | First-session instruction |
| [templates/SESSION.md](templates/SESSION.md) | Private audit record |
| [tests/ACCEPTANCE.md](tests/ACCEPTANCE.md) | Behavioral and infrastructure acceptance checks |
| [tests/REVIEW.md](tests/REVIEW.md) | Repository review and remaining deployment work |

## Public repository hygiene

Never commit filled scopes, real network addresses, SSH keys, credentials, captures, exploit output, VM images, local configuration, or session logs. This Markdown-only repository intentionally does not contain an ignore file: keep runtime state and private artifacts elsewhere, and inspect the staged diff before every publication. Examples use documentation addresses or placeholders and are not approved targets.

## Deployment status

The documents are prepared and reviewed. This repository has not configured or tested your Windows account, Hermes installation, Kali VM, Proxmox firewall, or network. Those are explicit go-live gates. Do not confuse a finished repository with a contained running agent.
