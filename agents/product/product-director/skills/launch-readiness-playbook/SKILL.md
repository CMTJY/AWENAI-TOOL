---
name: "launch-readiness-playbook"
description: "Guide software product launch through 6 steps: repay tech debt, build repeatable growth, embed security compliance, audit founder workload, establish PM processes, and resist premature scaling. Invoke when transitioning from MVP to launch stage to ensure the business is ready for sustainable growth."
---

# Launch Readiness Playbook

## Purpose

Guide software product teams through the launch stage—the critical transition from "product that works" to "business that grows sustainably." This skill ensures you repay MVP debts, build repeatable growth channels, free the founder from operational bottlenecks, and resist the temptation to scale prematurely.

The launch stage answers: **"Can this product become a sustainable business?"**

It does NOT answer: "How big can we get?" (that's scale stage).

## Key Concepts

### Launch Stage = Build the Organization Around the Product

| MVP Stage | Launch Stage |
|-----------|-------------|
| "Does the product work?" | "Does the business work?" |
| Founder in every loop | Founder designs systems |
| Speed over cleanliness | Repay debt before it compounds |
| Organic/word-of-mouth growth | Build repeatable channels |
| Security as afterthought | Security as continuous workflow |

### The Three Exit Gates

Before entering scale stage, ALL THREE must be green:

1. **Growth is repeatable and channel-driven** — CAC/LTV/payback known and stable
2. **Product withstands production load** — Tech debt repaid, security compliant, reliable
3. **Operations have no founder bottleneck** — Processes and automation run without founder

### The "Premature Scaling" Trap

The biggest threat in launch stage is not failure—it's **scaling a broken model**. A well-funded competitor copying your product is less dangerous than YOU scaling before PMF is solid.

## Application

### Step 1: Repay Technical Debt — 1-2 weeks

**Audit template**:
```markdown
## Tech Debt Audit

### Architecture Review
| Area | MVP Shortcut | Current Risk | Fix Priority |
|------|-------------|--------------|--------------|
| | | | P0/P1/P2 |

### Test Coverage
| Component | Current Coverage | Target | Gap |
|-----------|-----------------|--------|-----|
| | | 80% | |

### Documentation
| Document | Status | Owner |
|----------|--------|-------|
| Architecture decision log | | |
| API documentation | | |
| Runbooks | | |

### Fix Schedule
| Debt | Fix Effort | Blocker for Scale? | Sprint |
|------|-----------|-------------------|--------|
| | | Y/N | |
```

**Teaching**: MVP debt was borrowed at 0% interest. In launch stage, it starts compounding. AI makes borrowing faster—so repayment must be intentional.

---

### Step 2: Build Repeatable Growth — 2-3 weeks

**Channel audit**:
```markdown
## Growth Channel Analysis

### Historical Performance (last 3 months)
| Channel | Users | CAC | Retention | Repeatable? |
|---------|-------|-----|-----------|-------------|
| | | | | Y/N |

### Unit Economics
- CAC: $____
- LTV: $____
- LTV/CAC ratio: ____ (target >3)
- Payback period: ____ months (target <6)

### Repeatability Test
A channel is "repeatable" if:
- [ ] "Spend $X, get Y users" is predictable
- [ ] CAC stable across 3+ months
- [ ] Not dependent on one person/event/relationship
```

**Teaching**: "One viral post" or "one big customer" is not a growth engine. Repeatable = "Do it again and it still works."

---

### Step 3: Embed Security & Compliance — 1-2 weeks

**Transform from "project" to "workflow"**:

```markdown
## Security & Compliance Workflow

### Automated (CI/CD)
- [ ] Dependency vulnerability scan
- [ ] Static code analysis
- [ ] Secret detection
- [ ] Infrastructure as code validation

### Per-Release
- [ ] Security review for auth/data changes
- [ ] Privacy impact assessment (if user data changes)
- [ ] Compliance documentation update

### Quarterly
- [ ] Penetration test or bug bounty review
- [ ] Access audit (who has what)
- [ ] Incident response drill

### On Incident
1. Document within 1 hour
2. Assess scope: single user / batch / systemic
3. Triage: Engineering + Security + Legal
4. Notify per regulatory requirements
5. Post-mortem within 1 week
```

**Teaching**: In MVP, a vulnerability is a "theoretical risk." With real users and real data, it's a "real liability." Compliance is not a one-time project—it's a muscle you build.

---

### Step 4: Audit Founder Workload — 1 week

**Categorize everything the founder does**:

```markdown
## Founder Workload Audit

| Task | Frequency | Can Automate? | Can Delegate? | Must Be Founder? |
|------|-----------|---------------|---------------|-----------------|
| | | Y/N | Y/N | Y/N |

### Automation Targets
| Task | Trigger | Action | Output |
|------|---------|--------|--------|
| | | | |

### Delegation Targets
| Task | Delegate To | Transition Plan |
|------|-------------|-----------------|
| | | |

### Founder-Only Zone
| Task | Why Only Founder? |
|------|-------------------|
| Product narrative | Vision + context |
| Board/investor relations | Accountability |
| Strategic partnerships | Relationship + judgment |
| Crisis decisions | Authority + context |
```

**Teaching**: In MVP, "founder in every loop" is an asset. In launch, it's a constraint. The hardest transition is psychological—no one tells you it's time to let go.

---

### Step 5: Establish Product Management Process — 1 week

**Lightweight, repeatable system**:

```markdown
## Product Management OS

### Sprint Rhythm
- Cycle: 2 weeks
- Planning: Monday Week 1
- Review: Friday Week 2
- Retro: Friday Week 2

### Before Building
| Requirement | Template | Owner |
|-------------|----------|-------|
| Problem statement | 1 paragraph | PM |
| Hypothesis | "We believe..." | PM |
| Success metric | One primary metric | PM |
| Out of scope | Explicit list | PM |

### Bug Triage
| Severity | Response Time | Escalation |
|----------|--------------|------------|
| P0 (down) | Immediate | Founder |
| P1 (broken core) | 24 hours | Engineering lead |
| P2 (workaround exists) | 1 sprint | PM |
| P3 (nice-to-fix) | Backlog | PM |

### Weekly Metrics Brief
| Metric | Current | Target | Trend | Action |
|--------|---------|--------|-------|--------|
| | | | | |
```

**Teaching**: Process is not bureaucracy—it's the system that lets you sleep while the company runs.

---

### Step 6: Resist Premature Scaling — Ongoing

**The "Three Questions" before any expansion**:

1. **Is the new audience/channel identical to our proven PMF segment?**
   - If NO → Run separate validation. Don't assume transfer.

2. **Will expansion introduce so many variables that we can't read our data?**
   - If YES → Delay until core metrics are stable.

3. **Will pursuing the new opportunity divert resources from our proven core?**
   - If YES → Core comes first. New opportunity = separate team or time block.

**Hard stops** (do NOT expand if):
- [ ] Core retention < 40% at D30
- [ ] Unit economics not yet profitable
- [ ] Product has >5% critical bug rate
- [ ] Cash runway < 12 months
- [ ] Team bandwidth requires hiring before expansion

**Teaching**: The biggest opportunity that comes knocking in launch stage is often a trap. "Similar but different" audiences kill more products than competitors do.

## Common Pitfalls

### Pitfall 1: "We'll Fix Debt Later"
**Reality**: Later = more expensive. Debt compounds. In software, compounding means slower development, more bugs, and eventually a rewrite.

### Pitfall 2: "One Big Customer Will Save Us"
**Reality**: A single enterprise customer demanding custom features is not product-market fit—it's consulting. Build for a segment, not a customer.

### Pitfall 3: "The Founder Can Handle It"
**Reality**: If the founder is the bottleneck for >20% of operational decisions, the business cannot scale. Build systems.

### Pitfall 4: Scaling Into "Similar" Markets
**Reality**: "Similar" audiences often have different behaviors, compliance needs, and competitive landscapes. Validate separately.

## References

- Source: Chapter 5 — Launch Stage Methodology & Case Study (Product Development Full-Cycle Playbook)
- Core insight: "Launch stage is not 'make the product bigger'—it's 'make the business sustainable while resisting the temptation to scale prematurely'"
