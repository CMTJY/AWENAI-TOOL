---
name: "hardware-evidence-metrics"
description: "Build pre-launch measurement framework and PMF validation metrics for hardware/IoT products. Invoke before any hardware goes to production to define activation, retention, and false-positive detectors."
---

# Hardware Evidence & Metrics Framework

## Purpose

Define a measurement framework for hardware/IoT products BEFORE production begins. Hardware has no "deploy patch" safety net—once units ship, data collection must already be in place. This skill ensures you can distinguish real PMF from "launch energy" (early adopters, novelty effect, gift purchases).

This is not analytics setup—it's a **decision framework** that defines: What evidence would convince us this hardware deserves to exist?

## Key Concepts

### Hardware PMF Is Different from Software PMF

| Dimension | Software PMF | Hardware PMF |
|-----------|-------------|--------------|
| Activation | Sign up + complete first action | Unbox + connect + complete first meaningful use |
| Retention | D7/D30 login | D7/D30 active use (not "sitting in drawer") |
| Revenue | Subscription/transaction | Device margin + attach rate (consumables/services) |
| Churn signal | Cancel subscription | Device stops sending data / goes offline |
| False positive | Trial signup | Gift purchase, Kickstarter backer, novelty buy |

### The "Drawer Test"

The ultimate hardware PMF question: **Is the device out of the drawer and doing its job?**

- Software: User can re-engage with an email
- Hardware: Once in drawer, re-engagement cost is near-infinite

### False-Positive Catalog for Hardware

| False Positive | What It Looks Like | What PMF Actually Looks Like |
|----------------|-------------------|------------------------------|
| Kickstarter success | Thousands of backers, most never use it | Repeat purchase rate >15% after initial batch |
| Gift purchases | High holiday sales | Post-holiday activation rate >60% |
| Novelty effect | High first-week usage | Sustained D30 usage >40% of activated |
| Enterprise pilot | One big company tries it | Expansion to additional sites/departments |
| Reviewer units | Positive press coverage | Organic user reviews without solicitation |

## Application

### Phase 1: Define Activation (15 min)

**Hardware activation = Unbox + Setup + First meaningful use**

**Template**:
```markdown
## Activation Definition

### Step 1: Unbox Success Rate
- Target: >95% can unbox and identify all components without manual
- Measure: Support tickets tagged "unboxing confusion"

### Step 2: Setup Completion Rate
- Target: >80% complete setup within 24 hours of unboxing
- Measure: App pairing success / WiFi connection / account creation

### Step 3: First Meaningful Use
- Target: >70% complete core job within 48 hours
- Measure: [Define device-specific action]
  - Example (air purifier): Run auto-mode for >2 hours
  - Example (smart lock): Lock/unlock remotely 3+ times
  - Example (IoT sensor): First data upload + dashboard view
```

### Phase 2: Define Retention (20 min)

**Hardware retention = Device is actively serving its purpose**

**Template**:
```markdown
## Retention Metrics

### D7 Retention
- Definition: Device online + performing core function in Week 2
- Target: >50% of activated devices
- False positive: Device online but not used (detect via interaction logs)

### D30 Retention
- Definition: Device online + performing core function in Week 5
- Target: >40% of activated devices
- Critical: This is the PMF line for hardware

### D90 Retention
- Definition: Device still in active use at Month 3
- Target: >30% of activated devices
- Signal: Habit formation complete

### "Drawer Rate"
- Definition: Device offline for >14 consecutive days
- Target: <20% of activated devices by D90
- Action trigger: If >30%, investigate: power issue? UX failure? Job not real?
```

### Phase 3: Define Revenue Evidence (15 min)

**Template**:
```markdown
## Revenue Evidence

### Unit Economics (Must Know Before Scaling)
- BOM cost: $____
- Landed cost (BOM + assembly + logistics): $____
- Retail price: $____
- Gross margin: ____%
- Target: >40% gross margin at 1K units

### Attach Rate (If Applicable)
- Consumable attach: ____% buy refills within 60 days
- Service attach: ____% subscribe to premium features
- Target: >20% attach rate indicates product-ecosystem fit

### Payback Evidence
- CAC (customer acquisition cost): $____
- LTV (lifetime value): $____
- Target: LTV/CAC > 3x
```

### Phase 4: Build False-Positive Detector (15 min)

**Template**:
```markdown
## False-Positive Checklist

Before declaring PMF, verify NONE of these are the primary driver:

- [ ] Sales are not primarily gifts (survey: "Did you buy this for yourself?")
- [ ] Usage is not concentrated in first week only (check D7→D30 drop-off)
- [ ] Reviews are not from seeded/reviewer units (check verified purchase)
- [ ] Growth is not from one-time channel (e.g., single influencer post)
- [ ] Retention is not from a single enterprise customer (need 3+ independent accounts)

### Sean Ellis Test for Hardware
"If this device stopped working tomorrow and you couldn't replace it, how would you feel?"
- >40% "Very disappointed" = PMF signal
- Run at D30, not at unboxing
```

### Phase 5: Evidence Review Cadence (10 min)

| Milestone | Data Review | Decision |
|-----------|-------------|----------|
| Week 2 post-launch | Activation rate | If <50%, investigate setup UX |
| Week 5 post-launch | D30 retention + Sean Ellis | If <40% retention, no PMF yet |
| Week 12 post-launch | D90 retention + unit economics | If margin <40%, fix cost structure before scaling |
| Monthly | Segment analysis | Which user segment retains best? Double down. |

## Common Pitfalls

### Pitfall 1: Measuring "Shipped" Instead of "Activated"
**Symptom**: "We shipped 1,000 units! We're successful!"
**Reality**: Shipped ≠ Used. 40% may never leave the box.
**Fix**: Activation rate is the only early metric that matters.

### Pitfall 2: Ignoring the "Drawer"
**Symptom**: Focusing on sales velocity, not usage persistence
**Reality**: Hardware PMF requires usage habit, not just purchase intent
**Fix**: Track "drawer rate" as rigorously as retention

### Pitfall 3: Declaring PMF on Launch Energy
**Symptom**: First-month numbers look great, declare victory
**Reality**: Early adopters are not representative; novelty effect is real
**Fix**: Require D30 data minimum before PMF discussion

## References

- Inspired by: MVP Stage Step 3 "Pre-Launch Metrics" and Step 7 "Evidence-Based Iteration" from Product Development Full-Cycle Playbook
- Hardware adaptations: Drawer test, attach rate, unit economics, unbox success
