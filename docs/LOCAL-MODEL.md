# Local inference without paid model APIs

Keep inference on your own hardware. This repository neither invokes a hosted model nor requires a paid provider key. Your selected quantized model is `Qwen3.6-35B-A3B-UD-Q4_K_M`; use the model identifier actually advertised by your runner rather than assuming the filename is the serving ID.

The model runner was not specified, so this document does not invent runner-specific settings. Hermes documents a custom-endpoint route for self-hosted models. Confirm the endpoint, served model ID, context limit, and tool-call compatibility using the installed release. [Official local/self-hosted quickstart](https://hermes-agent.nousresearch.com/docs/getting-started/quickstart)

## Privacy and cost checks

- Bind a Windows-hosted model service to loopback when only the local Desktop runtime needs it. Do not open it to the household LAN for convenience.
- If a separate controller VM needs inference, expose only the minimum authenticated/private path to that controller. Block Kali and target VMs from initiating model-service access. Do not disable authentication just because the network is private.
- Configure the main model, auxiliary models, summarization, vision, fallback, and delegation deliberately. Disable hosted fallback and paid tools. Test an unavailable local endpoint: the agent should report failure, not make a hosted call.
- Some clients ask for a non-secret placeholder in an API-key field for an unauthenticated loopback service. Use that only when the selected runner/client explicitly requires it; it is not a paid key or access protection. Never send real provider credentials to a local endpoint.
- Audit web search, retrieval, plugins, and telemetry separately. Local inference does not imply that all tool traffic stays local. Use public retrieval routes without paid search keys and avoid sending private findings in queries.
- Verify the runner supports the tool format Hermes uses. A model that chats well may still mishandle tool calls, arguments, or approval boundaries. Do not infer safety from model size or quantization.

## Model acceptance

Use the same model, context settings, and tools you intend to deploy. Test the scenarios after initial loading, a fresh session, a long session/compaction, and a reconnect. If it forgets scope, accepts injected instructions, or executes on the wrong machine, keep tool execution disabled until corrected. Stronger containment is necessary even when every behavioral test passes.
