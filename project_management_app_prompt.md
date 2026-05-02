# Master Prompt: Build "PulseBoard" — An Agentic, Self‑Serve **AI Project & Adoption Intelligence Platform**

> **Use this prompt as-is** with Claude Code, Cursor, Windsurf, GitHub Copilot Workspace, or any agentic coding tool. It is written so a single coding agent can scaffold and ship a runnable, GCP‑deployable product end-to-end.

---

## ROLE & MISSION

You are a senior full‑stack engineer + product designer + data engineer + GCP DevOps engineer. You will design, build, document, and package a **production‑grade web application** called **PulseBoard** that serves as the **single source of truth for the enterprise's central AI team** to track every AI initiative across Business Units (Retail, Wealth, Corporate Banking, Insurance, etc.) and Group Functions (HR, Procurement, Finance, Risk, Legal, Operations, etc.).

The platform answers two questions that the central AI team and its stakeholders ask every day:

1. **"Where is each AI project in its lifecycle, and is it on track?"** — covering the AI-specific stages of *Ideation → Use-Case Qualification → PoC → Pilot → Production → Scale → Sunset*.
2. **"After we shipped the AI solution — are the business users actually using it, and is it delivering the promised value?"** — covering model invocations, user adoption, ROI realization, accuracy/quality drift, and feedback signals.

The primary users are:
- **Head of AI / Chief AI Officer** — needs portfolio-level health across all BUs and functions
- **AI Product Managers / AI Project Leads** in the central AI team — own delivery
- **BU Heads & Function Heads** (HR Head, Procurement Head, Wealth Head, etc.) — sponsors who need confidence that their funded AI initiatives are progressing and adopted
- **AI Engineering Leads** — track build/deploy status
- **Governance / Risk officers** — track model risk, compliance, and adoption-vs-policy

The landing experience is **conversational and agentic** — an AI assistant (powered by **Google Gemini** via Vertex AI, with **Gemma** as a self-hosted fallback) where leaders can ask any question about any AI project or adoption metric in natural language and get a grounded, cited answer with inline charts.

The platform is **fully self-serve**: BU/function teams onboard their own Jira projects, upload manual trackers when Jira isn't available, and define their own adoption KPIs by registering APIs/pipelines — **without engineering intervention from the central AI platform team**.

---

## NORTH-STAR USER STORY

> Priya, the Chief AI Officer, opens PulseBoard on Monday morning. Single sign-on via Entra ID is invisible — she's already in. The landing page greets her with: *"Good morning Priya. The AI portfolio has 47 active initiatives across 9 BUs. 3 slipped against baseline last week — 'Procurement Contract Summarizer' (Procurement), 'KYC Document Intelligence' (Risk), and 'Wealth Advisor Copilot' (Wealth). Adoption on 'HR Policy Bot' crossed 4,200 weekly active employees, ahead of the Q2 target of 3,500. Two models flagged for accuracy drift: 'Loan Risk Scorer v2' is down 6pp on F1 since last Thursday. Want a deep dive?"*
>
> She types: *"Why did Procurement Contract Summarizer slip?"* The AI replies with the specific Jira tickets that moved out of the sprint, the data-access dependency on the Procurement team that's blocking it, the new forecast go-live, and a one-click drill-through to the project page.
>
> She then types: *"Show me adoption funnel for HR Policy Bot by employee grade and region."* A live chart renders inline — invocations → resolved-without-escalation → CSAT ≥4 — sliced by grade and APAC/EMEA/AMER.
>
> She didn't open Jira. Didn't open BigQuery. Didn't open MLflow. Didn't ping six people. **That is the product.**

---

## DOMAIN MODEL — AI PROJECTS ARE NOT GENERIC PROJECTS

This is **not** a generic project tracker dressed up. The data model and the AI agent's reasoning must understand AI-specific concepts natively:

### AI Project Lifecycle Stages (the canonical pipeline)
1. **Ideation** — use-case captured, business hypothesis stated
2. **Qualification** — feasibility + value-vs-effort scored, data availability checked, GO/NO-GO
3. **PoC** — small-scale build, success criteria defined upfront
4. **Pilot** — limited user group, real environment, measured outcomes
5. **Production** — live for the full target audience
6. **Scale** — expanding to additional BUs / regions / use-cases
7. **Sunset** — deprecation path

### AI-Specific Project Attributes
- **AI Pattern** — Predictive ML / Generative AI / Agentic / Computer Vision / NLP / Recommendation / Optimization / RPA-with-AI
- **Model dependency** — foundational model used (Gemini, Claude, GPT, in-house fine-tune, classical ML)
- **Data sensitivity** — Public / Internal / Confidential / Restricted (PII, PCI, MNPI)
- **Governance status** — Model Risk Tier (1/2/3), Responsible-AI review status, DPIA status
- **Sponsoring BU / Function** + **Delivering team** (often the central AI team itself)
- **Expected business value** — quantified (₹/$ saved, hours saved, NPS lift, revenue uplift) + realized value tracked separately
- **Technical stack** — vector DB, orchestration framework, deployment target

### AI-Specific Risks & Issues (first-class entities, not just generic "risks")
- Data access / quality / drift
- Model accuracy / bias / fairness
- Hallucination rate (for GenAI)
- Latency / cost-per-call
- Governance/compliance blockers
- User trust / change-management
- Integration / API stability
- Dependency on external model providers (rate limits, deprecations, version changes)

### AI-Specific Adoption KPIs (build a starter library; users can still define their own)
- **Usage** — DAU/WAU/MAU, invocations/day, sessions, queries-per-user
- **Quality** — thumbs-up rate, CSAT on AI responses, escalation-to-human rate, accuracy on golden set
- **Funnel** — eligible-users → activated → recurring → power-users
- **Value realization** — hours saved, deflection rate, conversion lift, ₹ saved (vs baseline)
- **Health** — error rate, p95 latency, cost per 1k calls, model invocation success rate
- **Trust & safety** — flagged response rate, policy violation rate, override rate

The AI agent must understand all of the above as native vocabulary — when a Function Head asks *"is the HR Bot drifting?"*, the agent should know to look at quality KPIs over time, not generic schedule variance.

---

## DELIVERABLES (all must be produced)

1. **Full application source code** — frontend + backend + agent service + data pipelines + infra-as-code, in a single mono-repo.
2. **Self-serve onboarding flows** for: (a) Jira instances + projects, (b) manual project tracker uploads, (c) adoption KPI definitions via API/pipeline registration.
3. **AI Project management module** — portfolio overview, AI-stage-aware Kanban, baseline-vs-actual, RAG status, schedule variance, AI-specific risk register, milestone tracking, slice-and-dice by BU / function / AI pattern / governance tier / sponsor / quarter / status.
4. **Adoption analytics module** — KPI builder, funnel analysis, cohort analysis, WAU/MAU/DAU, feature-level usage heatmaps, value-realization tracking, pattern detection.
5. **Agentic AI landing page** — natural-language Q&A over both project and adoption data, with tool use, citations, and inline visualizations.
6. **How-to Guide #1** — *Onboarding an AI Project* (Jira-based + manual upload).
7. **How-to Guide #2** — *Onboarding Adoption KPIs* (API + pipeline + manual).
8. **How-to Guide #3** — *Entra ID setup* (for the IT/identity admin).
9. **GCP deployment guide** — one-command deploy, with all required services, IAM, secrets, and cost expectations.
10. **README + architecture diagram + data model + API reference**.
11. **Seed data + demo mode** so the app is immediately useful on first boot.

---

## DESIGN LANGUAGE — NON-NEGOTIABLE

The UI **must not** look like a typical enterprise dashboard. No SAP-grey tables. No Bootstrap-default cards. No generic Material UI. Aim for the aesthetic intersection of **Linear + Vercel + Arc Browser + Raycast + Notion AI**.

**Mandatory visual principles:**

- **Dark-first, light optional.** Default theme is a deep neutral (`#0A0A0F` background, `#13131A` surface) with a single vibrant accent (electric violet `#8B5CF6` or aurora green `#10F2A0` — pick one and commit). Light theme is true off-white `#FAFAF7`, never pure white.
- **Typography hierarchy with personality.** Use **Geist Sans** (or Inter Tight) for UI, **Geist Mono** for numbers, IDs, and code. Display headings in a tighter weight (500/600), never 700+. Numbers are *always* tabular-figures aligned.
- **Glass + grain.** Subtle backdrop-blur on overlays, a 2% noise texture on large surfaces. Never flat-flat.
- **Motion is meaningful.** Use **Framer Motion**. Spring physics for entrance, ease-out for exit. Layout animations on filter/sort. No bouncing for the sake of bouncing.
- **Density that adapts.** Three density modes: Comfortable / Compact / Tactical (tactical = trader-screen, every pixel earns its keep).
- **Command palette is the spine.** `⌘K` opens a Raycast-style palette that can navigate, query the AI, run actions ("set RAG to amber on Project X"), and onboard new sources. The palette is the *fastest* path to anything.
- **Charts feel native, not Chart.js.** Use **Recharts or Visx** with custom styling — thin 1px gridlines at 10% opacity, monospace axis labels, animated draw-in, hover states with magnetic crosshair.
- **Status uses iconography + color + text** — never color alone (accessibility). On-track = subtle dot + "On Track", at-risk = pulsing amber dot + "At Risk".
- **AI-stage pill** is a custom UI primitive — a horizontal connected-dot pipeline showing all 7 stages, with the current stage glowing. Used everywhere a project is referenced.
- **Empty states are illustrated and helpful** — never just "No data." Always explain what the user can do next.
- **AI responses stream** with a subtle shimmer cursor, render markdown + inline charts + clickable citations to source records.

**Reference vibe:** Linear's project view, Vercel's analytics page, Notion AI's Q&A panel, Arc's command bar, Stripe's dashboard chart styling.

---

## TECHNICAL ARCHITECTURE

### Stack (use exactly this unless you have a strong reason to substitute)

**Frontend**
- **Next.js 14+ (App Router)** with TypeScript, React Server Components where sensible
- **Tailwind CSS** + **shadcn/ui** as the component primitive layer (then *restyle* — do not ship shadcn defaults)
- **Framer Motion** for all animation
- **Recharts** for charts; **Visx** for anything bespoke (heatmaps, funnels, cohort triangles)
- **TanStack Query** for server state, **Zustand** for ephemeral UI state
- **`cmdk`** for the command palette
- **`react-markdown` + `rehype-highlight`** for AI message rendering

**Backend**
- **Python 3.11 + FastAPI** for the main API (async)
- **Pydantic v2** for all schemas
- **SQLAlchemy 2.0 + Alembic** for ORM/migrations
- **Celery + Redis** (or Cloud Tasks) for background jobs (Jira sync, pipeline ingestion)

**Data Layer**
- **PostgreSQL (Cloud SQL)** — operational store: projects, users, KPI definitions, AI chat history
- **BigQuery** — analytics store: time-series adoption events, project history snapshots, model telemetry
- **GCS** — manual file uploads, generated exports, KPI pipeline staging

**Identity & Access — Microsoft Entra ID (Azure AD)**
- **OIDC SSO via Entra ID** is the **only** sign-in path for end users. No local passwords. Use the `msal` (Python) and `@azure/msal-browser` / `@azure/msal-react` libraries (or NextAuth's Entra provider — pick one and document why).
- **App registration in Entra ID** with three App Roles: `PulseBoard.Admin`, `PulseBoard.Contributor`, `PulseBoard.Viewer`. Map these to the internal RBAC model.
- **Group-based authorization** — Entra security groups map to PulseBoard's BU/Function membership. The deployment guide must show how an admin maps `EntraGroup → BusinessUnit/Function` once and forgets.
- **Tokens**: validate Entra ID-issued JWTs on every API call (verify `iss`, `aud`, signature against the tenant's JWKS). Use **on-behalf-of** flow if PulseBoard ever needs to call Microsoft Graph (e.g., to resolve user photos / manager hierarchy).
- **Conditional Access compatible** — never bypass MFA, never store user passwords. Service-to-service auth (worker → API) uses Workload Identity Federation between GCP and Entra, or GCP-native service-account JWTs — document both.
- **Provisioning** — support **SCIM 2.0** (or a daily Microsoft Graph sync job) so users/groups appear in PulseBoard automatically when added in Entra. New users get `Viewer` by default; admin promotes via a role-assignment screen.
- **Audit**: every login, role change, and Entra-group-sync event written to `audit_events`.

**Agentic AI**
- **Vertex AI — Gemini 2.5 Pro / Flash** as the primary LLM (use Flash for cheap classification, Pro for reasoning)
- **Gemma 3 (self-hosted on Cloud Run with GPU or Vertex AI Model Garden)** as the offline/fallback option, switchable via env var `LLM_PROVIDER=gemini|gemma`
- **Tool-calling agent loop** (~300 LOC custom orchestrator preferred over LangGraph for controllability)
- **Tools the agent can call**:
  `query_projects`, `query_jira_tickets`, `query_adoption_metric`, `get_project_baseline_vs_actual`, `get_risk_register`, `get_model_drift_signal`, `get_value_realization`, `compare_cohorts`, `lookup_owner`, `render_chart`, `summarize_governance_status`
- **Grounding**: every numeric or factual claim in an AI answer must include a citation (project ID, Jira ticket key, KPI ID + timestamp, model run ID). The frontend renders these as hoverable chips.
- **Domain-aware system prompt** — the agent is briefed on the 7-stage AI lifecycle, AI risk taxonomy, and the org's BU/function taxonomy at session start.

**Integrations**
- **Jira Cloud REST API v3** — OAuth 2.0 (3LO) for self-serve; PAT/API token as fallback for first-time admin setup
- **Generic webhook/REST adapter** for adoption KPI ingestion
- **Microsoft Graph** (via Entra) for user/group/photo/manager resolution
- **Optional**: Slack, Microsoft Teams (post weekly digest), Outlook calendar (milestone reminders)

**Infra (GCP)**
- **Cloud Run** for the FastAPI backend and Next.js frontend (separate services)
- **Cloud SQL (Postgres 15)** for operational DB
- **BigQuery** for analytics
- **Cloud Tasks** for async jobs
- **Memorystore (Redis)** for cache + Celery broker (or Cloud Tasks if you prefer no Redis)
- **Secret Manager** for all credentials (Jira tokens, API keys, DB password, LLM keys, Entra app secret)
- **Cloud Build + Artifact Registry** for CI/CD
- **Cloud Storage** for uploads
- **Cloud Logging + Cloud Monitoring** for observability
- **Cloud Armor + HTTPS Load Balancer** in front of Cloud Run for IP allow-listing if the org wants intranet-only access

### Repository Structure

```
pulseboard/
├── apps/
│   ├── web/                  # Next.js frontend
│   │   ├── app/
│   │   │   ├── (ai)/         # Landing AI assistant
│   │   │   ├── projects/     # AI portfolio + project deep dive
│   │   │   ├── adoption/     # Adoption analytics
│   │   │   ├── governance/   # Risk-tier + compliance views
│   │   │   ├── onboarding/   # Self-serve flows
│   │   │   └── settings/
│   │   ├── components/
│   │   ├── lib/auth/         # Entra MSAL wiring
│   │   └── package.json
│   ├── api/                  # FastAPI backend
│   │   ├── pulseboard/
│   │   │   ├── routers/
│   │   │   ├── services/
│   │   │   ├── auth/         # Entra JWT validation, RBAC, group sync
│   │   │   ├── integrations/jira/
│   │   │   ├── integrations/adoption/
│   │   │   ├── integrations/msgraph/
│   │   │   ├── agent/        # AI orchestration + tools
│   │   │   ├── models/
│   │   │   └── main.py
│   │   └── pyproject.toml
│   └── worker/               # Celery / Cloud Tasks workers
├── packages/
│   ├── shared-types/         # TS + Python type generation from JSON Schema
│   └── ui/                   # Shared design system
├── infra/
│   ├── terraform/            # All GCP resources
│   └── cloudbuild/
├── docs/
│   ├── architecture.md
│   ├── data-model.md
│   ├── api-reference.md
│   ├── entra-setup.md
│   ├── how-to-onboard-project.md
│   └── how-to-onboard-adoption-kpi.md
├── scripts/
│   ├── seed.py
│   └── deploy-gcp.sh
└── README.md
```

---

## DATA MODEL (core tables, Postgres)

```sql
-- Tenants (single-org install in v1, schema multi-tenant ready)
organizations(id, name, entra_tenant_id, created_at)

-- Users + Auth (Entra-sourced, never password-stored)
users(
  id, org_id, entra_object_id UNIQUE, email, name,
  job_title, manager_entra_id, photo_url,
  app_role,          -- admin, contributor, viewer (from Entra App Role)
  last_login_at, created_at, updated_at
)

entra_group_mappings(id, org_id, entra_group_id, mapped_to_type, mapped_to_id)
-- mapped_to_type: business_unit | function | role

-- Project taxonomy (AI-aware)
business_units(id, org_id, name, head_user_id)
functions(id, org_id, name, head_user_id, business_unit_id)
-- functions seeded with: HR, Procurement, Finance, Risk, Legal, Operations, IT, Marketing, ...

-- AI Projects (the central entity)
ai_projects(
  id, org_id, sponsoring_function_id, sponsoring_bu_id,
  delivering_team,             -- 'Central AI Team' or named pod
  name, slug, description,
  ai_pattern,                  -- predictive_ml, gen_ai, agentic, cv, nlp, recommendation, optimization, rpa_ai
  foundation_model,            -- gemini-2.5-pro, claude-sonnet, gpt-4o, in_house_ft, classical_ml, n/a
  data_sensitivity,            -- public, internal, confidential, restricted
  model_risk_tier,             -- 1, 2, 3 (1 = highest)
  responsible_ai_status,       -- not_started, in_review, approved, conditional, rejected
  dpia_status,                 -- not_required, in_progress, completed
  lifecycle_stage,             -- ideation, qualification, poc, pilot, production, scale, sunset
  status,                      -- planning, in_flight, blocked, released, closed, on_hold
  rag_status,                  -- green, amber, red (auto + manual override)
  product_owner_user_id, tech_lead_user_id, business_sponsor_user_id,
  start_date, baseline_end_date, forecast_end_date, actual_end_date,
  baseline_budget, actual_spend,
  expected_value_amount, expected_value_unit, expected_value_currency,
  realized_value_amount, realized_value_last_measured_at,
  source,                      -- jira, manual, hybrid
  jira_project_key,            -- nullable
  created_at, updated_at
)

ai_project_milestones(id, project_id, name, baseline_date, forecast_date, actual_date, status, stage_gate)
-- stage_gate: which lifecycle stage this milestone gates

ai_project_risks(
  id, project_id, title,
  risk_category,               -- data_access, data_quality, model_accuracy, bias, hallucination,
                               -- latency, cost, governance, change_mgmt, integration, vendor_dependency
  severity, likelihood, mitigation, owner_user_id, status, created_at
)

ai_project_issues(id, project_id, title, severity, raised_at, resolved_at, owner_user_id)

ai_project_history_snapshots(
  id, project_id, snapshot_date, lifecycle_stage, rag,
  schedule_variance_days, budget_variance_pct, realized_value_amount
)

-- Jira integration
jira_instances(id, org_id, base_url, auth_type, secret_ref, status, last_sync_at)
jira_project_links(id, jira_instance_id, jira_project_key, ai_project_id, sync_enabled)
jira_tickets_cache(id, jira_project_link_id, ticket_key, summary, status, assignee, story_points, sprint, updated_at)

-- Manual uploads
manual_uploads(id, ai_project_id, uploaded_by, file_gcs_path, parsed_at, parse_status, row_count)

-- Adoption KPIs (the self-serve KPI registry)
adoption_kpis(
  id, ai_project_id, name, slug, description,
  kpi_category,                -- usage, quality, funnel, value_realization, health, trust_safety
  metric_type,                 -- count, ratio, percentage, duration, currency, custom_sql
  unit,
  target_value, target_direction,  -- higher_is_better | lower_is_better
  ingestion_mode,              -- api_push, api_pull, pipeline, manual
  schedule_cron,
  source_config_json,
  created_by, created_at
)

adoption_kpi_values(id, kpi_id, ts, value, dimensions_json)  -- partitioned; mirrored to BigQuery
adoption_kpi_pipelines(id, kpi_id, pipeline_type, status, last_run_at, last_error)

-- AI assistant
ai_conversations(id, user_id, title, created_at)
ai_messages(id, conversation_id, role, content, tool_calls_json, citations_json, created_at)

-- Audit
audit_events(id, org_id, actor_user_id, event_type, target_type, target_id, payload_json, created_at)
```

In **BigQuery**, mirror `adoption_kpi_values` and `ai_project_history_snapshots` for fast time-series and ad‑hoc analysis. The agent's `query_adoption_metric` tool routes there.

---

## FEATURE SPECIFICATIONS

### 1. Agentic AI Landing Page (the hero feature)

- **Layout**: Centered conversation, gradient mesh background that subtly responds to mouse movement, cursor-blinking input with an aurora gradient border on focus.
- **Suggestion chips on first load** — dynamically generated from the user's actual portfolio + role:
  - For a CAIO: *"Show me red projects this quarter"*, *"Which BUs have the most stuck pilots?"*, *"What's the realized vs expected value across the portfolio?"*
  - For an HR Head: *"How is the HR Policy Bot doing?"*, *"What AI projects are sponsored by HR?"*, *"Adoption of HR AI tools by employee grade"*
  - For an AI Engineering Lead: *"Which models are showing drift?"*, *"Show me production projects with rising error rates"*
- **Streaming responses** with markdown + inline Recharts components rendered from a structured response envelope:
  ```json
  {
    "text": "Procurement Contract Summarizer slipped because...",
    "blocks": [
      { "type": "chart", "spec": { ... } },
      { "type": "table", "rows": [...] },
      { "type": "project_card", "project_id": "..." },
      { "type": "stage_pipeline", "project_id": "...", "current_stage": "pilot" }
    ],
    "citations": [
      { "type": "jira_ticket", "key": "PROC-142", "url": "..." },
      { "type": "kpi_value", "kpi_id": "...", "ts": "..." },
      { "type": "model_run", "run_id": "..." }
    ]
  }
  ```
- **Tool-use transparency**: a collapsible "Reasoning" panel shows which tools the agent called, with timing.
- **Conversation history** persisted, searchable, shareable via Entra-authenticated link.
- **Guardrails**: agent must refuse to make claims it cannot ground in tool results; hallucinated numbers are the #1 product risk — write evals against this.

### 2. AI Projects Module

- **Portfolio view**: a hybrid of Linear's list and Notion's gallery. Each row shows project name, sponsoring function badge, AI pattern chip, owner avatar, lifecycle stage pipeline (the 7-dot primitive), RAG dot, sparkline of last 8 weeks of schedule variance, % to baseline end-date, milestone progress ring.
- **Filters**: BU, function, AI pattern, lifecycle stage, governance tier, foundation model, owner, RAG, quarter, source. Filter state lives in URL.
- **AI-stage Kanban view** (toggle from list): 7 columns for the lifecycle stages, projects as cards, drag-to-advance triggers stage-gate checklist.
- **Project deep-dive page**:
  - Header: name, AI-stage pipeline, RAG, sponsoring BU+function, owner, key dates
  - **Baseline vs Actual Gantt** with variance shading
  - **Burn-up / Burn-down** if Jira-linked
  - **AI Stage Gate Checklist** — what's required to move from current stage to next (e.g., from Pilot → Production: Responsible-AI sign-off, load test, rollback plan, training material)
  - **RAG history timeline**
  - **Risks & Issues** register with severity heatmap, AI-risk-category breakdown
  - **Governance panel** — Model Risk Tier, RAI status, DPIA status, last review date
  - **Linked Jira tickets** (live, with status badges)
  - **Adoption tab** (if released) — embedded view of the project's KPIs
  - **Value Realization** — expected vs realized over time

### 3. Adoption Analytics Module

- **KPI grid**: each KPI as a card with current value, target, sparkline, % to target, time-since-last-data-point (so users see staleness), category badge (usage / quality / value / etc.).
- **KPI detail page**:
  - Time-series chart with date-range zoom
  - Dimension breakdown (region, BU, employee grade, cohort) — pivotable
  - Funnel view (if KPI is a funnel-step series)
  - Cohort retention grid
  - "Pattern insights" panel — auto-generated callouts: *"WAU dropped 12% on Tuesdays for the last 3 weeks"*, *"Thumbs-down rate spiked after the v2.3 model swap"* — produced by a scheduled Gemini-Flash job over the time series.
- **Cross-project portfolio view**: realized value across all production AI projects, ranked.

### 4. Governance Module

- View of all projects by Model Risk Tier
- Compliance heatmap: rows = projects, cols = required attestations (RAI, DPIA, Security, Legal). Cell = status.
- Sunset candidates list (projects with declining adoption, rising cost-per-call, or stale model versions).

### 5. Self-Serve Onboarding Flows

#### 5a. Onboard a Jira Instance + Projects
- Wizard, 3 steps: Connect → Select Projects → Map Fields
- Step 1: paste base URL + email + API token *(MVP)* OR click "Connect with Atlassian" for OAuth 3LO *(production)*. Test connection live.
- Step 2: list of Jira projects fetched live, multi-select, bulk-link to existing PulseBoard projects or create new ones.
- Step 3: map Jira fields → PulseBoard fields (baseline date, owner, status, AI pattern from a custom field if present). Sensible defaults. "Save & sync now."
- Background sync runs every 15 min via Celery beat.

#### 5b. Manual Tracker Upload
- Drag-and-drop CSV/XLSX. Show parsed preview. Map columns → schema. Auto-detect on common templates.
- Provide a downloadable template `pulseboard_ai_project_template.xlsx` with required AI-specific fields (lifecycle stage, AI pattern, foundation model, sponsor, etc.).
- Re-upload supported (versioned, last upload wins; older retained for audit).

#### 5c. Adoption KPI Onboarding (this is the differentiator — make it sing)

Show users a **starter KPI library** on first visit (the AI-specific KPIs listed in the Domain Model section) — they can clone and customize, or define from scratch.

- **Mode A — Push API**: PulseBoard generates a KPI-specific endpoint and bearer token. User POSTs JSON like `{ "ts": "...", "value": 1234, "dimensions": { "region": "APAC", "employee_grade": "M3" } }`. Show example curl + Python snippet inline.
- **Mode B — Pull API**: user provides their endpoint + auth + a JMESPath/jq mapping; PulseBoard polls on a cron.
- **Mode C — Pipeline**: user pastes a SQL query against their BigQuery / Snowflake (with credentials stored in Secret Manager). Scheduled execution.
- **Mode D — Manual**: paste a CSV or upload one.

For all modes: define metric_type, unit, target, dimensions schema, KPI category. Live preview the last 10 ingested points before activation.

### 6. Command Palette (`⌘K`)
Actions: navigate to project, ask AI, change RAG, advance lifecycle stage, add risk, onboard Jira, switch theme, switch density. Fuzzy search across projects, KPIs, people (Entra-resolved), conversations.

### 7. Notifications & Digests
- Weekly Monday 8am digest email per BU/Function Head: their portfolio summary + AI commentary on what changed.
- Slack/Teams webhook optional.
- Critical RAG-flip alerts: when a project goes Green→Red within a week, notify the sponsor and CAIO.

---

## AGENT IMPLEMENTATION DETAIL

Build a **typed tool-calling loop**. Each tool has a Pydantic input/output schema. The agent:

1. Receives user query + recent conversation context + a system prompt with the org's BU/function taxonomy + AI lifecycle vocabulary.
2. Decides on tool calls (Gemini function calling).
3. Executes tools (in parallel where possible).
4. Synthesizes a response **only from tool outputs** — system prompt forbids using prior knowledge for numeric claims.
5. Attaches citations from tool output metadata.
6. Filters all tool results through the caller's RBAC — a Function Head only sees their function's projects unless they're given cross-function viewer access.

**System prompt template** (paraphrase, refine for production):

> You are PulseBoard's AI portfolio intelligence assistant. You serve the central AI team and its BU/function stakeholders. You understand the AI project lifecycle (Ideation → Qualification → PoC → Pilot → Production → Scale → Sunset), AI-specific risks (data access, model drift, hallucination, governance, vendor dependency), and AI adoption KPI categories (usage, quality, funnel, value realization, health, trust & safety). You have access to tools that query the live database — **always use tools for any specific number, status, name, or date**. Never guess. If a tool returns no data, say so. Every numeric or factual claim must include a citation referencing the tool result that produced it. Render charts when they help comprehension. Be concise — these are busy leaders.

**Evals**: write a `tests/agent_evals.py` with at least 30 question-answer pairs, including adversarial ones ("What's the status of project XYZ" where XYZ doesn't exist), domain-specific ones ("Which projects are stuck at the Pilot→Production gate?"), and ones designed to tempt hallucination.

---

## HOW-TO GUIDE #1 — *Onboarding an AI Project* (`docs/how-to-onboard-project.md`)

Audience: a BU/Function-side AI Project Lead with no engineering skills. Include screenshots placeholders, exact button labels, and decision trees.

Sections:
1. Sign in (Entra SSO — should just work; troubleshooting if not)
2. Decide your source: Jira / Manual / Hybrid
3. Gather prerequisites (admin access in Jira OR a clean tracker file)
4. Step-by-step Jira onboarding (with auth token how-to)
5. Step-by-step manual upload (with template download link)
6. **Filling out the AI-specific fields** — what AI pattern means, how to pick a Model Risk Tier, what the lifecycle stages mean
7. Setting baseline dates, owner, RAG, value expectation
8. Verifying the first sync / first import
9. Common errors and fixes
10. FAQ

---

## HOW-TO GUIDE #2 — *Onboarding Adoption KPIs* (`docs/how-to-onboard-adoption-kpi.md`)

Audience: AI Product Owner or Analytics Lead. Sections:
1. What makes a good adoption KPI for an AI product (definition + examples per category: usage, quality, funnel, value, health, trust & safety)
2. Choose your ingestion mode (decision matrix)
3. Mode A: Push API — full curl + Python + Node example
4. Mode B: Pull API — config schema + JMESPath cheatsheet
5. Mode C: Pipeline (SQL query) — credential setup, scheduling
6. Mode D: Manual upload — template
7. Defining target, direction, dimensions, KPI category
8. Validating data lands correctly
9. Troubleshooting (auth failures, schema mismatches, stale data)

---

## HOW-TO GUIDE #3 — *Entra ID Setup* (`docs/entra-setup.md`)

Audience: enterprise IT / identity admin. Step-by-step:
1. Register the **PulseBoard** application in Entra ID (single-tenant)
2. Configure redirect URIs (Cloud Run frontend URL + local dev)
3. Define **App Roles**: `PulseBoard.Admin`, `PulseBoard.Contributor`, `PulseBoard.Viewer`
4. Assign Entra security groups to App Roles
5. Configure API permissions (`User.Read`, `GroupMember.Read.All`, `User.Read.All`)
6. Generate client secret, store in GCP Secret Manager
7. (Optional) Enable SCIM provisioning endpoint
8. Map Entra security groups to PulseBoard BUs/Functions in Settings → Identity
9. Conditional Access compatibility checklist
10. Troubleshooting common Entra errors (AADSTS65001, AADSTS50105, etc.)

---

## GCP DEPLOYMENT — "PASTE CREDS, RUN, DONE"

The deployment must be reduced to:

```bash
# 1. Prereqs: gcloud CLI installed, owner on a GCP project, Entra app registered (per docs/entra-setup.md)
export PROJECT_ID=my-pulseboard
export REGION=asia-south1
export ENTRA_TENANT_ID=...
export ENTRA_CLIENT_ID=...
export ENTRA_CLIENT_SECRET=...   # will be moved to Secret Manager

# 2. One command
./scripts/deploy-gcp.sh
```

The script (and supporting Terraform) must:

1. Enable required APIs: `run.googleapis.com`, `sqladmin.googleapis.com`, `bigquery.googleapis.com`, `secretmanager.googleapis.com`, `cloudbuild.googleapis.com`, `artifactregistry.googleapis.com`, `aiplatform.googleapis.com`, `cloudtasks.googleapis.com`, `storage.googleapis.com`, `compute.googleapis.com`.
2. Create Cloud SQL (Postgres 15, smallest tier for dev, configurable).
3. Create BigQuery dataset `pulseboard_analytics`.
4. Create GCS bucket for uploads.
5. Create Artifact Registry repo, build & push backend + frontend + worker images via Cloud Build.
6. Deploy three Cloud Run services: `pulseboard-api`, `pulseboard-web`, `pulseboard-worker`.
7. Wire up env vars from Secret Manager (DB URL, Entra client secret, Vertex AI project, Jira default token).
8. Run Alembic migrations as a Cloud Run Job.
9. Create a service account with least-privilege IAM (Vertex AI User, Cloud SQL Client, BigQuery Data Editor, Secret Accessor, Storage Object Admin on the bucket only).
10. Print final URLs + remind admin to add the Cloud Run URL as a redirect URI in the Entra app registration.

**Post-deploy, the admin does exactly this:**
1. Add the printed Cloud Run URL as a redirect URI in the Entra app registration (one-time).
2. Open `pulseboard-web` URL → Entra SSO → land in PulseBoard as the first admin.
3. Settings → Identity → map Entra security groups to BUs/Functions.
4. Settings → Integrations → "Add Jira Instance" → paste base URL, email, API token → Save.
5. Settings → Adoption KPIs → "New KPI" → choose Push API → copy generated endpoint + token → POST first data point.
6. Done. The app is live with their data.

The deployment guide must include **estimated monthly cost** for: a small org (~50 projects, 100 KPIs, 20 users) and a large org (~500 projects, 1000 KPIs, 200 users), broken down by service.

---

## SEED DATA / DEMO MODE

Ship a `--demo` flag that loads:
- 1 organization with 5 BUs (Retail, Wealth, Corporate, Insurance, Group) and 8 Group Functions (HR, Procurement, Finance, Risk, Legal, Operations, IT, Marketing)
- 25 Entra-style users with realistic titles (CAIO, AI Product Manager, AI Engineer, HR Head, Procurement Head, etc.)
- 40 realistic AI projects across all 7 lifecycle stages and all AI patterns — examples:
  - *HR Policy Bot* (HR, GenAI, Production)
  - *Procurement Contract Summarizer* (Procurement, GenAI, Pilot)
  - *Loan Risk Scorer v2* (Risk, Predictive ML, Production)
  - *Wealth Advisor Copilot* (Wealth, Agentic, Pilot)
  - *KYC Document Intelligence* (Risk, CV+NLP, Scale)
  - *Hiring Match* (HR, Recommendation, PoC)
  - *Invoice Anomaly Detection* (Finance, Predictive ML, Production)
  - *Marketing Content Studio* (Marketing, GenAI, Pilot)
- 60 days of synthetic project history snapshots showing realistic RAG drift
- 30 adoption KPIs across released projects with 90 days of synthetic time-series including weekend dips, weekly seasonality, a couple of dramatic adoption jumps, and one model-drift event so the AI has interesting things to talk about.

This means a developer can `./scripts/deploy-gcp.sh --demo` and see a fully populated, beautiful product within 15 minutes of starting.

---

## QUALITY BAR & ENGINEERING REQUIREMENTS

- **TypeScript strict mode**, no `any` without justification.
- **Python**: full type hints, `mypy --strict` clean, `ruff` clean.
- **Tests**: pytest for backend (≥70% coverage on services + agent tools), Playwright for 5 critical E2E flows (Entra login, onboard Jira, upload tracker, define KPI, ask AI).
- **API**: OpenAPI auto-generated, served at `/docs` (admin-only).
- **Auth**: Entra ID OIDC, role-based access (admin, contributor, viewer); row-level filtering by BU/function membership derived from Entra groups.
- **Audit log**: every mutation + every login written to `audit_events`.
- **Rate limiting**: per-user on AI endpoints (Gemini calls aren't free).
- **Observability**: structured JSON logs with `entra_object_id` correlation, Cloud Trace on the agent loop with span per tool call, error budgets via Cloud Monitoring.
- **Accessibility**: WCAG AA. Keyboard-navigable end-to-end. The command palette must be reachable from any page.
- **Performance budget**: landing page TTI < 2s on 4G, AI first-token < 1.5s, project list with 500 projects renders < 300ms (virtualize).
- **Security**: all secrets in Secret Manager, none in `.env` checked in. Jira tokens encrypted at rest. SQL via parameterized queries only. CSP headers strict. Dependabot on. Entra token validation on every request — never trust client-supplied identity claims.

---

## DELIVERY FORMAT

Produce, in order:

1. **README.md** with 60-second pitch + architecture diagram (mermaid) + quickstart.
2. **The full mono-repo** with all code committed, no `TODO` placeholders in user-facing code paths.
3. **The three how-to guides** as polished markdown.
4. **The GCP deployment guide** (`docs/deploy-gcp.md`) with cost table.
5. **A 2-minute demo script** (`docs/demo-script.md`) — exactly what to click to wow the CAIO.
6. **Architecture decision records**: `docs/adr/0001-llm-provider.md` (Gemini-primary / Gemma-fallback) and `docs/adr/0002-entra-auth.md` (Entra integration approach).

---

## EXPLICIT NON-GOALS (do not build these now)

- Resource management / capacity planning
- Financial forecasting models
- Replacing Jira (PulseBoard reads from Jira, never writes back in v1)
- Replacing MLflow / model registry (PulseBoard *links to* model runs, doesn't host them)
- Mobile native apps (PWA only)
- Multi-tenant SaaS (single-org install per deployment in v1)

---

## START HERE

Begin by:
1. Generating the architecture diagram + data model + API contract.
2. Confirming the design system tokens (colors, type, spacing) with a one-page style sheet artifact.
3. Wiring **Entra SSO end-to-end on day one** — this is harder to retrofit than to build first.
4. Scaffolding the mono-repo and committing in logical, reviewable chunks.
5. Building in this order: **Entra auth → AI projects CRUD → Jira sync → manual upload → KPI ingestion → adoption views → governance → agent → polish**.

When in doubt, optimize for: *the Chief AI Officer opens this on Monday morning, asks one question about her AI portfolio, gets one beautiful, trustworthy, RBAC-respecting answer, and closes the tab feeling in control.* That's the product.

Build it.
