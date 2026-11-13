# Verification: ruby

- repository: /home/wsollers/projects/appsec-review-smoke-ruby
- head: c82179dbe7a7aa6f56e523160627476fe9cf8148
- commits: 38
- source lines (excluding third_party, vendor, node_modules, tools): 196

## Build (offline, user 10001, image none)
- SKIPPED: no build profile image for ruby (recorded gap)

## Syft (dir:/target)
- artifacts: 9
    - kramdown 2.3.1 (gem)
    - mustermann 1.0.3 (gem)
    - rack 2.0.0 (gem)
    - rack-protection 2.0.0 (gem)
    - rexml 3.2.4 (gem)
    - sinatra 2.0.0 (gem)
    - thread_safe 0.3.6 (gem)
    - tilt 2.0.9 (gem)
    - tzinfo 1.2.10 (gem)

## Semgrep (rules/semgrep/*.yml + rules/sei-cert/rules mounted as the evidence adapter does)
- findings: 0 total, 0 outside vendored trees, 0 semgrep errors

## History
- git log --follow on lib/archive.rb:
    - cf6c6d2 2026-03-27 Rename exports.rb to archive.rb
    - 54ab285 2025-11-07 Add an exports controller that returns the client to its page
- fix commits (git log --grep CWE-):
    - 1944a87e6f7dfdea7e1668dd14fad528978cb98c Fix path traversal in read_attachment (CWE-22)
    - 189f496baa996d560f7f02c7b2947aac6333ef9c Fix command injection in run_report (CWE-78)
- dependency upgrade commits (git log --grep -E 'CVE-|GHSA-|RUSTSEC-|GO-20'):
    - 2dc154f5fd4669af7b7afdd0e465ccf6a071975d Upgrade tzinfo from 1.2.9 to 1.2.10
- revert/reapply:
    - c1cf23d92adc7ed9f822e793c69a9dcd8aa9c3f0 Reapply "Append an X-Count header with the request counter to every reply"
    - d24fc5a48e92705847febc9cf00d5309bd265e49 Revert "Append an X-Count header with the request counter to every reply"
- merges: 0
- commits touching more than three files:
    - e809cc4 Initial commit (117 files)
- churn (commits per file, top 5):
    -      19 lib/reports_controller.rb
    -       6 lib/helpers.rb
    -       6 Gemfile.lock
    -       6 Gemfile
    -       5 CHANGELOG.md
- SECURITY.md and CHANGELOG.md present: yes

## Complexity (lib/reports_controller.rb show via tool-tree-sitter and complexity.py)
    {"qualified_name": "ReportsController.show", "start_line": 24, "end_line": 63, "cyclomatic": 22, "decisions": {"boolean": 5, "case": 5, "if": 9, "ternary": 2}, "parse_error": false}
    units: [('ReportsController.read_attachment', 1), ('ReportsController.run_report', 1), ('ReportsController.show', 22)]

## Dates
- first: 2025-05-06  last: 2026-09-03
- authors: Ada Lindqvist <ada@example.com>;Bao Nguyen <bao@example.com>;Cleo Marsh <cleo@example.com>;
