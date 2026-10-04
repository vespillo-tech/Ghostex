# Static Kitty image review evidence

## Independent audit correction — 2026-10-04

Current renderer review head: [`fc538d1a2a2f`](https://github.com/vespillo-tech/Ghostex/commit/fc538d1a2a2fc190dd9725eb9782086fa51a25ed); **28 files total**, seven-file audit correction after `4e58bf74`. zmx remains `ff399831` with no executable changes in this audit.

- Resolve image offsets with Ghostty's current cell dimensions after font/pixel resizes.
- Accept valid RGBA16 PNGs whose encoded bytes exceed the final RGBA8 size. Encoded input is independently capped at **40 MiB**, allowing encoding overhead; decode allocation stays 32 MiB, final pixels stay 16 MiB/4 Mi pixels, and default source storage stays 10,000,000 bytes.
- Render ordinary relative descendants of Unicode placeholder images using Ghostty's parent-chain, minimum visible-origin, crop and layer rules. This concerns live rendering; relative **replay remains excluded**.
- Register the result type in the native ABI metadata. C headers, Rust layouts and actual compiled descriptors agree (64-byte render info, 80-byte placeholder/descendant result). App and embedded library must be rebuilt together, as the normal Cargo build does.

All three defects reproduce on archived published source and pass on final source. Additional native cases cover nested chains, signed edges, culling, parent absence/deletion, own z layers and PNG compression variants. The full-pixel PNG overhead fixture raises source storage only in a disposable terminal. Text error recovery, owned admission, 15 upload/cursor checks and 70,797 parser boundary cases pass. Locked optimized desktop and shared wasm compilation pass with unchanged warning counts. Actual Claude Code Opus 5.5, CLI `--effort xhigh`, reviewed the fixes and final refinements; no blocking findings remain. The later one-line descriptor registration was independently compiled and checked.

Read `evidence/final-audit/AUDIT-REPORT.txt` in the public archive for exact provenance, process corrections and remaining verification gaps. Earlier sections and logs retain their historical scope. Latest upstream main `c5001c48` accepts the complete current patch; its combined tree is not newly built or launched. Both image PRs remain drafts pending upstream zmx landing, the exact pin and focused combined checks. No new whole-window acceptance or Linux/Windows/Intel/SSH forwarding acceptance is claimed. Detailed bot review does not cover this correction.

**Linked drafts:** [Ghostex #186](https://github.com/maddada/Ghostex/pull/186) and [zmx #3](https://github.com/maddada/zmx/pull/3).

[Download the public review package](static-images-pr-review.zip?raw=true). It contains portable fixtures and probes, patches, full validation logs, implementation review maps, checked Claude findings, resource limits and known gaps.

| Contribution | Exact review head | Target |
| --- | --- | --- |
| Ghostex renderer | [fc538d1a2a2f](https://github.com/vespillo-tech/Ghostex/commit/fc538d1a2a2fc190dd9725eb9782086fa51a25ed) | `maddada/Ghostex:main` at `56a620fe8313` |
| zmx replay and optional grid coordination | [ff399831abdc](https://github.com/vespillo-tech/zmx/commit/ff399831abdc33e55c9841d324ff3bc70cfd7115) | `maddada/zmx:nightly` at `feaefff98723` |

## Review order

1. Read `review-overview.md`, then the owner-specific PR bodies and report.
2. For current Ghostex main, use `renderer-current-main.patch`; the older patch is retained for traceability.
3. Review zmx first. Ghostex must pin the exact reviewed upstream zmx feature commit and repeat focused integration checks before release. Its current gitlink is unchanged.

## Verification and limits

Apple Silicon macOS runtime acceptance covers ordinary and Unicode-placeholder static images, PNG, search, split panes, resizing, history, viewer reattachment and pane ID isolation. The current-main optimized desktop build and shared wasm compilation passed; native runtime observations used the previous main with identical feature additions/deletions. The full unchanged Ghostty core passed 6,472 tests with 52 skips on both base and candidate; zmx passed 108 existing tests and 39 semantic replay cases.

This is bounded static image support. Full animation/identity restoration, browser rendering and native Windows retained state remain separate work. Linux/Windows/Intel runtime acceptance, CJK preedit and deliberate link hover are unverified. Existing mixed-mode history widths and partial-UTF-8-before-Init issues are documented. Aggregate memory and power are unmeasured. See the report for exact resource limits and exclusions.

The archive uses a public allowlist, has verified CRCs and entry hashes, and excludes private inventories, auth, profiles, raw Claude outputs, caches and binaries. This documentation branch contains no application changes or workflows.

## Publication status

Both drafts are mergeable with exact reviewed heads and file lists. Manual CodeRabbit reviewed both drafts: zmx returned no actionable comments; the renderer's two reproduced findings were corrected. Renderer follow-up completed with no new actionable comments, but skipped all three correction files as similar. Actual Claude and local/native checks cover the corrected Rust. Its default docstring advisory is disclosed in the report. Macroscope skipped draft correctness review; the maintainer requested six changes and reported a successful local merge/build; final merge approval remains theirs. Ghostex storage-access passed. Latest source compatible upstream main is `c5001c48f31e`. Only Help shares a file, with disjoint Windows SSH and Terminal image paragraphs; a disposable-index check applies the feature patch cleanly and preserves upstream updates. The latest combination is not yet built; the tested base remains `56a620fe8313`. The release gate remains the exact reviewed zmx dependency pin and focused integration checks.

## Renderer review correction

The current head adds a three-file correction for placeholder cursor glyphs and aggregate upload-cache admission (64 MiB padded buffers/256 generations per view). Fifteen production-function checks and desktop/web compilation passed. Actual Opus 5.5 `xhigh` review found no blocking issues; Help wording was clarified afterward. Read `evidence/coderabbit-followup/checked-review-report.txt` for failing controls, exact limits and probe scope. This upload-cache budget is not a total-process or GPU-memory cap. A fresh targeted native follow-up passed the 256-generation omission/recovery case and displayed a placeholder without a cursor glyph overlay. Focused cursor semantics remain covered by the production-function probe. The library source-storage default is 10,000,000 bytes per screen; the synthetic cache byte-boundary probe is not evidence that five large RGBA assets coexist under that default. Temporary lab overrides were restored and the installed main app remained healthy. Read the included native observation and storage-limit receipts; broader UI/platform gaps remain as stated.

## Maintainer six-request follow-up

Read `evidence/maintainer-review/checked-review-report.txt` for dispositions and limits. The current renderer keeps text updating after image errors, logs once per streak outside the VT lock, bounds owned copies at64 MiB/256 assets, searches ESC first, and simplifies Help. Both sources document the ordered-grid contract; pixel-only claims stay intentional. Fresh actual native fault/ownership probes,70,797 boundary cases, optimized desktop/shared wasm checks, and actual Opus 5.5 `xhigh` reviews pass. Earlier native UI/core/replay evidence remains historical. Use `zmx-current-review.patch` for the current comment-only follow-up; original patches remain unchanged. Both drafts still need upstream zmx landing, the exact pin, and combined integration checks before release.
