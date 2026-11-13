# Verification: javascript

- repository: /home/wsollers/projects/appsec-review-smoke-javascript
- head: 84e3c01a2b312c87b6f2fe804b397990abf74388
- commits: 38
- source lines (excluding third_party, vendor, node_modules, tools): 277

## Build (offline, user 10001, image audit-buildenv-typescript:local)
- command: sh -c node node_modules/typescript/bin/tsc -p tsconfig.json --outDir /scratch/out
- exit: 0
- elapsed: 5.1 s
- log tail:

## Syft (dir:/target)
- artifacts: 9
    - appsec-review-smoke-javascript 1.0.0 (npm)
    - lodash 4.17.15 (npm)
    - minimist 0.0.8 (npm)
    - mkdirp 0.5.1 (npm)
    - node-fetch 2.6.7 (npm)
    - tr46 0.0.3 (npm)
    - webidl-conversions 3.0.1 (npm)
    - whatwg-url 5.0.0 (npm)
    - ws 7.4.5 (npm)

## Semgrep (rules/semgrep/*.yml + rules/sei-cert/rules mounted as the evidence adapter does)
- findings: 5 total, 5 outside vendored trees, 0 semgrep errors
    - src/helpers.js:6 rules.appsec-review.javascript-dangerous-eval
    - src/helpers.js:14 rules.appsec-review.javascript-dangerous-eval
    - src/helpers.js:23 rules.appsec-review.javascript-dangerous-eval
    - src/helpers.js:28 rules.appsec-review.javascript-dangerous-eval
    - src/helpers.js:33 rules.appsec-review.review-signal.privilege_shift.node-tls-verification-disabled

## History
- git log --follow on src/filter.js:
    - e20a6fe 2026-04-17 Rename search.js to filter.js
    - 3f51d2d 2025-11-23 Add a search module with a filter route
- fix commits (git log --grep CWE-):
    - 2b2d8e170f2b3d3f2c250eedc782ba3131793ef8 Fix path traversal in readTemplate (CWE-22)
    - cb812c1eb2da96aa0f74fb475872f1a51c205f1e Fix command injection in runReport (CWE-78)
- dependency upgrade commits (git log --grep -E 'CVE-|GHSA-|RUSTSEC-|GO-20'):
    - 7f95a0aff215078e7e777aa60031f3dd61fe7282 Upgrade node-fetch from 2.6.0 to 2.6.7
- revert/reapply:
    - 6c073b244b7e0c620a9a55eb25856075720b5e2a Reapply "Add an X-Request-Id header to API replies"
    - 26ff3b4a9172a69313ec77fd235dfae2d7cb5fa9 Revert "Add an X-Request-Id header to API replies"
- merges: 0
- commits touching more than three files:
    - e139164 Vendor typescript 5.6.3 (53 files)
    - 4291c1c Initial commit (117 files)
- churn (commits per file, top 5):
    -      19 src/server.js
    -       5 src/helpers.js
    -       5 package.json
    -       5 package-lock.json
    -       5 CHANGELOG.md
- SECURITY.md and CHANGELOG.md present: yes

## Complexity (src/server.js handleApi via tool-tree-sitter and complexity.py)
    {"qualified_name": "handleApi", "start_line": 38, "end_line": 95, "cyclomatic": 25, "decisions": {"boolean": 6, "case": 3, "if": 12, "loop": 1, "ternary": 2}, "parse_error": false}
    units: [('handleApi', 25), ('handleAudit', 1), ('readTemplate', 1), ('runReport', 3), ('serve', 1)]

## Dates
- first: 2025-05-12  last: 2026-09-09
- authors: Ada Lindqvist <ada@example.com>;Bao Nguyen <bao@example.com>;Cleo Marsh <cleo@example.com>;
