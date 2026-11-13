# Verification: go

- repository: /home/wsollers/projects/appsec-review-smoke-go
- head: 5f83d50620529d94a07ef0d1765462ada17f239e
- commits: 34
- source lines (excluding third_party, vendor, node_modules, tools): 268

## Build (offline, user 10001, image audit-buildenv-go:local)
- command: go build -o /scratch/bin/ ./...
- exit: 0
- elapsed: 5.3 s
- log tail:

## Syft (dir:/target)
- artifacts: 5
    - github.com/gorilla/websocket v1.5.3 (go-module)
    - github.com/spf13/cobra v0.0.5 (go-module)
    - github.com/tidwall/gjson v1.6.0 (go-module)
    - golang.org/x/text v0.3.0 (go-module)
    - gopkg.in/yaml.v2 v2.2.2 (go-module)

## Semgrep (rules/semgrep/*.yml + rules/sei-cert/rules mounted as the evidence adapter does)
- findings: 6 total, 6 outside vendored trees, 0 semgrep errors
    - devtls.go:13 rules.appsec-review.review-signal.privilege_shift.go-tls-verification-disabled
    - main.go:42 rules.appsec-review.review-signal.sink.go-sql-string-concatenation
    - store.go:23 rules.appsec-review.review-signal.sink.go-sql-string-concatenation
    - store.go:35 rules.appsec-review.review-signal.sink.go-sql-string-concatenation
    - store.go:41 rules.appsec-review.review-signal.sink.go-sql-string-concatenation
    - store.go:47 rules.appsec-review.review-signal.sink.go-sql-string-concatenation

## History
- git log --follow on logging.go:
    - e663215 2026-06-01 Rename audit.go to logging.go
    - dd03bdd 2025-10-31 Add an audit op that writes an access line to the server log
- fix commits (git log --grep CWE-):
    - b96ed3cdbe6293080a6d921a185a962266b20d13 Fix path traversal in readAsset (CWE-22)
    - 3ffe06083562874bbfa35c5b73697c583e8d3460 Fix command injection in runTool (CWE-78)
- dependency upgrade commits (git log --grep -E 'CVE-|GHSA-|RUSTSEC-|GO-20'):
    - 42eb97da6e41acd68d409486e8e3396b3b9ff057 Upgrade gorilla/websocket from 1.4.0 to 1.5.3
- revert/reapply:
    - 4cb21a4dc1cf640ab1842d0a9dcd14ec7d3ba16b Reapply "Add an X-Admin-Op header to every reply"
    - db4ad634c2a0dc4696d42a592467ce69ef9e37c5 Revert "Add an X-Admin-Op header to every reply"
- merges: 0
- commits touching more than three files:
    - 1f6ea61 Initial commit (105 files)
- churn (commits per file, top 5):
    -      16 admin.go
    -       6 store.go
    -       5 CHANGELOG.md
    -       4 ops.go
    -       4 go.mod
- SECURITY.md and CHANGELOG.md present: yes

## Complexity (admin.go adminHandler via tool-tree-sitter and complexity.py)
    {"qualified_name": "adminHandler", "start_line": 16, "end_line": 82, "cyclomatic": 24, "decisions": {"boolean": 3, "case": 8, "if": 12}, "parse_error": false}
    units: [('adminHandler', 24), ('init', 1)]

## Dates
- first: 2025-06-03  last: 2026-10-12
- authors: Ada Lindqvist <ada@example.com>;Bao Nguyen <bao@example.com>;Cleo Marsh <cleo@example.com>;
