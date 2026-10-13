## Change delivered

Describe what changed and which user-visible feature it affects.

**Exact HEAD SHA:** `<40-character SHA>`

## Fast Live Visibility

- [ ] Focused change; other agent/Claude uncommitted work preserved
- [ ] Affected checks run; required full exact-head CI confirmed before merge
- [ ] Preview URL, screenshot or verified build artifact shared where supported (or `NOT AVAILABLE` explained)
- [ ] Production safety and rollback assessed; no secrets/customer data leaked
- [ ] Zero unexpected paid dependencies/services
- [ ] Report exact deployment stage: `PR | CI | PREVIEW | STAGING | PRODUCTION`

**Preview/artifact URL:** `NOT AVAILABLE / <link>`

**Production:** `NOT DEPLOYED` (change this only after actual live smoke checks with exact SHA)

**Blocker / next action:**

Use the [KMJ Fast Live Visibility policy](https://github.com/kmjtechno/.github/blob/main/docs/FAST-LIVE-VISIBILITY.md). Repository-specific gates take precedence. A green PR does not automatically mean production live.
