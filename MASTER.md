# LessonsIQ — Master Project Reference

> **For Claude Code:** Read this document at the start of every session before writing any code.
> After completing work, update the "Build Status" section to reflect what has been built.

---

## Vision

LessonsIQ is a platform that captures, synthesises and shares lessons learned from government and privately funded programs. It solves the problem that institutional knowledge evaporates when programs end — there is no single place where lessons from program investments are systematically captured, analysed and made available.

The platform enables program managers to:
- Structure programs, projects and activities in a hierarchy
- Invite partners to submit lessons via frictionless magic links
- Launch targeted surveys at any level of the hierarchy
- Use AI to synthesise raw lessons into strategic insights
- Build funder-ready reports with a full evidence trail

---

## Data Hierarchy

```
ORGANISATION
└── PROGRAM (e.g. "USAID Rural Resilience Initiative")
    ├── Funder(s), sector, geography, dates, reporting themes
    │
    ├── PROJECT A (e.g. "Community Water Access")
    │   ├── Internal description + links
    │   ├── Public description + links  ← shown to partners in surveys
    │   ├── ACTIVITY 1 (e.g. "Borehole Construction")
    │   │   ├── Internal description + links
    │   │   └── Public description + links
    │   ├── ACTIVITY 2 (e.g. "Water Committee Training")
    │   └── ACTIVITY 3 (e.g. "Sanitation Campaign")
    │
    ├── PROJECT B (e.g. "Agricultural Extension Training")
    │   ├── ACTIVITY 1 (e.g. "Farmer Field Schools")
    │   └── ACTIVITY 2 (e.g. "Input Supply Chain Support")
    │
    └── PROJECT C (e.g. "Women's Economic Empowerment")
        ├── ACTIVITY 1 (e.g. "VSLA Group Formation")
        ├── ACTIVITY 2 (e.g. "Business Skills Training")
        └── ACTIVITY 3 (e.g. "Market Linkages")
```

---

## User Roles & Permissions

### Role Definitions

| Role | Level | Description |
|------|-------|-------------|
| Super Admin | Platform | Platform operator — full access |
| Org Admin | Organisation | Owns all programs within their org |
| Program Manager | Program | Runs the program, owns reports |
| Project Lead | Project | Manages specific project(s) |
| Partner Contributor | Survey/Activity | Submits lessons via magic link |
| Funder | Program (read + submit) | Views funded programs, submits lessons |
| Governance Board Member | Program (persistent portal) | Strategic oversight, persistent link |

### Permissions Matrix

| Action | Super Admin | Org Admin | Program Manager | Project Lead | Partner | Funder |
|--------|:-----------:|:---------:|:---------------:|:------------:|:-------:|:------:|
| Create program | ✅ | ✅ | ❌ | ❌ | ❌ | ❌ |
| Create project | ✅ | ✅ | ✅ | ❌ | ❌ | ❌ |
| Launch survey | ✅ | ✅ | ✅ | ✅ own project | ❌ | ❌ |
| Submit lesson | ✅ | ✅ | ✅ | ✅ | ✅ via link | ✅ |
| View all responses | ✅ | ✅ | ✅ | Own project only | Own only | ❌ |
| Curate roll-up | ✅ | ✅ | ✅ | Flag only | ❌ | ❌ |
| Edit AI insights | ✅ | ✅ | ✅ | ❌ | ❌ | ❌ |
| Comment on insights | ✅ | ✅ | ✅ | ✅ | ❌ | ✅ |
| Export funder report | ✅ | ✅ | ✅ | ❌ | ❌ | Own programs |
| Cross-program view | ✅ | ✅ | ❌ | ❌ | ❌ | Own funded only |

### Access Inheritance
- Added to **Organisation** → inherits all programs within org
- Added to **Program** → inherits all projects within program
- Added to **Project** → that project only
- **Project Leads cannot see peer project data** — even if they inherit all projects
- **Partners** always use magic links — no persistent account

### Link Types
| Role | Link Type |
|------|-----------|
| Governance Board Member | Persistent — program lifespan |
| Funder | Persistent — program lifespan |
| Governance Partner | Persistent — program lifespan |
| Government Agency | Persistent — program lifespan |
| University Partner | Persistent — program lifespan |
| Project Lead | Persistent — project lifespan |
| Delivery Partner | Survey-specific + persistent portal |
| Industry Partner | Survey-specific + persistent portal |
| Civil Society | Survey-specific |
| Community Group | Survey-specific, simplified |

---

## Partner Types

Extensible taxonomy — platform defaults below, org and program level custom types supported.

### Platform Default Types (V1)

| Emoji | Type | Description |
|-------|------|-------------|
| 🏭 | Industry | Private sector, contractors, suppliers |
| 🚀 | Delivery | Implementing NGOs, service providers |
| 🏛️ | Governance | Government ministries, local authorities |
| 🏢 | Government Agency | Statutory bodies, regulatory agencies, public service delivery |
| 🎓 | University | Research, evaluation, academic institutions |
| 💰 | Funder | Donors, multilaterals, foundations |
| 🌐 | Civil Society | Community groups, advocacy orgs |
| 🏥 | Health & Social | Hospitals, clinics, social services |
| 🌍 | International Org | UN agencies, regional bodies, IGOs |
| 📡 | Media & Comms | Media outlets, communications orgs |
| 🤝 | Community Group | Local leaders, grassroots, CBOs |

### Extensibility Rules
- **Level 1:** Platform defaults (Super Admin manages, quarterly review)
- **Level 2:** Org-defined types (Org Admin, immediate, org-visible only)
- **Level 3:** Program-specific types (Program Manager, immediate, program-visible only)
- **Partner type is assigned per program role** — same org can be Delivery on one program, University on another
- **"Suggest a type" feature** — any user can flag a missing type for Org Admin approval

### Governance vs Government Agency Distinction
- **Governance** = policy-making bodies (Ministry of Health, County Council, Mayor's Office)
- **Government Agency** = statutory delivery/regulatory bodies (Roads Authority, Revenue Service, Water Board)

---

## Survey Architecture

### Who Can Launch Surveys
| Role | Can Target |
|------|-----------|
| Program Manager | Program / Project / Activity / Specific partner types |
| Project Lead | Their project / Their activities / Their partners |

### Survey Scope Levels
- **Program level** — whole program, all partners
- **Project level** — specific project and its partners
- **Activity level** — specific activity, activity-assigned partners only

### Recipient Experience Types
| Recipient Type | Experience | Rationale |
|----------------|-----------|-----------|
| Delivery Partner | Activity-level survey | Operational, specific |
| Governance / Government Agency | Consolidated portal | Systemic, cross-cutting |
| Funder | Consolidated portal | Strategic oversight |
| Governance Board | Consolidated portal | Panoramic view |
| University Partner | Project or activity | Evidence-focused |
| Industry Partner | Activity-level survey | Procurement, delivery |
| Civil Society | Activity-level survey | Community, local |
| Community Group | Simplified activity survey | Plain language, mobile |

Program Manager can override any default.

### Partner Magic Link Flows
1. **Survey invite** — unique tokenised link, configurable expiry
2. **Lesson submission (ad hoc)** — single-use direct lesson link
3. **Report share** — read-only tokenised link, aggregated findings only

### Persistent Link Security
- Unique cryptographic token per recipient
- Token refreshes every 90 days (silent — same URL, new token)
- Program Manager can revoke instantly
- Every access logged with timestamp

---

## Internal vs Public View

Every Project and Activity has two views:

| Internal View | Public View |
|---------------|-------------|
| Full operational detail | Clean partner-facing summary |
| Budget, staffing notes | Purpose & objectives only |
| Internal challenges/issues | Key links & resources |
| Private annotations | What we're asking about & why |
| Never exposed via magic link | Shown in survey context panel |

**Rule:** Public description is required before a survey can be sent.

---

## Bulk Partner Import

### Import Methods
1. **Upload CSV/Excel** — up to 1,000 contacts, column mapping step
2. **Paste from clipboard** — any format, AI-parsed
3. **Manual** — one by one for small additions

### Import Flow
1. Upload file or paste content
2. Map columns to system fields (flexible — columns don't need exact names)
3. Preview with validation — errors flagged, don't block import
4. Duplicate detection — cross-program matching
5. Assign to projects/activities (bulk or individual)

### Required Fields
- Email address (only mandatory field)

### Optional Fields
- First name, last name, organisation, partner type, job title, phone, project assignment, activity assignment, notes

### Downloadable Template
Pre-formatted XLSX with valid partner types on Tab 2 and example data on Tab 3.

### Validation Rules
- Invalid email format → flagged, skippable
- Missing email → flagged, must fix or skip row
- Unrecognised partner type → map to existing or create new
- Duplicate email → update existing or skip

---

## Lesson Data Structure

Each lesson record contains:

```
LESSON RECORD
├── Content
│   ├── What happened (observation)
│   ├── Why it matters (insight)
│   └── Recommendation (action)
├── Provenance
│   ├── Organisation
│   ├── Program
│   ├── Project
│   ├── Activity (nullable)
│   ├── Partner / partner type
│   └── Survey round
├── Classification
│   ├── Rollup status (staged / approved / rejected / held)
│   ├── Sensitivity flag
│   ├── Tags (AI suggested + manual)
│   └── Embedding vector (for clustering)
└── Source type (survey response / direct submission / board comment)
```

---

## AI Roll-up Flow

### Step 1: Staging Area
- Program Manager reviews lessons flagged by Project Leads
- Actions: Approve / Reject / Hold per lesson
- Filter by project, partner type, flag type

### Step 2: AI Analysis (async background job)
- Reads all approved lessons
- Clusters by semantic similarity (embeddings)
- Extracts strategic themes
- Detects contradictions and tensions
- Generates 5–10 insight statements

### Step 3: AI Insights Review
- Program Manager reviews each AI-generated insight
- Actions per insight: Accept / Edit / Merge / Reject
- Edit wording, add annotation, set confidence, actionability, sensitivity
- Tension insights show supporting AND contradicting lessons separately
- AI suggests nuanced reframe for tension insights
- Add manual insights

### Step 4: Report Builder
- Configure report structure (drag to reorder sections)
- Select which insights to include
- Set audience: Funder / Internal / Public
- Auto-generate executive summary
- Preview exactly what funder sees

### Step 5: Publish
- Share via link (view only)
- Export as PDF
- Export as Word (.docx)
- Send directly to funder email
- Add to public repository

---

## Insight Tree Structure

```
STRATEGIC INSIGHT (AI-generated, program manager curated)
"Community-led approaches consistently outperformed top-down implementation"
    │
    ├── Confidence level
    ├── Supporting lesson count
    ├── Projects covered
    │
    ▼ [Click to expand]
    │
    ├── PROJECT B — Partner Org
    │   └── Activity: Farmer Field Schools
    │       "Local women's groups as mobilisers doubled participation"
    │
    └── PROJECT C — Partner Org
        └── Activity: VSLA Formation
            "Community-selected leaders had 3x longer tenure"
```

Same lesson can appear under multiple strategic themes (tagging, not duplication).

---

## Board Member / Persistent Contributor Portal

### Key Principles
- One email → One link → One consolidated view
- Link persists for life of program
- No login required
- Shows all their past contributions consolidated (not by year/timeline)
- New items flagged with 🆕 since last visit
- Edit existing contributions or add new ones alongside

### Consolidated View Structure
```
YOUR CONTRIBUTIONS
├── Program Level comment [✏️ Edit] [+ Add]
├── Project A comment [✏️ Edit] [+ Add]
│   └── Activity 1 comment [✏️ Edit] [+ Add]
└── [No comment yet on Project B] [+ Add]
```

### Edit vs Add Distinction
- **Edit** → amends existing response (original preserved in internal audit trail)
- **Add** → fresh input alongside existing (accumulates, doesn't overwrite)

### Notification Triggers (persistent contributors)
- New activity added to program
- Survey round opens
- Strategic insights published (especially if related to their previous comments)
- Program milestone reached
- Annual reminder
- Program close (60 days before)

---

## Database Schema (Core Tables)

```sql
organisations         (id, name, type, settings, partner_types jsonb)
programs              (id, org_id, name, sector, geography, start_date, end_date, funder_details jsonb, reporting_themes jsonb)
projects              (id, program_id, name, description_internal, description_public, links_internal jsonb, links_public jsonb)
activities            (id, project_id, name, type, description_internal, description_public, links_internal jsonb, links_public jsonb)
partners              (id, org_id, name, partner_type, email, phone)
partner_program_roles (partner_id, program_id, project_id nullable, activity_id nullable, link_token, link_expires_at, link_type)
surveys               (id, created_by, scope_level, program_id, project_id nullable, activity_id nullable, status, open_date, close_date)
questions             (id, survey_id, type, content, hint_text, order, required)
responses             (id, survey_id, partner_id, submitted_at, is_complete)
response_answers      (id, response_id, question_id, answer jsonb)
lessons               (id, program_id, project_id, activity_id nullable, partner_id, source_type, what_happened, why_it_matters, recommendation, rollup_status, sensitivity, embedding vector, tags jsonb)
insights              (id, program_id, theme, statement, ai_generated bool, confidence_level, actionability, lesson_ids jsonb, contradicting_lesson_ids jsonb)
reports               (id, program_id, title, audience_type, structure jsonb, status, published_at, insight_ids jsonb)
```

---

## Technology Stack

### Frontend
- **Framework:** Next.js 14 (App Router)
- **Styling:** Tailwind CSS + shadcn/ui
- **State:** Zustand
- **Forms:** React Hook Form + Zod
- **Rich Text:** TipTap

### Backend
- **API:** Next.js API Routes + tRPC
- **Database:** PostgreSQL via Supabase
- **ORM:** Prisma
- **Auth:** Supabase Auth (accounts + magic links)
- **Storage:** Supabase Storage

### AI Layer
- **Primary LLM:** Anthropic Claude API (claude-sonnet-4-20250514)
- **Embeddings:** OpenAI text-embedding-3-small or Supabase pgvector
- **Vector Store:** pgvector (built into Supabase)

### Infrastructure
- **Hosting:** Vercel
- **Email:** Resend
- **Background Jobs:** Trigger.dev
- **Monitoring:** Sentry + Vercel Analytics

### Document Export
- **PDF:** Puppeteer or React-PDF
- **Word:** docx.js
- **Data Export:** CSV via Papaparse

---

## Build Phases

### Phase 1 — Core MVP (Months 1–3)
Goal: One program manager can run a full cycle end to end

- [ ] Auth — accounts + magic links
- [ ] Program / Project / Activity CRUD with internal/public views
- [ ] Link management (paste + rich text via TipTap)
- [ ] Partner management + type system
- [ ] Bulk import (CSV/Excel + paste)
- [ ] Basic survey builder
- [ ] Magic link survey experience (mobile optimised)
- [ ] Lesson capture form
- [ ] Basic roll-up (manual, no AI)
- [ ] Basic report export

### Phase 2 — AI Layer (Months 4–5)
Goal: AI makes the roll-up powerful

- [ ] Lesson embeddings + clustering
- [ ] AI insight generation
- [ ] Contradiction / tension detection
- [ ] Survey question suggestions by activity type
- [ ] Executive summary generation
- [ ] Report builder with insight tree

### Phase 3 — Scale & Governance (Months 6–8)
Goal: Multi-org, cross-program intelligence

- [ ] Org Admin layer + multi-tenancy
- [ ] Persistent contributor portals (board members, funders)
- [ ] Cross-program pattern detection
- [ ] Public repository (anonymised)
- [ ] Advanced permissions model
- [ ] Funder view role
- [ ] Data sovereignty options

---

## Prototype Screens (Clickable MVP — No Backend)

All screens use hardcoded mock data. Every button either navigates or shows a toast.

### Navigation Structure
```
Sidebar:
├── Dashboard (home)
├── Programs
│   └── [Program Name]
│       ├── Overview
│       ├── Projects
│       ├── Partners
│       ├── Surveys
│       ├── Lessons
│       └── Report
└── Settings
```

### Screen List

| # | Screen | Route |
|---|--------|-------|
| 1 | Dashboard | `/dashboard` |
| 2 | Create Program | `/programs/new` |
| 3 | Program Home | `/programs/[id]` |
| 4 | Add/Edit Project | `/programs/[id]/projects/new` |
| 5 | Add/Edit Activity | `/programs/[id]/projects/[pid]/activities/new` |
| 6 | Partner Management | `/programs/[id]/partners` |
| 7 | Bulk Import — Upload | `/programs/[id]/partners/import` |
| 8 | Bulk Import — Map Columns | `/programs/[id]/partners/import/map` |
| 9 | Bulk Import — Preview | `/programs/[id]/partners/import/preview` |
| 10 | Survey Builder | `/programs/[id]/surveys/new` |
| 11 | Partner Landing Page | `/survey/[token]` |
| 12 | Partner Survey Questions | `/survey/[token]/questions` |
| 13 | Partner Review & Submit | `/survey/[token]/review` |
| 14 | Partner Confirmation | `/survey/[token]/confirmation` |
| 15 | Board Member Portal | `/portal/[token]` |
| 16 | Roll-up Staging Area | `/programs/[id]/rollup` |
| 17 | AI Insights Review | `/programs/[id]/rollup/insights` |
| 18 | Report Builder | `/programs/[id]/report/builder` |
| 19 | Report Preview | `/programs/[id]/report/preview` |

---

## Mock Data (Use Throughout Prototype)

### Organisation
- Name: USAID Kenya
- Org Admin: Sarah Omondi

### Program
- Name: Rural Resilience Initiative
- Funder: USAID
- Grant: AID-615-A-24-00001
- Geography: Kenya
- Sector: Agriculture
- Dates: Jan 2024 – Dec 2027
- Reporting Themes: Sustainability, Gender & Inclusion, Community Ownership, Value for Money, Partnerships

### Projects
1. Agricultural Extension Training (Kisumu County)
2. Community Water Access (Nakuru County)
3. Women's Economic Empowerment (Mombasa County)

### Activities (Project 1 — Agricultural Extension)
- Farmer Field Schools (Training)
- Input Supply Chain Support (Procurement)

### Activities (Project 2 — Community Water Access)
- Borehole Construction (Construction)
- Water Committee Training (Training)
- Sanitation Awareness Campaign (Community Engagement)

### Activities (Project 3 — Women's Economic Empowerment)
- VSLA Group Formation (Community Engagement)
- Business Skills Training (Training)
- Market Linkages (Advocacy) — 🆕 recently added

### Partners (Sample)
| Name | Organisation | Type | Email |
|------|-------------|------|-------|
| James Omondi | Kisumu Agricultural Services NGO | Delivery | j.omondi@kasn.org |
| Dr. Alice Ochieng | University of Nairobi | University | a.ochieng@uon.ac.ke |
| John Mwangi | Ministry of Agriculture | Governance | j.mwangi@agri.go.ke |
| Dr. Kamau Njoroge | Rural Resilience Board | Governance Board | k.njoroge@board.org |
| Sarah Chen | USAID HQ | Funder | s.chen@usaid.gov |
| Peter Kariuki | Mombasa Delivery NGO | Delivery | p.kariuki@mdn.org |

### Sample Lessons
1. "Groups of 15 farmers were significantly more engaged than groups of 25" — Farmer Field Schools, Delivery
2. "Women participants in mixed groups contributed less than in women-only groups" — Farmer Field Schools, University
3. "Community-selected water committee leaders had 3x longer tenure than externally appointed ones" — Water Committee Training, Governance
4. "Participatory planning took longer but produced more durable outcomes" — VSLA Formation, Delivery
5. "Procurement delays caused 4-month project delay and budget overrun" — Borehole Construction, Industry

### Sample AI Insights
1. **Community Ownership** — "Smaller cohort sizes consistently improved outcomes across all training activities" (8 lessons, High confidence)
2. **Gender & Inclusion** — "Gender-sensitive design significantly improved participation across all three projects" (9 lessons, Very High confidence)
3. **⚡ Tension** — "Participatory approaches drive sustainability but conflict with funder timelines" (7 lessons, tension detected)
4. **Value for Money** — "Procurement planning invested upfront reduced delays by 60%" (5 lessons, Corroborated)
5. **Partnerships** — "Cross-project partner coordination was strongest where leads met monthly" (4 lessons, Anecdotal)

---

## Naming Conventions

- **Components:** PascalCase — `ProgramCard`, `SurveyBuilder`, `LessonCard`
- **Pages:** kebab-case routes — `/programs/new`, `/survey/[token]`
- **Hooks:** camelCase with `use` prefix — `useProgram`, `useSurvey`
- **Utils:** camelCase — `formatDate`, `generateToken`
- **Types:** PascalCase with `T` prefix — `TProgram`, `TLesson`, `TPartner`
- **Mock data files:** `mock-[entity].ts` — `mock-programs.ts`, `mock-lessons.ts`

---

## Design Principles

1. **Frictionless for partners** — magic links, no accounts, mobile first, progress saved
2. **Context drives quality** — public descriptions shown in surveys so partners understand what they're responding to
3. **Curated roll-up** — project lessons don't auto-promote; program manager selects and annotates
4. **AI assists, human decides** — AI suggests categorisation and synthesis, manager approves
5. **Full evidence trail** — every strategic insight links back to source lessons and raw responses
6. **Confidentiality by default** — partner responses not visible to peers; aggregated only
7. **Closed loop** — partners receive aggregated findings after survey closes

---

## Build Status

### What Has Been Built
*Nothing yet — prototype starting now*

### Current Phase
*Phase 0 — Clickable Prototype*

### Last Updated
*[Update this after each Claude Code session]*

---

## Session Log

| Date | Session Focus | Completed | Notes |
|------|--------------|-----------|-------|
| — | — | — | Starting fresh |
