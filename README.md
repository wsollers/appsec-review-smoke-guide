# appsec-review-smoke-guide

The evaluation answer key for the `appsec-review-smoke-<language>` repositories: nine minimal,
deliberately vulnerable targets (C/C++, Java, JavaScript, Python, Ruby, Go, C#, Rust, PHP) built so
that a review of each has one correct answer at topology, discovery, build, SBOM, scanning, code
intelligence, history and triage. A failure anywhere on a smoke target is a defect of the review
pipeline, not of the target. The smoke tier says nothing about recall or scale.

**This repository is evaluation-only.** Never clone it under an appsec-review checkout's `targets/`
directory or anywhere a review can see it, and never read it to steer a job while a walk is in
progress. Clone it to a sibling directory of the checkout:

```sh
git clone https://github.com/wsollers/appsec-review-smoke-guide.git ../appsec-review-smoke-guide
```

## Layout

```
<language>/
  answer-key.json      appsec-review/smoke-answer-key/1: repository, tagged commit, build, the
                       planted inventory with spans, SHAs, advisories and expected dispositions,
                       the high-complexity function, expected history signals, verification
                       results and expected gaps
  expected-facts.json  the code-graph fixture's expectations, copied verbatim from
                       appsec-review tests/fixtures/graph/codeql_export/<fixture>/ (PHP: hand-authored,
                       no CodeQL extractor exists)
  report.md            the Stage 3 verification report recorded when the target was tagged
docs/answer-key-schema.md   the record format
```

Each target's `PLANTED.md` describes the target; the files here are the key. Line numbers and
commit ids refer to the tag named in each `answer-key.json`.

## Dispositions

- `reported`: a live true positive (code path or dependency) the review must report.
- `reported-as-fixed`: an item present in an earlier commit and fixed at the tagged head; only
  history analysis can find it, and it must not be reported as live.
- `squelched`: a construct a pattern scanner flags that an exportable code-intelligence fact
  refutes (`guard_fact`, `path_sanitizers`, `range_fact`, or the absence of a `dataflow_path`); the
  review must not report it as a finding. Whether the pipeline squelches these is the measure the
  smoke tier exists for.

## Known limits

Every `answer-key.json` carries `expected_gaps` and `substitutions`. The recurring ones:

- Vendored C libraries (cpp) have no package-manager manifest and no OSV ecosystem records, so Syft,
  Grype and OSV-Scanner list nothing for them; the detection path is cve-bin-tool version strings.
- There is no Ruby build profile or image in appsec-review, so the Ruby target has no offline-build
  proof (appsec-review `docs/TODO.md` T-139).
- There are no Semgrep rules for Ruby or Rust under appsec-review `rules/`, so their planted false
  positives are recorded as unflagged by the mounted rules.
- PHP plants `guzzlehttp/guzzle` 7.4.0 instead of the originally planned `monolog/monolog` 1.23.0,
  which has no OSV record.

## Provenance

Built on 2026-11-13 from appsec-review's `docs/tasks/2026-11-13-smoke-targets-prompt.md`
(T-134 to T-145). Each target's history is reproducible from its own `tools/make-history.sh`.
