# Verification: php

- repository: /home/wsollers/projects/appsec-review-smoke-php
- head: ef0c942de7d2b109351075b5275c1308b98bb892
- commits: 34
- source lines (excluding third_party, vendor, node_modules, tools): 291

## Build (offline, user 10001, image audit-buildenv-php:local)
- command: sh -c for f in $(find public src -name "*.php"); do php -l "$f" || exit 1; done
- exit: 0
- elapsed: 4.8 s
- log tail:
      No syntax errors detected in src/synthetic.php
      No syntax errors detected in src/store.php
      No syntax errors detected in src/legacy.php
      No syntax errors detected in src/handler.php
      No syntax errors detected in src/manifest.php

## Syft (dir:/target)
- artifacts: 12
    - guzzlehttp/guzzle 7.4.0 (php-composer)
    - guzzlehttp/promises 1.5.3 (php-composer)
    - guzzlehttp/psr7 2.1.0 (php-composer)
    - phpmailer/phpmailer v6.5.0 (php-composer)
    - psr/http-client 1.0.3 (php-composer)
    - psr/http-factory 1.1.0 (php-composer)
    - psr/http-message 1.1 (php-composer)
    - ralouphie/getallheaders 3.0.3 (php-composer)
    - symfony/deprecation-contracts v2.5.4 (php-composer)
    - symfony/polyfill-ctype v1.37.0 (php-composer)
    - symfony/polyfill-mbstring v1.43.3 (php-composer)
    - twig/twig v3.3.0 (php-composer)

## Semgrep (rules/semgrep/*.yml + rules/sei-cert/rules mounted as the evidence adapter does)
- findings: 5 total, 5 outside vendored trees, 0 semgrep errors
    - src/legacy.php:9 rules.appsec-review.review-signal.sink.php-unserialize-request
    - src/legacy.php:17 rules.appsec-review.review-signal.privilege_shift.php-curl-verification-disabled
    - src/store.php:12 rules.appsec-review.review-signal.sink.php-sql-string-concatenation
    - src/store.php:24 rules.appsec-review.review-signal.sink.php-sql-string-concatenation
    - src/store.php:31 rules.appsec-review.review-signal.sink.php-sql-string-concatenation

## History
- git log --follow on src/manifest.php:
    - 53f9024 2026-03-26 Rename import.php to manifest.php
    - d363434 2025-08-30 Add an import action that reads a posted XML manifest
- fix commits (git log --grep CWE-):
    - 9b41a18a76f9db6635620b6e36e85b495da80929 Fix path traversal in read_asset (CWE-22)
    - 64e75c0cefd2221367183d6b2e829093d0f0e0b5 Fix command injection in run_tool (CWE-78)
- dependency upgrade commits (git log --grep -E 'CVE-|GHSA-|RUSTSEC-|GO-20'):
    - ee43122b2a7ab9bdc11fe193f38f23d579f16e84 Upgrade phpmailer/phpmailer from 6.4.0 to 6.5.0
- revert/reapply:
    - 1eec7af94b39ed4ae2bbf43e007d436226d1e268 Reapply "Send an X-Count header with the request counter on every reply"
    - f6b2e01fadc50259985648f70704b1fb869fede7 Revert "Send an X-Count header with the request counter on every reply"
- merges: 0
- commits touching more than three files:
    - d86087d Initial commit (105 files)
- churn (commits per file, top 5):
    -      19 src/handler.php
    -       5 CHANGELOG.md
    -       4 src/store.php
    -       3 composer.json
    -       2 src/legacy.php
- SECURITY.md and CHANGELOG.md present: yes

## Complexity (src/handler.php handle_request via tool-tree-sitter and complexity.py)
    {"qualified_name": "handle_request", "start_line": 53, "end_line": 101, "cyclomatic": 32, "decisions": {"boolean": 6, "if": 11, "null_coalescing": 8, "ternary": 6}, "parse_error": false}
    units: [('audit', 1), ('handle_request', 32), ('read_asset', 2), ('run_tool', 3), ('serve_template', 2)]

## Dates
- first: 2025-04-14  last: 2026-08-23
- authors: Ada Lindqvist <ada@example.com>;Bao Nguyen <bao@example.com>;Cleo Marsh <cleo@example.com>;
