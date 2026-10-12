# Restricted SSH access to Kali

The administrator performs this setup. Do not give the agent a shell on Windows, Proxmox, a bastion, or the firewall to configure access. Keep an existing console or administrative session open while validating changes.

## Accounts and keys

Create a dedicated unprivileged Kali user such as `hermeslab`, with a private workspace such as `/home/hermeslab/research`. It should not belong to sudo, docker, libvirt, or other groups that effectively grant administration. Restrict inbound SSH outside the guest to the one approved workstation source and endpoint.

Use a dedicated SSH key that is valid only for this Kali account. Keep its private half on the dedicated controller account, protected by that account's file permissions, and never copy it into Kali or this repository. Prefer an encrypted key and a human-unlocked agent if the installed backend supports that workflow. The SSH agent must not be forwarded to Kali. Do not weaken key protection to work around a compatibility problem.

Verify Kali's host-key fingerprint from its trusted Proxmox console before first connection. Prepopulate the controller account's known-hosts entry. A changed key requires investigation; do not delete the entry and accept the new key automatically. Check the installed Hermes backend's host-key behavior as part of acceptance.

## Illustrative server restriction

After verifying compatibility with Kali's installed OpenSSH, the administrator can consider a per-user stanza:

```text
Match User hermeslab
    AuthenticationMethods publickey
    PasswordAuthentication no
    KbdInteractiveAuthentication no
    AllowAgentForwarding no
    AllowTcpForwarding no
    X11Forwarding no
    PermitTunnel no
    PermitTTY no
```

This restricts authentication and SSH forwarding features. Validate effective configuration with the installed server's syntax-check and effective-config facilities before reload. Test a second login before closing the original session. [OpenSSH server configuration](https://man.openbsd.org/sshd_config)

Do not paste a global `AllowUsers` change without accounting for administrator access. Do not turn off a needed subsystem blindly: Hermes file operations may need it. If non-PTY execution is incompatible with the installed version, review a narrowly documented exception rather than weakening unrelated controls.

## What these restrictions cannot do

An unrestricted remote shell can run programs, open network sockets, and create its own tunnels despite SSH's forwarding switches. Those switches reduce convenience paths, not the shell's fundamental capability. External firewall rules enforce reachability. A full shell cannot be accurately called a per-command allowlist.

A forced-command gateway can enforce a narrow command API, but it is not a drop-in replacement for Hermes' general shell/file backend. Never wrap arbitrary command text in an improvised string filter and call that isolation. If you need that boundary, build and separately review a structured broker with fixed operations and validated arguments.

## Privileged work

Start without sudo. User-level tool environments can still do substantial research. For package installation, have the administrator install named reviewed packages or provide a separately reviewed broker with fixed operations. Do not allow passwordless `apt`, `pip`, a shell, interpreters, arbitrary file writes, service management, or wildcard command arguments as a supposed narrow sudo rule: these can lead to full root access.

When a test truly requires guest root or raw sockets, request the exact command, target, duration, and recovery plan. Root inside Kali increases guest compromise risk; the external network boundary must remain enforced. The agent never receives Proxmox or firewall administrative credentials.
