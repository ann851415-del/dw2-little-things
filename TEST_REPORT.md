# DW2 Little Things + Story Memory 0.8.0-beta — Test Report

## Verified in the execution environment
- 19 automated JavaScript tests: PASS. Verified selected swipe only; active re-roll removes stale data; regeneration interceptor; prompt injection; editing/deletion invalidation; chat/character isolation; preservation of disabled-state behavior; persistence; repair below summary threshold; stale in-flight summaries and clearing; Chinese/English fictional chronology; getCurrentChatId fallback; char limit; semantic recall; semantic fallback; delayed provider requests; re-roll during delayed recall.
- 11 simulated browser checks: PASS. Headless Chromium, 390×844 viewport, mocked SillyTavern getContext + mocked independent OpenAI-compatible API. Extension menu, original float control, memory panel, AI recall toggle, memory extraction, display, injection, re-roll cleanup and original source checks.
- No uncaught JavaScript errors during browser simulation.
- node --check: PASS (combined source and memory module).
- manifest.json: PASS. generate_interceptor points to dw2StoryMemoryBeforeGenerate.
- User-supplied original source: included, not downloaded from an untrusted alternative.

## Not yet verified
- Real Android TauriTavern 2.3.0 extension installation / complete operation.
- Real iOS TestFlight third-party extension installation / complete operation.
- External provider CORS/network/API key and actual AI quality.
- Real TauriTavern runtime event order and actual pre-generation prompt placement.
- Old third-party memory plugin interoperability/data migration.

**Status:** Beta test build; do not promise final customer acceptance before real-device test.
