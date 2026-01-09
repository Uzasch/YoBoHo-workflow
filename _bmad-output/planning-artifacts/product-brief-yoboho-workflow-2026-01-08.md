---
stepsCompleted: [1, 2, 3, 4, 5]
inputDocuments:
  - "_bmad-output/analysis/brainstorming-session-2026-01-08.md"
date: 2026-01-08
author: Uzair
partyModeInsights: true
---

# Product Brief: YoBoHo Internal Production Tool

## Executive Summary

**YoBoHo** is a YouTube-first content company managing 10+ active channels with internal and external production. As production scales, the biggest operational challenge is **transparency** - knowing what's happening across the production pipeline, who's working on what, and what's in everyone's queue.

Currently, handoffs between Writers, Editors, and Channel Managers happen via email. Channel managers often receive **no visibility at all** into what's ready for upload. This creates blind spots, delays, and the endless question: "Where is X?"

This internal tool solves that by providing a **production intelligence platform** - not just tracking what's happening, but surfacing what matters: What are editors working on? What's in their queue? How much did we produce this month?

**The dashboard IS the answer. Email is just the nudge. AI is the brain that queries production data instantly.**

### North Star Metric

> **Zero "where is X?" emails** - when people stop asking because the answer is always visible on the dashboard, we've won.

---

## Core Vision

### Problem Statement

YoBoHo's production team lacks transparency across the content pipeline. With 10+ channels actively producing, there's no single source of truth for:
- What stage each piece of content is in
- **What each editor is working on right now**
- **What's in each person's queue**
- When content is ready for upload
- When something is taking longer than usual

### Problem Impact

- **Lost time:** Managers spend hours chasing status updates via email
- **Missed handoffs:** Content sits waiting because the next person wasn't notified
- **Blind channel managers:** Currently receive NO visibility into what's ready - complete darkness
- **No production metrics:** Can't easily answer "how many scripts this month?"
- **Hidden delays:** Problems only surface when deadlines are missed

### Why Existing Solutions Fall Short

Generic project management tools (Asana, Monday, Notion) aren't built for content production intelligence. They lack:
- **Queue visibility** - seeing what someone is doing + what's waiting for them
- **AI-native architecture** - designed for "how many X this month?" queries
- **Production-specific workflows** - scripting → editing → upload pipeline
- **IP-centric organization** - view by channel/show, not just by task

### Proposed Solution

A **production intelligence platform** purpose-built for YoBoHo's video content operations.

**Architecture Principle:**
> We're not building a workflow tool and adding AI later.
> We're building an **AI-queryable production database** with a workflow UI on top.

**Core Capabilities:**

| Capability | Description |
|------------|-------------|
| **Canvas** | Design visual workflows with drag-drop process stages |
| **Dashboard** | Personal queue view - "What do I need to do?" |
| **Queue Visibility** | See what anyone is working on + what's in their queue |
| **AI Query Layer** | "What did editors do this month?" answered instantly |
| **Smart Dependencies** | Linear, partial, and simultaneous handoffs |

**Notification Philosophy:**
- Dashboard is primary - the answer is always visible
- Email is the nudge - "You have work" not comprehensive updates
- Simplicity over notification overload

### Key Differentiators

1. **AI-core architecture** - every action logged, timestamped, queryable from day one
2. **Production intelligence** - answers "what matters?" not just "what's happening?"
3. **Queue transparency** - see what they're doing + what's in their queue (that's bandwidth)
4. **Zero "where is X?" design** - if you have to ask, the dashboard failed
5. **Built for YoBoHo** - no compromises, exactly what video production needs

---

## V1 Scope: Video Production Focus

### Target Users

| User | What They Get | Current State |
|------|---------------|---------------|
| **Editors** | "My queue" - what to work on now + what's next | Email chaos |
| **Writers** | See editor queues before finishing scripts | Guessing |
| **Channel Managers** | "Ready to upload" list | **Nothing!** |
| **Leadership** | AI-powered production queries across all IPs | Asking around |

### Fixed vs Flexible Architecture

**Fixed (Same for all video workflows):**
```
┌─────────────┬───────────┬─────────┬──────────┬───────────┐
│ Not Started │ Scripting │ Editing │ Uploaded │ Completed │
└─────────────┴───────────┴─────────┴──────────┴───────────┘
      ↑ Major status categories (columns) - consistent across all workflows
```

**Flexible (User-defined):**
- Processes within each category (user creates via canvas)
- Approval gates (optional - some workflows have them, some don't)
- Process dependencies (linear, partial, simultaneous)

**Permissions:**
- Workflow edit: Admin OR workflow creator only
- Mid-stream edits: Allowed (with permission)

### Data Architecture (AI-Ready from Day 1)

```
Every state change is an event:
├── timestamp
├── ip_id
├── workflow_id
├── process_id
├── user_id
├── action (created, started, partial, completed)
├── metadata (time_spent, notes, files)

This enables:
├── "How many scripts this month?" → Instant answer
├── "What's taking too long?" → Anomaly detection
├── "What's Ali working on?" → Real-time queue view
```

### V1 Success Criteria

| Metric | Target |
|--------|--------|
| "Where is X?" emails | Zero |
| Editor knows their queue | Always visible |
| Channel manager knows what's ready | Always visible |
| Leadership can query production | AI answers instantly |

---

## Bandwidth Definition

> **Bandwidth = What they're doing + What's in their queue**

No calculations. No thresholds. No algorithms. Just transparency.

```
EDITOR: Ali
─────────────────────────────
🔵 WORKING ON NOW:
   Show A - Ep 5

📋 IN QUEUE:
   1. Show B - Ep 2
   2. Show C - Ep 8
   3. Show A - Ep 6
─────────────────────────────
Everyone sees this. No asking required.
```

---

## Complete Module Architecture

```
                              YOBOHO PRODUCTION TOOL
                                       │
    ┌──────────────┬───────────────────┼───────────────────┬──────────────┐
    │              │                   │                   │              │
 CANVAS        DASHBOARD           DATABASE            FEATURES        SYSTEM
 (Design)      (Views)             (Status)            (Intelligence)  (Foundation)
    │              │                   │                   │              │
    │              │                   │                   │              │
    ▼              ▼                   ▼                   ▼              ▼
```

### 1. CANVAS MODULE (Workflow Design)

| Component | Description |
|-----------|-------------|
| **Drag-Drop Builder** | Visual workflow creation |
| **Process Configuration** | Per-process settings |
| ↳ User/Group Assignment | Who works on this process |
| ↳ Dependency Type | Linear / Partial / Simultaneous |
| ↳ Category Assignment | Maps to major status column |
| ↳ Notification Settings | Email, WhatsApp, In-app |
| ↳ Data Schema | Custom fields, file uploads, required/optional |
| **Copy Workflow** | Duplicate existing workflows |
| **Gantt Preview** | See timeline before saving |

### 2. DASHBOARD MODULE (User Views)

**Module A: "My Work"**
| View | Description |
|------|-------------|
| Table | List of assigned tasks |
| Board | Kanban by process stage |
| Gallery | Card view by title |

**Module B: "Process Observatory"**
| Feature | Description |
|---------|-------------|
| Process Selector | Choose which process to view |
| All Tasks View | See all tasks in that process |
| Who's Working | See assignments across team |
| Date Range Filter | Filter by task active dates |
| **View Only** | Awareness without interference |

### 3. DATABASE MODULE (Status Tracking)

**Fixed Major Columns:**
```
┌─────────────┬───────────┬─────────┬──────────┬───────────┐
│ Not Started │ Scripting │ Editing │ Uploaded │ Completed │
└─────────────┴───────────┴─────────┴──────────┴───────────┘
```

- Processes are grouped under major categories
- Task moves through processes → lands in "Completed" when last process done
- Unified table structure across all workflows (Notion-style)

### 4. FEATURES MODULE (Intelligence & Tools)

**AI Chat (Core)**
| Capability | Example |
|------------|---------|
| Answer Questions | "What did editors do this month?" |
| Create Tasks | "Create episode 5 task for Show A" |
| Proactive Notify | "You have 2 shorts, 2 long pending" |
| Natural Language Dates | "What was completed last week?" |

**Gantt Chart**
| Level | Shows |
|-------|-------|
| IP Level | Major status category progress |
| Workflow Level | Individual sub-processes |

**Other Features**
| Feature | Description |
|---------|-------------|
| 🔍 Search | Find tasks, IPs, filter by status/assignee/date |
| 📁 File Management | Google Cloud integration |
| 🗄️ Archive | Time-travel view of completed work |
| 📋 Operational Tasks | Separate table for non-workflow tasks |

### 5. SYSTEM MODULE (Foundation)

**Hierarchy:**
```
IP (e.g., "Show A")
  └─► Workflow(s) (e.g., "Video Production", "Marketing")
        └─► Process(es) (e.g., Script, Screenplay, Edit)
              └─► Grouped by Major Status Category
```

**User Management:**
| Role | Permissions |
|------|-------------|
| Admin | Create workflows, edit any workflow, manage users |
| Producer | Create workflows, edit own workflows |
| Editor/Viewer | Use workflows only |

**Assignment Model:**
- Users assigned to **IP + Workflow** pair
- See all processes within their assignment

**Notifications:**
| Channel | Use |
|---------|-----|
| Email | "You have work" nudge |
| WhatsApp | Critical alerts |
| In-app | Dashboard primary |

**Workflow Permissions:**
- Edit: Admin OR workflow creator only
- Mid-stream edits: Allowed with permission

---

## Process Dependency Types

| Type | Behavior | Use Case |
|------|----------|----------|
| **Linear** | Wait for previous to fully complete | Script must finish before Screenplay starts |
| **Partial** | Start when previous clicks "Partially Done" | Screenplay can start when Scene 1 script done |
| **Simultaneous** | Run alongside previous/next process | Audio and Video edit in parallel |

```
LINEAR:        [A] ════════► [B] ════════► [C]
                    (wait)        (wait)

PARTIAL:       [A] ──◐──► [B] ──◐──► [C]
                 (partial)   (partial)

SIMULTANEOUS:  [A] ════╦════► [B]
                       ║
               [C] ════╝
                 (parallel)
```

---

## Target Users & Personas

### Primary Users

#### 1. Editor / Animator
**Who they are:** Video editors who receive screenplays and produce final content. They work on assigned tasks from script writers/producers.

**Current workflow:**
- Receive screenplay via email
- Edit video according to direction
- Complete and notify (somehow)

**Pain point:** When leadership asks "what did you do this month?" - they have no standard way to show their work. The data doesn't exist. It's frustrating to be asked questions they can't easily answer.

**What success looks like:**
- Open dashboard → see their queue clearly
- Complete work → it's automatically logged
- When asked "what did you do?" → instant proof of productivity

---

#### 2. Script Writer / Producer
**Who they are:** Creative leads who generate ideas, write scripts, create screenplays, and direct editors. Often work across multiple IPs. They ARE the producers - they direct the editing process.

**Current workflow:**
- Generate ideas
- Write scripts
- Create screenplays
- Email to editors with direction
- Wait and hope

**Pain point:** No visibility into editor queues. Don't know if their editor is available or buried in work.

**What success looks like:**
- See editor's current work + queue before finishing a script
- Know exactly when to hand off
- Direct editors with full visibility into their workload

---

#### 3. Channel Manager
**Who they are:** Responsible for uploading finished content to YouTube and other platforms.

**Current workflow:**
- Wait for someone to tell them content is ready
- Currently get NO notifications at all

**Pain point:** Complete blindness. They don't know what's ready to upload until someone manually tells them.

**What success looks like:**
- Dashboard shows "Ready to Upload" list
- No asking required - just look and upload

---

### Secondary Users

#### Leadership / Management
**Who they are:** Need production-wide visibility across all IPs and team members. Ask the big questions.

**Questions they constantly ask:**
- "How many scripts did we produce this month?"
- "What did the editors do?"
- "Where are the flaws/bottlenecks?"

**Pain point:** No standard data exists. Have to ask people individually, who then have to remember or reconstruct their work from memory.

**What success looks like:**
- Ask AI → get instant answer with data
- Glance at dashboard → know production status across all IPs
- Identify bottlenecks before they become crises

---

### Key User Insight

> **The frustration isn't with the WORK - it's with the REPORTING.**
>
> Editors do their job fine, but can't easily prove what they did.
> Leadership can't easily see what was produced.
> The data simply doesn't exist in a queryable format.
>
> **This tool creates that data automatically, as a byproduct of doing the work.**

---

## Success Metrics

### North Star Metric
> **Zero "where is X?" emails** - The dashboard answers every status question automatically.

---

### User Success Metrics

| Role | Success Indicator | Measurement |
|------|-------------------|-------------|
| **Editor** | Clearer picture of their work history | Can show "what I did" in n days/weeks without keeping separate records |
| **Editor** | Less confusion | Tasks and queue always visible, no ambiguity |
| **Script Writer** | One place for all records | All scripts, screenplays, assignments tracked in single system |
| **Channel Manager** | Clear picture of what's cooking | "In Progress" and "Ready to Upload" always visible |
| **Leadership** | All data in one place | No more piecing together info from multiple sources |
| **Leadership** | AI answers questions | "How many scripts this month?" answered in seconds |
| **Leadership** | Less meetings | Status meetings reduced or eliminated |
| **Leadership** | Accurate information | Data is real-time, not reconstructed from memory |

---

### Business Objectives (3-Month Goals)

| Objective | Target |
|-----------|--------|
| **Time chasing updates** | Reduced by 80%+ |
| **Visibility into bottlenecks** | Instant - see delays before they become crises |
| **Status meetings** | Reduced or eliminated for routine updates |
| **"Where is X?" questions** | Zero via email/chat - answered by dashboard |

---

### Key Performance Indicators

| KPI | How We'll Measure | Target |
|-----|-------------------|--------|
| **Status inquiry emails** | Count of "where is X?" messages | → 0 |
| **Time to answer production question** | Leadership query response time | < 30 seconds (via AI) |
| **Editor self-tracking effort** | Need for separate spreadsheets/notes | Eliminated |
| **Channel manager blindness** | Days content sits "ready" before upload | < 1 day |
| **Bottleneck detection** | Time to identify delays | Real-time (automatic flags) |

---

### Leading Indicators (Early Signs of Success)

| Indicator | What It Means |
|-----------|---------------|
| Editors check dashboard daily | Tool is useful, not ignored |
| Fewer Slack/WhatsApp status questions | Dashboard is the answer |
| Leadership uses AI queries weekly | Intelligence layer is valuable |
| Channel managers upload faster | Visibility reduces delays |

---

## MVP Scope

### Core Features (V1 Must-Have)

| Feature | Description | Why Essential |
|---------|-------------|---------------|
| **Canvas Module** | Drag-drop workflow builder with process configuration | Core tool for designing production pipelines |
| **Process Config** | Dependencies (linear/partial/simultaneous), user assignment, category mapping | Defines how work flows |
| **Dashboard - My Work** | Personal queue with Table/Board/Gallery views | Every user needs to see their tasks |
| **Dashboard - Observatory** | View-only access to any process within assigned IP+Workflow | Team awareness without interference |
| **Fixed Major Columns** | Not Started → Scripting → Editing → Uploaded → Completed | Consistent status tracking across all workflows |
| **AI Query Layer** | Natural language questions about production data | Core differentiator - instant answers |
| **Email Notifications** | "You have work" nudges when tasks are assigned/ready | Basic handoff enablement |
| **User Management** | Admin, Producer, Editor/Viewer roles with permissions | Access control foundation |
| **Data Architecture** | Event-based logging of all state changes | AI-ready from day one |

---

### Out of Scope for MVP

| Feature | Deferred To | Rationale |
|---------|-------------|-----------|
| Reporting dashboards with charts | V2 | AI queries cover basic needs; charts are polish |
| Comments/collaboration on tasks | V2 | Adds complexity; not solving core visibility problem |
| WhatsApp notifications | V2 | Start simple with email; expand channels later |
| Gantt chart editing | V2 | Preview-only in V1; editing adds complexity |
| Operational tasks table | V2 | Focus on video workflows first |
| Advanced analytics | V2+ | Build data foundation first, analyze later |
| Mobile app | V2+ | Web-first; mobile when core is proven |

---

### MVP Success Criteria

| Criteria | Validation Method |
|----------|-------------------|
| Editors see their queue clearly | User testing - can they find their tasks in <10 seconds? |
| Channel managers see "ready to upload" | Zero "what's ready?" questions after 2 weeks |
| Leadership can query production | AI answers "how many scripts this month?" accurately |
| "Where is X?" emails drop | Track before/after email counts |
| Team adopts dashboard | Daily active usage by >80% of team within 1 month |

---

### Future Vision (V2+)

**Short-term (V2):**
- WhatsApp/Slack notifications
- Reporting dashboards with charts
- Comments and collaboration
- Gantt chart editing
- Operational tasks table

**Medium-term (V3+):**
- Mobile app
- Advanced analytics and predictions
- Anomaly detection ("this is taking longer than usual")
- Bandwidth forecasting
- Integration with external tools (Google Drive, etc.)

**Long-term Vision:**
> YoBoHo's production intelligence platform becomes the single source of truth for all content operations - a real-time nervous system that shows what's happening, predicts what's coming, and ensures nothing falls through the cracks.

---

*Vision refined through Party Mode collaboration with PM, UX Designer, and Architect perspectives.*
