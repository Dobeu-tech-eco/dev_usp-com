# PR 130 local repair

Starting head: bd9ac1be800acd0b63ffd8e66090e504b6bbc319. Base: d14005c.

Removed unused runtime netlify-cli and regenerated npm lock using legacy peer resolution required by AGENTS.md. No application import, package script, or CI workflow invokes this installed CLI. Deployment instructions explicitly use npx or a global CLI; those commands remain available. No deployment executed. No .agents directory exists.

Fresh npm audit comparison (2026-11-13):
- Base: 0 critical, 21 high, 11 moderate, 1 low.
- Original PR: 6 critical, 47 high, 30 moderate, 3 low.
- Repair: 0 critical, 21 high, 11 moderate, 1 low.
Base and repaired vulnerability records are identical. Thus removal eliminates the npm advisory regression; remaining findings predate this PR. npm audit exits 1 for remaining vulnerabilities. Trivy was not rerun locally; npm audit is not Trivy proof.

Verification: npm ci --legacy-peer-deps initially failed on a pre-existing incomplete Puppeteer shared browser cache (headless-shell executable missing). Retry with PUPPETEER_SKIP_DOWNLOAD=true succeeded. npm test passed 3/3; npm run build passed with CSS and bundle-size warnings; npm run lint passed with 22 warnings and zero errors; git diff --check passed. No new test needed for a dependency-only removal. Base install/build/lint were not executed; base comparison is limited to audit records.

Read-only GitHub check inspection: application build passes. Datadog API rejects pipeline tagging with Forbidden; credential/site/account authorization needs owner investigation, and no secret validity is established. Claude initializes then returns is_error:true after one turn, zero model usage and zero cost; public output hides the cause. Owner must inspect protected execution diagnostics and service configuration. No secrets, permissions, billing, thresholds, or workflows changed.

Detailed local logs and audit JSON: /tmp/usp130-evidence (temporary, outside Git). No push, merge, deployment, external messages, or production action performed. Owner should review local diff, resolve pre-existing vulnerabilities separately, and authorize normal PR CI reruns after publication.
