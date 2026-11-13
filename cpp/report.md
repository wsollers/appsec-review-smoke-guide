# Verification: cpp

- repository: /home/wsollers/projects/appsec-review-smoke-cpp
- head: bededb650d0c576e27b0041e9f675040b9a7bd97
- commits: 38
- source lines (excluding third_party, vendor, node_modules, tools): 397

## Build (offline, user 10001, image audit-buildenv-cpp:local)
- command: sh -c cmake -S . -B /scratch/build && cmake --build /scratch/build -j8
- exit: 0
- elapsed: 1.9 s
- log tail:
            |          ^
            |          "%s", 
      1 warning generated.
      [100%] Linking CXX executable smoke_server
      [100%] Built target smoke_server

## Syft (dir:/target)
- artifacts: 0

## Semgrep (rules/semgrep/*.yml + rules/sei-cert/rules mounted as the evidence adapter does)
- findings: 228 total, 70 outside vendored trees, 38 semgrep errors
    - src/main.cpp:13 rules.appsec-review.review-signal.sink.cpp-banned-function-warning
    - src/main.cpp:16 rules-sei-cert.c.appsec-review.sei-cert.cpp.err34-c.unchecked-conversion-function
    - src/main.cpp:16 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:28 rules-sei-cert.c.appsec-review.sei-cert.cpp.fio30-c.nonliteral-format-without-arguments
    - src/request.cpp:28 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:35 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:50 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:51 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:54 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:54 rules.appsec-review.review-signal.sink.cpp-banned-function-warning
    - src/request.cpp:74 rules.appsec-review.review-signal.sink.cpp-narrow-size-product
    - src/request.cpp:75 rules.appsec-review.review-signal.sink.cpp-allocation-size-from-narrow-product
    - src/request.cpp:75 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:79 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:79 rules.appsec-review.review-signal.sink.cpp-copy-length-not-bounded
    - src/request.cpp:85 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:86 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:88 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:89 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:103 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:110 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:114 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:117 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:123 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:129 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:132 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:134 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:136 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:137 rules-sei-cert.c.appsec-review.sei-cert.cpp.env33-c.command-processor-call
    - src/request.cpp:137 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:142 rules.appsec-review.review-signal.sink.cpp-banned-function-warning
    - src/request.cpp:146 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:147 rules.appsec-review.review-signal.sink.cpp-banned-function-warning
    - src/request.cpp:149 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:150 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:152 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:153 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/request.cpp:161 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/session.cpp:8 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/session.cpp:12 rules.appsec-review.review-signal.sink.cpp-banned-function-warning
    - src/session.cpp:16 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/session.cpp:16 rules.appsec-review.review-signal.sink.cpp-copy-length-not-bounded
    - src/session.cpp:19 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/session.cpp:32 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/session.cpp:33 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/session.cpp:35 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/session.cpp:39 rules.appsec-review.review-signal.sink.cpp-banned-function-warning
    - src/session.cpp:43 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/session.cpp:43 rules.appsec-review.review-signal.sink.cpp-copy-length-not-bounded
    - src/session.cpp:53 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/session.cpp:54 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/synthetic.cpp:15 rules.appsec-review.review-signal.sink.cpp-banned-function-high
    - src/synthetic.cpp:19 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/synthetic.cpp:34 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/synthetic.cpp:34 rules.appsec-review.review-signal.sink.cpp-copy-length-not-bounded
    - src/synthetic.cpp:45 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/synthetic.cpp:45 rules.appsec-review.review-signal.sink.cpp-copy-length-not-bounded
    - src/synthetic.cpp:49 rules.appsec-review.review-signal.sink.cpp-banned-function-warning
    - src/synthetic.cpp:54 rules-sei-cert.c.appsec-review.sei-cert.cpp.err34-c.unchecked-conversion-function
    - src/synthetic.cpp:54 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/synthetic.cpp:55 rules-sei-cert.c.appsec-review.sei-cert.cpp.err34-c.unchecked-conversion-function
    - src/synthetic.cpp:55 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/util.c:10 rules.appsec-review.review-signal.sink.cpp-banned-function-high
    - src/util.c:20 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/util.c:20 rules.appsec-review.review-signal.sink.cpp-copy-length-not-bounded
    - src/util.c:29 rules.appsec-review.review-signal.sink.cpp-banned-function-high
    - src/util.c:34 rules.appsec-review.review-signal.sink.cpp-banned-function-review
    - src/util.c:34 rules.appsec-review.review-signal.sink.cpp-copy-length-not-bounded
    - src/util.c:39 rules-sei-cert.c.appsec-review.sei-cert.c.env33-c.command-processor-call
    - src/util.c:39 rules.appsec-review.review-signal.sink.cpp-banned-function-review

## History
- git log --follow on src/session.cpp:
    - 9642eb9 2026-04-11 Rename cache.cpp to session.cpp
    - 612480f 2025-11-17 Add a per-connection session cache
- fix commits (git log --grep CWE-):
    - b65fbfd9e1b57de4dab74708cb42358f55b77cec Fix path traversal in read_asset (CWE-22)
    - 81bc2eb44d8cecb6f6aac731af843439017e83aa Fix command injection in run_tool (CWE-78)
- dependency upgrade commits (git log --grep -E 'CVE-|GHSA-|RUSTSEC-|GO-20'):
    - 9620e2df62fff8173b2b986289595df84ac0e477 Upgrade vendored cJSON from 1.7.16 to 1.7.17
- revert/reapply:
    - b9fdd812cde85f9c928a23cb4aeeb1520c3d8250 Reapply "Append an X-Count header with the request counter to every reply"
    - 036f800151230627e1aa9fc0cfffaf28865c6f52 Revert "Append an X-Count header with the request counter to every reply"
- merges: 0
- commits touching more than three files:
    - 9596b63 Vendor cJSON 1.7.16 (4 files)
    - 3046a91 Vendor lz4 1.9.1 as a static library (11 files)
    - 147e1f3 Vendor bzip2 1.0.6 as a static library (11 files)
    - d57a5cc Vendor zlib 1.2.11 as a static library (28 files)
    - 7454967 Add the smoke server with a PING verb (4 files)
    - 751acb4 Initial commit (122 files)
- churn (commits per file, top 5):
    -      17 src/request.cpp
    -      10 CMakeLists.txt
    -       5 CHANGELOG.md
    -       4 src/util.c
    -       4 src/main.cpp
- SECURITY.md and CHANGELOG.md present: yes

## Complexity (src/request.cpp handle_request via tool-tree-sitter and complexity.py)
    {"qualified_name": "handle_request", "start_line": 95, "end_line": 164, "cyclomatic": 36, "decisions": {"boolean": 10, "if": 16, "loop": 2, "ternary": 7}, "parse_error": false}
    units: [('decode_image', 3), ('handle_request', 36), ('log_message', 1), ('read_asset', 4), ('run_tool', 5), ('serve_file', 2), ('serve_once', 2)]

## Dates
- first: 2025-05-06  last: 2026-09-03
- authors: Ada Lindqvist <ada@example.com>;Bao Nguyen <bao@example.com>;Cleo Marsh <cleo@example.com>;
