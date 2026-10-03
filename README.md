# Static Kitty image review evidence

**Linked drafts:** [Ghostex #186](https://github.com/maddada/Ghostex/pull/186) and [zmx #3](https://github.com/maddada/zmx/pull/3).

[Download the public review package](static-images-pr-review.zip?raw=true). It contains portable fixtures and probes, patches, full validation logs, implementation review maps, checked Claude findings, resource limits and known gaps.

| Contribution | Exact review head | Target |
| --- | --- | --- |
| Ghostex renderer | [57a756dee3e8](https://github.com/vespillo-tech/Ghostex/commit/57a756dee3e84114f2e95d6c11ac03895b87950a) | `maddada/Ghostex:main` at `56a620fe8313` |
| zmx replay and optional grid coordination | [c630130eb7aa](https://github.com/vespillo-tech/zmx/commit/c630130eb7aa007407d6f63d0c77932009798e16) | `maddada/zmx:nightly` at `feaefff98723` |

## Review order

1. Read `review-overview.md`, then the owner-specific PR bodies and report.
2. For current Ghostex main, use `renderer-current-main.patch`; the older patch is retained for traceability.
3. Review zmx first. Ghostex must pin the exact reviewed upstream zmx feature commit and repeat focused integration checks before release. Its current gitlink is unchanged.

## Verification and limits

Apple Silicon macOS runtime acceptance covers ordinary and Unicode-placeholder static images, PNG, search, split panes, resizing, history, viewer reattachment and pane ID isolation. The current-main optimized desktop build and shared wasm compilation passed; native runtime observations used the previous main with identical feature additions/deletions. The full unchanged Ghostty core passed 6,472 tests with 52 skips on both base and candidate; zmx passed 108 existing tests and 39 semantic replay cases.

This is bounded static image support. Full animation/identity restoration, browser rendering and native Windows retained state remain separate work. Linux/Windows/Intel runtime acceptance, CJK preedit and deliberate link hover are unverified. Existing mixed-mode history widths and partial-UTF-8-before-Init issues are documented. Aggregate memory and power are unmeasured. See the report for exact resource limits and exclusions.

The archive uses a public allowlist, has verified CRCs and entry hashes, and excludes private inventories, auth, profiles, raw Claude outputs, caches and binaries. This documentation branch contains no application changes or workflows.

## Publication status

Both drafts are mergeable with exact reviewed heads and file lists. Manual CodeRabbit reviewed both drafts: zmx returned no actionable comments; the renderer's two reproduced findings were corrected. Renderer follow-up completed with no new actionable comments, but skipped all three correction files as similar. Actual Claude and local/native checks cover the corrected Rust. Its default docstring advisory is disclosed in the report. Macroscope skipped draft correctness review; no maintainer approval is claimed. Ghostex storage-access passed. Latest observed upstream main is `993eba2f3b00`. Only Help shares a file, with disjoint Windows SSH and Terminal image paragraphs; a disposable-index check applies the feature patch cleanly and preserves upstream updates. The latest combination is not yet built; the tested base remains `56a620fe8313`. The release gate remains the exact reviewed zmx dependency pin and focused integration checks.

## Renderer review correction

The current head adds a three-file correction for placeholder cursor glyphs and aggregate upload-cache admission (64 MiB padded buffers/256 generations per view). Fifteen production-function checks and desktop/web compilation passed. Actual Opus 5.5 `xhigh` review found no blocking issues; Help wording was clarified afterward. Read `evidence/coderabbit-followup/checked-review-report.txt` for failing controls, exact limits and probe scope. This upload-cache budget is not a total-process or GPU-memory cap. A fresh targeted native follow-up passed the 256-generation omission/recovery case and displayed a placeholder without a cursor glyph overlay. Focused cursor semantics remain covered by the production-function probe. The library source-storage default is 10,000,000 bytes/screen; the synthetic cache byte-boundary probe is not evidence that five large RGBA assets coexist under that default. Temporary lab overrides were restored and the installed main app remained healthy. Read the included native observation and storage-limit receipts; broader UI/platform gaps remain as stated.
