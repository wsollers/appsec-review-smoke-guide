# Verification: rust

- repository: /home/wsollers/projects/appsec-review-smoke-rust
- head: 6a11cc9677028a0eba366177019e599f35bcc978
- commits: 38
- source lines (excluding third_party, vendor, node_modules, tools): 345

## Build (offline, user 10001, image audit-buildenv-rust-wasm:local)
- command: cargo build --offline --locked --target-dir /scratch/target
- exit: 0
- elapsed: 1.9 s
- log tail:
         Compiling rusqlite v0.0.0 (/workspace/vendor/rusqlite)
         Compiling log v0.4.22
         Compiling serde_json v0.0.0 (/workspace/vendor/serde_json)
         Compiling appsec-review-smoke-rust v0.1.0 (/workspace)
          Finished `dev` profile [unoptimized + debuginfo] target(s) in 0.42s

## Syft (dir:/target)
- artifacts: 17
    - appsec-review-smoke-rust 0.1.0 (rust-crate)
    - autocfg 1.1.0 (rust-crate)
    - cfg-if 1.0.0 (rust-crate)
    - crossbeam-utils 0.8.6 (rust-crate)
    - lazy_static 1.4.0 (rust-crate)
    - libc 0.2.155 (rust-crate)
    - log 0.4.22 (rust-crate)
    - memoffset 0.6.2 (rust-crate)
    - reqwest 0.0.0 (rust-crate)
    - rusqlite 0.0.0 (rust-crate)
    - serde_json 0.0.0 (rust-crate)
    - smallvec 0.6.9 (rust-crate)
    - time 0.1.43 (rust-crate)
    - unicode-normalization 0.1.9 (rust-crate)
    - winapi 0.3.9 (rust-crate)
    - winapi-i686-pc-windows-gnu 0.4.0 (rust-crate)
    - winapi-x86_64-pc-windows-gnu 0.4.0 (rust-crate)

## Semgrep (rules/semgrep/*.yml + rules/sei-cert/rules mounted as the evidence adapter does)
- findings: 0 total, 0 outside vendored trees, 0 semgrep errors

## History
- git log --follow on src/server/session.rs:
    - 14c90c0 2026-06-29 Sweep expired sessions when a session opens
    - ab414b9 2026-04-25 Rename cache.rs to session.rs
    - 3dc83e6 2026-01-10 Let SESSION reserve scratch pages
    - 3423cf7 2025-12-16 Add a per-connection session cache
- fix commits (git log --grep CWE-):
    - c0b76953ee7664a9ddc5313c695d0d08bc803ec7 Fix path traversal in read_asset (CWE-22)
    - 3c293984eb7acfc43a23e521145fe183415c3e06 Fix command injection in run_maintenance (CWE-78)
- dependency upgrade commits (git log --grep -E 'CVE-|GHSA-|RUSTSEC-|GO-20'):
    - dd0d5ad5ca9299fcd6140157f3a4a45c0fbeea75 Upgrade memoffset from 0.5.5 to 0.6.2
- revert/reapply:
    - c378bd75f28be619f4ce666602ec1b552fc8e771 Reapply "Append an X-Count trailer with the request counter to every reply"
    - 20f0153ee5cb694061128437bf8aeba4048cecc2 Revert "Append an X-Count trailer with the request counter to every reply"
- merges: 0
- commits touching more than three files:
    - dd0d5ad Upgrade memoffset from 0.5.5 to 0.6.2 (10 files)
    - 959575b Vendor log 0.4.22 (16 files)
    - 3891831 Vendor memoffset 0.5.5 behind the offsets feature (20 files)
    - 527c77a Vendor crossbeam-utils 0.8.6 behind the threads feature (36 files)
    - c9156d2 Vendor unicode-normalization 0.1.9 behind the normalize feature (23 files)
    - 301558e Vendor time 0.1.43 behind the legacy-time feature (672 files)
    - 3a059de Vendor offline stand-ins for reqwest, rusqlite and serde_json (10 files)
    - a8e1a06 Initial commit (123 files)
- churn (commits per file, top 5):
    -      15 src/server/request.rs
    -       8 Cargo.toml
    -       7 Cargo.lock
    -       6 src/server/main.rs
    -       5 src/server/util.rs
- SECURITY.md and CHANGELOG.md present: yes

## Complexity (src/server/request.rs handle_request via tool-tree-sitter and complexity.py)
    {"qualified_name": "handle_request", "start_line": 41, "end_line": 107, "cyclomatic": 20, "decisions": {"boolean": 2, "guard": 1, "if": 10, "loop": 1, "multiway_arm": 5}, "parse_error": false}
    units: [('handle_request', 20), ('read_asset', 3), ('run_maintenance', 3), ('serve_file', 1), ('serve_once', 3)]

## Dates
- first: 2025-05-20  last: 2026-09-17
- authors: Ada Lindqvist <ada@example.com>;Bao Nguyen <bao@example.com>;Cleo Marsh <cleo@example.com>;
