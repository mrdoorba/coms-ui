# @coms-portal/ui

COMS UI components for the AHA Commerce suite. Consumed by the portal and every H-app.

> **Status:** v1.0.0 ships the chrome shells (`ServiceBar`, `Sidebar`, `MobileTopBar`, `MobileBottomNav`). Primitives and compositions are reserved for future phases (Phase 4 of Rev 3 Spec 02).

## Install

Production (after the repo is pushed to GitHub with a v1.0.0 tag):

```sh
bun add git+https://github.com/mrdoorba/coms-ui.git#v1.0.0
```

Local development (during initial portal dogfooding before the package is pushed):

```jsonc
// apps/web/package.json
"dependencies": {
  "@coms-portal/ui": "file:../../../coms-ui"
}
```

Swap the `file:` line for the `git+url` form once the package is pushed.

## Layout

```
src/
  primitives/    — (reserved for Phase 4 — empty index.ts today)
  chrome/        — ServiceBar, Sidebar, MobileTopBar, MobileBottomNav
  compositions/  — (reserved for Phase 4 — empty index.ts today)
```

## Use

The chrome shells are presentational and host-agnostic. Each consuming app passes data + state via props and mounts host-specific widgets (notably the account widget) into the right-slot snippets.

### Minimal portal example

```svelte
<script lang="ts">
  import { ServiceBar, Sidebar, MobileTopBar, MobileBottomNav } from '@coms-portal/ui/chrome'
  import { LayoutDashboard, Users } from 'lucide-svelte'
  import { page } from '$app/stores'

  const navSections = [
    { items: [{ href: '/', label: 'Dashboard', icon: LayoutDashboard }] },
    { label: 'Admin', items: [{ href: '/admin/employees', label: 'Employees', icon: Users }] },
  ]

  const services = [
    { slug: 'portal', label: 'COMS' },
    { slug: 'heroes', label: 'Heroes', formAction: '/api/auth/broker/launch/heroes' },
  ]

  let theme = $state<'light' | 'dark'>('dark')
  let collapsed = $state(true)

  function toggleTheme() {
    theme = theme === 'dark' ? 'light' : 'dark'
    document.documentElement.classList.toggle('dark', theme === 'dark')
  }
</script>

<ServiceBar {services} currentApp="portal" {theme} onToggleTheme={toggleTheme}>
  {#snippet right()}
    <!-- mount <AccountWidget> here -->
  {/snippet}
</ServiceBar>

<Sidebar
  sections={navSections}
  currentPath={$page.url.pathname}
  {collapsed}
  onCollapsedChange={(v) => (collapsed = v)}
>
  {#snippet logo({ collapsed })}
    <span class="font-extrabold">{collapsed ? 'C' : 'COMS'}</span>
  {/snippet}
</Sidebar>
```

### Right-slot contract

`ServiceBar` and `MobileTopBar` accept an optional `right` snippet prop. The host renders whatever should appear at the far right — typically `<AccountWidget>`. The chrome itself does not own avatar / sign-out / app-launcher UI; that is widget territory.

### Theme toggle

The chrome ships a presentational theme toggle (sun/moon glyph). The host owns the `theme` state and passes a `theme` value plus an `onToggleTheme` handler. The chrome never reads `localStorage` or DOM classes on its own.

### Tailwind tokens

Chrome components use Tailwind utility classes that resolve through `@coms-portal/design-tokens`. The consuming app must `@import "@coms-portal/design-tokens/css"` in its Tailwind v4 entry point so utilities like `bg-card`, `text-foreground`, `bg-deep-navy`, etc. resolve correctly.

## Development

```sh
bun install
bun run typecheck     # svelte-check across src/
```

## Component reference

See `DESIGN.md` for the canonical visual specification. The components in `src/chrome/` implement the visual shapes documented there, with host-supplied data filling the slots.
