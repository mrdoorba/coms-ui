# COMS Design System — Changelog

Version history for the design system reference (this directory) and the published packages (`@coms-portal/design-tokens`, `@coms-portal/ui`, `@coms-portal/account-widget`).

Format: each entry lists the doc revision and any package version that ships alongside it. Breaking changes (major bumps) include a migration section.

---

## Unreleased

### Docs
- Initial extraction from `coms_aha_heroes/my-design-guideline/DESIGN.md` into `coms_portal/docs/design-system/` as the canonical source.
- Added `ONBOARDING.md` (integration playbook) and `CHANGELOG.md` (this file).
- Frontmatter `version: alpha` → `version: 1.0`. Frontmatter is now declared the single source of truth for token values.
- Component sections rewritten to reference `@coms-portal/ui` components instead of describing implementation details.

### Packages
- `@coms-portal/design-tokens@0.0.0` — package skeleton; not yet published.
- `@coms-portal/ui@0.0.0` — package skeleton; not yet published.
- `@coms-portal/account-widget@0.0.0` — package skeleton; defined in Rev 3 Spec 01.

### Migration notes
- Heroes' `my-design-guideline/DESIGN.md` is reduced to a redirect note. Any references to that path in Heroes' codebase should be updated to point at `coms_portal/docs/design-system/DESIGN.md`.

---

## Versioning policy

- **0.x.y** — pre-1.0 development. Breaking changes allowed in minor bumps, documented here.
- **1.0.0** — first stable release. Cuts when both portal and Heroes consume the package and have run in production for 7+ days.
- **Post-1.0 majors** — breaking changes require a major bump, a migration section in this changelog, and explicit upgrade PRs in each consumer.
- **Minors** — additive changes (new components, new variants, new tokens that don't override existing ones).
- **Patches** — bug fixes, visual tweaks within the same intent (e.g. shadow rgba adjustment), no API changes.

Consumers pin by tag (`git+...#vX.Y.Z`). No automatic updates.
