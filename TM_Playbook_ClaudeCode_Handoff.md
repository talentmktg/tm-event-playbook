# TM Event Playbook 2.0 — Claude Code Handoff Document

## Project Overview
Build a single-file interactive HTML dashboard called the **TM Event Playbook 2.0** for Intuit's Talent Marketing team. This is a single-page application (no frameworks, no build tools) — everything lives in one `.html` file with embedded CSS and JavaScript.

The working source file is `event_playbook_2.0.html` — this handoff document explains every design decision, content structure, interaction, and link so Code can rebuild, extend, or modify it accurately.

---

## File Structure
Single file: `event_playbook_2.0.html`
- Inline `<style>` block (CSS variables + all component styles)
- HTML body (header → hero → nav → panels)
- Inline `<script>` block (localStorage persistence, checkbox toggle, progress bars, reset, panel nav)

---

## Design System

### Fonts
```
DM Serif Display (italic) — hero H1 only
DM Sans 300/400/500/600 — all body text
Import from Google Fonts
```

### Color Tokens (CSS variables)
```css
--ink: #0f0f0e          /* near-black, primary text */
--ink-2: #3a3935        /* body text */
--ink-3: #7a7870        /* muted text */
--ink-4: #b8b5ad        /* placeholder / disabled */
--cream: #f7f5f0        /* page background */
--cream-2: #edeae2      /* card backgrounds */
--cream-3: #e2ded4      /* borders */

/* Track themes */
--virtual: #1a4d3a          /* Virtual Events — deep green */
--virtual-light: #e6f2ec
--virtual-mid: #2d7a5a

--inperson: #3d2b1a         /* In-Person Events — deep brown */
--inperson-light: #f5ede4
--inperson-mid: #a0522d

--governance: #1a2a4d       /* Governance & DACE — deep navy */
--governance-light: #e6eaf5
--governance-mid: #3a5bbf

--ai: #3d1a4a               /* AI / Gem prompts — deep purple */
--ai-light: #f0e8f5
--ai-mid: #8b35bf

--accent: #d4521a           /* Orange — reset confirm, highlights */
--white: #ffffff

--radius: 12px
--radius-sm: 6px
```

---

## Page Structure

### 1. Site Header (`.site-header`)
- Dark ink background, 60px height
- Left: "TM Event Playbook" + `<span>2.0</span>` (orange accent color)
- Right: "Talent Marketing · FY26 · Future-Forward" (muted text)

### 2. Hero Section (`.hero`)
- Dark ink background
- Eyebrow: "SINGLE SOURCE OF TRUTH FOR ALL TM EVENTS" (small caps, orange)
- H1: "Run every event" + line break + `<em>with confidence.</em>` (DM Serif italic)
- Body: "The TM team's single source of truth for virtual and in-person events — with AI Gem prompts, step-by-step checklists, Zoom setup guidance, DACE role clarity and post-event reporting tools all in one place."
- Stats row (`.hero-stats`): 4 stat blocks
  - **2** Event tracks
  - **7** Virtual planning phases
  - **75+** Checklist tasks
  - **10+** AI Gem prompts

### 3. Navigation (`.nav-tabs`)
6 tabs, each with a colored dot indicator:
```
Virtual Events      — green dot  (#2d7a5a)
In-Person Events    — brown dot  (#a0522d)
Zoom Setup Guide    — blue dot   (#2255cc)
Governance & DACE   — navy dot   (#3a5bbf)
Metrics & Reporting — amber dot  (#cc8800)
Resources & Templates — gray dot (#666)
```

---

## Tab Panels

### Panel 1: Virtual Events (`#panel-virtual`, `.virtual-theme`)

**Header:**
- Eyebrow: "Track 01 — Virtual Events"
- Title: "Webinars, simulives & virtual chats"
- Description: "Full lifecycle for CP2E and Pro virtual events. Use the Virtual Event Checklist below as the standard template. Steps are shared across teams — team-specific callouts are noted inline where workflows differ."

**Frequency & Timing Callout** (`.callout.callout-tip`):
- Avoid: Winter holidays (late Nov–Jan), early summer (June–July), spring break, Intuit company-wide event weeks
- Best windows: Sept–Oct and Feb–Apr
- Spacing: 2–3 weeks between events targeting same audience
- Timing: Mid-week (Tue–Thu), 8am–12pm PT

**T4i Update Callout** (`.callout`):
"T4i no longer manages Zoom webinar setup as of FY26. TM hosts now self-configure all Zoom settings using the Zoom Setup Guide tab. T4i still provides day-of production support when engaged."

**Google Sheets Banner** → links to: `https://docs.google.com/spreadsheets/d/1d7g-5snlq4G7unH8R4bLe71zlP7KW0fU/edit?usp=sharing&ouid=111325661992984101647&rtpof=true&sd=true`
- Label: "Open the Virtual Event Checklist in Google Sheets"

**Progress Bar + Reset Button**

**7 Step Cards** (expandable, `.step-card`):

#### Step 01 — Pre-Planning & Strategy (5–8 weeks out)
Tasks:
1. Define event objective and target audience (awareness, conversion, nurture)
2. Identify and confirm speakers/panelists — lean on recruiters to source [TA assist tag]
3. Request speaker headshots and bios
4. Confirm date, time, and webinar format (live / simulive / rebroadcast)
5. Send calendar holds for speakers, Q&A support, and dry run
6. Submit Zoom support ticket (if needed) [Zoom tag]

Gem Prompt: "I'm planning a [CP2E / Pro] webinar for [audience segment] on [topic]. Target date is [date]. Suggest 3 topic angles, a speaker profile template, and a 6-week planning timeline."

Speaker Selection Criteria section (expandable within step):
- What to look for: Resonates with brand & audience, brings relevant expertise, diverse backgrounds, has presented before, available for dry run
- Sourcing process: Ask recruiters, check past panelist lists, look for conference speakers, TTL/QBL speakers via Resources & Templates tab, brief speakers on goals
- Gem prompt for speaker outreach

#### Step 02 — Choose Your Event Format (5–8 weeks out)
3 format cards:
- **Live Webinar**: Real-time interaction. Best for Q&A-heavy events, new audiences, high-conversion goals. Best for: recruitment, brand awareness, high-intent audiences
- **Simulive**: Pre-recorded content played live with host moderating chat/Q&A. Reduces speaker dependency. Best for: recurring series, cost efficiency, consistent delivery
- **Rebroadcast**: Fully pre-recorded, no live host. Best for: Canada/international audiences, off-peak reach

Comparison table (Live vs Simulive vs Rebroadcast):
- Speaker needed day-of: Yes / Host only / No
- Live Q&A: Yes / Yes (host moderates) / No
- Production effort: High / Medium / Low
- Zoom setup required: Full / Full / Minimal
- Typical use: Pro series, IM events / CP2E TTL/QBL series / Canada, off-season reach

Gem Prompt: "I'm planning a [CP2E / Pro] event for [audience] on [topic]. Should this be a live webinar, simulive, or rebroadcast? Consider our team capacity, audience size, and goal of [awareness / conversion / nurture]."

#### Step 03 — Assets & Setup (4 weeks out)
Tasks:
1. Draft all email copy: invite 1, invite 2, confirmation, reminders, post-event [AI draft tag]
2. Design Zoom registration banner (use Adobe Express template) [Template tag]
3. Build registration page in Eloqua
4. Set up Zoom webinar with all required settings (see Zoom Setup Guide tab) [Zoom tag]
5. Create CID tracking links for all emails and registration page
6. Set up SurveyMonkey post-event survey with standard questions
7. Add event to Airtable campaign tracker
8. Define audience segmentation — CP2E: segment by hire-ability, manage suppression lists · Pro: define audience parameters and special requirements

Gem Prompt: "Write 3 subject line options and full email copy for a webinar invite. Audience: [segment]. Topic: [title]. Tone: [professional/conversational]. Include a clear CTA to register."

Culture of Testing section:
- Run one test per send — change only one variable at a time
- Email testing: subject lines, send day & time, number of reminder emails, content & creative, CTA copy and placement
- Webinar testing: day/time, length, title, format (Live vs Simulive), ads & promotion channels
- Gem prompt for testing suggestions

#### Step 04 — Promotion & Comms (2–3 weeks out)
Tasks (in this exact order):
1. Send email invite 1 via Eloqua — CP2E: 1 week out · Pro: 2–3 weeks out — verify send counts and suppressions
2. Schedule email invite 2 (1 week later) and all reminder emails 1 week and 1 day prior to event
3. Send panelists their promotion materials and speaker brief
4. Post on Handshake and relevant Slack channels [Pro tag]
5. Post on Intuit Alumni Network LinkedIn group [Pro tag]
6. Run LinkedIn ads via Pro Campaign Manager or ad agency support [Pro tag]
7. Share social copy with Digital Ambassadors and partner orgs
8. Partner with diversity orgs for additional promotion — leverage partner networks to amplify reach
9. Prepare canned responses for common attendee questions during event [Pro tag]

#### Step 05 — Final Prep & Dry Run (1 week out)
Tasks:
1. Finalize webinar slide deck and share with all panelists
2. Complete T4i briefing doc: timing, slide notes, Q&A instructions, run-of-show [T4i brief tag]
3. Conduct 30-min dry run with host and all panelists — confirm video, audio, poll flow
4. Prepare backup Q&A questions in case audience is quiet
5. Verify Zoom email settings: banner updated, reminders scheduled [Zoom tag]
6. Check inbox for attendee questions and send Zoom join links
7. Prepare live chat messages: hiring links, survey link, academy info

T4i Brief Reminder callout: "Send the completed T4i Briefing Template to your T4i rep at least 48 hours before the event. Find the template in the Resources & Templates tab."

#### Step 06 — Event Execution (Day of event)
Tasks:
1. Start Zoom webinar 15 min early — practice session with panelists and hosts only
2. Play intro music loop while attendees join (audio file in Resources & Templates tab)
3. Disable chat for attendees, enable Q&A, confirm panelist chat settings [Zoom tag]
4. Launch polls at designated slide moments — allow panelists to vote, share results
5. Post live chat messages: survey link, talent community link, job application link

#### Step 07 — Post-Event & Reporting (Within 1 week after)
Tasks:
1. Send thank you email to attendees (with recording link, survey, application link)
2. Send "missed you" email to non-attendees (recording link, nurture)
3. Download and upload Zoom attendee list, registration list, Q&A list and recording to Google Drive
4. Upload recording to Vidyard — add to CP2E and Pro Talent Community Hubs
5. Analyze metrics: registrations, attendees, attendance rate, NPS, email open/click rates [AI analyze tag]
6. Log your event results for your own records (see Metrics tab)
7. Convert landing page to on-demand with form/gated approach (Pro)

Gem Prompt: "Analyze these event results: [paste Eloqua data, Zoom attendance, SurveyMonkey export]. Summarize key metrics, identify top insights from qualitative comments, and suggest 3 improvements for next time."

Feedback & Continuous Improvement section:
- SurveyMonkey: Primary post-event feedback tool. Send within 24 hours of event close.
- Speaker debrief: Informal Slack or quick call within 1–2 days. Send spotlight as thank you.
- Audience interviews (FMH): Periodic 1:1 interviews with target audience members. At least once per series or quarter.
- Gem prompt for survey comment analysis

---

### Panel 2: In-Person Events (`#panel-inperson`, `.inperson-theme`)

**Header:**
- Eyebrow: "Track 02 — In-Person Events"
- Title: "Networking events, IM events & conferences"
- Description: "Full lifecycle for in-person TM events. Use the In-Person Event Checklist below as the standard template — adapt to your event size and site location."

**Frequency & Timing Callout**: Same as virtual but timing reads "Mid-week (Tue–Thu), 12pm PT"

**Google Sheets Banner** → links to: `https://docs.google.com/spreadsheets/d/1NwmOPe9BssfRLQ8UJMC4VeDNUvQtlE4PWxUclQh6bIM/edit?gid=307869881#gid=307869881`

**Progress Bar + Reset Button**

**Site-Specific Planning Callout**: "Every Intuit campus has different contacts, booking processes, and badge/parking requirements. Always check the Intuit Event Builder on Insight for your site before starting."

**6 Step Cards:**
1. Event Definition & Strategy (6–8 weeks out)
2. Logistics & Venue (4–6 weeks out)
3. Promotion & Comms (3–4 weeks out)
4. Final Prep (1–2 weeks out)
5. Day-Of Execution (Day of event)
6. Post-Event & Follow-Up (Within 1 week after)

Each step has a full task list and Gem prompt. [Full task content is in the source HTML]

---

### Panel 3: Zoom Setup Guide (`#panel-zoom`)

**Header:**
- Title: "Configure your Zoom webinar"
- Description: "T4i no longer manages webinar setup. Use this guide every time you create a new Zoom webinar. These are the standard settings."

**T4i Production Assist callout**: "You still set up the Zoom webinar, but T4i runs slides day-of. Complete all settings below — T4i begins their role on event day (see dry run step to brief T4i on their role in Virtual track)."

**Two Setup Modes callout**: Explains self-run vs T4i-assisted modes.

**Google Sheets Banner** → links to: `https://docs.google.com/spreadsheets/d/1XcyZSnSSZBOzq0tP_nhiky7YTVBLS07l/edit?gid=998888117#gid=998888117`

**8 Setting Categories** (each as `.zoom-section`):
1. Registration: Required ON, auto-approve ON, close after event ON, multiple devices ON, social share ON
2. Video: Host OFF, Panelist ON, Attendee OFF
3. Audio: Both telephone and computer audio, mute all on entry ON
4. Webinar Options: Q&A ON, Practice Session ENABLE, HD video ENABLE, Auto-record IN THE CLOUD
5. Email Settings: Confirmation on registration, reminders at 1hr/1day/1week, banner updated, sender email correct series address
6. Polls: Single choice, download basic+individual breakdowns, allow panelists to vote
7. Q&A: Anonymous your choice, attendees view answered only
8. Survey: SurveyMonkey (NOT Zoom native), show in browser on end, backup post in chat

**Day-of Production Sequence Table:**
| Time | Action | T4i Instructions | Who |
|------|---------|-----------------|-----|
| 15 min before | Start Practice Session | Tech check, confirm video/audio, assign co-host roles, review slide flow | T4i / Host |
| At open | Admit attendees + play intro music | Open to attendees, play music loop | T4i |
| Start signal | Stop music → welcome slide | Stop music on moderator signal, advance to welcome slide | T4i |
| During webinar | Slide progression + polls | Advance slides per run-of-show, launch polls, allow panelist vote, share results | T4i |
| Chat duty | Post live chat messages | Post hiring links, academy links, survey link, job CTA | TM support |
| Q&A section | Q&A slide | Display blank/speaker slide (NOT presentation), moderate questions | T4i / Host |
| Closing | End webinar | Trigger post-event survey, play outro music, end webinar for all | T4i / Host |

---

### Panel 4: Governance & DACE (`#panel-governance`)

**Header:**
- Title: "Roles, responsibilities & event intake"
- Description: "Clear ownership prevents dropped balls. Use DACE to assign roles before every event — and use the intake criteria to right-size your planning approach."

**Event Intake / Triage Criteria** (4-tier table):
- Tier 1 Full COE Support: 500+ expected registrations, new event series or format, exec visibility or cross-functional stakeholders, budget >$5K
- Tier 2 Standard Planning: 100–499 registrations, established series with prior results, standard TM-owned workflow
- Tier 3 Light-Touch: <100 registrations, repeat/rebroadcast format, minimal new asset creation required
- Tier 4 Self-Serve: Internal team events, no external promotion, no Eloqua send required

**DACE Framework** explained:
- D = Driver (owns the outcome, makes final calls)
- A = Approver (must sign off before moving forward)  
- C = Contributor (provides input, executes assigned tasks)
- E = Executor (carries out specific day-of tasks)

**DACE Table — Virtual Events:**
Full table with rows for: Set event goals, Source/confirm speakers, Build Eloqua assets, Zoom setup, Email sends, Day-of production, Post-event reporting
Columns: Task | TM Lead | TA | T4i | Design (Scott)

**DACE Table — In-Person Events:**
Full table with rows for: Set event goals, Logistics & venue, Invitee list, Promotion, Day-of execution, Post-event follow-up
Columns: Task | TM Lead | TA | Conference Event Services | T4i

---

### Panel 5: Metrics & Reporting (`#panel-metrics`)

**Header:**
- Title: "Measure every event the same way"
- Description: "Standard KPI targets by event type, an individual event results log template, and the AI workflow for pulling and analyzing post-event data."

**KPI Cards — Virtual CP2E targets:**
- 20% Attendance rate
- +50 NPS score
- Weekly MQL goals set

**KPI Cards — Virtual Pro targets (ITS):**
- 28% Attendance rate
- 50+ NPS score
- 30% Email open rate
- 2% Click-through rate

**Post-Event AI Analysis Workflow** (3 steps):
- Step 1 — Aggregate your data sources: Collect Eloqua email report (CSV) + Zoom registration list + Zoom attendee list + Zoom poll results + SurveyMonkey export. Upload all to Notebook LM or paste into Event Gem.
- Step 2 — Event Gem Prompt: "Here are results from my [event name] on [date]. Attached: Eloqua email report, Zoom attendee list, poll results, SurveyMonkey export. Summarize: (1) key quantitative metrics vs. targets, (2) top 3 qualitative themes from survey comments, (3) what worked, (4) what to improve next time, (5) any candidates who should be flagged for recruiter follow-up based on their answers."
- Step 3 — Log it: Add a row to your personal event results log.

**My event results log — template** section:
- Subtitle: "Use this as a personal reference to track your own events over time — make a copy and add a row after each event you run."
- Link on word "template": `https://docs.google.com/spreadsheets/d/19_Hq9oEUCQm622QQjprMHyB6BwD-Tr46/edit?usp=sharing&ouid=111325661992984101647&rtpof=true&sd=true`
- Table with 12 columns: Event Name | Date | Type | Team | Registrants | Attendees | Att. Rate | NPS | Email Open Rate | Top Learning | Next Action | Full Deck
- 1 sample row: Intuit Tech Stories — SWE | Sep 10, 2025 | Virtual (Pro) | Pro | 820 | 198 | 24% | 54 | 32% | Attendees responded well to demo format — make demos recurring | Apply demo format to Oct webinar | ↗ View (unlinked)
- "Your next event goes here →" placeholder row

---

### Panel 6: Resources & Templates (`#panel-resources`)

**Header:**
- Title: "Everything in one place"
- Description: "All planning templates, creative assets, site guides, AI tools, and key partner contacts in one tab."

**Adobe Express Library callout** (in-progress banner):
"Standardized email banner templates and event creative are being built in Adobe Express."

**Section: Planning templates**
Buttons (`.resource-link`):
- 📋 Virtual Event Checklist → `https://docs.google.com/spreadsheets/d/1d7g-5snlq4G7unH8R4bLe71zlP7KW0fU/edit?usp=sharing&ouid=111325661992984101647&rtpof=true&sd=true`
- 📋 In-Person Event Checklist → `https://docs.google.com/spreadsheets/d/1NwmOPe9BssfRLQ8UJMC4VeDNUvQtlE4PWxUclQh6bIM/edit?gid=307869881#gid=307869881`
- 📝 T4i Briefing Template → `https://docs.google.com/document/d/173F31yF1FuEk02BCk83bLRY6i7Rsdnrc/edit?usp=sharing&ouid=111325661992984101647&rtpof=true&sd=true`

**Section: Creative assets**
Buttons:
- 🎨 Adobe Express Templates — Coming Soon (no link)
- 📐 Brand Guidelines (no link)

**Section: Site-specific in-person guide**
Buttons:
- 📍 Workplace Experience Site Guide → `https://docs.google.com/document/d/1ken5jNvcShYj7iRn1h4-jswlqvsgkILpexsSQSeUM9A/edit?tab=t.wwhll3vqq0bw#heading=h.964dbmly320v`

**Section: Event Gem**
"How to use the Event Gem" callout explaining what it is and how to access it.
Buttons:
- ✦ Open Event Gem (no link yet)
- 📄 Gem Knowledge Base Doc (no link yet)
- 📄 Gem Prompt Library (no link yet)

**Section: Key partner contacts** (table)
| Team / Function | Contact / Process | Used for |
|----------------|------------------|---------|
| T4i - Virtual Event Services | Submit support ticket → `https://intuit.service-now.com/sp?id=sc_cat_item&sys_id=1a1cd230db63f74003166451ca961924` | Day-of webinar production |
| Conference Event Services | Submit support ticket (same URL) + catering at all sites → `https://intuit.catertrax.com/index.asp?x=x?intCustomerID=%2A%7B%28%7E%C9` | Room reservations, A/V, catering |
| Tax Specialists (CP2E) | Priscilla Soto | Sourcing Tax Specialist speakers |
| Local Tax Experts (CP2E) | Kimberly Purvis & Carrie Gunnell | Sourcing Local Tax Expert speakers |
| Remote Bookkeeping Experts (CP2E) | Nikeita Wynn | Sourcing Remote Bookkeeping Expert speakers |
| Local Bookkeeping Experts (CP2E) | Luca Cataldo | Sourcing Local Bookkeeping Expert speakers |
| Scott (Design) | Internal design request | Major creative assets |
| SurveyMonkey | Team account — login in 1Password | All post-event surveys |
| Eloqua | Via campaign request form (CRF) | Email build, send, audience segmentation |

---

## Interactive Features (JavaScript)

### 1. Checkbox Toggle
- Each task has a `.task-check` div that toggles `.checked` class on click
- Checked state: dark ink background with white checkmark
- State persists via localStorage key: `tm_playbook_checks_v1`
- Storage format: JSON object keyed by `{panelId}::{taskText.slice(0,80)}`

### 2. Progress Bar
- Each panel has a `.progress-bar` and `.progress-count`
- Updates on every checkbox toggle
- Shows "X / Y complete" and fills bar proportionally

### 3. Reset Button
- Two-tap confirmation system (no `confirm()` dialog — blocked in some browsers)
- First tap: button turns orange, text changes to "Tap again to confirm"
- Second tap within 3 seconds: clears all checks for that panel
- Auto-resets back to normal if not confirmed within 3 seconds

### 4. Panel Navigation
- `.nav-tab` buttons call `showPanel(name, event)`
- Shows/hides `.panel` divs by toggling `.active` class
- Active tab gets bottom border in ink color

### 5. Step Card Expand/Collapse
- `.step-card` divs toggle `.expanded` class on click
- `.step-body` is `display:none` by default, shown when expanded
- `.step-expand` button rotates 45° when expanded (+ becomes ×)

---

## Tags / Badges

Task items can have inline tags:
```html
<span class="tag tag-ai">AI draft</span>       /* purple */
<span class="tag tag-zoom">Zoom</span>          /* blue */
<span class="tag tag-dace">TA assist</span>     /* navy */
<span class="tag tag-template">Template</span>  /* amber */
```

---

## Component Patterns

### Callout Box
```html
<div class="callout callout-tip">
  <div class="callout-title">Title</div>
  <p>Content</p>
</div>
```
Variants: `.callout-tip` (green), `.callout-warning` (amber), default (cream)

### Gem Prompt
```html
<div class="gem-prompt">
  <div class="gem-label">Event Gem Prompt</div>
  <div class="gem-text">"Prompt text here..."</div>
</div>
```

### Google Sheets Banner
```html
<div class="sheets-banner">
  <div class="sheets-banner-left">
    <div class="sheets-icon">📊</div>
    <div class="sheets-banner-text">
      <strong>Banner title</strong>
      <span>Description text</span>
    </div>
  </div>
</div>
<a class="sheets-link-btn" href="URL" target="_blank">↗ Open in Google Sheets</a>
```

### Resource Link Button
```html
<a class="resource-link" href="URL" target="_blank">
  <span class="link-icon">📋</span> Label
</a>
```

### Owner Badge (in Zoom table)
```html
<span class="owner-badge owner-t4i">T4i</span>
<span class="owner-badge owner-tm">TM host</span>
<span class="owner-badge owner-ta">TA</span>
```

---

## Key URLs Reference

| Resource | URL |
|----------|-----|
| Virtual Event Checklist (Google Sheets) | `https://docs.google.com/spreadsheets/d/1d7g-5snlq4G7unH8R4bLe71zlP7KW0fU/edit?usp=sharing` |
| In-Person Event Checklist (Google Sheets) | `https://docs.google.com/spreadsheets/d/1NwmOPe9BssfRLQ8UJMC4VeDNUvQtlE4PWxUclQh6bIM/edit?gid=307869881` |
| Zoom Setup Reference (Google Sheets) | `https://docs.google.com/spreadsheets/d/1XcyZSnSSZBOzq0tP_nhiky7YTVBLS07l/edit?gid=998888117` |
| T4i Briefing Template (Google Doc) | `https://docs.google.com/document/d/173F31yF1FuEk02BCk83bLRY6i7Rsdnrc/edit?usp=sharing` |
| My Event Results Log (Google Sheets) | `https://docs.google.com/spreadsheets/d/19_Hq9oEUCQm622QQjprMHyB6BwD-Tr46/edit?usp=sharing` |
| Workplace Experience Site Guide (Google Doc) | `https://docs.google.com/document/d/1ken5jNvcShYj7iRn1h4-jswlqvsgkILpexsSQSeUM9A/edit?tab=t.wwhll3vqq0bw` |
| T4i Support Ticket (ServiceNow) | `https://intuit.service-now.com/sp?id=sc_cat_item&sys_id=1a1cd230db63f74003166451ca961924` |
| CaterTrax (Catering) | `https://intuit.catertrax.com/index.asp?x=x?intCustomerID=%2A%7B%28%7E%C9` |

---

## What Makes This Different from FY25 Playbook

The FY25 playbook was a static PowerPoint. The 2.0 is:
1. **Interactive** — expandable steps, checkboxes, progress tracking
2. **Persistent** — localStorage saves checkbox state across sessions
3. **Unified** — CP2E and Pro workflows in one place (team-specific callouts inline)
4. **AI-integrated** — Gem prompts at every step
5. **Self-serve Zoom** — full setup guide (T4i no longer manages setup)
6. **Linked** — all templates, checklists, and contacts are live hyperlinks
7. **DACE-first** — role clarity built into every section

---

## Notes for Claude Code

- The source file `event_playbook_2.0.html` is the single source of truth — use it as the base
- All content is accurate as of April 15, 2026
- Placeholder buttons (Adobe Express, Event Gem links) are intentional — links TBD
- The Reset button intentionally avoids `confirm()` — use the two-tap pattern instead
- localStorage key is `tm_playbook_checks_v1` — do not change this key or existing user progress will be lost
- The dashboard is designed to be opened directly as a local HTML file OR hosted — no server required
- Do NOT add external JavaScript dependencies — keep it pure vanilla JS
- Google Fonts import is the only external dependency allowed
