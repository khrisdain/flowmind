# UI Context

## Theme

Supports **dark mode** (default) and **light mode**. The visual language is a technical workspace — layered surfaces, vivid accent colors, and clean typography that works in both modes.

Theme is toggled via a Sun/Moon button in the editor navbar (`components/theme-toggle.tsx`). The active theme is stored in `localStorage` under the key `theme`. On page load, an inline script in `app/layout.tsx` applies the `.dark` class to `<html>` before React hydrates, preventing flash.

**Implementation files:**
- `lib/theme-provider.tsx` — context, toggle logic, localStorage persistence
- `components/theme-toggle.tsx` — Sun/Moon button using `useTheme()`
- `app/globals.css` — `:root` = light values, `.dark` = dark values
- `@custom-variant dark (&:is(.dark *))` enables `dark:` Tailwind prefix

All colors are defined as CSS custom properties in `globals.css` and mapped to Tailwind tokens via `@theme inline`. Components must use these tokens — no hardcoded hex values or raw Tailwind color classes like `zinc-*`.

### Light Mode Values (`:root`)

| Role             | CSS Variable           | Hex / Value               |
| ---------------- | ---------------------- | ------------------------- |
| Page background  | `--bg-base`            | `#ffffff`                 |
| Surface          | `--bg-surface`         | `#f5f5f7`                 |
| Elevated surface | `--bg-elevated`        | `#ebebef`                 |
| Subtle surface   | `--bg-subtle`          | `#e2e2e8`                 |
| Default border   | `--border-default`     | `#d0d0d8`                 |
| Subtle border    | `--border-subtle`      | `#c0c0cc`                 |
| Primary text     | `--text-primary`       | `#0a0a0f`                 |
| Secondary text   | `--text-secondary`     | `#3a3a50`                 |
| Muted text       | `--text-muted`         | `#606075`                 |
| Faint text       | `--text-faint`         | `#909099`                 |
| Brand accent     | `--accent-primary`     | `#00c8d4` (cyan)          |
| Brand dim        | `--accent-primary-dim` | `rgba(0, 200, 212, 0.12)` |
| AI accent        | `--accent-ai`          | `#6457f9` (indigo-purple) |
| AI text          | `--accent-ai-text`     | `#4a3ee8`                 |
| Error            | `--state-error`        | `#dc2626`                 |
| Success          | `--state-success`      | `#16a34a`                 |
| Warning          | `--state-warning`      | `#d97706`                 |

### Dark Mode Values (`.dark`)

| Role             | CSS Variable           | Hex / Value               |
| ---------------- | ---------------------- | ------------------------- |
| Page background  | `--bg-base`            | `#080809`                 |
| Surface          | `--bg-surface`         | `#111114`                 |
| Elevated surface | `--bg-elevated`        | `#18181c`                 |
| Subtle surface   | `--bg-subtle`          | `#1e1e23`                 |
| Default border   | `--border-default`     | `#2a2a30`                 |
| Subtle border    | `--border-subtle`      | `#3a3a42`                 |
| Primary text     | `--text-primary`       | `#f0f0f4`                 |
| Secondary text   | `--text-secondary`     | `#c0c0cc`                 |
| Muted text       | `--text-muted`         | `#808090`                 |
| Faint text       | `--text-faint`         | `#505060`                 |
| Brand accent     | `--accent-primary`     | `#00c8d4` (cyan)          |
| Brand dim        | `--accent-primary-dim` | `rgba(0, 200, 212, 0.12)` |
| AI accent        | `--accent-ai`          | `#6457f9` (indigo-purple) |
| AI text          | `--accent-ai-text`     | `#8b82ff`                 |
| Error            | `--state-error`        | `#ff4d4f`                 |
| Success          | `--state-success`      | `#34d399`                 |
| Warning          | `--state-warning`      | `#fbbf24`                 |

Tailwind utility names map to these variables. Use `bg-bg-base`, `bg-bg-surface`, `text-text-primary`, `text-text-muted`, `border-border-default`, `text-accent-primary`, `bg-accent-primary-dim`, etc.

## Typography

| Role      | Font       | CSS Variable        |
| --------- | ---------- | ------------------- |
| UI text   | Geist Sans | `--font-geist-sans` |
| Code/mono | Geist Mono | `--font-geist-mono` |

Both fonts are loaded via `next/font/google` and applied as CSS variables on the `<html>` element. The base `body` uses Geist Sans with `antialiased`.

## Border Radius

Radius increases with surface depth — smaller for inner elements, larger for outer containers.

| Context           | Class         |
| ----------------- | ------------- |
| Inline / small UI | `rounded-xl`  |
| Cards / panels    | `rounded-2xl` |
| Modal / overlay   | `rounded-3xl` |

## Canvas

### Node Color Palette

8 defined color pairs. Defined in `types/canvas.ts` as `NODE_COLORS`. These are dark-mode colors stored as hex in Liveblocks canvas state. Canvas node colors are baked into the canvas data and do not switch with the UI theme.

#### Dark mode node colors (stored in canvas, used by AI agent)

| Node fill | Text color | Character              |
| --------- | ---------- | ---------------------- |
| `#1F1F1F` | `#EDEDED`  | Neutral dark (default) |
| `#10233D` | `#52A8FF`  | Blue                   |
| `#2E1938` | `#BF7AF0`  | Purple                 |
| `#331B00` | `#FF990A`  | Orange                 |
| `#3C1618` | `#FF6166`  | Red                    |
| `#3A1726` | `#F75F8F`  | Pink                   |
| `#0F2E18` | `#62C073`  | Green                  |
| `#062822` | `#0AC7B4`  | Teal                   |

#### Light mode node colors (reference — `NODE_COLORS_LIGHT`)

| Node fill | Text color | Character |
| --------- | ---------- | --------- |
| `#f0f0f4` | `#1a1a2e`  | Neutral   |
| `#dceeff` | `#1a5fa8`  | Blue      |
| `#eeddf8` | `#7b3aad`  | Purple    |
| `#fff0d9` | `#c46800`  | Orange    |
| `#fde2e3` | `#c0262a`  | Red       |
| `#fde0eb` | `#c4305a`  | Pink      |
| `#d8f5e0` | `#1e7a35`  | Green     |
| `#d0f5f2` | `#097a70`  | Teal      |

Default node color: `#1F1F1F` with `#EDEDED` text.

### Edge Style

Smooth-step path with a closed arrow marker. Edge colors are theme-aware via CSS variables — black in light mode, white in dark mode. Stroke width is thin (1.5px) — edges are visually secondary to nodes.

| State        | CSS Variable    | Light value          | Dark value              |
| ------------ | --------------- | -------------------- | ----------------------- |
| Rest         | `--edge-rest`   | `rgba(0,0,0,0.45)`   | `rgba(255,255,255,0.35)` |
| Active/hover | `--edge-active` | `rgba(0,0,0,0.8)`    | `rgba(255,255,255,0.7)`  |
| Arrow marker | `--edge-arrow`  | `rgba(0,0,0,0.5)`    | `rgba(255,255,255,0.4)`  |
| Label border | `--edge-label-border` | `rgba(0,0,0,0.15)` | `rgba(255,255,255,0.15)` |
| Hint text    | `--edge-hint`   | `rgba(0,0,0,0.3)`    | `rgba(255,255,255,0.3)`  |

Never hardcode `rgba(255,255,255,...)` for edge colors — always use the CSS variables above.

### Node Shapes

6 supported shapes, defined in `types/canvas.ts` as `NODE_SHAPES`. Complex shapes (diamond, hexagon, cylinder) are rendered as inline SVGs rather than CSS borders.

- `rectangle` — default general-purpose node
- `diamond` — decision / gateway
- `circle` — event / endpoint
- `pill` — service / process
- `cylinder` — database / storage
- `hexagon` — external system / boundary

### Connection Handles

Small white circular handles, hidden by default, revealed on node hover. Appear at all four sides of a node.

### Canvas Background

React Flow `<Background>` component. Canvas sits on the base background color.

## Component Library

shadcn/ui on top of Tailwind. No custom design system. Components live in `components/ui/`. Use the `shadcn` CLI to add new components rather than writing them from scratch.

## Layout Patterns

- Editor workspace: full-viewport layout — floating sidebar overlay on the left, center canvas, slide-over AI sidebar on the right.
- Sidebars: floating overlay with semi-transparent background and subtle border.
- Modals and dialogs: centered overlay, `rounded-3xl`, background with backdrop blur.
- Navbar: top bar with bottom border. Contains the ThemeToggle on the right side.

## Icons

Lucide React. Stroke-based icons only — no filled variants. Icon sizes: `h-4 w-4` for inline, `h-5 w-5` for buttons, `h-8 w-8` for feature icons in empty states.
