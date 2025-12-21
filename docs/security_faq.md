## Security FAQ

### Zero Trust – core components
- **Policy Engine:** evaluates context (identity, device posture, location, risk signals) and decides allow/deny/step-up for each request.
- **Policy Administrator/Enforcement (PDP/PEP):** translates engine decisions into session controls, token issuance, and network or app-level gating.
- **Policy Information Points:** telemetry and posture feeds (IdP, EDR, MDM, vulnerability data, network analytics) that supply evidence to the engine.

### 3-D Secure – three domains
- **Acquirer/Merchant Domain** (merchant + acquirer gateway).
- **Issuer Domain** (cardholder’s issuing bank / Access Control Server).
- **Interoperability Domain** (card scheme directory servers + infrastructure).

### 3-D Secure 1.0 vs 2.0 (high level)
- 1.0: static password, browser redirects/iframes, high friction, weak mobile support.
- 2.0: risk-based, rich data exchange, embedded/mobile-native challenges, supports biometrics/OTP, liability shift preserved.

### American Express SafeKey (3DS-based)
- Brand implementation of EMV 3-D Secure.
- Uses frictionless flow by default; challenges via push/OOB OTP/PIN when risk is elevated.
- Provides liability shift to issuer after successful auth; requires up-to-date contact channels.

### EtherRAT – blockchain C2 consensus
- Queries nine public Ethereum RPC endpoints in parallel, reads an immutable smart contract, and **majority-votes** the returned C2 URL.
- Purpose: prevent sinkholing/poisoning of a single RPC and resist takedown of static domains.
- Detection idea: flag bursty eth_call traffic to multiple public RPCs followed by rapid polling of a resolved host with CDN-like paths.

### EtherRAT – five Linux persistence mechanisms
- systemd user service in `~/.config/systemd/user/` with random name.
- XDG autostart entry in `~/.config/autostart/` hidden `.desktop` file.
- `@reboot` cron entry (often with `sleep 30`).
- `.bashrc` injection launching the RAT on shell start.
- `.profile` injection as fallback for login shells.

### Mean Time to Detect (MTTD)
- Definition: average elapsed time from incident start to first detection.
- Calculation: sum of (detection_time − start_time) for all incidents ÷ number of incidents.

### Prompt injection types
- **Direct:** attacker-controlled user input that overrides system/developer instructions (e.g., “ignore previous instructions”).
- **Indirect:** malicious instructions hidden in external content the model processes (docs, webpages, email signatures, metadata, images with text), leading the model to execute unintended actions.

### Why PROMPTFLUX uses Gemini / PROMPTSTEAL uses Hugging Face
- PROMPTFLUX: hourly self-rewrites via Gemini API to change hashes and evade signature AV; stores regenerated script in Startup folder for persistence.
- PROMPTSTEAL: offloads reconnaissance/collection command generation to Hugging Face (e.g., Qwen2.5-Coder) to avoid hardcoded TTPs and stay adaptive.

