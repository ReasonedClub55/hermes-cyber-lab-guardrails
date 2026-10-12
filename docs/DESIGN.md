# Design decisions and their reasons

## Separate reasoning, execution, and administration

The model can run on the gaming PC for performance. Research commands should run in Kali. Windows and Proxmox administration stay with the human. Keep the lab firewall and SSH access configuration out of the research user's control. This makes a bad agent decision less likely to become a host or network change.

Recommended baseline: a dedicated Windows standard account and Hermes research profile; a dedicated unprivileged Kali account; a separate lab network behind an administrator-controlled firewall; and a narrow inbound SSH path to Kali. A Hermes profile by itself is not an OS isolation boundary.

For stronger containment, place the agent runtime in a separate hardened controller VM, use a narrowly reachable local model endpoint, and keep Kali as a separate execution VM. This limits the risk of host tools and synchronized state, but requires deliberate endpoint access controls. Running the agent directly on Kali exposes its controller state to compromised research tools and is a weaker separation of roles. The model endpoint does not need a paid API key; it still needs network access protection.

## The autonomy budget

Grant techniques and bounded resources against exact lab targets, rather than approving every harmless command. The agent can change tools and iterate within that budget. Adding targets, relaxing containment, increasing privileges, or using destructive techniques changes the budget and needs human review.

Authorization has two dimensions: **where** the agent may interact, and **what** it may do there. A named target does not authorize denial of service, credential attacks, persistence, or destruction by default.

## Allow downloads without allowing Internet pentesting

Documentation and downloads support research. They do not add the download host to the test scope. Keep source verification, signature checking where available, installer review, and first execution separate. A pinned commit improves repeatability; it does not guarantee safety.

## Keep the guest disposable

No personal files, browser sessions, production credentials, host shares, USB passthrough, Proxmox tokens, or reusable administrative keys belong in Kali. Use synthetic target credentials and snapshots. A guest that becomes compromised should be replaceable without losing important data or exposing the household.

## Treat the workstation as still exposed

Moving terminal execution to SSH does not establish that every enabled connector, browser, computer-use tool, file tool, MCP server, and subprocess has moved. Audit each one. If a research action can run on Windows, disable that route in the research profile and enforce account restrictions. Keep exported files inert and quarantined until reviewed.

## Keep the policy small enough to remain present

AGENTS.md carries the compact rules; detailed documents explain implementation and decisions. SOUL.md reinforces durable boundaries. Critical rules should remain in context after reset and compaction. More Markdown is not necessarily more protection: acceptance tests should show which instructions the actual model retains.

## Evidence over guarantees

Deployment is successful only when both behavioral scenarios and real network/account checks pass. Track the installed Hermes version, model runner, model identifier, tool inventory, and acceptance results. Repeat the affected checks after changes. Never claim the repository alone secured a machine.
