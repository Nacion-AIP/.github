# Issue Ownership Guide

Every issue needs a clear owner. This guide helps you determine who should own what and how ownership works in a team with specialized roles.

---

## The Core Principle

**Assign ownership based on where the complexity and uncertainty lives, not where the final output appears.**

Just because a feature shows up in the UI doesn't mean the frontend engineer owns it. The person who owns the hardest, most uncertain part should own the feature.

---

## Ownership Framework

### Ask These Questions (In Order):

1. **Where is most of the new logic?**  
   (Frontend, backend API, algorithm, data pipeline)

2. **Where is the risk/uncertainty?**  
   (What's most likely to be wrong or take longer?)

3. **Who has the most context for the problem?**  
   (Domain knowledge, previous related work)

4. **What's the hardest part?**  
   (That person should own it)

The answers point to your owner.

---

## Decision Tree for Our Team

```
Is the feature primarily about:

├─ Displaying/interacting with existing data?
│  └─ Owner: Full-stack engineer
│  └─ Examples: Dashboards, forms, navigation, CRUD operations
│
├─ Getting data into the system correctly?
│  └─ Owner: Data pipeline engineer
│  └─ Examples: Ingestion, validation, transformation, ETL
│
├─ Forecasting/predicting demand?
│  └─ Owner: Forecasting engineer
│  └─ Examples: ML models, seasonality, accuracy improvements
│
├─ Optimizing decisions (inventory, orders)?
│  └─ Owner: Optimization engineer
│  └─ Examples: Purchase orders, reorder points, cost minimization
│
├─ AI understanding/generating content?
│  └─ Owner: AI agent engineer
│  └─ Examples: Natural language queries, recommendations, explanations
│
└─ Equally split (50/50)?
   └─ Owner: Person with most uncertainty/risk
   └─ Or: Break into 2 slices with different owners
```

---

## Examples by Owner

### ✅ Full-Stack Engineer Owns

**"User can filter products by category on dashboard"**
- **Why**: Mostly UI work, simple backend query
- **Center of gravity**: Frontend filtering logic, UX
- **Collaborators**: Backend engineer for query optimization (if needed)
- **Work split**: 80% frontend, 20% backend
- **Deliverable**: Working filter dropdown with results

---

**"User can see their account settings and update email"**
- **Why**: CRUD operations, UI forms, validation
- **Center of gravity**: Form handling, validation logic
- **Collaborators**: Backend for API endpoint (straightforward)
- **Work split**: 70% frontend, 30% backend
- **Deliverable**: Settings page with save functionality

---

**"User can export current view to CSV"**
- **Why**: UI interaction, client-side data formatting
- **Center of gravity**: Export UX, data formatting
- **Collaborators**: None needed (handle in frontend)
- **Work split**: 90% frontend
- **Deliverable**: Export button that downloads CSV

---

### ✅ Data Pipeline Engineer Owns

**"User sees real-time inventory levels updated within 5 minutes"**
- **Why**: Core challenge is pipeline speed and reliability
- **Center of gravity**: Data ingestion, processing, scheduling
- **Collaborators**: Full-stack adds simple UI indicator (easy)
- **Work split**: 75% pipeline, 25% frontend
- **Deliverable**: Dashboard shows current inventory with timestamp

---

**"User can upload sales CSV and see it processed correctly"**
- **Why**: Parsing, validation, transformation is complex
- **Center of gravity**: Data quality, error handling
- **Collaborators**: Full-stack creates upload form (simple)
- **Work split**: 80% pipeline, 20% frontend
- **Deliverable**: Upload works with real messy data

---

**"User sees data quality report highlighting issues"**
- **Why**: Detecting data issues requires domain knowledge
- **Center of gravity**: Validation rules, anomaly detection
- **Collaborators**: Full-stack displays report (given structured data)
- **Work split**: 85% pipeline, 15% frontend
- **Deliverable**: Report showing gaps, duplicates, outliers

---

### ✅ Forecasting Engineer Owns

**"User sees demand forecast that accounts for seasonality"**
- **Why**: Algorithm complexity, model training
- **Center of gravity**: Feature engineering, model selection
- **Collaborators**: Full-stack displays number/chart (straightforward)
- **Work split**: 85% forecasting, 15% frontend
- **Deliverable**: Seasonally-adjusted forecasts in dashboard

---

**"User sees why forecast changed from last week"**
- **Why**: Requires model explainability, tracking
- **Center of gravity**: Feature importance, comparison logic
- **Collaborators**: Full-stack shows explanation (given text/data)
- **Work split**: 90% forecasting, 10% frontend
- **Deliverable**: Explanation panel showing factors driving change

---

**"Forecast accuracy improves to <10% MAPE"**
- **Why**: Pure model improvement
- **Center of gravity**: Algorithm research, hyperparameter tuning
- **Collaborators**: None needed initially
- **Work split**: 100% forecasting
- **Deliverable**: Model with validated accuracy improvement

---

### ✅ Optimization Engineer Owns

**"User receives purchase order recommendations that minimize costs"**
- **Why**: Optimization algorithm is complex
- **Center of gravity**: Constraint handling, objective function
- **Collaborators**: Full-stack shows recommendations (table/cards)
- **Work split**: 85% optimization, 15% frontend
- **Deliverable**: PO recommendations visible in dashboard

---

**"User can set constraints for optimization (max order size, budget)"**
- **Why**: Constraint logic is the hard part
- **Center of gravity**: Updating optimization model with constraints
- **Collaborators**: Full-stack creates settings form
- **Work split**: 60% optimization, 40% frontend
- **Deliverable**: Settings persist and affect recommendations

---

**"System shows cost savings from following recommendations"**
- **Why**: Calculating savings requires optimization knowledge
- **Center of gravity**: Baseline comparison, metrics
- **Collaborators**: Full-stack displays metrics
- **Work split**: 70% optimization, 30% frontend
- **Deliverable**: Savings calculation visible to user

---

### ✅ AI Agent Engineer Owns

**"User can ask 'what should I order this week' and get an answer"**
- **Why**: NLP, prompt engineering, orchestration
- **Center of gravity**: Agent reasoning, tool use
- **Collaborators**: Full-stack creates chat interface
- **Work split**: 80% AI agent, 20% frontend
- **Deliverable**: Working chat that gives recommendations

---

**"Agent explains its reasoning for recommendations"**
- **Why**: Agent needs to track and articulate reasoning
- **Center of gravity**: Prompt engineering, structured output
- **Collaborators**: Full-stack displays explanation
- **Work split**: 85% AI agent, 15% frontend
- **Deliverable**: Recommendations with clear explanations

---

**"Agent can access inventory data to answer questions"**
- **Why**: Tool integration, context management
- **Center of gravity**: Agent orchestration, API calls
- **Collaborators**: Backend exposes data API (if needed)
- **Work split**: 75% AI agent, 25% backend
- **Deliverable**: Agent answers questions using real data

---

## How to Write Issues for Different Owners

The issue title and description should make ownership obvious.

### Template

**[User-facing outcome] ([technical emphasis])**

### Examples

#### For Backend/Algorithm Owners:

**"User sees accurate 30-day demand forecast (new CatBoost model)"**
- Title emphasizes: "accurate" and "CatBoost model"
- Clear this is about the algorithm
- Owner: Forecasting engineer

**"User sees sales data with no gaps or duplicates (automated validation)"**
- Title emphasizes: "no gaps or duplicates" and "validation"
- Clear this is about data quality
- Owner: Data pipeline engineer

**"User receives cost-optimal PO recommendations (new optimization algorithm)"**
- Title emphasizes: "cost-optimal" and "algorithm"
- Clear this is about optimization logic
- Owner: Optimization engineer

#### For Frontend Owners:

**"User can filter products by multiple criteria via searchable dropdown"**
- Title emphasizes: UI interaction
- Clear this is about frontend
- Owner: Full-stack engineer

**"User sees loading states and error messages throughout the app"**
- Title emphasizes: UI/UX polish
- Clear this is about frontend
- Owner: Full-stack engineer

#### For Ambiguous Cases:

**"User can schedule automatic report generation (backend: cron job + email)"**
- Title makes clear where complexity lives
- Owner: Backend engineer (scheduling is hard part)

---

## What Ownership Means

### The Owner:

✅ **Owns the demo** - Can show it working end-to-end on Thursday  
✅ **Coordinates integration** - Schedules pairing with collaborators  
✅ **Makes tradeoff decisions** - "Let's simplify UI" or "Use simpler algorithm"  
✅ **Unblocks themselves** - Asks for help proactively  
✅ **Reports status** - In daily standup, reports for whole feature  
✅ **Ensures it ships** - Steps in if collaborator is blocked

### The Owner Does NOT:

❌ Do 100% of the work themselves  
❌ Work in isolation then "hand off"  
❌ Blame collaborators if integration fails  
❌ Need to know every technology in the stack

---

## Collaboration Pattern

### Example: "User sees forecast with confidence intervals"

**Owner**: Forecasting engineer (Mateo)  
**Collaborator**: Full-stack engineer (Sofia)

#### ❌ Bad Way:

- **Week 1**: Mateo builds forecast API alone
- **Week 1**: Sofia builds UI with mock data alone  
- **Week 2**: Try to integrate, API format doesn't match UI
- **Week 3**: Fixing integration issues

#### ✅ Good Way:

**Day 1** (Monday):
- **30-min kickoff together**:
  - Agree on API contract (what fields, format)
  - Sofia shows mockup
  - Mateo confirms it's feasible
  - Schedule Wednesday pairing session

**Day 1-2** (Mon-Tue):
- Sofia: Builds UI with hardcoded data (matching agreed format)
- Mateo: Builds simplest forecast (even just moving average)

**Day 3** (Wednesday):
- **2-hour pairing session**:
  - Mateo exposes API endpoint
  - Sofia integrates with real API
  - Together: Test, find issues, fix immediately
  - Result: Working end-to-end

**Day 4-5** (Thu-Fri):
- Mateo: Upgrades to CatBoost model (API stays same)
- Sofia: Adds polish based on real data
- **Mateo deploys** (he's the owner)
- Friday: Demo together

**Notice**: Sofia did meaningful work, but Mateo owned the outcome.

---

## Handling Edge Cases

### "What if it's truly 50/50 frontend/backend?"

**Option 1**: Assign owner based on slight edge

**"User can export forecast to Excel (frontend 50%, backend 50%)"**
- Owner: Full-stack engineer (export UX matters more)
- Collaborators: Backend for export logic
- Schedule pairing upfront

**Option 2**: Split into two slices

**Slice 1**: "User sees 'Export' button (generates CSV)"
- Owner: Full-stack (frontend heavy)
- Backend provides simple CSV endpoint

**Slice 2**: "Export includes formatted Excel with charts"
- Owner: Backend engineer
- Frontend just triggers download

---

### "What if full-stack engineer is overloaded?"

This reveals one of two issues:

**1. Your features are too UI-heavy** (Good problem!)
- Solution: Train other engineers on Next.js basics
- Solution: Create component library so others can add UI

**2. You're assigning wrong** (Bad problem)
- Solution: Review assignment framework above
- Backend-heavy features going to full-stack engineer

---

### "What if owner doesn't have frontend skills?"

**They don't need them.** They coordinate.

**Example**: Data pipeline engineer owns "User sees real-time inventory"

**How it works**:
1. Pipeline engineer builds the pipeline (their expertise)
2. Schedules pairing with full-stack engineer
3. In pairing: full-stack writes UI code
4. Pipeline engineer owns ensuring it works
5. Pipeline engineer demos it (full-stack can help if needed)

---

## Quick Reference: Work Split Estimation

When breaking down features, quickly estimate:

```
Frontend work: X%
Backend API work: Y%
Algorithm/data work: Z%
```

**Assign owner to whoever has highest %.**

### Examples:

**"User sees product recommendations based on purchase history"**
- Frontend: 20% (display cards)
- Backend: 25% (retrieve data, format)
- Recommendation algorithm: 55%
- **Owner**: AI agent engineer

**"User can edit product details in a modal"**
- Frontend: 60% (modal, form, validation)
- Backend: 40% (update endpoint)
- **Owner**: Full-stack engineer

**"User sees inventory replenishment alerts"**
- Frontend: 30% (notification UI)
- Backend: 20% (notification API)
- Replenishment logic: 50%
- **Owner**: Optimization engineer

---

## Red Flags

### Watch for these signs of wrong assignment:

- 🚨 Full-stack engineer owns 80%+ of issues
- 🚨 Backend engineers say "I can't own it, no frontend skills"
- 🚨 Issues sit unassigned because ownership is unclear
- 🚨 Constant "this should be assigned to someone else" comments
- 🚨 Owner never demos (someone else always presents)

**Fix**: Review this guide, discuss in retro, reassign based on framework.

---

## Checklist: Before Assigning an Issue

Use this when creating or assigning work:

- [ ] Issue title makes ownership clear
- [ ] Center of gravity identified (where's the complexity?)
- [ ] Owner assigned based on that complexity
- [ ] Collaborators identified and notified
- [ ] Integration points documented
- [ ] Pairing session scheduled (if needed)
- [ ] Everyone understands their role

---

## Remember

**Owner ≠ Solo worker**

Ownership is about accountability and coordination, not doing everything yourself.

The owner ensures the feature ships. The team makes it happen.

---

*Last updated: November 2025*  
*Document owner: Raul*
