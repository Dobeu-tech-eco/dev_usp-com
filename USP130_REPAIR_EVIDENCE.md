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

Independent lockfile review: 1,189 package entries removed, none added. Retained package versions, integrity hashes, resolved URLs and dependency relationships are unchanged; only dev/devOptional classification changes remain.

The tracked .netlify/plugins/package-lock.json remains a separate scanner source and is unchanged by this repair. The historical Trivy check annotates yaml@2.8.2 there with CVE-2026-33532 (medium; fixed in 2.8.3 or 1.10.3). This plugin lockfile differs between base and original PR, so its findings are separate from the root baseline comparison. No existing Trivy binary was found; no tooling was installed. Historical Trivy alerts do not establish repaired scan results. Browser and hosted verification of the repair remain outstanding.

Publication scope: repair branch and draft PR against the original PR branch only; no merge or deployment authorized. Production workflow triggers only on main pushes or explicit dispatch; neither is part of this repair. Local logs are not included in the repository.
