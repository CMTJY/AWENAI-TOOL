---
name: "hardware-compliance-workflow"
description: "Build continuous compliance workflow for hardware certifications (3C, FCC, CE, RoHS, etc.). Invoke when preparing for market entry or when adding new markets/regions to ensure certification is embedded in development cycles, not treated as a one-time project."
---

# Hardware Compliance Workflow

## Purpose

Transform hardware certification from a "one-time project" into a **continuous workflow** embedded in the product development cycle. For hardware/IoT products, compliance is not a checkbox—it's a recurring liability that grows with each new market, each design change, and each regulatory update.

This skill ensures compliance keeps pace with product evolution rather than blocking releases.

## Key Concepts

### Certification as Liability, Not Checkbox

| Phase | Compliance Risk | Cost of Failure |
|-------|----------------|-----------------|
| MVP | Minimal (single market) | Market exclusion, fines |
| Launch | Moderate (multi-market) | Recall, legal liability, brand damage |
| Scale | High (global + enterprise) | Contract cancellation, class action |

### The "Certification Tax"

Every design change must answer: **Does this trigger re-certification?**

| Change Type | Re-certification Trigger? | Examples |
|-------------|--------------------------|----------|
| Firmware only | Usually NO | Bug fixes, feature additions |
| PCB layout | MAYBE | If RF section unchanged, often no |
| RF module | YES | New antenna, new wireless protocol |
| Power supply | YES | New adapter, voltage change |
| Housing material | MAYBE | If flame rating changes |
| Manufacturing location | YES | Most certifications are site-specific |

### Market-Specific Certification Matrix

| Market | Required Certifications | Typical Cost | Typical Timeline |
|--------|------------------------|--------------|------------------|
| China | 3C (CCC), SRRC (radio), RoHS | $15K-$50K | 2-4 months |
| USA | FCC Part 15/18, UL (safety), Prop 65 | $10K-$40K | 1-3 months |
| EU | CE (RED + LVD + RoHS), WEEE | $10K-$30K | 1-3 months |
| Japan | TELEC (radio), PSE (safety) | $10K-$25K | 1-2 months |
| Global | UN38.3 (battery transport) | $5K-$10K | 2-4 weeks |

## Application

### Phase 1: Compliance Baseline (30 min)

**Template**:
```markdown
## Compliance Baseline

### Target Markets (in order of entry)
| Priority | Market | Certifications Required | Budget | Timeline | Status |
|----------|--------|------------------------|--------|----------|--------|
| 1 | | | | | |
| 2 | | | | | |
| 3 | | | | | |

### Product Risk Classification
- [ ] Mains-powered (>50V or >2A)
- [ ] Battery-powered (lithium-ion)
- [ ] RF transmitter (WiFi/BLE/Cellular/Sub-GHz)
- [ ] Medical device (any health claim)
- [ ] Children's product
- [ ] Food contact

### Certification Partner
- Primary lab: ___________
- Backup lab: ___________
- Regulatory consultant: ___________
```

### Phase 2: Design-for-Compliance Checklist (20 min)

**Template**:
```markdown
## DFC (Design for Compliance) Checklist

### Electrical Safety
- [ ] Creepage and clearance distances meet target market standards
- [ ] Fuse/circuit protection adequate for fault conditions
- [ ] Isolation barriers properly rated

### RF / EMC
- [ ] Antenna design reviewed by RF engineer
- [ ] Shielding strategy defined for high-speed signals
- [ ] EMC filter components included in BOM

### Environmental
- [ ] RoHS compliance verified for ALL components
- [ ] REACH compliance checked (if EU market)
- [ ] Battery chemistry and packaging meet UN38.3

### Labeling & Documentation
- [ ] Model number scheme defined and traceable
- [ ] Rating label includes all required markings (voltage, current, certifications)
- [ ] User manual includes all required safety warnings
- [ ] FCC/CE/3C markings correctly specified
```

### Phase 3: Change-Control Workflow (20 min)

**Template**:
```markdown
## Compliance Change-Control Workflow

### For ANY design change, ask:
1. Does this change the RF characteristics? → RF re-test required?
2. Does this change safety-critical components? → Safety re-test required?
3. Does this change the BOM? → RoHS/REACH re-verification required?
4. Does this change the manufacturing site? → Factory audit required?

### Decision Tree
```
Change proposed
├── Firmware only, no RF impact → Engineering review → Document → Proceed
├── Hardware change, no RF/safety impact → Compliance review → Document → Proceed
├── RF or safety-critical change → Full re-certification assessment → Budget + timeline → Decision
└── New market → Gap analysis against existing certs → New certification plan → Budget + timeline
```

### Compliance Review Board
- Members: Product, Engineering, Operations, Legal
- Cadence: Weekly during development, monthly during production
- Authority: Can block release if compliance risk unacceptable
```

### Phase 4: Continuous Monitoring (15 min)

**Template**:
```markdown
## Regulatory Monitoring

### Subscription List
- [ ] FCC rule updates (if US market)
- [ ] EU Official Journal (RED, LVD, RoHS directives)
- [ ] China SAMR announcements (3C catalog updates)
- [ ] Industry association newsletters

### Quarterly Compliance Review
| Check | Owner | Frequency |
|-------|-------|-----------|
| Any new regulations in target markets? | | Quarterly |
| Any components approaching EOL / regulatory change? | | Quarterly |
| Any customer complaints with safety implications? | | Monthly |
| Any competitor recalls or regulatory actions? | | Monthly |

### Incident Response
If safety incident or regulatory inquiry:
1. Document within 24 hours
2. Assess scope: single unit vs. batch vs. design flaw
3. Legal + Operations + Product triage
4. Decide: field fix / recall / regulatory notification
5. Execute within regulatory timelines
```

## Common Pitfalls

### Pitfall 1: "Certify After Design"
**Symptom**: Design complete, then send for certification
**Reality**: Certification failures at this stage require expensive redesign
**Fix**: Design-for-compliance from day one. Engage certification lab early for pre-scan.

### Pitfall 2: "One Certification Covers All"
**Symptom**: Getting FCC and assuming CE is "basically the same"
**Reality**: FCC and CE have different test methods, limits, and documentation requirements
**Fix**: Treat each certification as independent project with independent budget.

### Pitfall 3: Ignoring Component-Level Compliance
**Symptom**: "The final product is RoHS compliant, that's enough"
**Reality**: If any component is non-RoHS, the entire product is non-compliant
**Fix**: Require RoHS/REACH certificates from EVERY supplier, validated at incoming inspection.

### Pitfall 4: "We'll Add Markets Later"
**Symptom**: Designing for one market without considering expansion
**Reality**: Retrofitting for multi-market compliance is 3× more expensive than designing it in
**Fix**: Define target market roadmap in Phase 1, design for the strictest standard.

## References

- Inspired by: Launch Stage Step 3 "Security & Compliance as Continuous Workflow" from Product Development Full-Cycle Playbook
- Hardware adaptations: 3C/FCC/CE/TELEC certification, RoHS/REACH, UN38.3, design-for-compliance
