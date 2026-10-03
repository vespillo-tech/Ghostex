# Static Kitty image review evidence

[Download the public review package](static-images-pr-review.zip?raw=true). It contains portable fixtures and probes, patches, full validation logs, implementation review maps, checked Claude findings, resource limits and known gaps.

| Contribution | Exact review head | Target |
| --- | --- | --- |
| Ghostex renderer | [a5011395da68](https://github.com/vespillo-tech/Ghostex/commit/a5011395da6827874e9c47d548b8094f7116a84d) | `maddada/Ghostex:main` at `56a620fe8313` |
| zmx replay and optional grid coordination | [c630130eb7aa](https://github.com/vespillo-tech/zmx/commit/c630130eb7aa007407d6f63d0c77932009798e16) | `maddada/zmx:nightly` at `feaefff98723` |

## Review order

1. Read `review-overview.md`, then the owner-specific PR bodies and report.
2. For current Ghostex main, use `renderer-current-main.patch`; the older patch is retained for traceability.
3. Review zmx first. Ghostex must pin the exact reviewed upstream zmx feature commit and repeat focused integration checks before release. Its current gitlink is unchanged.

## Verification and limits

Apple Silicon macOS runtime acceptance covers ordinary and Unicode-placeholder static images, PNG, search, split panes, resizing, history, viewer reattachment and pane ID isolation. The current-main optimized desktop build and shared wasm compilation passed; native runtime observations used the previous main with identical feature additions/deletions. The full unchanged Ghostty core passed 6,472 tests with 52 skips on both base and candidate; zmx passed 108 existing tests and 39 semantic replay cases.

This is bounded static image support. Full animation/identity restoration, browser rendering and native Windows retained state remain separate work. Linux/Windows/Intel runtime acceptance, CJK preedit and deliberate link hover are unverified. Existing mixed-mode history widths and partial-UTF-8-before-Init issues are documented. Aggregate memory and power are unmeasured. See the report for exact resource limits and exclusions.

The archive uses a public allowlist, has verified CRCs and entry hashes, and excludes private inventories, auth, profiles, raw Claude outputs, caches and binaries. This documentation branch contains no application changes or workflows.
