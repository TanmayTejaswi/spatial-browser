# Task 19 — Full Project Audit, Quality Fixes, and GitHub Synchronization

**Status:** Assigned — do not begin human-participant recruitment or a study session as part of this task.

**Report due:** [`../task-19-output.md`](../task-19-output.md)

## Objective

Perform a thorough, evidence-based audit of the complete Spatial Browser History project. Find and fix reproducible defects, check the extension packages and study-readiness materials, and leave the intended project source and documentation synchronized with the configured GitHub repository. “Flawless” means no known actionable defects remain in the audited scope and all required checks pass; it does not mean unverified browser versions or external approvals can be claimed as complete.

## Important starting state and preservation rules

At assignment time, the repository is on `main` at commit `0402790`, which is synchronized with `origin/main`. The working tree is **not clean**. It contains uncommitted Task 18 follow-up edits to project code, documentation, test evidence, and study fixtures, plus a local `Materials for user study/` directory containing user-supplied PDFs. These changes must be inspected and preserved; do not assume they are disposable or overwrite them.

1. Before editing, record the current branch, commit, remote tracking state, and complete tracked/untracked change inventory. Review each existing diff and untracked file and classify it as intentional project work, generated evidence, user material, or unrelated.
2. Do not use destructive cleanup or broad staging. In particular, do not run `git reset --hard`, `git clean`, path-wide restore/checkout, force-push, or commands that discard/rewrite the pre-existing work.
3. Do not edit the user-supplied PDFs. Do not commit or push `Materials for user study/` unless distribution rights for every included document are explicitly established. Keep the local materials available to the project owner and retain the project’s materials crosswalk.
4. Do not stage with `git add -A` or otherwise include unreviewed files. Stage only reviewed project source, documentation, tests, and appropriate non-sensitive evidence.
5. Do not recruit participants, run a human pilot, access anyone’s personal browsing data, create a release/tag, or publish extension binaries as part of this assignment.

If the current branch/remote has changed since this assignment was written, report the actual state and proceed without overwriting remote or local work. If safe synchronization is blocked by divergence, branch protection, unavailable credentials, or an unexpected conflict, preserve all changes and report the exact blocker and safest next action.

## Audit scope

### 1. Repository and documentation integrity

- Inspect the full repository tree, `.gitignore`, package scripts, task reports/indexes, release notes, and current uncommitted changes.
- Check Markdown links and local file references in the project documentation. Fix broken references, stale instructions, conflicting version/status claims, incorrect test totals, or duplicated/confusing task state.
- Review the study materials crosswalk against the locally supplied materials without modifying the source PDFs. Keep any claims about course deadlines or approval requirements qualified and consistent with the source documents.
- Ensure all reports clearly distinguish automated checks, live browser checks, unverified compatibility, and human-study approval. Do not claim efficacy or ethics approval.

### 2. Extension source, build, and privacy review

Review the source and generated Chrome/Firefox packages for:

- Manifest versions, permissions, service-worker/background setup, CSP, packaging completeness, and Chrome/Firefox source parity.
- Navigation tracking and graph relationships, including tab/opener lineage, same-tab branches, SPA/history events, redirects, reload/hash exclusions, title updates, and download provenance.
- Storage serialization, schema handling, pruning, recovery, and cross-tab concurrency behavior.
- Map overview/detail navigation, visible branching, keyboard use, focus behavior, narrow layouts, and empty/error states.
- Study mode default-off behavior, active-trial boundaries, corpus allowlisting, target detection, event/error classification, NASA-TLX scoring, export contents, reset behavior, and deletion.
- Privacy/security boundaries: no remote telemetry or upload, no accidental collection outside an active study trial, no raw URLs/titles/search text or unrelated browsing data in study exports, and no exposed secrets or credentials in tracked files, logs, or packages.

Fix concrete defects found in scope. Keep the minimum browser versions, permissions, release tag, normal history schema, and established privacy contract unchanged unless a specific defect makes a change necessary; explain any necessary compatibility or data-contract change prominently in the report. Do not introduce dependencies or unrelated product features.

### 3. Verification

Inspect the browser automation script and confirm it uses isolated test profiles and synthetic fixtures before running it. Then run and record fresh results for:

1. `npm.cmd run build`
2. `npm.cmd test`
3. `py scripts/e2e-task18-runtime.py` for current Chrome and Firefox, if both are available
4. Markdown/local-reference checks and any existing repository validation scripts

Inspect the generated packages, checksums, test logs, screenshots, and browser error audits. Verify the built outputs contain the expected current source and manifests. Do not rely on previously recorded logs as proof of a fresh passing run. If a check creates or updates files, inspect its diff and keep only intentional, reproducible evidence.

Record exact browser names and versions. The project’s branded Chrome 109 support-floor check has previously remained unverified; do not convert current-browser success or Chromium proxy results into a Chrome 109 claim. If a browser or check is unavailable, state that plainly and leave its acceptance status open.

### 4. GitHub and CI synchronization

- Fetch and inspect the configured `origin`; confirm the repository URL, current branch, upstream, latest remote commit, and ahead/behind state. Do not assume a clean local status means the remote is current.
- After the audit passes, commit the reviewed, intended project changes with a clear message and push to the appropriate existing branch on `origin`, following repository branch protection. Do not force-push or rewrite shared history. Do not push course PDFs or unrelated local files.
- Confirm the pushed commit is visible on the remote and check the associated GitHub Actions CI run to completion. If the workflow fails, fix the underlying issue and push a corrected commit, then verify the new run. If remote access is unavailable, report that synchronization was not completed; do not state that GitHub is up to date.
- Do not create a release, tag, or public binary release.

## Required report

Submit [`../task-19-output.md`](../task-19-output.md) with:

- Starting and final branch/commit/remote state; a concise classification of the pre-existing changes; and an explicit statement that all owner work and the local PDFs were preserved.
- Findings by severity, each with affected file/area, evidence, correction made, and any remaining limitation. If no defect is found in an area, say what was inspected and how.
- Build, automated test, browser E2E, documentation-link, checksum/package, and CI results, including exact counts, browser versions, and links/paths to fresh logs/screenshots.
- A privacy and packaging summary, including confirmation that no course PDFs or unrelated personal data were pushed.
- The exact commit SHA and GitHub URL, push status, and CI run URL/conclusion. If any step could not be completed, identify the blocker without presenting it as a pass.
- Any remaining open issue and the concrete next action. Do not mark this task accepted; wait for lead review.

## Acceptance criteria

- All pre-existing owner changes have been reviewed and preserved; no unreviewed or restricted materials are staged or pushed.
- All in-scope reproducible defects found during the audit are fixed, with corresponding regression coverage where appropriate.
- Fresh build and automated tests pass; current-browser E2E checks pass where available, with evidence inspected and retained.
- Chrome and Firefox packages are generated from the audited source and their manifests, parity, and checksums are verified.
- Documentation and task indexes accurately reflect current status, and local references are valid.
- Reviewed intended project changes are pushed to the correct GitHub branch without rewriting history; the remote commit and hosted CI result are verified, or the exact blocker is reported.
- No participant study, release, tag, or binary publication occurs under this task.
- The developer submits the required output report and waits for lead review before starting another task.
