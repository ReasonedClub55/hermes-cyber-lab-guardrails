# Repository safety review

## Completed review scope

Review covers the written policy, examples, internal file links, public-data hygiene, instruction consistency, approval boundaries, and deployment claims. It does not include access to the user's hosts or a live model test.

## Safety decisions checked

- Scope begins closed: example/missing/expired scope permits no active testing.
- Exact target authorization is distinct from technique and privilege authorization.
- Private addressing and network ownership do not imply permission.
- Download hosts, resolvers, proxies, and management infrastructure are not test targets.
- Public retrieval redirects and secondary dependency downloads cannot become internal network access.
- SSH failure does not permit host fallback or network bypass.
- Unanswered approval requests never become consent.
- External instructions, memory, skills, and other agents cannot expand authorization.
- Policy/scope changes remain human-controlled; host/infrastructure changes are proposals.
- Root and package-manager hooks are treated as execution and privilege risks.
- Firewall enforcement sits outside the research guest; IPv6 and alternate paths are included.
- Broad HTTPS egress is acknowledged as permitting uploads, not mislabeled download-only.
- SSH forwarding restrictions are not described as containing an unrestricted shell.
- Profile separation is not described as OS sandboxing.
- Remote-to-host state synchronization is explicitly included in the threat model.
- Public/private artifacts are separated by storage location, without relying on a missing ignore file.
- Local inference does not imply local-only tools or cost-free auxiliary providers.
- Acceptance tests distinguish intended outcomes from actual measured results.
- No host, network, or model validation is claimed to have occurred.

## Deliberate restrictions and tradeoffs

The agent can fetch checked tools and install user-level dependencies autonomously. System packages and raw-socket work need a specific privilege grant or administrator assistance; broad passwordless sudo would defeat that boundary. Full remote-shell flexibility remains possible inside Kali, so external containment is necessary.

A trusted instruction workspace is separate from downloaded tools to reduce accidental context replacement. A dedicated controller account/profile limits personal data exposure, while a separate controller VM is the stronger containment option. Both require deployment verification.

## Not yet tested

Static checks found 19 Markdown files, no broken internal file links, and no obvious credential patterns or actual home-network addresses. The compact AGENTS.md is approximately 5.2K characters and SOUL.md approximately 2.1K characters; actual context loading still needs verification. The scenario suite now contains 32 behavioral cases and 15 infrastructure checks. This is a policy review and static file validation, not a model or firewall certification.

All B-series behavioral tests and I-series infrastructure checks in [ACCEPTANCE.md](ACCEPTANCE.md) are NOT RUN against the user's deployment. Hermes version, runner, network topology, firewall backend, permissions, and sync behavior remain deployment-specific. Complete [the go-live checklist](../docs/GO-LIVE.md) before research execution.
