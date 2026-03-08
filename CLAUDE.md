# CLAUDE.md — Instructions for Claude Code

This file is read automatically by Claude Code on startup.
**Always read MASTER.md before starting any task in this project.**

---

## Project Overview

You are building **LessonsIQ** — a platform for capturing, synthesising and sharing lessons learned from government and privately funded programs. Full specification is in MASTER.md.

---

## How to Work on This Project

### Start of Every Session
```
1. Read MASTER.md fully
2. Check "Build Status" section to understand what exists
3. Confirm the task with the user before writing code
4. Work in small, focused increments
5. Test each piece before moving to the next
```

### End of Every Session
```
1. Update MASTER.md "Build Status" with what was built
2. Update "Session Log" with date, focus, completed items
3. Note any decisions made or patterns established
```

---

## Current Task: Clickable Prototype

We are building a **clickable Next.js prototype** — no backend, no database, all hardcoded mock data.

### Prototype Rules
- Use shadcn/ui components throughout
- Use Tailwind CSS for all styling
- Use realistic mock data from MASTER.md (mock data section)
- Every button either navigates somewhere or shows a toast notification
- No auth required — land directly on dashboard
- Mobile screens required for the partner survey journey (screens 11–14)
- Deploy to Vercel as early as possible for a shareable link

### What "Done" Looks Like for Each Screen
- Looks like the real product
- All navigation works
- Realistic data displayed
- Key interactions (expand/collapse, tabs, modals) work
- No broken links or dead ends

---

## Tech Stack (Prototype)

```
Framework:    Next.js 14 (App Router)
Styling:      Tailwind CSS
Components:   shadcn/ui
Icons:        lucide-react
Mock Data:    Hardcoded TypeScript files in /lib/mock/
State:        React useState (no Zustand needed for prototype)
Toasts:       shadcn/ui sonner
```

---

## Project Structure

```
/app
  /dashboard          → Screen 1: Dashboard
  /programs
    /new              → Screen 2: Create Program
    /[id]
      /page.tsx       → Screen 3: Program Home
      /projects
        /new          → Screen 4: Add Project
        /[pid]
          /activities
            /new      → Screen 5: Add Activity
      /partners
        /page.tsx     → Screen 6: Partner Management
        /import
          /page.tsx   → Screen 7: Upload
          /map        → Screen 8: Column Mapping
          /preview    → Screen 9: Preview & Validate
      /surveys
        /new          → Screen 10: Survey Builder
      /rollup
        /page.tsx     → Screen 16: Staging Area
        /insights     → Screen 17: AI Insights Review
      /report
        /builder      → Screen 18: Report Builder
        /preview      → Screen 19: Report Preview
/survey
  /[token]
    /page.tsx         → Screen 11: Partner Landing
    /questions        → Screen 12: Survey Questions
    /review           → Screen 13: Review & Submit
    /confirmation     → Screen 14: Confirmation
/portal
  /[token]            → Screen 15: Board Member Portal
/components
  /ui/                → shadcn/ui components (auto-generated)
  /layout/            → Sidebar, Header, Navigation
  /programs/          → Program-specific components
  /surveys/           → Survey-specific components
  /lessons/           → Lesson-specific components
  /partners/          → Partner-specific components
  /reports/           → Report-specific components
/lib
  /mock/              → All hardcoded mock data
    programs.ts
    projects.ts
    activities.ts
    partners.ts
    lessons.ts
    surveys.ts
    insights.ts
```

---

## Component Naming Conventions

- **Components:** PascalCase — `ProgramCard`, `SurveyBuilder`, `LessonCard`
- **Pages:** `page.tsx` in App Router directories
- **Hooks:** camelCase with `use` prefix — `useProgram`
- **Types:** PascalCase with `T` prefix — `TProgram`, `TLesson`
- **Mock data files:** `mock-[entity].ts`

---

## Design System Rules

### Colours (Tailwind)
- **Primary:** `blue-600` for primary actions
- **Success:** `green-600` for approved/active states
- **Warning:** `amber-500` for pending/hold states
- **Danger:** `red-500` for rejected/delete actions
- **Tension:** `orange-500` for AI-detected tensions
- **Background:** `gray-50` for page backgrounds
- **Cards:** `white` with `border border-gray-200 rounded-lg`

### Key UI Patterns
- **Cards:** `bg-white border border-gray-200 rounded-lg p-4 shadow-sm`
- **Tabs:** Use shadcn/ui Tabs component
- **Modals:** Use shadcn/ui Dialog component
- **Toasts:** Use shadcn/ui Sonner — "Coming soon" for unbuilt features
- **Progress:** Use shadcn/ui Progress component
- **Badges:** Use shadcn/ui Badge for status indicators

### Internal vs Public View Pattern
Always use shadcn/ui Tabs with:
- Tab 1: "🔒 Internal" 
- Tab 2: "🌐 Public"
Include info banner: "This is what partners see in their survey"

### Sidebar Layout
- Fixed left sidebar, 240px wide
- Logo + "LessonsIQ" at top
- Navigation items with icons (lucide-react)
- Active state: `bg-blue-50 text-blue-700 font-medium`
- User info at bottom

---

## Mock Data to Use

See MASTER.md "Mock Data" section for full details. Key program:

**Program:** Rural Resilience Initiative (USAID Kenya)
**3 Projects:** Agricultural Extension, Community Water Access, Women's Economic Empowerment
**8 Activities** across the 3 projects
**6 Sample Partners** of various types
**5 Sample Lessons** with realistic content
**5 Sample AI Insights** including 1 tension

---

## Screen-Specific Notes

### Screen 4 (Add/Edit Project) & Screen 5 (Add Activity)
- Internal/Public tabs are CRITICAL — must work correctly
- TipTap not needed for prototype — use simple textarea
- Links section: title + URL pairs, add/remove dynamically
- "Preview Partner View" button → shows modal of what partner sees

### Screen 7–9 (Bulk Import)
- Screen 7: Drag/drop zone + browse button (no actual file processing needed)
- Screen 8: Show hardcoded column mapping with dropdowns
- Screen 9: Show 241 "ready" + 6 "issues" using mock data

### Screens 11–14 (Partner Survey Journey)
- MUST be mobile-optimised (max-width 390px, mobile-first layout)
- No sidebar on these screens
- Progress indicator at top
- Context panel (collapsible) alongside questions on desktop
- Stacked (context above questions) on mobile

### Screen 15 (Board Member Portal)
- No sidebar
- Shows consolidated contributions (not timeline)
- 🆕 badge on Market Linkages activity
- Edit/Add buttons per item

### Screen 17 (AI Insights)
- Show insights with expand/collapse for supporting lessons
- Tension insight (Screen 3 in mock data) must show BOTH supporting and contradicting lessons
- AI suggested nuance text with "Use This ✓" button

### Screen 19 (Report Preview)
- Simulate expandable insight tree
- Looks like a real published report
- Export buttons at bottom (show toast for each)

---

## Common Mistakes to Avoid

1. **Don't build auth** — prototype lands directly on dashboard
2. **Don't connect to any backend** — all data is hardcoded
3. **Don't use localStorage** — not supported in this environment
4. **Don't skip mobile styles** for partner survey screens
5. **Don't leave dead-end buttons** — every button needs a destination or toast
6. **Don't forget the Internal/Public tab pattern** on project/activity forms
7. **Always import shadcn components properly** — run `npx shadcn@latest add [component]` if missing

---

## Deployment

Deploy to Vercel after scaffold is complete:
```bash
vercel --prod
```

Share the URL with user after each major milestone so they can review on mobile too.

---

## If You Get Stuck

1. Re-read MASTER.md for the relevant screen specification
2. Check the Screen List in MASTER.md for what should be on each screen
3. Use the mock data exactly as specified
4. When in doubt, keep it simple — prototype, not production
