# appsec-review/smoke-answer-key/1

One `answer-key.json` per language directory in `appsec-review-smoke-guide`. Authored by the
session that built the target, from the target's `PLANTED.md`, the Stage 3 verification report
and the fixture's `expected-facts.json`. Line numbers and SHAs are for the tagged head.

```json
{
  "schema": "appsec-review/smoke-answer-key/1",
  "language": "cpp",
  "repository": "https://github.com/wsollers/appsec-review-smoke-cpp",
  "tag": "v1.0.0",
  "commit": "<40-hex sha of the tagged commit>",
  "build": {
    "profile": "native",
    "image": "audit-buildenv-cpp:local",
    "command": "cmake -S . -B /scratch/build && cmake --build /scratch/build",
    "elapsed_seconds": 6.1,
    "expected_build_units": 1,
    "notes": "free text: anything the build needed (e.g. HAVE_UNISTD_H for zlib under clang)"
  },
  "planted": [
    {
      "class": "true_positive_code",
      "id": "TP-C1",
      "cwe": "CWE-78",
      "title": "command injection through the EXEC verb",
      "file": "src/request.cpp",
      "function": "handle_request",
      "span": {"start_line": 137, "end_line": 137},
      "source": {"file": "src/request.cpp", "function": "serve_once", "line": 170, "api": "recv"},
      "sink": {"api": "popen", "line": 137},
      "expected_disposition": "reported"
    },
    {
      "class": "true_positive_dependency",
      "id": "TP-D1",
      "package": "zlib", "version": "1.2.11", "ecosystem": "vendored-c",
      "osv": "GHSA-jc36-42cf-vqwj", "cve": "CVE-2018-25032", "fixed_version": "1.2.12",
      "location": "third_party/zlib",
      "visible_to": ["cve-bin-tool version string", "source text"],
      "not_visible_to": ["syft lockfile catalogers", "osv-scanner lockfile scan"],
      "expected_disposition": "reported"
    },
    {
      "class": "fixed_code",
      "id": "FX-C1",
      "cwe": "CWE-78",
      "title": "command injection in run_tool",
      "file": "src/request.cpp",
      "function": "run_tool",
      "introduced_commit": "<sha>",
      "introduced_span": {"start_line": 0, "end_line": 0},
      "fixed_commit": "<sha>",
      "fix_kind": "sink_removed | sanitizer_added | guard_added",
      "fixed_state_fact": "none | path_sanitizers realpath | guard_fact dominating strncmp",
      "expected_disposition": "reported-as-fixed"
    },
    {
      "class": "fixed_dependency",
      "id": "FX-D1",
      "package": "cjson", "ecosystem": "vendored-c",
      "vulnerable_version": "1.7.16", "fixed_version": "1.7.17",
      "osv": "CVE-2023-50472", "cve": "CVE-2023-50472",
      "introduced_commit": "<sha>", "fixed_commit": "<sha>",
      "expected_disposition": "reported-as-fixed"
    },
    {
      "class": "false_positive",
      "id": "FP-1",
      "file": "src/util.c",
      "function": "frame_fill",
      "span": {"start_line": 20, "end_line": 20},
      "flagged_by": ["appsec-review.review-signal.sink.cpp-copy-length-not-bounded"],
      "refuted_by": {"fact_family": "guard_fact", "detail": "n < sizeof(f->data) dominates the sink, polarity true_branch, constrains_sink_operand", "location": {"file": "src/util.c", "line": 19}},
      "expected_disposition": "squelched"
    }
  ],
  "complexity": {
    "file": "src/request.cpp", "function": "handle_request", "cyclomatic": 36,
    "holds": "TP-C1", "expected_top_rank": true, "cyclomatic_high_risk_share_above_zero": true
  },
  "graph_facts": {
    "fixture": "tests/fixtures/graph/codeql_export/synthetic",
    "expected_facts_file": "expected-facts.json",
    "line_numbers_moved": false,
    "adjustment": null
  },
  "language_matrix": {"languages": ["C", "C++"], "tools": ["codeql", "semgrep", "opengrep", "cppcheck", "syft", "grype", "osv-scanner", "cve-bin-tool"]},
  "history": {
    "commits": 38,
    "authors": ["Ada Lindqvist <ada@example.com>", "Bao Nguyen <bao@example.com>", "Cleo Marsh <cleo@example.com>"],
    "first_date": "2025-05-06", "last_date": "2026-09-03",
    "fix_commits": ["<sha>", "<sha>"],
    "upgrade_commit": "<sha>",
    "rename": {"from": "src/cache.cpp", "to": "src/session.cpp", "commit": "<sha>"},
    "revert": {"reverted_commit": "<sha>", "revert_commit": "<sha>", "reapply_commit": "<sha>"},
    "not_exploitable_commit": {"commit": "<sha>", "about": "FP-1"},
    "highest_churn_file": "src/request.cpp",
    "security_md": true, "changelog": true
  },
  "verification": {
    "syft_reported": [],
    "semgrep_flagged_false_positives": ["FP-1", "FP-2", "FP-3", "FP-4", "FP-5"],
    "semgrep_unflagged_false_positives": []
  },
  "expected_gaps": [
    {"gap": "syft lists no vendored C library", "reason": "no package-manager manifest; OSV has no ConanCenter records for these packages", "affects": ["TP-D1", "TP-D2", "TP-D3", "FX-D1"]}
  ],
  "substitutions": [
    {"planned": "monolog/monolog 1.23.0", "actual": "guzzlehttp/guzzle 7.4.0", "reason": "no OSV record for monolog"}
  ]
}
```

Rules:
- `class` is one of `true_positive_code`, `true_positive_dependency`, `fixed_code`,
  `fixed_dependency`, `false_positive`. `expected_disposition` is `reported`, `reported-as-fixed`
  or `squelched`.
- Every false positive names the rule id(s) the Stage 3 Semgrep run actually reported for its span
  in `flagged_by`. If no mounted rule reported it, `flagged_by` is `[]` and the item also appears in
  `verification.semgrep_unflagged_false_positives` and in `expected_gaps`.
- `refuted_by.fact_family` is one of `guard_fact`, `path_sanitizers`, `range_fact`,
  `no_dataflow_path` (constant operand or dead code).
- Dependencies: `ecosystem` uses the OSV ecosystem name (`npm`, `PyPI`, `Maven`, `Go`,
  `crates.io`, `RubyGems`, `NuGet`, `Packagist`) or `vendored-c`.
- SHAs are copied from `git log` of the tagged head after `make-history.sh` ran; never typed by hand.
