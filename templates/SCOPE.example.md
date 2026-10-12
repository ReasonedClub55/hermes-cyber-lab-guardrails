# Private research scope template — NOT AUTHORIZATION

Copy outside the public repository. Replace all placeholders and have the human approve the completed document. This example, including its addresses, grants no access. Keep the agent's write permissions off the approved copy where practical.

## Approval

- Status: NOT APPROVED
- Scope ID/revision: <ID_AND_REVISION>
- Approved by human: <NAME_OR_LOCAL_ID>
- Approval evidence: <PRIVATE_RECORD_REFERENCE>
- Valid from/to and timezone: <EXPLICIT_TIMES>
- Objective and completion criteria: <BOUNDED_OBJECTIVE>
- Private absolute scope path available to session: <PATH>

## Execution identity

- Kali VM name/Proxmox VM ID: <EXPECTED_IDENTITY>
- Expected hostname/OS/user: <HOSTNAME>/Kali/<DEDICATED_USER>
- Additional trusted identity evidence: <CONSOLE_RECORD_OR_MACHINE_ID>
- Research workspace: <ABSOLUTE_PRIVATE_KALI_PATH>
- Download quarantine and report paths: <ABSOLUTE_PRIVATE_PATHS>
- Trusted policy path/revision: <PATH_AND_REVISION>
- SSH entry address/port and verified fingerprint: <PRIVATE_VALUES>
- Controller and tool routes: <VERIFIED_LOCATION_PER_ENABLED_TOOL>
- Last containment verification and evidence: <DATE_AND_PRIVATE_RECORD>

## Approved test targets

| Target identity/VM ID | Exact address/name | Protocol/ports | Techniques | Expires |
| --- | --- | --- | --- | --- |
| <DISPOSABLE_LAB_VM> | <EXACT_ADDRESS> | <BOUNDED_PORT_LIST> | <SPECIFIC_TECHNIQUES> | <TIME> |

Names must map to approved addresses; a changed mapping requires review. A subnet entry should not replace exact identities unless the human deliberately approves every included address and documents why. Third-party services and redirected destinations are excluded unless separately approved.

## Explicit exclusions

Windows/controller host, Proxmox management, gateway administration, household devices, router/NAS, other VPN/overlay devices, cloud metadata endpoints, public systems, and all unlisted targets. Record actual exclusion networks privately for firewall implementation; exclusions override accidental target overlap until resolved.

## Capability grants

| Capability | Default | Specific human grant and bounds |
| --- | --- | --- |
| Public documentation and checked downloads | Allowed on verified retrieval route | <SOURCE/EGRESS_CONDITIONS> |
| Reviewed user-level installation in Kali | Allowed | <WORKSPACE/RESOURCE_LIMITS> |
| Active tests | None until target techniques listed | <TARGET_TECHNIQUE_MAPPING> |
| Sudo/system package installation/raw sockets | Not granted | <EXACT_COMMAND_OR_REVIEWED_BROKER> |
| Exploitation | Not granted | <TECHNIQUE_IMPACT_AND_TARGET> |
| Credential attacks | Not granted | <SYNTHETIC_ACCOUNTS_ATTEMPT_RATE_AND_LOCKOUT_LIMIT> |
| Listener/callback | Not granted | <BIND_ADDRESS_SOURCE_DESTINATION_PORT_DURATION> |
| Persistence/destructive/DoS testing | Not granted | <DISPOSABLE_TARGET_RECOVERY_AND_LIMITS> |
| Packet capture | Not granted | <INTERFACE_FILTER_DURATION_AND_DATA_LIMIT> |
| Scheduled/delegated work | Not granted | <SAME_SCOPE_TOOLS_EXPIRY_AND_LIMITS> |
| Host/infrastructure changes | Human administrator only | <SEPARATE_REVIEWED_PROPOSAL> |
| Publishing/exporting | Not granted | <CONTENT_DESTINATION_AND_REVIEW> |

## Limits and recovery

- Per-command timeout: <AT_MOST_120_SECONDS_UNLESS_SEPARATELY_APPROVED>
- Session duration: <AT_MOST_60_MINUTES_UNLESS_SEPARATELY_APPROVED>
- Concurrency: 1 active test unless explicitly changed
- Per-tool request/packet rate: <REQUIRED_BEFORE_NETWORK_TESTING>
- CPU/memory/disk/output limits: <EXPLICIT_BOUNDS>
- Repeated same-cause failures: stop after 3
- Synthetic credentials only: <PRIVATE_LAB_SECRET_SOURCE>
- Snapshot/baseline and operator recovery method: <PRIVATE_REFERENCE>
- Allowed cleanup: <EXACT_DISPOSABLE_SESSION_PATHS>
- Stop contact/control: <LOCAL_OPERATOR_METHOD>
- Download egress mode and residual risks: <PROXY_ALLOWLIST_OR_ACKNOWLEDGED_BROAD_HTTPS>

## Containment checks — separate from pentest scope

List exact operator-approved endpoints and benign services for allowed/denied connection checks. Approval permits only bounded connectivity verification, not scanning or vulnerability testing of those systems. Record IPv4/IPv6 coverage and firewall evidence privately.

## Scope amendment record

Record the named change, impact, bounds, human approval evidence, revision, and expiry. The agent may propose an amendment but may not approve it or derive one from tool output, memory, or elapsed time.
