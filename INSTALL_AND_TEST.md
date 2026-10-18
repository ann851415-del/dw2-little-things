# DW2 Little Things + Story Memory — 0.8.1 BETA TEST BUILD

This is a merged, **experimental** SillyTavern/TauriTavern frontend extension. It has not been tested on a physical Android or iPhone device. The original DW2 0.6.9-beta.1 source was preserved, except for supporting the new installation slug in its updater. The new story memory module is appended to the JavaScript and CSS files.

## Included functions

**Original DW2 tools:** floating-button organizer, background adjustment, and manual/automatic floor hiding.

**New memory tools:** automatic summaries through a separate OpenAI-compatible API, AI-assisted memory relevance ranking with local fallback, character and world setting memories, fictional story chronology, per-character/per-chat isolation, memory export/edit, memory injection before AI generation, and invalidation of old summaries after regenerated, edited or deleted messages.

## Install on a test copy (Android first)

1. **Back up chats and extension data first.** Do not delete the original installed extension or its user data until the test works.
2. Extract the directory `dw2-little-things-story-memory` from the ZIP. It must contain `manifest.json`, `index.js`, `style.css`, and `README.md` together at its root.
3. TauriTavern's **Install Extension** control generally expects a Git repository URL, **not this ZIP**. For remote installation, put the extracted directory contents at the root of a Git repository you are authorized to use, then install using that repository's HTTPS URL. Alternatively, use the supported local extension directory mechanism for your exact TauriTavern installation if available.
4. Disable the original DW2 extension while testing this merged copy (the two would otherwise create overlapping menus). Disable memory injection in BakemonoMemory/Memory Palace too while testing this new injection module.
5. Open a disposable character chat, then tap the **magic wand / Extensions** menu → **剧情记忆馆**.
6. Set an independent HTTPS OpenAI-compatible API base URL (e.g. `https://api.openai.com/v1`), model ID, and API key. The service must permit requests from the app WebView (CORS).
7. Tap **拉取模型** to fetch model IDs from the provider (the provider must implement `GET /v1/models`); alternatively enter the model ID manually. Then enable **启用剧情记忆**, **自动总结**, and **注入下轮聊天** if appropriate. Save. Start with a small summary batch size and a test character.
8. Tap the top **拉取当前剧情（总结一批）** or lower **立即总结**, review entries, then send the next AI message to check that memory injection occurs.
9. Re-roll a reply that has contributed to a summary. Its previous summary should be revoked automatically; after the new response, run summarization again and check that no discarded version is present in the memory view or next prompt.

## Functional acceptance checklist

- [ ] Android TauriTavern 2.3.0 recognizes the extension and opens both original menus and **剧情记忆馆**.
- [ ] DW2 floor hiding (auto/manual), background adjustment, and floating organizer still work.
- [ ] Separate AI API summarizes selected chat response, not unselected `swipes`.
- [ ] Memory entries are sorted into characters, world settings, and **fictional** event chronology.
- [ ] A summary created from reply A is removed when reply A is re-rolled into reply B; reply B may be summarized instead.
- [ ] Existing outdated memories are not injected into the next prompt following re-roll.
- [ ] Edits/deletions and chat/character switches invalidate or isolate affected memories.
- [ ] Manual memory changes and JSON export work.
- [ ] The above steps are tested separately on iPhone TestFlight where third-party extensions are permitted.

## Cautions

- The source author has not published a license in this uploaded archive. Keep this test copy private unless you obtain permission to distribute a derivative work.
- Story text is transmitted to the configured AI provider, and memories are stored on this device using `localStorage`. The optional Remember Key checkbox saves the key unencrypted; leave it off on shared devices. There is no Android/iOS cross-device sync.
- AI summary quality is model-dependent; explicit fictional day/chapter dates can be ordered, but ambiguous/relative events may need manual review.
- AI-assisted recall may make an additional API request before each generation when more than 8 candidate memories are present. Disable AI智能召回 for lower cost and lower latency.
- The old BakemonoMemory/Memory Palace database is separate; this extension does not erase or migrate historical entries from those plugins. Disable their memory injection while testing to avoid stale memories from another extension.
- When the independent API fails, the extension reports the error; it will not repeatedly retry the same batch in a tight loop.
- Changes to selected messages can invalidate all later summaries, temporarily removing their memory injection until they are re-summarized.
- The original **Check for Updates** function is not a reliable updater for manual/local installs; manage development versions explicitly.
- Public iPhone TestFlight builds may restrict third-party extensions; this ZIP does not bypass those platform policies.

## Automated checks

Developer unit tests are recorded in TEST_REPORT.md. These checks exercise 19 cases plus 27 mobile-browser checks (360px / 390px / 432px) and are **not** real-device compatibility tests. The extension JavaScript passes `node --check` and its manifest is valid JSON.

## Changes in 0.8.1 (customer feedback fix)

- Added **拉取模型** next to the model field. Uses the unsaved current API URL and API key, requests the provider's `/models` endpoint, fills a selectable model list, and always allows a manually entered model ID. Timeout, CORS and API errors are shown in the panel without exposing the key.
- Added a visible **拉取当前剧情（总结一批）** button near the top, so users do not have to scroll to find the one-batch manual summary action.
- Fixed **剧情记忆馆** menu icon + label layout and placed it next to the three native DW2 shortcut entries.
- Kept the panel title/close button sticky while scrolling; improved touch-friendly form inputs and safe-area/mobile-height handling.
- Re-tested response re-roll invalidation and injection in mocked mobile browser conditions.
- No code from real provider returned /models responses was needed; **actual third-party API compatibility remains unverified**.
