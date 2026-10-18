# DW2 Little Things + Story Memory 0.8.1-beta — Testing

## Automated checks performed on 0.8.1

- **27/27 headless Chromium checks passed** using simulated TauriTavern / SillyTavern context and mocked AI API.
- Screen sizes tested: **360 × 780**, **390 × 844**, and **432 × 930**.
- For each size, checked: original DW2 menu alignment; modal title visible on opening; model-fetch URL and selection; manual one-batch summary; generated memory injection; re-roll invalidation of previous memory and prompt; rebuilding memory with the new selected re-roll; sticky title after scrolling; and absence of horizontal page overflow.
- **0 uncaught JavaScript page errors** in those simulations.
- **node --check**: PASS. JSON manifest: PASS.

## Earlier 0.8.0 tests (not a substitute for new device tests)

- Previous beta recorded 19 unit and 11 simulated browser passes. The new version rechecked critical memory, re-roll and injection paths in the 27 mobile simulation checks above.

## Not verified

- Actual Android or iPhone TauriTavern 2.3.0 runtime, installation, touch keyboard placement, and third-party API connectivity.
- Whether the customer's specific independent provider exposes a CORS-accessible `GET /models` endpoint. Manual model-ID entry remains available.
- Compatibility with simultaneous independent memory-injection extensions.

**Status: customer-testing beta. Do not call it production-verified.**
