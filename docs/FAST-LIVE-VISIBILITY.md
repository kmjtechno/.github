# KMJ TECHNO — Fast Live Visibility (organization-wide default)

**Owner policy — 2026-10-14:** Every authorized change should become **visible and verifiable as soon as safely possible**, with free or already-approved infrastructure and minimal additional dependencies.

This is the common default for `kmjtechno` projects, including Main Platform, CodeBridge, CineCore, OmniDesk, CloudOS, Calibration Pro, MotionDirector and future products. Repository-specific release, security, hardware-safety and customer-data protections **take precedence**. This document is a policy/acceptance contract, not a deployed cross-repository CI service. Do not claim the rule was automatically enforced on repositories that have independent templates/workflows.

## 1. Definitions (never conflate these states)

- **CODE AVAILABLE:** The exact commit and diff are pushed to the authorized GitHub PR/branch. State the PR URL and full commit SHA.
- **PREVIEW LIVE:** A real, linked, running preview or reviewable build is accessible and verified. A pending CI job, screenshot, design mock or draft PR does **not** count.
- **STAGING LIVE:** The exact candidate is deployed on a non-production environment, with smoke checks, isolated secrets and rollback. Record environment, SHA and evidence.
- **PRODUCTION LIVE:** The exact verified artifact is deployed to the live customer destination, smoke/health checks pass, and rollback is ready. Record public URL or approved device version, SHA, evidence and deployment time.
- **BLOCKED/NOT DEPLOYED:** No false `LIVE` status when validation, release capacity, GitHub Actions minutes, owner approval, network, secrets, hardware or infrastructure is unavailable.

## 2. Fast path for every engineering lane

1. Create an isolated branch/worktree. Preserve local/Claude/other-agent modifications and production data.
2. Push a focused PR promptly with its exact SHA. For every change affecting UI/UX, include a reviewable screenshot or preview artifact (no secrets, tokens, customer data) if the toolchain can generate it.
3. Run **affected, low-cost checks first** (format, lint, relevant unit tests); avoid rerunning entire CI unnecessarily. The required complete release gate still applies before merge/deploy.
4. Make preview links or downloadable test artifacts available from existing authorized infrastructure, preferably on each PR update. Publish a truthful status: `COMMIT → CI → PREVIEW → STAGING → PRODUCTION`. When external preview hosting is unavailable, show the verified build artifact and explain the limitation.
5. After the **exact PR head** has passed required tests and security review, merge only if protections allow it. Never bypass branch protection, force-push across another agent's work, or mark failed/running checks as green.
6. For public web/UI changes, deploy an immutable release to existing staging automatically **only when the repository already has a secure approved pipeline**; smoke-test, then perform the permitted, guarded production promotion with rollback. No automatic deployment of arbitrary PR code or untrusted third-party contributions to production.
7. Invalidate only affected application/CDN caches and use fingerprinted assets. Verify the served build/version and browser-visible state with real HTTP and functional UI checks at desktop and mobile sizes.
8. For desktop/OS, provide signed, verified release artifacts and safe update/rollback notices. Do not call a merged source commit a live binary installation.
9. Report concise evidence and the exact blocker immediately when progression stops. Work on independent ready tasks while blocked instead of waiting idly.

## 3. Targets (service goals, **not** guarantees)

- **Commit/PR visibility:** as soon as an authorized change is pushed.
- **Preview / CI feedback:** target *minutes* using affected checks and existing free infrastructure. Track actual median and p95 feedback latency; do not invent measured times.
- **Web production:** immediately after required exact-artifact checks, release authorization and a verified deploy window; no bypass for migrations, sensitive permissions, billing, licensing or data integrity.
- **Device updates:** after a signed release is available and each owner/device has approved the update channel; validate rollback/heartbeat.

## 4. Must never happen

- No direct production deployment from an unverified feature branch or PR.
- No unapproved schema migrations, payment/licensing changes, DNS cutovers, destructive operations or security-sensitive access changes.
- No exposure of repository credentials, API keys, provider secrets or customer data in previews, logs, artifacts or notifications.
- No artificial `PASS`, `LIVE` or percentage claims. Each status refers to an actual environment and exact SHA.
- No unexpected paid CI/hosting/provider API usage. Respect GitHub rate limits and usage quotas; if free capacity is exhausted, report `BLOCKED`.
- No tight CI loops, unbounded auto-retries or reliance on an always-on ChatGPT conversation.

## 5. Smallest useful delivery automation per repository

Implement only what is missing, in this order:

1. **Immediate status:** commit SHA + PR checks + changed-file/build artifact link; post a truthful status through existing GitHub/CodeBridge interfaces.
2. **Preview:** approved, ephemeral preview or artifact for safe UI changes on existing infrastructure, with secrets withheld and cleanup.
3. **Promotion:** existing gated deployment of immutable SHA to staging, smoke health, permitted production promotion, rollback.
4. **Live dashboard:** read-only service-reported deployment version, preview/prod URL and last verified state (not manually hardcoded green badges).
5. **Observability:** measure commit-to-preview, merge-to-production and rollback time, identifying slow gates before optimizing.

For Laravel Main Platform, honor `RELEASE_GATE.md` and existing production configuration. For CodeBridge, verify enrolled agent version, signed runtime, supervisor/agent health and reconnect. For CineCore/Calibration/Motion, require real hardware/safety evidence before release. For CloudOS, protect multi-tenant infrastructure and privileged changes.

## 6. Short mandatory status line

`PR | SHA | CHECKS PASS/FAIL/PENDING | PREVIEW URL or NOT AVAILABLE | STAGING | PRODUCTION | BLOCKER`

**Important:** A rule in `kmjtechno/.github` is a shared default **guideline/template**, not automatic account-wide deployment or branch protection. Repository owners must wire safe CI/CD individually. Rulesets, production approvals and credentials are separate controls and must be checked per repo.

[GitHub's default community health files](https://docs.github.com/en/communities/setting-up-your-project-for-healthy-contributions/creating-a-default-community-health-file) explain how shared contribution and PR templates are inherited.
