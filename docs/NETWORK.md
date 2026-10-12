# Proxmox network isolation

This is an administrator-reviewed architecture, not a script to apply to an unknown server. Preserve console access and a rollback path before changing Proxmox networking. Record actual bridges, routes, addresses, and firewall backend privately.

## Recommended shape

```text
Windows research account ── narrow SSH entry ──> Kali VM
                                                   │
                                             isolated lab switch
                                                   │
                                            approved target VMs
                                                   │
                                      administrator-controlled gateway
                                                   │
                                       filtered download/DNS access

Proxmox management and household devices: separate, blocked from lab initiation
```

Use a private virtual lab bridge with no physical uplink and no Proxmox host IP on that bridge. Attach Kali and disposable targets only to lab networks. Provide routing through a dedicated firewall/gateway VM managed by the human. Avoid adding a second Kali NIC directly to the home LAN. Proxmox bridges connect guests to networks; a bridge with a physical uplink may put guests directly on that network. [Proxmox networking reference](https://github.com/proxmox/pve-docs/blob/master/pve-network.adoc)

The SSH entry can be a narrow gateway port-forward from one workstation address to Kali TCP/22, or an administrator-managed bastion with forwarding limited to that one endpoint. Do not make Proxmox root SSH the agent's gateway. No router Internet port-forward, UPnP mapping, or public SSH exposure is needed.

## Required firewall behavior

Implement stateful filtering outside Kali. NAT alone does not establish this policy. The guest firewall is defense in depth because guest root could alter it.

| Flow | Decision |
| --- | --- |
| Named workstation address to Kali SSH entry | Allow only the selected TCP port |
| Established replies to allowed SSH sessions | Allow statefully |
| Kali to exact approved lab targets | Allow only approved protocols and ports |
| Kali to designated resolver | Allow DNS only; resolver is infrastructure, not a test target |
| Kali to reviewed download sources | Allow required web traffic through controlled egress |
| Kali/targets to workstation or household devices | Deny new connections |
| Kali/targets to Proxmox, gateway management, or bastion management | Deny |
| Targets to Internet | Deny by default; approve a specific need separately |
| Other inbound lab access | Deny by default |

Cover IPv4 and IPv6. If IPv6 is not needed, the administrator must ensure it cannot become an alternate path; don't merely omit IPv6 rules. Account for local/link-local services, multicast discovery, metadata endpoints, other routed subnets, and VPN/overlay addresses. Do not block a broad private range before the deliberate lab and resolver exceptions, and do not allow all private ranges as a shortcut.

Prefer a download proxy or controlled acquisition process when stricter outbound containment matters. Broad TCP/443 Internet access permits uploads and command-and-control traffic as well as downloads. A DNS allowlist alone is not a complete security boundary. Document any broad-egress residual risk in private scope; never call it download-only enforcement.

Proxmox provides guest-interface firewall controls. Verify that the relevant datacenter, guest, interface, and backend settings are actually active for your version. A checked box is not proof that packets are filtered. [Proxmox firewall reference](https://github.com/proxmox/pve-docs/blob/master/pve-firewall.adoc)

## Host and guest separation

- No Proxmox API tokens or administrative SSH credentials in the research account.
- No host filesystem mounts, shared personal folders, nested hypervisor access, or unnecessary device passthrough.
- Use fixed lab addressing and prevent unintended DHCP/address changes from silently moving targets.
- Keep lab firewall administration on a separate management path. Kali must not be able to change external rules even when root is temporarily approved in the guest.
- Limit CPU, memory, and disk so a research loop cannot starve the server. Snapshots and backups are handled by the human, not by exposing Proxmox administration to Hermes.

## Verify without scanning the household

The human administrator chooses exact test endpoints and benign listening services. Explicitly authorize these as **containment checks only**, separate from pentest scope. From Kali, use bounded single-endpoint connection attempts, and correlate them with firewall deny logs. A timeout alone does not prove isolation; the remote service might simply be absent.

Verify allowed SSH and a synthetic lab service; blocked workstation, hypervisor management, and one approved household test service; IPv6 and any second interface; and permitted downloads. Check every Kali NIC and route, then restart Kali and repeat. No subnet sweeps. If any forbidden flow succeeds, pause research and repair isolation before proceeding.
