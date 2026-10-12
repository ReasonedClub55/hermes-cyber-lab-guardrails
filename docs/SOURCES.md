# Primary references and verification limits

Reviewed on 2026-10-12. These are live sources; behavior in an older installed release may differ. The policies in this repository are original deployment recommendations, not claims that these products automatically implement every proposed control.

| Source | Used to verify |
| --- | --- |
| [Hermes configuration](https://hermes-agent.nousresearch.com/docs/user-guide/configuration) | SSH backend/environment settings and documented profile-state sync |
| [Hermes context files](https://hermes-agent.nousresearch.com/docs/user-guide/features/context-files) | Persistent instruction integration; verify selection in your release |
| [Hermes host safety](https://hermes-agent.nousresearch.com/docs/guides/secure-hermes-on-a-work-machine) | Manual flagged-command approvals, deny patterns, and limitations |
| [Hermes Desktop](https://github.com/NousResearch/hermes-agent/blob/main/website/docs/user-guide/desktop.md) | Official Desktop documentation location |
| [Hermes quickstart](https://hermes-agent.nousresearch.com/docs/getting-started/quickstart) | Custom endpoint route for local inference |
| [Proxmox network documentation source](https://github.com/proxmox/pve-docs/blob/master/pve-network.adoc) | Bridge concepts and network separation |
| [Proxmox firewall documentation source](https://github.com/proxmox/pve-docs/blob/master/pve-firewall.adoc) | Guest interface firewall capabilities and activation checks |
| [OpenSSH sshd_config manual](https://man.openbsd.org/sshd_config) | Server restriction directives; compare installed Kali manual |

Proxmox's rendered documentation pages could not be retrieved during preparation; its official documentation source was used instead. No version-specific Proxmox firewall commands are prescribed because the installed version and backend are unknown.

The Windows account permissions, Hermes configuration, SSH compatibility/host-key behavior, state sync, Kali networking, and target identity were not inspected or changed. No model behavioral or live containment tests have been run. Follow [GO-LIVE.md](GO-LIVE.md) and record those results before deployment.
