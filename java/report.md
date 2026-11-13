# Verification: java

- repository: /home/wsollers/projects/appsec-review-smoke-java
- head: 3219d1700d6913c37bdfccd9b89c1b14f4055a07
- commits: 34
- source lines (excluding third_party, vendor, node_modules, tools): 391

## Build (offline, user 10001, image audit-buildenv-java:local)
- command: sh -c javac -d /scratch/classes $(find src -name "*.java")
- exit: 0
- elapsed: 3.8 s
- log tail:
      Note: src/main/java/app/Server.java uses or overrides a deprecated API.
      Note: Recompile with -Xlint:deprecation for details.

## Syft (dir:/target)
- artifacts: 5
    - appsec-review-smoke-java 0.1.0 (java-archive)
    - commons-io 2.6 (java-archive)
    - commons-text 1.10.0 (java-archive)
    - log4j-core 2.14.1 (java-archive)
    - snakeyaml 1.30 (java-archive)

## Semgrep (rules/semgrep/*.yml + rules/sei-cert/rules mounted as the evidence adapter does)
- findings: 17 total, 17 outside vendored trees, 0 semgrep errors
    - src/main/java/app/Catalog.java:22 rules.appsec-review.review-signal.sink.java-sql-string-concatenation
    - src/main/java/app/Catalog.java:30 rules-sei-cert.java.appsec-review.sei-cert.java.ids00-j.concatenated-sql-statement
    - src/main/java/app/Catalog.java:30 rules.appsec-review.review-signal.sink.java-sql-string-concatenation
    - src/main/java/app/Catalog.java:43 rules-sei-cert.java.appsec-review.sei-cert.java.ids00-j.concatenated-sql-statement
    - src/main/java/app/Catalog.java:43 rules.appsec-review.review-signal.sink.java-sql-string-concatenation
    - src/main/java/app/Documents.java:21 rules.appsec-review.review-signal.sensitive_wrapper.java-xml-factory-without-hardening
    - src/main/java/app/Documents.java:22 rules-sei-cert.java.appsec-review.sei-cert.java.ids17-j.parser-without-entity-restriction
    - src/main/java/app/Documents.java:32 rules.appsec-review.review-signal.sensitive_wrapper.java-xml-factory-without-hardening
    - src/main/java/app/Documents.java:33 rules-sei-cert.java.appsec-review.sei-cert.java.ids17-j.parser-without-entity-restriction
    - src/main/java/app/FileStore.java:7 rules-sei-cert.java.appsec-review.sei-cert.java.err07-j.declares-generic-exception
    - src/main/java/app/Server.java:23 rules-sei-cert.java.appsec-review.sei-cert.java.err07-j.declares-generic-exception
    - src/main/java/app/Server.java:41 rules-sei-cert.java.appsec-review.sei-cert.java.err07-j.declares-generic-exception
    - src/main/java/app/Server.java:45 rules-sei-cert.java.appsec-review.sei-cert.java.err07-j.declares-generic-exception
    - src/main/java/app/Server.java:49 rules-sei-cert.java.appsec-review.sei-cert.java.err07-j.declares-generic-exception
    - src/main/java/app/Server.java:56 rules-sei-cert.java.appsec-review.sei-cert.java.err07-j.declares-generic-exception
    - src/main/java/app/Server.java:61 rules-sei-cert.java.appsec-review.sei-cert.java.err07-j.declares-generic-exception
    - src/main/java/app/Server.java:65 rules-sei-cert.java.appsec-review.sei-cert.java.err07-j.declares-generic-exception

## History
- git log --follow on src/main/java/app/Documents.java:
    - 750789f 2026-03-27 Rename Xml.java to Documents.java
    - 90937b5 2025-11-14 Add a DEFAULTS verb that parses the built-in defaults document
    - 04e73a3 2025-09-29 Add an XML verb that parses a submitted document
- fix commits (git log --grep CWE-):
    - b6a8be4a30ab01ec085216909e7e7104e0279f44 Fix path traversal in Assets.read (CWE-22)
    - b9f236456e2a86914f7426bfd66c17d6c7571c14 Fix command injection in Tools.run (CWE-78)
- dependency upgrade commits (git log --grep -E 'CVE-|GHSA-|RUSTSEC-|GO-20'):
    - 779ece368f7304d58b03656eca22354df18d7ff0 Upgrade commons-text from 1.9 to 1.10.0
- revert/reapply:
    - 745d978bd8f94cc3221095096fd535f80ebef28c Reapply "Append an X-Count trailer with the request counter to every reply"
    - 19cc2de49e1e0a39e58aca261e7ce3f6077b61a6 Revert "Append an X-Count trailer with the request counter to every reply"
- merges: 0
- commits touching more than three files:
    - eec21d6 Initial commit (111 files)
- churn (commits per file, top 5):
    -      15 src/main/java/app/Router.java
    -       7 pom.xml
    -       5 CHANGELOG.md
    -       4 src/main/java/app/Catalog.java
    -       3 src/main/java/app/Assets.java
- SECURITY.md and CHANGELOG.md present: yes

## Complexity (src/main/java/app/Router.java route via tool-tree-sitter and complexity.py)
    {"qualified_name": "Router.route", "start_line": 22, "end_line": 86, "cyclomatic": 37, "decisions": {"boolean": 10, "catch": 1, "if": 14, "loop": 1, "ternary": 10}, "parse_error": false}
    units: [('Router.Router', 1), ('Router.reply', 1), ('Router.route', 37)]

## Dates
- first: 2025-04-15  last: 2026-08-24
- authors: Ada Lindqvist <ada@example.com>;Bao Nguyen <bao@example.com>;Cleo Marsh <cleo@example.com>;
