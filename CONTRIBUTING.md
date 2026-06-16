# Contributing

This skill is only as good as what's been **verified and recorded**. renef is lightly documented
and its behavior varies across builds, so the most valuable contributions are findings confirmed on
a real device.

## Contribute a verified finding

1. **Reproduce it on-device** and run [`skills/renef/probe.lua`](skills/renef/probe.lua) so we know
   your environment.
2. Include: renef version/build, device model, Android version, and whether the finding is
   **`[verified on-device]`** or **`[unverified / from docs]`**. Keep that distinction — it's the
   point.
3. Prefer minimal, generic repros. New API facts, working class/method signatures, primitives
   (e.g. the reflection bridge), gotchas, and connection/error behaviors are all welcome.
4. Open a PR editing the relevant file (`SKILL.md`, `references/*.md`, or `probe.lua`), or file an
   issue with the repro.

## Do NOT include confidential or target-specific material

- **No proprietary or client/employer app data**: package names of apps under NDA, decompiled
  source, internal offsets, screenshots, traffic captures, or the specific names of a target's
  shielding/protection libraries.
- Use **generic, publicly-known** examples instead (well-known frameworks/products, synthetic
  package names like `com.example.app`, offsets clearly marked as build-specific placeholders).
- This protects both you and others. When in doubt, generalize.

## Scope & ethics

renef and this skill are for **authorized** security testing, app-hardening review, CTFs, and
analysis of software you own or are permitted to test. Contributions should reflect that — no
material that only makes sense for unauthorized use against third parties.
