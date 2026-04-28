# @coms-portal/ui

COMS UI components for the AHA Commerce suite — primitives, chrome shells, and generic compositions. Consumed by the portal and every H-app.

> **Status:** skeleton. Components will migrate from `coms_aha_heroes/packages/web` into this package across Phases 3–4 of Rev 3 Spec 02.

## Distribution model

Matches `@coms-portal/shared`: standalone GitHub repo, semver-tagged, consumed via `git+https://github.com/mrdoorba/coms-ui.git#vX.Y.Z`.

## Layout

```
src/
  primitives/    — Button, Card, Input, StatusBadge, Avatar, Tabs, Dialog
  chrome/        — ServiceBar, Sidebar, MobileTopBar, MobileBottomNav
  compositions/  — HeroGreeting, SummaryCard, NotificationPanel, MobileFab
```

## Usage

```svelte
<script lang="ts">
  import { Button, Card } from '@coms-portal/ui/primitives'
  import { ServiceBar, Sidebar } from '@coms-portal/ui/chrome'
  import { HeroGreeting, SummaryCard } from '@coms-portal/ui/compositions'
</script>
```

## Contribution

If you need a new component or variant, **open a PR here** rather than building it inline in your app. Variants land upstream so the suite stays consistent. See `ONBOARDING.md` §Step 7.

## Reference

See `DESIGN.md` for the canonical visual reference and component prop expectations.
