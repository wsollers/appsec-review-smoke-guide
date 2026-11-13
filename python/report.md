# Verification: python

- repository: /home/wsollers/projects/appsec-review-smoke-python
- head: 0821c008da6ef5b9055e7cd4cc27d71a5bb147a7
- commits: 35
- source lines (excluding third_party, vendor, node_modules, tools): 241

## Build (offline, user 10001, image audit-buildenv-python:local)
- command: python3 -m compileall -q .
- exit: 0
- elapsed: 5.5 s
- log tail:

## Syft (dir:/target)
- artifacts: 8
    - certifi 2026.10.18 (python)
    - charset-normalizer 3.4.1 (python)
    - idna 3.6 (python)
    - jinja2 3.1.6 (python)
    - markupsafe 3.0.2 (python)
    - pyyaml 5.3 (python)
    - requests 2.33.0 (python)
    - urllib3 1.24 (python)

## Semgrep (rules/semgrep/*.yml + rules/sei-cert/rules mounted as the evidence adapter does)
- findings: 4 total, 4 outside vendored trees, 0 semgrep errors
    - src/smoke/tools.py:9 rules.appsec-review.python-dangerous-eval
    - src/smoke/tools.py:17 rules.appsec-review.python-dangerous-eval
    - src/smoke/tools.py:24 rules.appsec-review.python-dangerous-eval
    - src/smoke/tools.py:29 rules.appsec-review.python-dangerous-eval

## History
- git log --follow on src/smoke/navigation.py:
    - c9386df 2026-04-21 Rename redirects.py to navigation.py
    - f8bb2ff 2025-10-09 Add a redirect helper for the login return path
- fix commits (git log --grep CWE-):
    - 990bdd6d025cd59e4005af3737ae7fad77f3eb56 Fix path traversal in read_report (CWE-22)
    - e1fd4ee32f3c83bf1db1803513a87cf0a66bcb71 Fix command injection in archive (CWE-78)
- dependency upgrade commits (git log --grep -E 'CVE-|GHSA-|RUSTSEC-|GO-20'):
    - 00a8a932ab75cbaac2b1c01f067e2bc84deaad00 Upgrade Jinja2 from 2.10 to 3.1.6
- revert/reapply:
    - 11cca677939fbd01bd6aad59c1b39bc1aca715bb Reapply "Append the request counter to every reply"
    - ab60640ea78b553d7a2497036edabc999141f34e Revert "Append the request counter to every reply"
- merges: 0
- commits touching more than three files:
    - 102946f Initial commit (108 files)
- churn (commits per file, top 5):
    -      15 src/smoke/service.py
    -       5 src/smoke/tools.py
    -       5 CHANGELOG.md
    -       4 src/smoke/maintenance.py
    -       4 requirements.txt
- SECURITY.md and CHANGELOG.md present: yes

## Complexity (src/smoke/service.py handle_request via tool-tree-sitter and complexity.py)
    Traceback (most recent call last):
      File "/home/wsollers/smoke-work/tools/complexity_check.py", line 33, in <module>
        spec = SPECS[record["grammar"]]
               ~~~~~^^^^^^^^^^^^^^^^^^^
    KeyError: 'python'

## Dates
- first: 2025-05-06  last: 2026-08-28
- authors: Ada Lindqvist <ada@example.com>;Bao Nguyen <bao@example.com>;Cleo Marsh <cleo@example.com>;
