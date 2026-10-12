# Go-live checklist

The human administrator records evidence privately. Every unchecked item is a deployment gate, not work automatically completed by reading this repository.

- [ ] Dedicated standard Windows research account with no accessible personal credentials/files.
- [ ] Dedicated Hermes research profile; installed version and actual profile home recorded.
- [ ] Local model runner, serving ID, endpoint, context, and tool-call support verified.
- [ ] Hosted auxiliary/fallback/delegation and paid search routes disabled or shown absent.
- [ ] Kali identity and dedicated unprivileged user recorded; no broad sudo/admin groups.
- [ ] All lab VM NICs and routes inspected; no direct home-LAN attachment.
- [ ] External firewall implements exact target access, restricted SSH, management blocks, and deliberate download egress.
- [ ] IPv4, IPv6, overlay routes, DNS, and metadata/link-local behavior accounted for.
- [ ] Narrow SSH path tested; host-key fingerprint verified through trusted console.
- [ ] No host mounts, forwarded agents, reusable admin keys, Proxmox tokens, or personal cookies in Kali.
- [ ] Trusted VM baseline and private recovery evidence available.
- [ ] All enabled tools audited for execution location, files, credentials, and network access.
- [ ] Profile state synchronization and host artifact import behavior understood and tested with dummy files.
- [ ] SOUL.md and AGENTS.md actually load; critical policy survives reset/compaction.
- [ ] Human-approved private scope loaded with exact targets, techniques, expiry, rate, and resource limits.
- [ ] Containment verification uses explicitly approved endpoints, bounded checks, and firewall evidence.
- [ ] Behavioral acceptance scenarios pass with the actual model and deployment tools.
- [ ] SSH failure and unavailable local inference do not trigger local or paid-provider fallback.
- [ ] Stop mechanism tested; child/background processes accounted for.
- [ ] Publication workflow excludes private scope, findings, configuration, and synchronized artifacts.

After a change to Hermes, the model, tools, SSH, VM network, privileges, or firewall, repeat the checks affected by that change. Review the whole boundary if the change introduces a new route to the workstation or new remote-to-host imports.
