ROLE
You are a senior frontend architect. Build a reusable, borderless, animated enterprise UI design system "ISSL UI" that works in ANY project type (ecommerce, LMS, project management, CRM/ERP, landing page) and in BOTH Next.js (App Router, TypeScript, Tailwind) and Django (templates + Tailwind + Alpine.js). Meta Business Suite inspired layout, but premium, modern, flat, compact.

PHASE 0 - AUDIT FIRST (no code changes yet)
Detect the stack of the current repo (Next.js or Django). Scan existing UI, list duplicated buttons/inputs/tables/modals, current icon library, CSS approach. Report findings + integration plan. STOP and wait for my approval before Phase 1.

CORE RULES
1. ZERO BORDERS. No border on cards, inputs, buttons, tables, modals, dropdowns, tabs, sidebar, topbar. border-width is 0 everywhere. Separation comes only from:
   - surface layering (workspace gradient > white card > #F1F4F7 muted surface)
   - spacing
   - elevation token: --shadow-card: 0 1px 2px rgba(28,43,51,.06); --shadow-float: 0 4px 16px rgba(28,43,51,.10) (dropdown/modal/drawer only)
   - inputs: filled bg #F1F4F7, hover #E9EDF1, focus = 2px ring via box-shadow (0 0 0 2px #0A78BE33 + bg white). Error ring uses #C91C2B.
   - table: no row lines; use hover bg, optional zebra, 8px row gap or spacing.
   - outline button = tinted bg (#E1EDF7 with #0A78BE text), not a border.
   Accessibility: focus-visible ring must always exist.
2. Everything is a reusable component. No page-specific buttons/inputs/tabs/tables/modals/drawers. Feature code only composes primitives.
3. Single source of truth for design tokens. Framework-agnostic CSS variables in tokens.css, mapped into tailwind config. Brand is overridable per project via --brand-primary, --action-primary, --action-hover (so each project can re-skin without touching components). Never hardcode colors/spacing/radius in feature code.
4. No purple/indigo as primary. No heavy gradients, no glassmorphism, no large radius (default 4px, modal 6px, badge/avatar 999px).
5. Backend owns business calculations, filtering, sorting, pagination. UI never computes from paginated data. URL query params = filter source of truth.

TOKENS (keep from existing spec)
brand-primary #0462D2, action-primary #0A78BE, action-hover #086AA8, tab-active-bg #E1EDF7, text-primary #1C2B33, text-secondary rgba(28,43,51,.65), text-muted #667781, sidebar-active #2F414A, surface-primary #fff, surface-secondary #F1F4F7, success #168A45, warning #E89A00, danger #C91C2B, info #0A78BE.
Workspace background gradient only on main workspace (radial #eaf8ef / #faf1f1 / #f3edf5 / #e5f0fa). Cards/tables/modals/nav stay solid.
Font: Inter (fallback Helvetica, Arial). Sizes: page heading 20/600, section 16/600, body 13, sidebar 12-13, button 12, table 12, caption 11. 4px spacing base. Button 32px, input 34px, tab 36px, topbar 52px, sidebar 224px expanded / 56px collapsed, table row 40 compact / 48 comfortable.

ICONS
Use Phosphor Icons only (one library, consistent). Weights: regular for default, bold for active/selected, duotone for empty states, feature cards and landing sections.
- Next.js: @phosphor-icons/react (import individual icons, tree-shaken).
- Django: inline SVG via a {% icon "name" weight="regular" size=18 %} template tag (or Phosphor SVG sprite). No icon fonts, no CDN.
Create ONE <Icon> wrapper component/tag with props: name, size (14/16/18/20/24), weight, className. Default size 18 in sidebar/buttons, stroke consistent. Central icon-map file for nav icons. No emoji as icons. No mixing of icon libraries.

MOTION SYSTEM (smooth, fast, functional)
Tokens: --ease-out: cubic-bezier(.2,.8,.2,1); --ease-in-out: cubic-bezier(.4,0,.2,1); --dur-fast 120ms; --dur-base 180ms; --dur-slow 260ms.
Animate only transform and opacity (plus width on sidebar with will-change). Respect prefers-reduced-motion (disable all non-essential motion). Never delay navigation or content.
- Buttons: hover bg transition 120ms, press scale .98, loading state keeps width.
- Cards: hover lift translateY(-1px) + shadow upgrade (only for clickable cards).
- Inputs: focus ring fades in 120ms.
- Tabs: active pill slides between tabs (shared layout indicator), 180ms.
- Dropdown/popover/tooltip: fade + scale .97->1 + translateY 4px, 140ms, origin-aware.
- Modal: backdrop fade + panel scale .98->1 + fade, 160ms. Drawer: slide from edge 200ms with backdrop fade.
- Toast: slide+fade in, auto-dismiss with progress.
- Skeletons: soft shimmer, stable dimensions (no layout shift).
- Lists/tables: staggered fade-in 20ms step, max 8 items, only on first mount.
- Sidebar: width collapse/expand 220ms --ease-out; labels fade (opacity) without text reflow jump; active item indicator slides smoothly between items; submenu expands with height + opacity 180ms; chevron rotates 180ms. Mobile: overlay drawer slide + backdrop fade. Sidebar toggle must not rerender the page tree (isolate state).
- Page transitions: content area fades + translateY 6px->0, 180ms on route change; the sidebar and topbar never re-animate. Show a thin top progress bar on navigation.
Implementation:
- Next.js: motion (framer-motion) in client islands only; page transition via app/template.tsx; sidebar via motion + layoutId indicator; keep pages SSR, "use client" only for interactive pieces; loading.tsx skeletons.
- Django: pure CSS transitions + Alpine.js (x-transition) for sidebar/dropdown/modal/drawer; page transitions via CSS View Transitions API (@view-transition { navigation: auto }) with fallback to a CSS fade-in animation on main content; htmx optional, not required.

COMPONENTS (framework parity: same names, same props/variants, same look in both stacks)
ui: Button (primary, tonal, ghost, danger, icon, split, loading, disabled), Input, Textarea, Select, Combobox, Checkbox, Radio, Switch, DatePicker, SearchField, FileUpload, FormField, Tabs (filled, underline, segmented, scrollable), Badge, Avatar, Tooltip, Dropdown, Modal, Drawer, Toast, Skeleton, Pagination, DataTable, Progress, Alert, EmptyState, ErrorState, Breadcrumb.
layout: AppShell, Sidebar (config-driven, permission-filtered, from one nav config), Topbar, PageHeader, MobileNavigation, PageTransition, SectionContainer (for landing pages).
data-display: StatCard, ActivityList, DescriptionList, StatusBadge, Timeline.
Optional domain layer (compose primitives only, never fork styles): ecommerce (ProductCard, CartDrawer, PriceTag, OrderStatus), LMS (CourseCard, LessonList, ProgressRing, CertificateCard), project (KanbanBoard, TaskCard, MemberStack), landing (Hero, FeatureGrid, PricingTable, Testimonial, CTA, Footer - uses tokens + duotone icons + same motion, no app shell).
Every component: className passthrough, typed variants/sizes, forwardRef where needed, loading/disabled/error/permission states, semantic HTML, keyboard nav, aria labels on icon-only controls.

STRUCTURE
Next.js: components/ui, components/layout, components/data-display, components/forms, components/domain/*, styles/tokens.css, lib/nav-config.ts, lib/motion.ts (shared variants).
Django: templates/components/ (include/cotton/template-tag components), static/css/tokens.css, static/js/ui.js (Alpine data), templatetags/ui.py, nav config in one Python file.
tokens.css + motion tokens + icon-map must be identical in both stacks so the design can be copied project to project.

QUALITY GATES
Mobile/tablet/desktop check, keyboard-only navigation, visible focus rings (borderless but never invisible), contrast check, loading/empty/error/disabled/permission states, zero layout shift, no horizontal page overflow, reduced-motion respected, no duplicated primitives, production build + lint + type-check pass. Grep must confirm: no "border" utilities remain except focus/outline accessibility fallbacks.

EXECUTION (step by step, wait for my approval between phases)
Phase 0 audit -> Phase 1 tokens, fonts, icons, motion tokens -> Phase 2 form primitives + Button/Tabs/Badge -> Phase 3 overlays (Dropdown, Modal, Drawer, Tooltip, Toast) -> Phase 4 AppShell + animated Sidebar + Topbar + PageTransition -> Phase 5 DataTable, filters, pagination, states -> Phase 6 refactor existing pages to shared components without changing business behavior -> Phase 7 tests + accessibility + responsive report.
Do not touch backend logic, auth, migrations or DB. Report after each phase with changed files list.
