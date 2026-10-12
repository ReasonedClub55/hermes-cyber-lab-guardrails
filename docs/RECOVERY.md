# Stop and recovery procedure

## Stop triggers

Wrong OS/user/VM; unexpected target or destination; failed containment test; suspicious installer activity; unexpected root execution; real credential exposure; trusted policy modification; unreviewed host synchronization; resource exhaustion; or expired authorization.

## Agent actions

Stop the affected research task. Terminate only processes demonstrably owned by that task if it is safe to do so. Do not run downloaded cleanup or remediation instructions. Record minimal non-secret evidence and tell the human what happened, what is still running, and which boundary may have failed. Do not claim containment based only on the guest's own report.

The agent may not change host firewall rules, revoke administrative credentials, restart Proxmox, wipe disks, delete broad directories, or weaken security settings to recover. Suggest a concrete operator action and wait for the relevant authorization.

## Operator containment

From a trusted management path, disconnect the affected VM's network or stop the VM. Check external firewall logs and controller-side state. Preserve necessary evidence privately without activating untrusted files. Avoid a normal teardown that automatically imports guest changes if compromised synchronization is suspected; determine safe handling for the installed Hermes version.

If credentials may have been exposed, rotate them from a trusted machine. The absence of paid API keys does not mean there are no secrets: SSH keys, session cookies, model endpoint tokens, and target passwords still matter.

## Recovery

Rebuild compromised guests from trusted images or a known-clean snapshot, then patch trusted software deliberately. A snapshot taken after compromise is not a clean baseline. Restore approved generic policies and private scope from trusted copies, and review synchronized memories, skills, configuration, and caches before reuse.

Recheck accounts, enabled tool routes, all NICs, IPv4/IPv6 routes, egress restrictions, SSH keys, and the allowed/blocked flow tests. Confirm background processes and listeners are gone. Repeat relevant acceptance scenarios before resuming.

Resume only when the human records what failed, what was corrected, and fresh approval for the affected scope. Keep the incident and findings private; do not publish raw logs or credentials.
