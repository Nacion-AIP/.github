# Issue Ownership Guide

Every issue needs a clear owner. This guide helps you assign ownership correctly.

---

## The Core Principle

**Assign ownership based on where the complexity and uncertainty lives, not where the output appears.**

Frontend display ≠ frontend ownership.  
The person who owns the hardest part owns the feature.

---

## Ownership Framework

Ask these questions:

1. **Where is most of the new logic?**
2. **Where is the risk/uncertainty?**
3. **Who has the most context?**
4. **What's the hardest part?**

That person owns it.

---

## Decision Tree

```
Feature is primarily about:

├─ Displaying/interacting with existing data
│  └─ Owner: Full-stack engineer
│
├─ Getting data into system correctly
│  └─ Owner: Data pipeline engineer
│
├─ Forecasting/predicting/optimizing
│  └─ Owner: ML/Optimization engineer
│
├─ AI understanding/generating content
│  └─ Owner: AI agent engineer
│
└─ 50/50 split
   └─ Owner: Person with most uncertainty
```

---

## Examples

### Full-Stack Owns

**"User can filter products by category"**
- Why: UI work, simple query
- Work split: 80% frontend, 20% backend

**"User can update account settings"**
- Why: Forms, validation, CRUD
- Work split: 70% frontend, 30% backend

### Data Pipeline Owns

**"User sees real-time inventory (updates every 5 min)"**
- Why: Pipeline speed is the hard part
- Work split: 75% pipeline, 25% frontend
- Frontend just displays the number

**"User uploads CSV and sees it validated"**
- Why: Parsing, validation is complex
- Work split: 80% pipeline, 20% frontend

### ML Engineer Owns

**"User sees seasonally-adjusted forecast"**
- Why: Algorithm is the complexity
- Work split: 85% forecasting, 15% frontend
- Frontend just shows the result

---

## What Ownership Means

### Owner:
✅ Owns the demo  
✅ Coordinates integration  
✅ Makes tradeoff decisions  
✅ Reports status  
✅ Ensures it ships

### Owner Does NOT:
❌ Do 100% alone  
❌ Work in isolation  
❌ Need every skill

---

## Collaboration Example

**Feature**: "User sees forecast with confidence intervals"  
**Owner**: Forecasting engineer (Mateo)  
**Collaborator**: Full-stack (Sofia)

**Day 1**: 30-min kickoff - agree on API contract, schedule Wed pairing  
**Day 1-2**: Both build their parts (Sofia: UI with mocks, Mateo: simple forecast)  
**Day 3**: 2-hour pairing - integrate, test, fix together  
**Day 4-5**: Mateo upgrades algorithm, Sofia polishes UI, Mateo deploys

Sofia did real work. Mateo owned the outcome.

---

## Edge Cases

**50/50 split?**  
→ Assign to person with most uncertainty, OR split into 2 slices

**Full-stack overloaded?**  
→ Train others on Next.js basics, OR create reusable components

**Owner lacks frontend skills?**  
→ They don't code it, they coordinate it. Schedule pairing with full-stack.

---

*Last updated: November 2025*
