# Verification: csharp

- repository: /home/wsollers/projects/appsec-review-smoke-csharp
- head: 887af65120b0395f1066bd5183017d00808b5b62
- commits: 36
- source lines (excluding third_party, vendor, node_modules, tools): 321

## Build (offline, user 10001, image audit-buildenv-dotnet:local)
- command: sh -c dotnet restore --locked-mode -p:BaseIntermediateOutputPath=/scratch/obj/ && dotnet build --no-restore -p:BaseIntermediateOutputPath=/scratch/obj/ -p:OutputPath=/scratch/bin/
- exit: 0
- elapsed: 18.2 s
- log tail:
      Build succeeded.
          0 Warning(s)
          0 Error(s)
      
      Time Elapsed 00:00:02.86

## Syft (dir:/target)
- artifacts: 9
    - Microsoft.NETCore.Platforms 5.0.0 (dotnet)
    - Newtonsoft.Json 12.0.1 (dotnet)
    - RestSharp 106.11.7 (dotnet)
    - SharpZipLib 1.3.3 (dotnet)
    - SixLabors.Fonts 1.0.0 (dotnet)
    - SixLabors.ImageSharp 2.1.5 (dotnet)
    - SixLabors.ImageSharp.Drawing 1.0.0 (dotnet)
    - System.Runtime.CompilerServices.Unsafe 5.0.0 (dotnet)
    - System.Text.Encoding.CodePages 5.0.0 (dotnet)

## Semgrep (rules/semgrep/*.yml + rules/sei-cert/rules mounted as the evidence adapter does)
- findings: 5 total, 5 outside vendored trees, 0 semgrep errors
    - src/MaintenanceController.cs:75 rules.appsec-review.review-signal.sink.csharp-process-shell
    - src/ShellHelpers.cs:15 rules.appsec-review.review-signal.sink.csharp-process-shell
    - src/ShellHelpers.cs:25 rules.appsec-review.review-signal.sink.csharp-process-shell
    - src/ShellHelpers.cs:36 rules.appsec-review.review-signal.sink.csharp-process-shell
    - src/ShellHelpers.cs:42 rules.appsec-review.review-signal.sink.csharp-process-shell

## History
- git log --follow on src/Navigation.cs:
    - 78db56e 2026-04-17 Rename Redirects.cs to Navigation.cs
    - 765a2f8 2025-09-19 Add a navigation controller for outbound links
- fix commits (git log --grep CWE-):
    - 085171e480eeddd35c00628d97e467ceda65e53e Fix path traversal in ReadReport (CWE-22)
    - a13e7d0d20036b3e4d51dd003d785fb08c14a726 Fix command injection in RotateLogs (CWE-78)
- dependency upgrade commits (git log --grep -E 'CVE-|GHSA-|RUSTSEC-|GO-20'):
    - a14812a81c3dc2c91a8f80fa2f0564afde291161 Upgrade SharpZipLib from 1.3.2 to 1.3.3
- revert/reapply:
    - a30f504c1e89eb8f6bc06209faaeb34f2129efd1 Reapply "Append an X-Hits header with the hook counter to every ops reply"
    - c7215e4333ab53a276a3fe51d74eae35898b4f60 Revert "Append an X-Hits header with the hook counter to every ops reply"
- merges: 0
- commits touching more than three files:
    - a14812a Upgrade SharpZipLib from 1.3.2 to 1.3.3 (5 files)
    - f8c7563 Add SixLabors.ImageSharp.Drawing 1.0.0 for report charts (8 files)
    - 8018816 Add Newtonsoft.Json 12.0.1 from a vendored package feed (4 files)
    - ed08867 Initial commit (116 files)
- churn (commits per file, top 5):
    -      17 src/MaintenanceController.cs
    -       7 Smoke.csproj
    -       5 src/ShellHelpers.cs
    -       5 packages.lock.json
    -       5 CHANGELOG.md
- SECURITY.md and CHANGELOG.md present: yes

## Complexity (src/MaintenanceController.cs Dispatch via tool-tree-sitter and complexity.py)
    {"qualified_name": "Smoke.MaintenanceController.Dispatch", "start_line": 40, "end_line": 102, "cyclomatic": 25, "decisions": {"boolean": 8, "if": 11, "loop": 1, "ternary": 4}, "parse_error": false}
    units: [('Smoke.MaintenanceController.Dispatch', 25), ('Smoke.MaintenanceController.ReadReport', 2), ('Smoke.MaintenanceController.RotateLogs', 2)]

## Dates
- first: 2025-05-13  last: 2026-09-15
- authors: Ada Lindqvist <ada@example.com>;Bao Nguyen <bao@example.com>;Cleo Marsh <cleo@example.com>;
