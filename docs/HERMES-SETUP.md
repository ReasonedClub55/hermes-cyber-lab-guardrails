# Connect the policy to Hermes Desktop

Apply this to a dedicated research profile, not a general personal assistant profile. Desktop labels and backend behavior vary by release; record the installed version and compare it with [official configuration guidance](https://hermes-agent.nousresearch.com/docs/user-guide/configuration).

## Persistent instructions

Back up the research profile's existing identity file before placing this repository's SOUL.md in that profile's actual `HERMES_HOME`. Attach a trusted policy workspace containing AGENTS.md. Test instruction loading; simply cloning a repository or mentioning its URL is insufficient. Inspect existing `.hermes.md`/`HERMES.md` and other context files for competing instructions. Keep downloaded tools outside the trusted instruction workspace. See [official context-file guidance](https://hermes-agent.nousresearch.com/docs/user-guide/features/context-files).

Keep private scope outside the public checkout. Configure its absolute path privately and explicitly load it into the session. Confirm that the model can describe the current scope and boundaries after a fresh session and compaction. Protect policy and approved scope with administrator ownership/read-only access where practical; generated work goes elsewhere.

## Minimal remote execution settings

Merge into the actual research profile, preserving existing unrelated settings and avoiding duplicate YAML keys:

```yaml
terminal:
  backend: ssh
  env_passthrough: []
```

In that profile's private environment configuration:

```text
TERMINAL_SSH_HOST=<KALI_SSH_ENTRY_ADDRESS>
TERMINAL_SSH_USER=hermeslab
TERMINAL_SSH_PORT=<APPROVED_PORT>
TERMINAL_SSH_KEY=<PRIVATE_KEY_PATH_ON_CONTROLLER>
```

Do not use example values as real configuration. Restart the relevant profile and verify effective settings. If native Windows SSH/backend compatibility fails, stop and assess a supported isolated controller arrangement; do not switch to local research execution.

**State synchronization matters:** the documented SSH backend can copy profile state to the remote machine and sync changed state back. Use a dedicated OS account and profile with no personal credentials; review synchronized skills/cache before reuse. Do not invent a sync-disable setting or assume a transfer-size limit disables sync. A remote runtime on a separate controller VM is the stronger option when host synchronization risk is unacceptable.

## Additional guardrails

Consider this profile-specific starting point:

```yaml
approvals:
  mode: manual
  timeout: 300
  deny:
    - "*curl*|*sh*"
    - "*wget*|*sh*"
    - "git push --force*"
security:
  redact_secrets: true
checkpoints:
  enabled: true
```

Manual mode handles flagged commands; it is not an every-command approval boundary. Pattern guards and file-write guards do not contain a hostile shell. Checkpoints are not VM snapshots. Keep external enforcement in place. Do not enable YOLO/off approval modes for this profile. [Official host-safety guidance](https://hermes-agent.nousresearch.com/docs/guides/secure-hermes-on-a-work-machine)

## Audit every tool route

List enabled tools, extensions, MCP servers, computer-use/browser tools, code runners, connectors, scheduling, delegation, and artifact import/export paths. For each, record privately: where it executes, what credentials it receives, what files it sees, and whether it can reach the host or Internet.

Disable unnecessary host-capable and messaging tools. A browser controlling the personal Windows session is outside the lab boundary even when the terminal uses SSH. Use separate browser/session state for public documentation, or a lab-side retrieval route. Do not expose personal browser cookies to the research agent. Scheduling and delegation must inherit the same policy and current scope; disable them until separately verified.

Test terminal, file read/write, and code execution independently using harmless identity checks and dummy files. Demonstrate that a broken SSH connection cannot cause a local action. Do not run an exploit to test integration.

The best baseline is a dedicated non-administrator Windows account with no personal files or credentials accessible to it. A profile separates application state; Windows account and filesystem permissions provide the stronger local boundary. These controls reduce risk but do not fully sandbox the Desktop process.
