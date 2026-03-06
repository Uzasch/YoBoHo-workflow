---
stepsCompleted: [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11]
inputDocuments:
  - "planning-artifacts/product-brief-yoboho-workflow-2026-01-08.md"
workflowType: 'prd'
lastStep: 11
documentCounts:
  briefCount: 1
  researchCount: 0
  brainstormingCount: 0
  projectDocsCount: 0
---

# Product Requirements Document - yoboho-workflow

**Author:** Uzair
**Date:** 2026-01-09

## Executive Summary

**The problem:** YoBoHo manages multiple YouTube channels, and decisions stall because information is scattered. Editors piece together their queue from emails. Writers guess at editor bandwidth. Channel managers have to chase people to find out what's ready - no proactive visibility. Leadership asks "how many scripts this month?" and waits for someone to dig through records.

**The solution:** A production dashboard purpose-built for how YoBoHo actually works.

- An editor opens the dashboard → sees exactly what to work on next
- A writer checks an editor's queue → knows when to hand off
- A channel manager sees "ready to upload" → no chasing required
- Leadership asks a question → gets an answer in seconds

**Zero decision delays.** Everyone knows what to do next without asking. That's the win.

### What Makes This Special

This isn't Asana or Monday adapted to fit. It's built from scratch for YoBoHo's video production workflow:

- Fixed stages that match how we actually work (Not Started → Scripting → Editing → Uploaded → Completed)
- Queue visibility designed for our handoff patterns
- Channel manager dashboard that surfaces what's ready
- Every action logged and queryable from day one

## Project Classification

**Technical Type:** Internal Web Application
**Domain:** Media/Content Production Operations
**Complexity:** Medium
**Project Context:** Greenfield - new project

Multi-tenant at the IP/channel level. Standard RBAC. No external regulatory requirements.

## Success Criteria

### User Success

**The "Aha!" Moment:** Leadership asks "how many scripts this month?" and gets an instant answer. No digging, no asking around - the data just exists.

| Role | Success Indicator |
|------|-------------------|
| Editor/Animator | Opens dashboard → sees exactly what to work on, no ambiguity |
| Editor/Animator | Can show "what I did this month" without keeping separate records |
| Script Writer | All scripts, screenplays, assignments tracked in single system |
| Script Writer | Sees editor queue before finishing scripts → knows when to hand off |
| Channel Manager | "Ready to Upload" always visible → no chasing required |
| Leadership | Asks production question → gets answer in seconds |

### Business Success

**3-Month Targets:**
- Core production team (editors, script writers, animators) using dashboard daily
- Time chasing updates reduced significantly
- Status meetings reduced or eliminated for routine updates
- Zero "where is X?" questions via email/chat

**Minimum Viable Adoption:** Editors, script writers, and animators using the system daily. Channel managers and leadership adoption is secondary - if the core crew adopts, data flows automatically.

### Technical Success

**Priority Order:**
1. **Data Accuracy (Non-negotiable):** Queue and status are always correct. If the queue lies once, trust is destroyed.
2. **Performance:** Page load < 2 seconds
3. **Availability:** Reliable during production hours (9-5). Downtime outside hours is acceptable.

### Measurable Outcomes

| Metric | Target |
|--------|--------|
| "Where is X?" emails | → 0 |
| Time to answer production question | < 30 seconds (via AI) |
| Editor self-tracking effort | Eliminated |
| Days content sits "ready" before upload | < 1 day |
| Bottleneck detection | Real-time |
| Core team daily usage | 100% of editors, writers, animators |

## Product Scope

### MVP - Minimum Viable Product

| Feature | Description |
|---------|-------------|
| Personal Queue Dashboard | Editors, writers, animators see their work (Table/Board/Gallery views) |
| Fixed Major Columns | Not Started → Scripting → Editing → Uploaded → Completed |
| Workflow Canvas | Drag-drop builder to define processes |
| Queue Visibility | See what anyone is working on + what's in their queue |
| Email Notifications | "You have work" nudges on assignment |
| AI Query Layer | Natural language questions ("how many scripts this month?") |
| Channel Manager Dashboard | "Ready to Upload" list - no chasing required |
| Gantt Chart Preview | Timeline view of workflow progress |

### Growth Features (Post-MVP)

- WhatsApp/Slack notifications
- Comments and collaboration on tasks

### Vision (Future)

- Mobile app
- Advanced analytics and predictions
- Anomaly detection ("this is taking longer than usual")
- Bandwidth forecasting
- Integration with external tools (Google Drive, etc.)

## User Journeys

### Journey 1: Ali the Editor - Finally, Proof of Work

Ali is an editor who works on assigned tasks from producers. When leadership asks "what did you do this month?" he has no standard way to show his work. The data doesn't exist. It's frustrating to be asked questions he can't easily answer.

**Before YoBoHo:** Monday morning. Ali opens his email, scrolls through 15 messages trying to figure out what's urgent. There's a screenplay from last week he forgot about. A producer is asking "did you start on Episode 5?" He's not sure - he has three projects half-done. He spends 20 minutes just figuring out what to work on.

**After YoBoHo:** Monday morning. Ali opens the dashboard. His queue is right there - Episode 5 is first, Episode 7 behind it, then the short for Channel B. He clicks "Start" on Episode 5, works for 4 hours, clicks "Complete." Done. No email. No "did you start?" questions. It's just... tracked.

**The breakthrough:** End of month. Leadership asks "what did editors produce?" Ali doesn't panic. He doesn't scramble through emails. He just... exists in the data. His work speaks for itself.

---

### Journey 2: Fatima the Producer - Timing the Handoff

Fatima generates ideas, writes scripts, creates screenplays, and directs editors. She has no visibility into editor queues. She doesn't know if her editor is available or buried in work.

**Before YoBoHo:** Thursday afternoon. Fatima just finished a killer screenplay for Episode 12. It's 4pm. She wants to hand it off to Ali, but... is he swamped? She checks Slack - no response. She sends an email asking "hey, bandwidth?" and waits. By the time Ali responds the next morning, she's moved on to something else. The handoff happens 18 hours later than it needed to.

**After YoBoHo:** Thursday afternoon. Fatima finishes Episode 12's screenplay. Before assigning it, she glances at Ali's queue - he's working on Episode 5, with Episode 7 next. Two items. She assigns Episode 12, it slots into position 3. Ali gets a notification. No waiting. No asking. She knows exactly when to expect it done based on his current load.

**The breakthrough:** Fatima starts planning her scripts around editor bandwidth. She checks queues *before* she starts writing, prioritizing screenplays for editors who are almost free. Production flows smoother because handoffs are timed, not random.

---

### Journey 3: Samir the Channel Manager - No More Chasing

Samir manages 3 channels. He waits for someone to tell him content is ready. Currently gets no notifications at all. Complete blindness until someone manually tells him.

**Before YoBoHo:** Every morning Samir sends the same message to 4 different people: "Anything ready for upload?" Sometimes he gets responses. Sometimes he doesn't. Last Tuesday, a finished video sat for 3 days because no one told him it was done. The algorithm doesn't forgive late uploads. He feels like he's always chasing, always behind.

**After YoBoHo:** Samir opens his dashboard. Three items in "Ready to Upload" - Episode 5 for Channel A, a short for Channel B, Episode 12 for Channel C. No chasing. No asking. He uploads Episode 5, marks it "Completed." The item disappears from his queue. He checks back after lunch - one new item appeared. Ali finished something. Samir didn't have to ask.

**The breakthrough:** For the first time, Samir feels *ahead*. He schedules uploads 2 days in advance because he can see what's coming through the pipeline. He stops being reactive. He starts being strategic.

---

### Journey 4: Uzair the CEO - Instant Answers

Uzair needs production-wide visibility across all channels and team members. He asks "how many scripts did we produce this month?" and has to ask people individually, who reconstruct from memory.

**Before YoBoHo:** End of month. Board wants production numbers. Uzair sends a message: "Team, how many videos did we produce in January?" He waits. Fatima guesses 12. Ali says "maybe 15?" Channel managers check their upload history. Three different spreadsheets get created. Numbers don't match. Uzair spends 2 hours reconciling data that should have taken 2 minutes.

**After YoBoHo:** End of month. Board wants production numbers. Uzair opens the AI chat: "How many videos were completed in January?" The answer comes instantly: "47 videos completed across 10 channels. 32 long-form, 15 shorts. Channel A led with 8 videos. Average time from script to upload: 6.2 days." Done. No asking. No waiting. No reconciling spreadsheets.

**The breakthrough:** Uzair starts asking different questions. Not "how many?" but "where are the bottlenecks?" and "which channel is behind schedule?" He shifts from counting to optimizing - because counting is now automatic.

---

### Journey 5: Hira the Admin - Workflows in Minutes

Hira is the operations person who keeps YoBoHo running. When a new channel launches or a new editor joins, she coordinates everything manually. There's no standard process.

**Before YoBoHo:** New channel launching? Hira creates Slack channels, email lists, shared folders. New editor joining? She introduces them to everyone via email and hopes they figure out the workflow. Every channel does things slightly differently. Onboarding takes weeks.

**After YoBoHo:** New channel launching? Hira opens the Canvas, duplicates an existing workflow template, adjusts a few process names, assigns the team. Done in 10 minutes. New editor joining? She adds them to the system, assigns them to their IP + Workflow pair, and they see their queue on day one. No guessing. No hoping.

**The breakthrough:** A producer wants to add an approval step before upload. Old world: meetings, emails, figuring out how to communicate the change. New world: Hira drags an "Approval" process into the workflow, assigns the approver, saves. Everyone sees it immediately. Workflow changes go from weeks to minutes.

---

### Journey Requirements Summary

| Journey | Capabilities Revealed |
|---------|----------------------|
| **Ali (Editor)** | Personal queue dashboard, task status tracking, work history logging, "Start/Complete" actions |
| **Fatima (Producer)** | Queue visibility for others, task assignment, workload transparency |
| **Samir (Channel Manager)** | "Ready to Upload" filtered view, status-based dashboard, completion tracking |
| **Uzair (Leadership)** | AI query layer, production analytics, cross-channel visibility |
| **Hira (Admin)** | Workflow canvas builder, template duplication, user management, permission assignment |

## Innovation & Novel Patterns

### Detected Innovation Areas

**1. Adaptation Spawning (One-to-Many Content Multiplication)**

Traditional task trackers assume 1 input = 1 output. YoBoHo handles content multiplication where one source spawns multiple derivative tasks.

**Pattern:**
- Script writer creates one script
- Selects "adaptation" option during handoff
- Chooses target IPs (channels) for adaptation
- System auto-spawns independent tasks for each selected IP
- Spawned tasks labeled "adaptation - {title}"
- Parent and children become independent after spawn (no linked tracking)

**Canvas Implication:** Workflow canvas needs a "spawn node" element that can multiply tasks at runtime based on IP selection. The visual design shows branching capability; actual task count is determined at execution time.

**2. Non-Linear Process Dependencies**

Traditional workflow: A → B → C (strictly sequential)
YoBoHo workflow: Flexible dependency types enabling parallel work streams.

**Dependency Types:**

| Type | Behavior |
|------|----------|
| Linear | Next process waits for complete finish |
| Parallel | Multiple processes run simultaneously |
| Partial | Next process starts when previous is partially done |

**Key Flexibility:** Same person can be assigned to parallel processes - the system doesn't enforce different assignees.

### Validation Approach

**Adaptation Spawning:**
- Validate with script writers: Does the spawn flow match how they think about adaptations?
- Test with real content: One script → multiple IP spawns → verify tasks created correctly
- Edge case: What if user selects 0 IPs? What if they select 10?

**Non-Linear Dependencies:**
- Validate with production team: Do partial handoffs match real workflow patterns?
- Test blocking scenarios: If one parallel process blocks, verify others continue independently

### Risk Mitigation

**Adaptation Spawning Risks:**
- Complexity: Spawn logic adds complexity to task creation flow
- Fallback: Manual entry if spawn UX proves confusing

**Non-Linear Dependency Risks:**
- User confusion: People expect linear flows
- Mitigation: Clear visual indicators in canvas and dashboard showing dependency type

## SaaS B2B Specific Requirements

### Project-Type Overview

Internal web application with SaaS B2B characteristics. Multi-tenant architecture at the IP (channel/show) level. No external customer billing or subscription management - this is a purpose-built internal tool for YoBoHo's production operations.

### Tenant Model

**Tenancy Level:** IP (Channel/Show)

Each IP operates as a logical tenant:
- Users are assigned to IP + Workflow pairs
- Data is scoped to IP level
- Cross-IP visibility for leadership/admin roles only
- Workflows can be duplicated across IPs but run independently

**Tenant Isolation:**
- Task data isolated per IP
- User assignments scoped to specific IPs
- AI queries can span IPs for leadership (cross-tenant reporting)

### RBAC Matrix

| Role | Create Workflows | Edit Any Workflow | Edit Own Workflow | Use Workflows | Manage Users | View All IPs |
|------|------------------|-------------------|-------------------|---------------|--------------|--------------|
| Admin | Yes | Yes | Yes | Yes | Yes | Yes |
| Producer | Yes | No | Yes | Yes | No | Assigned IPs |
| Editor/Viewer | No | No | No | Yes | No | Assigned IPs |

**Assignment Model:**
- Users assigned to IP + Workflow pair
- See all processes within their assignment
- Can view queue of others within same IP

### Subscription Tiers

**Not Applicable** - Internal tool with no external billing or tiered access. All YoBoHo team members get full access based on their role permissions.

### Integration Requirements

| Integration | Purpose | Priority |
|-------------|---------|----------|
| **YouTube API** | Upload tracking, publish status, video metadata | MVP |
| **Google Cloud Bucket** | File storage for scripts, screenplays, assets | MVP |

**YouTube API Integration:**
- Track when content is uploaded to YouTube
- Sync publish status back to dashboard
- Enable "Uploaded → Completed" status transitions

**Google Cloud Bucket Integration:**
- Store and retrieve production assets
- Link files to tasks (scripts, screenplays, raw footage references)
- Shared access based on IP assignment

### Compliance Requirements

**External Compliance:** None required (not healthcare, fintech, or regulated industry)

**Internal Data Handling:**
- Production data stays within YoBoHo systems
- Standard access controls via RBAC
- No special data retention or audit requirements

### Implementation Considerations

**Technical Architecture:**
- Web application (browser-based)
- Event-driven data layer for AI queryability
- Real-time updates for queue visibility
- Responsive design for desktop use (9-5 tool, not mobile-first)

**Performance Requirements:**
- Page load < 2 seconds
- Real-time queue updates
- AI query response < 30 seconds

**Availability:**
- Production hours (9-5) critical
- Acceptable downtime outside production hours

## Project Scoping & Phased Development

### MVP Strategy & Philosophy

**MVP Approach:** Problem-Solving MVP
Solve the core transparency problem with minimal features. If editors see their queue and leadership can query production data, we've validated the concept.

**Success Criteria for MVP:**
- Core production team using dashboard daily
- Zero "where is X?" questions
- AI answers production queries in < 30 seconds

### MVP Feature Set (Phase 1)

**Core User Journeys Supported:**
- Ali (Editor): Queue visibility, task tracking, work history
- Fatima (Producer): Queue visibility for others, task assignment
- Samir (Channel Manager): "Ready to Upload" dashboard
- Uzair (Leadership): AI query layer
- Hira (Admin): Workflow canvas, user management

**Must-Have Capabilities:**

| Feature | Rationale |
|---------|-----------|
| Personal Queue Dashboard | Core user value - everyone sees their work |
| Fixed Major Columns | Consistent status tracking across workflows |
| Workflow Canvas | Define processes with dependency types (linear/parallel/partial) |
| Queue Visibility | See what anyone is working on + their queue |
| Email Notifications | "You have work" nudges |
| AI Query Layer | Leadership's "aha!" moment - instant production answers |
| Channel Manager Dashboard | "Ready to Upload" visibility |
| Gantt Chart Preview | Timeline view of workflow progress |
| YouTube API Integration | Track upload status |
| Google Cloud Bucket | File storage for assets |

**Explicitly NOT in MVP:**
- Adaptation spawning (one-to-many) - moved to Growth
- WhatsApp/Slack notifications
- Comments and collaboration
- Mobile app

### Post-MVP Features

**Phase 2 (Growth):**
- Adaptation Spawning - one script spawns multiple IP tasks
- WhatsApp/Slack notifications
- Comments and collaboration on tasks
- Advanced notification preferences

**Phase 3 (Vision):**
- Mobile app
- Advanced analytics and predictions
- Anomaly detection ("this is taking longer than usual")
- Bandwidth forecasting
- Additional external integrations

### Risk Mitigation Strategy

**Technical Risks:**

| Risk | Mitigation |
|------|------------|
| AI Query Layer complexity | Start with predefined query templates, expand to natural language |
| Real-time updates at scale | Design for current team size (~20-50 users), optimize later |
| Non-linear dependencies | Clear visual indicators, user education |

**Market Risks:**

| Risk | Mitigation |
|------|------------|
| Team adoption resistance | Start with editors (biggest pain), let success spread |
| Feature creep during MVP | Strict scope boundaries, defer to Growth phase |

**Resource Risks:**

| Risk | Mitigation |
|------|------------|
| Smaller team than planned | Core dashboard + queue can ship with 1-2 developers |
| Timeline pressure | AI query layer can be simplified (template-based) if needed |

## Functional Requirements

### Dashboard & Queue Management

- FR1: Editors can view their personal task queue showing current work and upcoming assignments
- FR2: Editors can see tasks in multiple view formats (Table, Board, Gallery)
- FR3: Users can filter their queue by status, IP, or workflow
- FR4: Users can see another user's current task and queue (bandwidth visibility)
- FR5: Channel Managers can view a filtered "Ready to Upload" dashboard showing all completed content awaiting upload
- FR6: Users can mark tasks as "Started" to indicate active work
- FR7: Users can mark tasks as "Complete" to move them to the next process
- FR8: Users can mark tasks as "Partially Complete" to enable partial handoffs

### Workflow Canvas & Process Design

- FR9: Admins can create new workflows using a visual drag-drop canvas
- FR10: Admins can define processes within a workflow and assign them to major status columns
- FR11: Admins can assign each workflow process to a major column (Not Started, Scripting, Editing, Uploaded, Completed)
- FR12: Multiple processes can be assigned to the same major column within a workflow
- FR13: Admins can configure process dependency types (Linear, Parallel, Partial)
- FR14: Admins can assign users or groups to specific processes
- FR15: Admins can configure notification settings per process
- FR16: Admins can define custom data fields per process (text, files, dropdown, required/optional)
- FR17: Producers can create workflows for IPs they are assigned to
- FR18: Producers can edit workflows they created
- FR19: Users can duplicate existing workflows as templates
- FR20: Users can preview workflow as Gantt chart before saving

### Task Management

- FR21: Users can create new tasks within a workflow
- FR22: Users can assign tasks to specific users
- FR23: Users can add titles and metadata to tasks
- FR24: Users can attach files to tasks (linked to Google Cloud Bucket)
- FR25: Users can view task history showing all state changes with timestamps
- FR26: System automatically logs all task state changes as events
- FR27: Tasks automatically move through workflow based on process completion
- FR28: Tasks inherit their major column status from their current process assignment

### Workflow Table View (Notion-style)

- FR29: Users can view all tasks within a workflow in a Notion-style table with customizable columns
- FR30: Table columns display custom fields defined for that workflow's processes
- FR31: Users can sort workflow table by any column/field
- FR32: Users can filter workflow table by any column/field value
- FR33: Users can group workflow table rows by any field (e.g., by assignee, by status, by major column)
- FR34: Users can switch workflow view between Table, Board, and Gallery formats
- FR35: Board view groups tasks by major column (status)

### User & Permission Management

- FR36: Admins can create and manage user accounts
- FR37: Admins can assign users to roles (Admin, Producer, Editor/Viewer)
- FR38: Admins can assign users to IP + Workflow pairs
- FR39: Users can only see IPs and workflows they are assigned to (except Admins)
- FR40: Admins can view and manage all IPs and workflows
- FR41: Users can view their own profile and assignment information

### AI Query Layer

- FR42: Leadership can ask natural language questions about production data
- FR43: AI can answer questions about task counts (e.g., "how many scripts this month?")
- FR44: AI can answer questions about user activity (e.g., "what did editors complete?")
- FR45: AI can answer questions about status distribution (e.g., "what's in editing?")
- FR46: AI can answer questions across multiple IPs for users with cross-IP access
- FR47: AI responses include relevant data context (counts, dates, breakdowns)

### Notifications

- FR48: Users receive email notifications when tasks are assigned to them
- FR49: Users receive email notifications when a task enters their process queue
- FR50: Admins can configure which events trigger notifications per workflow
- FR51: Users can view notification history in the application

### Integrations

- FR52: System can sync task status with YouTube upload status
- FR53: Users can link Google Cloud Bucket files to tasks
- FR54: System can retrieve file metadata from Google Cloud Bucket for display

### Reporting & Visibility

- FR55: Users can view Gantt chart showing workflow progress for an IP
- FR56: Users can view production status across fixed major columns (Not Started → Scripting → Editing → Uploaded → Completed)
- FR57: Leadership can view cross-IP production dashboards
- FR58: Users can view their own work history for any time period

## Non-Functional Requirements

### Performance

| Requirement | Target | Rationale |
|-------------|--------|-----------|
| Page load time | < 2 seconds | Users check queue frequently, must be instant |
| AI query response | < 30 seconds | Leadership expects quick answers |
| Real-time updates | < 5 seconds | Queue changes should reflect quickly |
| Concurrent users | 50 simultaneous | Current team size with headroom |

### Security

| Requirement | Specification |
|-------------|---------------|
| Authentication | Secure login required for all users |
| Authorization | RBAC enforced - users only see assigned IPs/workflows |
| Data access | IP-level tenant isolation |
| Session management | Auto-logout after inactivity period |

**Note:** Internal tool with no payment processing or highly sensitive PII. Standard security practices apply.

### Reliability

| Requirement | Target | Rationale |
|-------------|--------|-----------|
| Data accuracy | 100% | If queue lies once, trust is destroyed |
| Availability (9-5) | 99% | Production hours are critical |
| Availability (off-hours) | Best effort | Downtime acceptable outside 9-5 |
| Data durability | No data loss | All events must be persisted |

### Integration

| Integration | Reliability Requirement |
|-------------|------------------------|
| YouTube API | Graceful degradation - system works if YouTube is down |
| Google Cloud Bucket | File links work; uploads/downloads should not block core workflow |

### Scalability (Deferred)

**Current design target:** ~50 concurrent users

**Future consideration:** If YoBoHo expands significantly, scalability review needed. For MVP, design for current team size and optimize later.
