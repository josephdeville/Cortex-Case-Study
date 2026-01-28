# Cortex GTM Engineer Case Study: Trigger-Based Signal Engine

## Executive Summary

**Project:** Build a Trigger-Based Signal Engine that identifies companies at the moment they're most likely to need Cortex—driving pipeline volume *and* quality simultaneously.

**Why this project first?** The mandate is pipeline growth + health. Most pipeline problems stem from targeting companies too early (not ready) or too late (already bought competitor). Trigger signals solve both by catching companies at the inflection point.

---

## My Philosophy: Owning the GTM Machine

The GTM Engineer role isn't about running projects—it's about **owning the system that produces pipeline**. I see this as building and maintaining the revenue engine, not just operating it.

### What "Ownership" Means to Me

| Traditional Approach | GTM Systems Owner Approach |
|---------------------|---------------------------|
| "Run this campaign" | "Why do campaigns succeed or fail? How do we systematize wins?" |
| "Generate more leads" | "What's the quality/quantity tradeoff? What's the constraint?" |
| "Hit this quarter's number" | "What system produces predictable, compounding growth?" |
| "Use these tools" | "What's the optimal tech stack? What's missing? What's redundant?" |
| "Follow this process" | "Is this process the bottleneck? How do we measure and improve?" |

### The Three Jobs of a GTM Systems Owner

```
┌─────────────────────────────────────────────────────────────────────┐
│                     GTM ENGINEER OWNERSHIP MODEL                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  1. ARCHITECT          2. OPERATE              3. OPTIMIZE           │
│  ────────────          ─────────               ──────────            │
│  Design systems        Run the machine         Measure & improve     │
│  that scale            day-to-day              continuously          │
│                                                                      │
│  • Signal detection    • Monitor dashboards    • A/B test variants   │
│  • Scoring models      • Route leads           • Refine weights      │
│  • Data pipelines      • Enable SDRs           • Remove waste        │
│  • Tool selection      • Fix broken flows      • Find leverage       │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

### Why I'm Starting with Signal Detection (Not "More Leads")

Most GTM problems are diagnosed as "we need more pipeline." But that's a symptom, not a cause. The real questions:

1. **Is the funnel leaky?** (conversion problem, not volume problem)
2. **Are we targeting the right accounts?** (quality problem)
3. **Are we reaching them at the right time?** (timing problem)
4. **Do we know what's working?** (measurement problem)

My hypothesis for Cortex: **Timing is the primary constraint.** The ICP is clear. The product is strong. The competition is known. What's likely missing is a systematic way to identify *when* a company moves from "interesting" to "ready."

### How This Connects to Cortex's DNA

Cortex exists because **engineering teams need systems of record**—a single source of truth that brings order to chaos. The irony? Most GTM teams operate the same way engineering teams did before Cortex:

- Fragmented data across tools
- No clear ownership of metrics
- Reactive instead of proactive
- Tribal knowledge instead of documented systems

I want to bring Cortex's philosophy to Cortex's own GTM: **a system of record for pipeline generation.**

---

## What I Know About Cortex's Situation

### Company Context

| Insight | What It Tells Me |
|---------|-----------------|
| ~78 employees (down 21% YoY) | Efficiency is paramount - do more with less |
| $60M Series C (Sep 2024) | Growth mandate, but capital-efficient |
| Sales (14) + Marketing (6) = 20 people | GTM Engineer is a force multiplier for a lean team |
| Already using Clay, Marketo, SFDC | Build on existing stack, don't propose new tools |
| Hiring GTM Engineer + Dir Product Marketing | Investing in growth engine now |

### GTM Team Structure

```
                    VP Sales (Scott Mullin)
                            │
            ┌───────────────┼───────────────┐
            │               │               │
    Enterprise Sales    Enterprise Sales    BDR/SDR
    (Matt Ball)         (Mike Connell)      Team

                    VP Marketing (Alan Hsia)
                            │
            ┌───────────────┼───────────────┐
            │               │               │
    Demand Gen         Field Marketing   Product Marketing
    (Cameron Bernard)  (Carolina Barberii)  (Hiring)

                    Rev Ops
                      │
            ┌─────────┴─────────┐
            │                   │
    Dir RevOps             Dir RevOps
    (Daria Borets)         (Matt McGonegle)

                    ↓
            GTM ENGINEER ← Where I fit
```

### Tech Stack I'll Be Working With

| Category | Tool | My Experience |
|----------|------|---------------|
| CRM | Salesforce | Flows, reports, lead routing |
| Marketing Automation | Marketo | Programs, scoring, nurture |
| Data Enrichment | Clay | Tables, enrichment, AI |
| Automation | Zapier | Multi-step zaps |
| Analytics | Segment | Event tracking |
| Sales Intel | LinkedIn Sales Navigator | Boolean search, alerts |

### Competitive Reality

| Competitor | Their Advantage | Our Counter |
|------------|-----------------|-------------|
| Backstage | Free, open-source | Maintenance burden - "you'll need 2 FTE just to run it" |
| OpsLevel | Fast setup, lower price | Deeper features, better at scale |
| Port.io | Flexibility | Opinionated best practices |
| DX | DevEx metrics focus | Full portal vs point solution |

**Key Insight:** 4 Cortex alumni now work at DX. Competitive pressure is real.

### Recent Messaging Priorities (from LinkedIn)

1. **"AI Readiness"** - IDP as foundation for AI adoption
2. **Velocity vs Quality** - "PRs up 20%, incidents up 23.5%"
3. **Governance** - System of record for AI era
4. **MTTR** - Customer stories about 67% reduction

**Implication for outbound:** Lean into AI readiness angle - it's timely and differentiated.

---

## Systems Thinking Approach

### The GTM System Map

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                           CORTEX GTM SYSTEM                                  │
│                                                                              │
│  ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌──────────┐    ┌────────┐ │
│  │ MARKET   │───▶│  LEADS   │───▶│ PIPELINE │───▶│  DEALS   │───▶│  ARR   │ │
│  │ (TAM)    │    │ (MQLs)   │    │ (Stages  │    │ (Closed  │    │        │ │
│  │          │    │          │    │  0-4)    │    │  Won)    │    │        │ │
│  └──────────┘    └──────────┘    └──────────┘    └──────────┘    └────────┘ │
│       │              │               │               │               │       │
│       ▼              ▼               ▼               ▼               ▼       │
│   LEVERAGE       LEVERAGE        LEVERAGE       LEVERAGE        LEVERAGE    │
│   POINT 1        POINT 2         POINT 3        POINT 4         POINT 5     │
│   Signal         Lead            Stage          Win rate        Expansion   │
│   Detection      Scoring         Velocity       Optimization    Signals     │
│                                                                              │
└─────────────────────────────────────────────────────────────────────────────┘
```

### Why I'm Starting at Leverage Point 1

In systems thinking, the most powerful interventions happen **upstream**. Fixing early funnel quality has compounding effects:

```
Better Signals → Better Leads → Better Pipeline → Better Conversion → Predictable ARR
     ↓              ↓               ↓                 ↓
   +10%           +15%            +20%              = 50%+ compound improvement
```

Contrast with late-stage interventions:
- Training AEs on negotiation (Point 4) = incremental win rate improvement
- Better signal detection (Point 1) = better everything downstream

### Feedback Loops to Leverage

**Reinforcing Loop (Virtuous Cycle):**
```
High-quality signals → SDRs trust the system → SDRs act quickly →
More wins → More data on what works → Better signals
```

**Balancing Loop (Watch for):**
```
Too many signals → SDR overwhelm → Signals ignored →
System loses credibility → Back to old habits
```

**Design Principle:** Start narrow (3-4 high-confidence signals), prove value, then expand.

---

## Quick Wins vs Strategic Investments

### QUICK WINS (Week 1-2)

| Initiative | Effort | Impact | Why It's Quick |
|------------|--------|--------|----------------|
| **Job posting monitor** | 2-3 days | High | LinkedIn + Clay can be set up immediately. "Hiring Platform Engineers" = instant ICP signal |
| **New VPE/CTO alerts** | 1 day | Medium | UserGems or LinkedIn trigger. New exec = budget unlock |
| **Funding round filter** | 1 day | Medium | Crunchbase data already available. Series C+ = infrastructure investment likely |
| **SDR signal playbook** | 2 days | Medium | Write 5 email templates tied to signals. Immediate outreach improvement |
| **Score top 50 accounts** | 1 day | High | Manual proof-of-concept. Show sales team what good looks like |

**Quick Win Value:** Demonstrate immediate pipeline impact, build credibility, get buy-in for bigger investments.

### MEDIUM-TERM WINS (Month 1-2)

| Initiative | Effort | Impact | Why It Takes Longer |
|------------|--------|--------|---------------------|
| **Technographic layer** | 2-3 weeks | High | Need to integrate BuiltWith/HG Insights, map to scoring model |
| **Historical backtest** | 1-2 weeks | High | Requires CRM access, data cleaning, analysis to validate weights |
| **CRM integration** | 2-3 weeks | High | Salesforce flows, lead/account assignment logic, alerting |
| **SDR training program** | 2 weeks | Medium | Build deck, run sessions, gather feedback, iterate |
| **A/B test framework** | 2 weeks | High | Split SDR cohorts, define metrics, tracking infrastructure |

### STRATEGIC INVESTMENTS (Quarter 1-2)

| Initiative | Effort | Impact | Why It's Strategic |
|------------|--------|--------|-------------------|
| **Competitive displacement engine** | 4-6 weeks | Very High | Catch companies who chose Backstage/OpsLevel and are unhappy. Requires: competitive intel, pain signal detection, timing model |
| **Predictive scoring model** | 6-8 weeks | Very High | ML on historical data to predict closed-won probability. Requires: data science, clean CRM data, validation period |
| **Signal-to-revenue attribution** | 4-6 weeks | High | Prove ROI of signal program. Requires: attribution modeling, exec buy-in on metrics |
| **Customer expansion signals** | 4-6 weeks | High | Apply same logic to existing customers for upsell. Requires: customer success integration, different signal set |
| **Full automation pipeline** | 6-8 weeks | Very High | Zero-touch signal detection → CRM → SDR outreach. Requires: engineering resources, reliability testing |

### The Investment Curve

```
IMPACT
  ▲
  │                                          ┌─────────────────┐
  │                                         │ STRATEGIC        │
  │                                        │  - Predictive ML  │
  │                                       │   - Full automation│
  │                         ┌────────────┘    - Competitive    │
  │                        │ MEDIUM-TERM      displacement     │
  │         ┌─────────────┘  - Techno layer                    │
  │        │ QUICK WINS      - CRM integration                 │
  │       │  - Job signals   - A/B testing                     │
  │      │   - VPE alerts                                      │
  │     │    - Funding filter                                  │
  │    │                                                       │
  └────┴───────────────────────────────────────────────────────▶ TIME
       Week 1    Month 1    Month 2    Quarter 1    Quarter 2
```

### My Recommendation: Start with Job Signals

**Why this specific quick win first:**

1. **Highest signal strength:** A company hiring Platform Engineers has already allocated budget for platform problems
2. **Easiest to implement:** LinkedIn + Clay = 2-3 day setup
3. **Most defensible logic:** When questioned, the reasoning is airtight
4. **Best story for SDRs:** "They're literally hiring someone to do what Cortex does automatically"

**Week 1 Deliverable:**
- Clay table monitoring ICP companies for Platform/DX/SRE job postings
- Score of 1-100 based on role seniority, volume, recency
- Top 20 accounts delivered to SDR team with personalized context
- Track response rates vs baseline

---

## Part 1: Research & Preparation (~5 min)

### Research Conducted

1. **Product Deep Dive**
   - Cortex = "System of Record for Engineering"
   - Aggregates data from CI/CD, monitoring, source control
   - Core value: Service ownership, operational health scorecards, DORA metrics

2. **Competitive Landscape**
   | Competitor | Positioning | Key Differentiator |
   |------------|-------------|-------------------|
   | Spotify Backstage | Open-source framework | Free, but requires heavy engineering investment |
   | Port.io | No-code portal builder | Flexibility, self-service focus |
   | OpsLevel | Fast implementation | 30-45 day setup vs months for others |
   | Atlassian Compass | Enterprise integrated | Atlassian ecosystem lock-in |
   | Datadog Service Catalog | Observability-first | Existing Datadog customers |

3. **ICP Trigger Analysis**
   - Document mentions: microservice sprawl, developer turnover, failed audits, efficiency initiatives
   - Real-world examples: Uber's 1,000+ services "Death Star", Spotify creating Backstage to solve this internally

4. **Intent Signal Research**
   - Job postings = 48% of pipeline at companies like Greenly
   - Technographics: 96% of enterprises using/evaluating K8s
   - Hiring intent signals can shorten sales cycles by 81%

### Assumptions Made

1. **CRM data exists** - Salesforce has historical closed-won/lost data to backtest signals
2. **Clay is operational** - Already in stack per job posting, can build on it
3. **Team has bandwidth** - SDRs can work signal-prioritized lists (not just more volume)
4. **Quality > Volume** - With 14 sales reps, better leads matter more than more leads
5. **Cross-functional buy-in** - Cameron (DemandGen), Daria/Matt (RevOps) will collaborate

### Tools - Building on Existing Stack

| Category | Existing Tool | How I'll Use It |
|----------|---------------|-----------------|
| CRM | **Salesforce** | Lead routing rules, signal fields on accounts, reporting |
| Marketing Automation | **Marketo** | Trigger-based nurture, lead scoring integration |
| Data Enrichment | **Clay** | Signal detection tables, enrichment workflows |
| Automation | **Zapier** | Connect data sources to SFDC/Marketo |
| Sales Intel | **LinkedIn Sales Nav** | Job posting alerts, champion tracking |
| Analytics | **Segment** | Track signal-to-conversion attribution |

**Philosophy:** No new tools in Week 1. Build on what's there. Earn trust before proposing changes.

---

## Part 2: The Problem & Solution (~12 min)

### The Problem

**Current State (Hypothesis):**
- SDRs/AEs prospect based on static ICP criteria (company size, industry)
- No systematic way to identify *when* a company is ready to buy
- Pipeline includes companies at wrong stage of maturity
- Win rates suffer because we're selling to companies who:
  - Haven't felt enough pain yet (too early)
  - Already bought Backstage/OpsLevel (too late)

**Impact:**
- Sales cycles longer than necessary
- Pipeline "looks healthy" but conversion is low
- Late-stage ARR unpredictable because early funnel quality is inconsistent

### The Solution: Trigger-Based Signal Engine

A system that identifies companies exhibiting **active buying signals** aligned with Cortex's value proposition.

#### Signal Categories

**1. HIRING SIGNALS (Strongest Intent)**

| Signal | What It Indicates | Data Source |
|--------|-------------------|-------------|
| Platform Engineer roles posted | Building/scaling platform team | LinkedIn, job boards |
| "Developer Experience" in title | Investing in DX (Cortex value prop) | LinkedIn |
| SRE/Reliability Engineer hiring surge | Operational health focus | Job aggregators |
| VP/Director of Platform role | New budget holder emerging | LinkedIn |

**Why strong:** Companies don't hire Platform Engineers unless they have a platform problem to solve. This is budget being allocated.

**2. TECHNOGRAPHIC SIGNALS (Readiness Indicators)**

| Signal | What It Indicates | Data Source |
|--------|-------------------|-------------|
| Kubernetes adoption (recent) | Microservices architecture | BuiltWith, job posts |
| Multiple observability tools | Tool sprawl, need for consolidation | Technographic providers |
| CI/CD complexity (Jenkins + GitHub Actions + CircleCI) | Inconsistency Cortex solves | Tech stack data |
| Service mesh adoption (Istio, Linkerd) | Advanced microservices maturity | Job posts, tech blogs |

**3. ORGANIZATIONAL SIGNALS (Trigger Events)**

| Signal | What It Indicates | Data Source |
|--------|-------------------|-------------|
| Engineering headcount growth >20% YoY | Scaling pains incoming | LinkedIn, company announcements |
| Series C+ funding | Budget to solve infrastructure problems | Crunchbase, news |
| New CTO/VP Eng hired | Mandate for change | LinkedIn, press releases |
| Acquisition | System integration challenges | News |

**4. PAIN SIGNALS (Active Problem)**

| Signal | What It Indicates | Data Source |
|--------|-------------------|-------------|
| "Incident" or "outage" in news | Operational health issues | News monitoring |
| Glassdoor reviews mentioning "tech debt" | Internal pain surfacing | Glassdoor |
| Blog posts about "microservice challenges" | Public admission of problem | Company engineering blogs |
| Failed SOC2/compliance audit (rare public) | Urgent compliance need | News, job posts for compliance roles |

#### Signal Scoring Model

```
ACCOUNT SCORE = (Signal Weight × Recency Factor × ICP Fit)

Signal Weights:
- Platform Engineer job posted: +30
- VP/Dir Platform hired: +25
- >20% eng headcount growth: +20
- Kubernetes in stack: +15
- Recent funding (C+): +15
- Multiple observability tools: +10
- Incident in news: +20
- New CTO/VPE: +15

Recency Factor:
- Last 30 days: 1.5x
- 31-60 days: 1.0x
- 61-90 days: 0.5x
- >90 days: 0.25x

ICP Fit (Binary Gates):
- 1,000+ employees: Required
- 100+ engineers: Required
- Target industry: +10 bonus
```

#### Example Scored Account

**Company: FinTech Corp**
- 2,500 employees, 400 engineers ✓
- Posted 3 Platform Engineer roles (last 14 days): +30 × 1.5 = 45
- Using Kubernetes (detected in job posts): +15
- Series D funding (6 months ago): +15 × 0.5 = 7.5
- New VP of Engineering (started 2 months ago): +15 × 1.0 = 15
- Financial Services industry: +10

**Total Score: 92.5** → High Priority

#### Workflow Integration

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│  Signal Sources │────▶│   Clay Table    │────▶│   Salesforce    │
│                 │     │   (Enrichment   │     │   (Account/Lead │
│ • Job boards    │     │    + Scoring)   │     │    assignment)  │
│ • LinkedIn      │     │                 │     │                 │
│ • Technographics│     │ Score threshold │     │ SDR gets alert  │
│ • News/funding  │     │ triggers push   │     │ with context    │
└─────────────────┘     └─────────────────┘     └─────────────────┘
```

#### How This Supports the Mandate

| Mandate Component | How Trigger Engine Helps |
|-------------------|-------------------------|
| **Increase pipeline** | New accounts surfaced that weren't on radar |
| **Improve pipeline quality** | Only accounts showing active signals enter |
| **Late-stage ARR through early funnel** | Better qualified leads = higher conversion = predictable ARR |

### Success Metrics

| Metric | Current (Hypothetical) | Target |
|--------|------------------------|--------|
| Lead-to-Qualified rate | 15% | 30% |
| Stage 1→2 conversion | 40% | 55% |
| Average deal cycle | 90 days | 70 days |
| Pipeline coverage ratio | 3x | 4x (with better quality) |

---

## Part 3: V2 Roadmap (~3 min)

### With 2 More Weeks, I Would:

**Week 1: Validation & Iteration**
1. **Backtest the model** against last 12 months of closed-won deals
   - Did these accounts show signals before they entered pipeline?
   - Which signals correlated strongest with closed-won?
   - Refine weights based on actual data

2. **A/B test signal-sourced leads vs traditional**
   - Split SDR team: half works signal-sourced, half works normal list
   - Track conversion rates, cycle time, ACV

**Week 2: Expand & Automate**
1. **Add competitive displacement signals**
   - Companies posting "Backstage" in job posts (build vs buy decision in progress)
   - Mentions of competitor pain in Glassdoor/Reddit
   - This catches companies who chose wrong and are ready to switch

2. **Build SDR enablement layer**
   - Signal-aware email templates ("I noticed you're hiring Platform Engineers...")
   - Battlecards triggered by tech stack (Backstage user? Here's the migration path)
   - One-pager on "why these signals matter" for SDR training

3. **Automate monitoring**
   - Weekly digest of new high-scoring accounts
   - Slack alerts when existing target accounts show new signals
   - CRM integration for signal history on account records

### Longer-Term Vision (V3+)

- **Predictive model:** ML on signal combinations that predict closed-won
- **Churn prevention:** Same signals on existing customers (new VPE = risk)
- **Expansion signals:** Customer hiring more engineers = upsell opportunity

---

## Bigger Bets: Transformational Investments

These require significant time/resources but could 10x the GTM motion.

### BIG BET 1: Competitive Displacement Engine

**The Opportunity:** Companies that chose Backstage 12-18 months ago are now feeling the pain of maintaining an open-source framework. They've already budget-approved the category—they just chose wrong.

**Signal Architecture:**
```
┌─────────────────────────────────────────────────────────────────────┐
│                 COMPETITIVE DISPLACEMENT ENGINE                      │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  DETECTION                    TIMING                 ACTIVATION      │
│  ─────────                    ──────                 ──────────      │
│  • "Backstage" in job posts   • 12-18 months post   • Migration      │
│  • Glassdoor: "internal       initial adoption        focused        │
│    tooling frustrating"       = maintenance pain      messaging      │
│  • Reddit/HN complaints       • New platform lead   • TCO            │
│  • Backstage GitHub issues    = mandate for change    comparison     │
│    from company domain                               • Case studies  │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

**Why It's a Big Bet:** Requires competitive intel infrastructure, pain signal NLP, and tight sales enablement. But these are *pre-qualified* buyers.

### BIG BET 2: The "Engineering Health Score" Lead Magnet

**The Opportunity:** Turn Cortex's product philosophy into a free assessment tool that generates qualified inbound.

**Concept:**
- Free web tool: "How healthy is your engineering organization?"
- 10-question survey covering: service ownership clarity, incident response time, deployment frequency, onboarding time
- Output: Score + benchmarks against similar companies + specific recommendations
- CTA: "See how Cortex can improve your score"

**Why It's a Big Bet:**
- Requires product/marketing collaboration
- Content creation for benchmarks
- Lead nurturing infrastructure
- But creates *inbound* from companies already thinking about engineering health

### BIG BET 3: Full-Stack GTM Data Infrastructure

**The Opportunity:** Build the data foundation that enables all future GTM optimization.

**Architecture:**
```
┌─────────────────────────────────────────────────────────────────────┐
│                    GTM DATA INFRASTRUCTURE                           │
├─────────────────────────────────────────────────────────────────────┤
│                                                                      │
│  DATA LAYER              PROCESSING              ACTIVATION          │
│  ──────────              ──────────              ──────────          │
│  • Salesforce (CRM)      • Unified account       • Scoring served    │
│  • LinkedIn (signals)      graph                   in real-time      │
│  • Technographics        • Signal processing     • SDR alerts        │
│  • Web analytics         • ML scoring            • Routing rules     │
│  • Product usage         • Attribution           • Personalization   │
│  • Support tickets                                                   │
│                                                                      │
│                    ↓                                                 │
│              SINGLE SOURCE OF TRUTH                                  │
│              (Account-level unified record)                          │
│                                                                      │
└─────────────────────────────────────────────────────────────────────┘
```

**Why It's a Big Bet:** This is a 6-12 month investment requiring data engineering. But it's the foundation for everything—predictive scoring, attribution, personalization at scale.

### Prioritization Framework: Quick Wins Fund Big Bets

```
                    IMPACT
                      ▲
                      │
           Big Bet 3  │  Big Bet 1
         (Data Infra) │  (Competitive
                      │   Displacement)
                      │
        ──────────────┼─────────────────▶ EFFORT
                      │
        Quick Win 1   │  Big Bet 2
        (Job Signals) │  (Health Score
                      │   Lead Magnet)
                      │
```

**My Approach:**
1. Ship quick wins in Week 1-2 → prove value, build credibility
2. Use wins to secure buy-in for medium-term investments
3. Build toward big bets as foundation solidifies
4. Quick wins create data that validates big bet hypotheses

---

## Presentation Structure (20 minutes)

### Part 1: Research & Preparation (5 min)
**Slide 1:** Title + My Background
**Slide 2:** Research approach - what I studied, tools used
**Slide 3:** Key findings - Cortex market position, competitive landscape
**Slide 4:** Assumptions I'm making (validate with questions)

### Part 2: The Problem & Solution (12 min)
**Slide 5:** The Core Problem - timing gap in pipeline generation
**Slide 6:** Systems Thinking - why early funnel is the leverage point
**Slide 7:** The Solution - Trigger-Based Signal Engine (overview)
**Slide 8:** Signal Categories - the four types with examples
**Slide 9:** Scoring Model - how prioritization works
**Slide 10:** Workflow Integration - how it fits existing process
**Slide 11:** Quick Wins vs Strategic Investments (visual)
**Slide 12:** Success Metrics - what we'd measure

### Part 3: V2 Roadmap (3 min)
**Slide 13:** Two-week iteration plan
**Slide 14:** Bigger Bets preview (plant seeds for future discussion)

### Q&A
**Prep:** Anticipated questions with crisp answers

---

## Q&A Prep: Anticipated Questions

### Technical/Tactical Questions

**Q: Why not just buy intent data from Bombora/6sense?**
A: Intent data shows topic interest, not action. Job postings show budget allocation. A company researching "developer portals" might be curious; a company hiring Platform Engineers is building one. Intent data is a "maybe"; hiring signals are a "yes, we're investing."

**Q: How do you know these signals actually correlate with buying?**
A: Day 1 hypothesis, but I'd validate in Week 2 by backtesting against your last 12 months of closed-won deals. My bet: companies that closed showed at least one of these signals in the 90 days before they entered pipeline.

**Q: What if competitors are using the same signals?**
A: Speed + relevance. First to reach a company with *specific* context wins. Not "I see you're growing" but "I noticed you posted 3 Platform Engineer roles last week—that usually means you're wrestling with service ownership at scale. Here's how Canva solved that."

**Q: This seems like a lot of tooling. What's the cost?**
A: You already have Clay and LinkedIn Sales Navigator. The signal engine is a *workflow*, not a new purchase. Incremental cost is near zero—just my time building it.

**Q: How does this help late-stage ARR specifically?**
A: Better qualified leads early = fewer zombie deals clogging Stage 3-4. Pipeline becomes predictable. Forecast accuracy improves. AEs spend time on deals that will close.

### Strategic Questions

**Q: Why this project instead of fixing something downstream?**
A: Upstream leverage. If I improve Stage 3→4 conversion by 10%, that's 10%. If I improve lead quality, that compounds through every stage. The math favors early funnel.

**Q: How will you work with Cameron's DemandGen team?**
A: Complementary, not competitive. DemandGen drives inbound and events. I make outbound smarter. We share signal data—their MQLs get enriched with my signals, my signal-sourced leads get their nurture sequences.

**Q: What's your relationship with RevOps (Daria/Matt)?**
A: They own Salesforce and data integrity. I propose, they validate. No cowboy changes to the CRM. I'll document everything and get their sign-off before any SFDC modifications.

**Q: Why should we trust you to own pipeline?**
A: Because I'll prove it fast. Week 1 deliverable: 20 signal-scored accounts with context, delivered to SDRs. Week 2: measure response rates. If it doesn't work, I'll tell you—and pivot.

### Company-Specific Questions

**Q: We're a lean team (78 people). How do you do more with less?**
A: Automation and prioritization. The signal engine means SDRs work fewer accounts, but the right ones. Quality over quantity. Every hour spent on a signal-prioritized account should convert at 2x the rate.

**Q: OpsLevel is cheaper. DX is pulling our talent. How do you think about competitive pressure?**
A: Competitive displacement is a future project. For now, I'd build a "Backstage pain" signal—companies 12-18 months into a DIY Backstage deployment who are feeling maintenance pain. They've already budget-approved the category. We're the upgrade path.

**Q: What's one thing you'd want to learn in your first week?**
A: Historical win/loss patterns. I want to see the last 50 closed-won and closed-lost deals, understand what they had in common, and see if my signal hypotheses hold up against real data.

---

## Sources

- [G2 Cortex Competitors](https://www.g2.com/products/cortex-io-cortex/competitors/alternatives)
- [Cortex Compare Page](https://www.cortex.io/compare)
- [OpsLevel: Cortex vs Backstage](https://www.opslevel.com/resources/cortex-vs-backstage-whats-the-best-internal-developer-portal)
- [Atlassian: Software Sprawl](https://www.atlassian.com/microservices/microservices-architecture/software-sprawl)
- [Demandbase: Intent Signals](https://www.demandbase.com/faq/intent-signals/)
- [UserGems: Buying Signals](https://www.usergems.com/blog/b2b-buying-signals)
- [Reo.Dev: Kubernetes Companies](https://www.reo.dev/technology/kubernetes)
- [Tigera: Kubernetes Statistics](https://www.tigera.io/learn/guides/kubernetes-security/kubernetes-statistics/)
