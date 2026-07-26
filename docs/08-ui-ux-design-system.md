# UI/UX Design System

## 1. Design principles

- **The dashboard is a workspace, not a landing page.** Users open Aurora to *continue* work (recent chats, pinned projects, running automations), not to face a blank input box.
- **Chat is one surface, not the whole product.** The Canvas, Document Studio, and Coding Studio need their own layouts optimized for their content, not a chat transcript stretched to fit.
- **Every AI action is legible.** Which model answered, what sources it used, and what it's confident about are always visible, never hidden behind a generic "AI response."
- **Accessibility is a v1 requirement**, not a post-launch audit item — WCAG 2.1 AA across all first-party surfaces (stated in [Product Requirements §4](02-product-requirements.md)).

## 2. Core surfaces

| Surface | Purpose | Key components |
|---|---|---|
| Home Dashboard | Orientation and quick resume | Activity feed, pinned projects, quick actions, notifications |
| Universal Chat | Primary conversational interface | Message thread, model selector, attachment tray, citation panel |
| AI Canvas | Multi-format collaborative workspace | Panel system (chat + doc + diagram + code side by side) |
| Document Studio | Document-centric editing | Inline editor, version diff view, comment threads |
| Agent Console | Building and monitoring agents | Agent config form, run history, approval queue |
| Admin Panel | Org and security management | User table, audit log viewer, usage dashboard |

## 3. Design tokens (starting point)

```
Color
  --color-primary:      #2E5CE6   /* primary actions, links */
  --color-primary-dark: #1C3FA8
  --color-surface:      #FFFFFF   /* light mode base */
  --color-surface-dark: #0F1115   /* dark mode base */
  --color-text:          #14171F
  --color-text-dark:     #E7E9EE
  --color-success:       #1C9A5B
  --color-warning:       #C77E11
  --color-danger:        #C2382C
  --color-confidence-high: #1C9A5B
  --color-confidence-low:  #C77E11

Typography
  --font-family-ui:   "Inter", system-ui, sans-serif
  --font-family-mono: "JetBrains Mono", monospace
  --font-size-body:   15px
  --font-size-small:  13px
  --font-size-h1:     28px
  --font-size-h2:     22px

Spacing (4px base unit)
  --space-1: 4px   --space-2: 8px   --space-3: 12px
  --space-4: 16px  --space-6: 24px  --space-8: 32px

Radius
  --radius-sm: 6px   --radius-md: 10px   --radius-lg: 16px
```

Dark mode is a first-class token set (`-dark` suffix above), not a CSS filter over the light theme — required because a meaningful share of the target developer/researcher persona works dark-mode-first.

## 4. Confidence and citation UI pattern

Any AI output that makes a factual claim (Research Engine, Knowledge Engine responses) renders with:

1. Inline citation markers linking to source panel entries
2. A confidence badge (High / Moderate / Low) using the token colors above — never a bare percentage without a label, which tests poorly for interpretability
3. A "verify" affordance that opens the source directly, not just a citation string

## 5. Responsive strategy

- **Desktop-first for Canvas and Coding Studio** (multi-panel layouts don't meaningfully collapse to mobile; mobile gets a simplified single-panel view with a surface switcher instead of a squeezed layout).
- **Mobile-first for Chat and Dashboard** (these are the surfaces used on the go).
- Breakpoints: 480px / 768px / 1024px / 1440px.

## 6. Componentization

Built as a shared component library consumed by web and (via React Native, see [Tech Stack](09-tech-stack.md)) mobile, so the design tokens above are the single source of truth rather than being redefined per platform.

## 7. What's deferred

Full interaction specs for the Automation visual builder and the Agent Console's node-based editor are scoped in detail at Phase 3, once the underlying execution model (see [Security & Compliance §3](07-security-and-compliance.md)) is finalized — designing the UI before the approval-tier semantics are locked would mean redesigning it.
