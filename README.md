# Meta_Dashboard_UI_Desgin


# ISSL Meta-Inspired Enterprise UI Design System

> Reusable UI foundation for ISSL CRM, Attendance Management, ERP and future enterprise dashboards.

## 1. Design Principles

- Meta Business Suite inspired: clean, compact, organized and information-dense.
- Flat interface; avoid glassmorphism, heavy gradients, large shadows and decorative effects.
- Use low padding, small gaps and clear visual hierarchy.
- Every repeated pattern must be a reusable component.
- Desktop-first enterprise experience with full tablet and mobile support.
- SSR-first architecture; client components only where interaction requires them.
- Animations must be subtle, fast and functional.
- Do not use purple or indigo as primary interface colors.

## 2. Color Tokens

| Token | Value | Usage |
|---|---:|---|
| `brand-primary` | `#0462D2` | Brand accents, links, selected states |
| `action-primary` | `#0A78BE` | Primary buttons and important actions |
| `action-hover` | `#086AA8` | Primary action hover |
| `tab-active-bg` | `#E1EDF7` | Active tab background |
| `tab-active-text` | `#0A78BE` | Active tab text/icon |
| `text-primary` | `#1C2B33` | Main text |
| `text-secondary` | `rgba(28, 43, 51, 0.65)` | Subtitle and supporting text |
| `text-muted` | `#667781` | Metadata and placeholders |
| `text-inverse` | `#FFFFFF` | Text on dark/primary backgrounds |
| `sidebar-active` | `#2F414A` | Active sidebar item |
| `surface-primary` | `#FFFFFF` | Cards, tables, sidebar and modal |
| `surface-secondary` | `#F1F4F7` | Hover and muted surfaces |
| `border-default` | `#CBD2D9` | Inputs and structural dividers |
| `divider` | `rgba(28, 43, 51, 0.15)` | Soft separators |
| `success` | `#168A45` | Success state |
| `warning` | `#E89A00` | Warning state |
| `danger` | `#C91C2B` | Error and destructive action |
| `info` | `#0A78BE` | Informational state |

### Workspace Background

```css
background:
  radial-gradient(
    103.89% 81.75% at 95.41% 106.34%,
    #eaf8ef 6%,
    #eaf8ef00 79.68%
  ),
  radial-gradient(
    297.85% 151.83% at -21.39% 8.81%,
    #faf1f1 0% 15.29%,
    #f3edf5 21.39%,
    #e5f0fa 40.79%
  );
```

Use this gradient only on the main workspace. Cards, tables, drawers, modals and navigation surfaces remain solid.

## 3. Typography

| Element | Font | Size | Weight | Line height |
|---|---|---:|---:|---:|
| Page heading | Optimistic 95 | 20px | 600–700 | 1.3 |
| Section heading | Optimistic 95 | 16px | 600 | 1.4 |
| Tab | Optimistic 95 | 14px | 400–600 | 1.42858 |
| Subtitle | Optimistic 95 | 14px | 400 | 1.42858 |
| Body | Helvetica | 13px | 400 | 1.45 |
| Sidebar menu | Helvetica | 12px | 400–500 | 1.4 |
| Button | Helvetica | 12px | 400–600 | 1 |
| Table header | Helvetica | 12px | 600 | 1.4 |
| Table body | Helvetica | 12px | 400 | 1.4 |
| Caption | Helvetica | 11px | 400 | 1.4 |

If Optimistic 95 is not legally available for self-hosting, use:

```css
font-family: Inter, Helvetica, Arial, sans-serif;
```

## 4. Spacing and Sizing

Use a `4px` base unit.

| Token | Value | Usage |
|---|---:|---|
| `space-0.5` | 2px | Micro separation |
| `space-1` | 4px | Icon/text gap |
| `space-2` | 8px | Control padding and menu padding |
| `space-3` | 12px | Compact section gap |
| `space-4` | 16px | Card and section padding |
| `space-5` | 20px | Desktop page gutter |
| `space-6` | 24px | Maximum major section gap |

Avoid unnecessary large padding, gaps and empty areas.

## 5. Radius, Border and Shadow

- Default radius: `4px`
- Input/button/card radius: `4px`
- Modal/drawer radius: `4px–6px`
- Badge/avatar radius: `999px`
- Default shadow: none
- Floating element shadow only when necessary: `0 2px 8px rgba(0, 0, 0, 0.10)`
- Avoid high-contrast borders around every container.
- Use borders and dividers only to clarify structure.

## 6. Application Shell

### Sidebar

- Expanded width: `224px`; maximum `256px`.
- Collapsed width: `56px`.
- Background: white.
- Menu row height: `36px`.
- Menu padding: `8px`.
- Active item: `#2F414A` background with white text/icon.
- Hover item: `#F1F4F7`.
- Submenu indentation: `28px`.
- Settings, Help and User controls remain at the bottom.
- Tablet/mobile uses an overlay drawer.
- Navigation must be generated from one configuration source and filtered by permission.

### Topbar

- Recommended height: `52px`; maximum `55px`.
- Sticky position.
- White or transparent surface with a subtle bottom divider.
- Left: breadcrumb and page title.
- Right: search, notifications, quick-create and profile menu.
- Avoid heavy shadow.

### Content Area

- Use all remaining width after the sidebar.
- Dashboard content max-width: `1180px–1280px`.
- Data-heavy pages and tables use the full available width.
- Desktop gutter: `16px–20px`.
- Mobile gutter: `12px`.

## 7. Core Components

### Button

Required variants:

- Primary
- Secondary/outline
- Ghost
- Danger
- Icon-only
- Split/dropdown
- Loading
- Disabled

Specification:

```text
Height: 32px
Padding: 8px 12px
Primary background: #0A78BE
Primary text: #FFFFFF
Outline border: #A7B3BF
Outline text: #1C2B33
Radius: 4px
```

All variants support left/right icons, tooltip, keyboard focus and loading state without changing width.

### Input and Form Controls

```text
Height: 34px
Background: #FFFFFF
Border: 1px solid #CBD2D9
Radius: 4px
Padding: 7px 11px
Text: #1C2B33
Focus: #0A78BE
Error: #C91C2B
```

- Joined controls use `0px` radius on connected edges.
- Labels, help text and field errors are standardized through `FormField`.
- Required controls: input, textarea, select, combobox, checkbox, radio, switch, date/time picker, search and file upload.

### Tabs

```text
Height: 36px
Font: Optimistic 95, 14px
Active background: #E1EDF7
Active text: #0A78BE
Inactive text: #1C2B33
Padding: 8px 12px
Radius: 4px
```

Required variants: filled, underline, segmented and mobile-scrollable.

### Card

- White surface.
- `4px` radius.
- `12px–16px` padding.
- No default shadow.
- Optional soft divider.
- Reusable header, body, footer and action slots.

### Data Table

- Compact row height: `40px`.
- Comfortable row height: `48px`.
- Sticky header.
- Sorting, selection, bulk action and column visibility.
- Server-side pagination, filtering and searching.
- Skeleton, empty, error and permission-denied states.
- Responsive mobile row/card presentation.
- Business calculations must never depend on paginated client-side records.

### Modal

- Sizes: small, medium, large and full-screen.
- Focus trap, Escape close and accessible labels.
- Confirmation modal required for destructive actions.
- Unsaved-change guard for forms.
- Open/close animation: approximately `140ms`.

### Side Drawer

- Widths: `360px`, `480px`, `640px`.
- Full width on small mobile screens.
- Header, scrollable body and sticky footer slots.
- Slide animation: approximately `180ms`.

### Pagination

- Server-authoritative page, page size and total count.
- Previous/next, numbered pages and page-size selector.
- URL query parameters are the source of truth.
- Responsive condensed mode on mobile.

### Feedback Components

- Toast
- Inline alert
- Status badge
- Loading spinner
- Skeleton
- Empty state
- Error state
- Progress indicator
- Tooltip

## 8. Motion

- Standard duration: `120ms–180ms`.
- Use only `transform` and `opacity` where possible.
- Avoid large bounce, spring or decorative motion.
- Hover feedback must be subtle.
- Respect `prefers-reduced-motion`.
- Page transitions must never delay navigation or content rendering.

## 9. Responsive Rules

- Desktop: expanded/collapsible sidebar and full tables.
- Tablet: collapsed sidebar or drawer; condensed filters.
- Mobile: overlay navigation, full-width modal/drawer and responsive table rows.
- Touch targets should remain accessible even when the visual design is compact.
- No horizontal page overflow; data tables may use controlled internal scrolling.

## 10. Component Architecture

```text
components/
├── ui/
│   ├── button
│   ├── input
│   ├── select
│   ├── tabs
│   ├── modal
│   ├── drawer
│   ├── dropdown
│   ├── badge
│   ├── tooltip
│   ├── toast
│   ├── skeleton
│   ├── pagination
│   └── data-table
├── layout/
│   ├── app-shell
│   ├── sidebar
│   ├── topbar
│   ├── breadcrumb
│   ├── page-header
│   └── mobile-navigation
├── data-display/
│   ├── stat-card
│   ├── empty-state
│   ├── status-badge
│   ├── activity-list
│   └── description-list
└── forms/
    ├── form-field
    ├── date-picker
    ├── file-upload
    ├── search-field
    └── filter-bar
```

Feature-specific components must compose these primitives instead of duplicating markup or styling.

## 11. Component API Standards

- Every component supports `className` without breaking default styles.
- Variants and sizes use a consistent typed API.
- Components forward refs where focus or measurement is required.
- Interactive components expose loading, disabled, error and permission states.
- Use semantic HTML and accessible names.
- Keyboard navigation is mandatory.
- Avoid business logic inside visual primitives.
- Shared navigation, status and permission definitions have one source of truth.

## 12. SSR and Performance Rules

- Pages and data fetching are SSR-first.
- Use `"use client"` only for interactive islands.
- Filters, sorting and pagination run server-side.
- URL search parameters are the filter source of truth.
- Dynamically import charts, editors and other heavy interactive modules.
- Use request deduplication/caching and targeted revalidation after mutations.
- Virtualize large lists and grids.
- Provide skeletons with stable dimensions to prevent layout shift.
- Sidebar state changes must not rerender the entire page tree.
- Optimize icons and images; avoid oversized asset bundles.
- Keep business rules and aggregate calculations in backend services/API.
- Do not fetch the same dataset separately for multiple dashboard widgets.

## 13. Required Quality Gates

- Responsive verification at mobile, tablet and desktop breakpoints.
- Keyboard-only navigation.
- Visible and consistent focus states.
- Screen-reader labels for icon-only controls.
- Color contrast verification.
- Loading, empty, error, disabled and permission-denied state tests.
- No layout shift during loading.
- No duplicated primitive components or styling constants.
- No frontend calculation from incomplete paginated data.
- Component tests plus page-level integration tests.
- Production build, lint and type-check must pass.

## 14. Non-Negotiable Rules

1. Do not introduce a new visual style when an existing component variant can handle it.
2. Do not hardcode repeated colors, spacing, radius or typography inside feature components.
3. Do not create page-specific buttons, inputs, tabs, tables, modals or drawers.
4. Do not use purple/indigo as the primary UI identity.
5. Do not add heavy shadows, large radius or excessive spacing.
6. Do not move backend business calculations into React components.
7. Do not sacrifice accessibility for compactness.
8. Do not copy Meta branding, logo or proprietary assets; only follow the interaction and layout principles.
9. All new dashboard modules must use this design system.

## 15. Implementation Order

1. Design tokens, fonts and global background.
2. Button, input, form field, tabs and badge.
3. Modal, drawer, dropdown, tooltip and toast.
4. App shell, sidebar, topbar, breadcrumb and page header.
5. Data table, filters, pagination and bulk actions.
6. Loading, empty, error and permission states.
7. Refactor existing pages to shared components without changing business behavior.
8. Add component tests, accessibility checks and responsive verification.
