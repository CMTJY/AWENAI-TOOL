---
name: "mvp-development-playbook"
description: "Guide software MVP development through 7 steps: architecture lock, scope freeze, metrics framework, build execution, security review, feedback loop, and evidence-based iteration. Invoke when building a software MVP to validate PMF with minimal waste and avoid false positives."
---

# MVP Development Playbook

## Purpose

Guide software product teams through the MVP stage with a battle-tested 7-step methodology. This skill ensures you build the smallest thing that can generate real PMF evidence—while avoiding the three MVP killers: technical debt compounding, scope creep, and false PMF signals.

This is not "how to code fast"—it's **how to build the right thing, measure it correctly, and know when you have real traction vs. launch energy**.

## Key Concepts

### MVP Is Evidence Collection, Not Product Completion

The MVP stage answers: **"Does our solution solve a real problem for a real audience?"**

It does NOT answer: "Is our product feature-complete?" or "Can we scale?"

### The 3 MVP Killers

| Killer | Symptom | Prevention |
|--------|---------|------------|
| Technical Debt Compounding | No architecture doc, decisions drift per session | Write CLAUDE.md before first line of code |
| Scope Creep | "Since we're here, let's add..." | Lock scope contract with evidence thresholds |
| False PMF | Declaring victory on early numbers | Pre-define metrics + false-positive detectors |

### Evidence Hierarchy

Not all evidence is equal. From weakest to strongest:

1. **Vanity metrics** (signups, page views) — ignore
2. **Activation** (first meaningful use) — table stakes
3. **Retention** (D7/D30 sustained use) — PMF signal
4. **Sean Ellis Test** (>40% "very disappointed") — strong PMF signal
5. **Effort Test** (product "pulls" users without pushing) — strongest signal

## Application

### Step 1: Lock Architecture (CLAUDE.md) — 30 min

**Before writing production code**, document architecture decisions.

**Template**:
```markdown
# CLAUDE.md — [Product Name]

## What We're Building
[One paragraph]

## Who We Serve
[Target audience + scale assumption for next 6 months]

## Architecture Principles
- [ ] Pattern: [e.g., monolith, microservices, serverless]
- [ ] Database: [choice + why]
- [ ] Auth: [strategy]

## Conscious Trade-offs
| Decision | Rationale | Revisit When |
|----------|-----------|--------------|
| | | |

## Hard Constraints
- [ ] Security: [specific requirements]
- [ ] Performance: [target latency/throughput]
- [ ] Compliance: [GDPR/SOC2/etc.]

## Anti-patterns to Avoid
- [ ] [Specific bad practice]

## Decision Log
| Date | Decision | Context |
|------|----------|---------|
| | | |
```

**Teaching**: CLAUDE.md is your project's persistent memory. Without it, every new session re-derives decisions from scratch—decisions drift, architecture fragments, and you end up with an unmanageable codebase.

---

### Step 2: Freeze MVP Scope — 45 min

Define what you're building, what you're NOT building, and the evidence required to expand.

**Template**:
```markdown
# MVP Scope Contract

## Core Value Proposition
[One sentence: What job does this do?]

## In Scope (Locked)
| Feature | Why Required |
|---------|-------------|
| | |

## Out of Scope (Locked Until PMF)
| Feature | Why Excluded | Evidence to Reconsider |
|---------|--------------|------------------------|
| | | |

## Evidence Threshold for Expansion
Any new feature requires:
- [ ] ≥30% of 20+ active users explicitly demand it
- [ ] Removing it blocks core value delivery
- [ ] Safety/regulatory requirement

## Signed Off
- Product: ______ Date: ______
- Engineering: ______ Date: ______
```

**Teaching**: In the AI era, adding a feature takes an afternoon. The "engineering time is expensive" brake is gone. Your scope document IS the brake.

---

### Step 3: Build Metrics Framework (Pre-Launch) — 30 min

**Before the first user arrives**, define what success looks like and what false positives look like.

**Template**:
```markdown
## Metrics Framework

### Activation
- Definition: [specific action]
- Target: >__%

### Retention
- D7 Target: >__%
- D30 Target: >__%

### False-Positive Detector
| Trap | What It Looks Like | How to Detect |
|------|-------------------|---------------|
| Friend signups | High registrations, low activation | Track activation rate, not signup count |
| One-time use | Spike in week 1, flatline after | Monitor D7→D30 drop-off |
| Seeded reviews | Positive press, no organic usage | Separate organic vs. solicited feedback |

### Sean Ellis Test
"If you could no longer use this product, how would you feel?"
- Run at: D30 (not at onboarding)
- PMF threshold: >40% "Very disappointed"
```

**Teaching**: The only way to not fool yourself is to write down "what false PMF looks like" BEFORE you have any data. Once you have data, you'll want to believe.

---

### Step 4: Build with Claude Code — Ongoing

**Rule**: Every session = execute ALREADY made decisions. Not a place to make new ones.

**Session Template**:
```
1. Read CLAUDE.md
2. Read scope document
3. Execute ONE scoped task
4. Log any new decisions back to CLAUDE.md
5. Verify output against scope
```

**Teaching**: 5 minutes writing a decision log at session end is the cheapest insurance against architecture drift.

---

### Step 5: Security Review (Before Any Real User) — 30 min

**Checklist**:
- [ ] Authentication and session handling
- [ ] API response data exposure
- [ ] Input validation and injection risks
- [ ] Dependency vulnerability scan
- [ ] Any finding involving auth/keys/data → manual human review

**Teaching**: AI generates "runs" code, not "secure" code. Bugs have feedback loops—you know when something breaks. Vulnerabilities don't—you only find out when it's too late.

---

### Step 6: Run Feedback Loop (Tool Collects, Human Interprets) — Ongoing

**Weekly cadence**:
1. Collect: Automated bug reports, feature requests, usage data
2. Interpret: YOU decide what's a core need vs. nice-to-have
3. Categorize: Bug / Core need / Nice-to-have / Out of scope
4. Feed into next iteration

**Teaching**: "Users say they want X" is not a requirement. "Users need X to get value" is. Only a human can tell the difference.

---

### Step 7: Iterate Toward Evidence, Not Completeness — Ongoing

**Decision framework**:
```
Weekly data review
├── D30 retention < 40% → No PMF yet. Iterate or pivot.
├── Sean Ellis < 40% → No PMF yet. Investigate segment differences.
├── Retention good, but only in one segment → Double down on that segment.
├── Retention good across segments → GO to launch stage.
└── Multiple iterations, no improvement → Pivot. Return to discovery.
```

**Teaching**: Pretty early numbers are usually "launch energy" (friends, press, novelty), not PMF. Real PMF is a pattern that holds across multiple iteration cycles.

## Common Pitfalls

### Pitfall 1: "We Have 1000 Signups!"
**Reality**: Signups ≠ usage. Activation rate is the only early metric that matters.

### Pitfall 2: "Let's Add This Feature, It'll Only Take an Hour"
**Reality**: Death by a thousand cuts. Each addition seems reasonable; together they drown the core value.

### Pitfall 3: "We'll Measure Later"
**Reality**: If you don't define "false PMF" upfront, you'll find a way to interpret early numbers as success.

### Pitfall 4: Pivoting Too Late
**Reality**: If 3+ iterations show no retention improvement, the data is telling you something. Listen.

## References

- Source: Chapter 4 — MVP Stage Methodology & Case Study (Product Development Full-Cycle Playbook)
- Core insight: "MVP is not 'build a complete product'—it's 'trade the smallest thing for real PMF evidence'"
