# Tool acquisition and execution policy

## Allowed autonomous path

Within a verified Kali session, the agent may fetch public documentation and reviewed tools, inspect them, create isolated user-level environments, and run bounded tests against approved targets. Elevated installation requires a specific prior grant or administrator action. Every new tool must pass the following checks; a previously approved project does not automatically approve a different artifact or version.

1. Identify the canonical maintainer or official distribution source. Check spelling, ownership, release history, and whether the requested project matches the intended tool. Prefer distribution-signed Kali packages or upstream releases over random mirrors.
2. Record the source URL, resolved redirect destinations, version/commit, license, fetch date, artifact hash, and signature/checksum verification result. A checksum from the same untrusted download page gives integrity evidence, not independent authenticity. When upstream provides signatures, verify them against an independently established signing key.
3. Review the actual acquisition path, including repository hooks, submodules, Git filters, archives, dependency resolution, and build/install steps. Do not clone or install under privileged or credential-bearing accounts. Inspect archive paths and links before extraction; reject traversal outside the workspace and suspicious symlink/hardlink destinations.
4. Inspect installers and dependencies for host detection, credential access, network callbacks, startup changes, privilege escalation, destructive operations, unexplained obfuscation, and extra downloads. Installing a dependency may execute code before the main tool starts. Treat package-manager hooks and source builds as execution.
5. Pin the tool and practical dependency versions. Use a private per-tool environment. Do not overwrite system Python or add unsigned package repositories. Do not disable certificate or package-signature validation to get an installation through.
6. Before execution, confirm scope, target arguments, privilege, resource limits, output location, and a way to stop the process. First run help/version or a synthetic offline input where feasible. Keep the process unprivileged; do not use root as a convenience.
7. Record observed outbound requests and unexpected behavior. Stop and isolate on credential requests, target expansion, unexplained callbacks, privilege changes, or modification of trusted policy/state.

For public retrieval, validate every redirect and secondary download before following it. Permit only the intended HTTPS source path; reject redirects to local/loopback, private lab or household addresses, metadata endpoints, file URLs, alternate protocols, or credential-bearing URLs. Recheck DNS results at connection time where the retrieval tool supports it. Apply the same checks to submodules, dependencies, and installer-triggered downloads. If the tool cannot expose or constrain these paths, use an administrator-reviewed acquisition route. External egress filtering is needed against DNS rebinding and hidden fetches; model reasoning alone cannot enforce these checks.

## Stop and ask

- The source cannot be established, a signature fails, or download redirects lead to a new unreviewed source.
- A precompiled binary has insufficient provenance or cannot be assessed to the required confidence. Prefer a better documented alternative; otherwise request a separate disposable quarantine environment with no credentials and controlled networking.
- The tool requires guest root, raw sockets, kernel modules, disabling protections, a listener/callback, or new network access outside the current grant.
- A package installation requires system changes without a previously reviewed administration mechanism.
- The action involves credential attacks, persistence, destructive tests, malware detonation, or broad capture outside explicit capability grants.

Approval does not turn uncertain code into trusted code. Document the residual risk and use stronger containment if the human chooses to proceed. No approval inside this lab authorizes workstation or hypervisor compromise.

## Download traffic versus research traffic

Outbound web access allows retrieving a project's ordinary public pages and artifacts. It does not allow vulnerability probing, authentication bypass, fuzzing, scanning, scraping private content, or uploading lab artifacts to that site. DNS resolvers, proxies, gateways, and package servers are infrastructure, not pentest targets.

Public HTTPS can carry uploads. If the external firewall allows arbitrary HTTPS, acknowledge that it cannot enforce download-only behavior. For suspicious specimens, use a separate offline/disposable analysis environment rather than ordinary Kali with live Internet access.

## Host artifact handling

Do not copy tool executables, payloads, startup files, or generated skills onto Windows automatically. Text reports must be inspected and sanitized. Use a separate quarantine transfer directory; do not preview untrusted active documents in a privileged application. Review any remote-to-host state changes before activating them in future sessions.
