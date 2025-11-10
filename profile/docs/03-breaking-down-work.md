# Breaking Down Work: The Slicing Guide

The ability to break big features into small, shippable slices is the most important skill for fast delivery. This guide teaches you how.

---

## The Core Principle

**Build the thinnest possible slice that delivers value and teaches us something.**

Not the complete feature. Not the perfect implementation. The smallest version that:
- ✅ Works end-to-end (UI → API → algorithm → database → back)
- ✅ Can be demoed to a client (even if behind feature flag)
- ✅ Delivers some value (even if small)
- ✅ Teaches us something (validates assumptions, reveals problems)

---

## The Five Slicing Techniques

### 1. Fake It Before You Make It

Start with hardcoded data, then progressively make it real.

**Example: Demand Forecast**
- Slice 1: Display hardcoded forecast number (150 units)
- Slice 2: Calculate with simple algorithm (7-day moving average)
- Slice 3: Use real ML model (CatBoost)
- Slice 4: Add confidence intervals

### 2. One Before Many

Make it work for a single case before generalizing.

**Example: Product Selection**
- Slice 1: Forecast for Product X only (hardcoded SKU)
- Slice 2: Forecast for any one product (dropdown selector)
- Slice 3: Bulk forecast for multiple products
- Slice 4: Forecast for all products (optimized query)

### 3. Manual Before Automated

Let humans do the work first, automate later.

**Example: Purchase Order Generation**
- Slice 1: User clicks "Generate PO", we email them a CSV manually
- Slice 2: System generates CSV, user downloads it
- Slice 3: System sends PO directly to supplier API
- Slice 4: Fully automated - PO generated and sent on schedule

### 4. Ugly Before Pretty

Make it work with basic UI first, polish later.

**Example: Forecast Visualization**
- Slice 1: Plain HTML table with numbers
- Slice 2: Basic chart (recharts line chart)
- Slice 3: Interactive chart (tooltips, zoom)
- Slice 4: Beautiful dashboard (animations, multiple views)

### 5. Happy Path Before Edge Cases

Make it work when everything is perfect, handle errors later.

**Example: Data Upload**
- Slice 1: Upload CSV with perfect data
- Slice 2: Validate CSV format, show errors
- Slice 3: Handle missing values (imputation)
- Slice 4: Handle outliers and data quality issues

---

## Real Examples from Our Domain

### Example 1: User Can See Demand Forecast

**❌ Wrong Way (2 weeks, nothing to show until end)**

One big issue: "Build demand forecasting feature"
- Build CatBoost model
- Create forecast API
- Add database tables
- Build UI components
- Connect everything

**✅ Right Way (5 slices, each 1-2 days)**

**Slice 1** (1 day): "User sees hardcoded forecast number for Product X"
- Just UI: `<div>Predicted demand: 150 units</div>`
- **Value**: Validate placement, format with client
- **Learning**: Do they understand what "forecast" means? Want it weekly/monthly?
- **Deploy**: Feature flag OFF, show to team

**Slice 2** (2 days): "User sees real forecast for Product X (simple algorithm)"
- Backend: 7-day moving average
- API: Returns one number for hardcoded product
- Frontend: Replace hardcoded with API call
- **Value**: Entire flow works end-to-end
- **Learning**: Pipeline has the data we need? Latency OK?
- **Deploy**: Enable for internal team

**Slice 3** (2 days): "User can select product from dropdown"
- Add product selector (reuse existing product list)
- API takes `product_id` parameter
- Still using simple algorithm
- **Value**: Client can use this for real work
- **Learning**: Which products do they check most?
- **Deploy**: Enable for one beta client

**Slice 4** (2 days): "Forecast uses CatBoost model"
- Replace moving average with ML model
- API contract stays the same
- **Value**: Forecast is now accurate
- **Learning**: Is accuracy meaningfully better?
- **Deploy**: Enable for all clients

**Slice 5** (1 day): "User sees confidence interval"
- Add confidence range to response
- Show shaded area on chart
- **Value**: User can gauge reliability
- **Deploy**: Full release

**Future slices** (ship later if needed):
- Slice 6: Historical accuracy tracking
- Slice 7: Day/week/month breakdown
- Slice 8: User can adjust assumptions

---

### Example 2: AI Agent Generates Purchase Orders

**❌ Wrong Way (3 weeks)**

"Build AI agent for PO generation"

**✅ Right Way**

**Slice 1** (2 days): "User clicks button, sees mock PO that AI 'would' generate"
- Just hardcoded HTML showing example PO
- **Value**: Validate PO format with client
- **Learning**: Is this the information they need? Right format?

**Slice 2** (2 days): "AI explains why we should order Product X (no PO yet)"
- Agent generates text explanation
- Show in chat interface
- **Value**: See if AI reasoning makes sense
- **Learning**: Is explanation helpful? What info is missing?

**Slice 3** (3 days): "AI generates actual PO for one product"
- Full agent logic for one SKU
- Generate proper PO format
- User copy-pastes to their system
- **Value**: PO is actually useful
- **Learning**: Does agent make good ordering decisions?

**Slice 4** (2 days): "PO automatically sent to supplier system"
- Integrate with supplier API
- **Value**: Fully automated for one product
- **Learning**: API integration challenges

**Slice 5** (2 days): "Works for all products"
- Scale to handle any product
- **Value**: Complete feature
- **Learning**: Performance at scale

---

### Example 3: User Uploads Sales Data

**❌ Wrong Way (2 weeks)**

"Build complete data upload and validation pipeline"

**✅ Right Way**

**Slice 1** (1 day): "User uploads CSV, sees 'File received' message"
- Just file upload UI
- Store file, don't process it
- **Value**: Upload UX works
- **Learning**: What file formats do clients use?

**Slice 2** (2 days): "Uploaded data appears in dashboard"
- Basic CSV parsing
- Insert into database
- Display in simple table
- No validation, assumes perfect data
- **Value**: End-to-end works
- **Learning**: What does "perfect" data look like?

**Slice 3** (2 days): "System validates CSV format, shows errors"
- Check required columns
- Validate data types
- Show specific error messages
- **Value**: Catches bad uploads
- **Learning**: What errors do clients actually make?

**Slice 4** (2 days): "System handles missing values"
- Imputation strategies
- User sees which values were filled
- **Value**: Works with real messy data
- **Learning**: What imputation strategy works best?

**Slice 5** (1 day): "System detects and flags outliers"
- Statistical outlier detection
- User can review before import
- **Value**: Data quality assurance
- **Learning**: What counts as an outlier in this domain?

---

## The Magic Question

When someone says a task will take 2 weeks, ask:

**"What could we show the client after 2 days that would get us 10% of the value and 90% of the learning?"**

That's your first slice.

---

## Red Flags: Your Slice Is Too Big

Stop and re-slice if:

- ❌ Can't complete in 3 days
- ❌ Requires multiple people working in parallel
- ❌ Can't demo something visible at the end
- ❌ Depends on something that doesn't exist yet
- ❌ Has words like "complete", "full", "proper", "production-ready"
- ❌ Can't merge to main for 3+ days

---

## Good Slice Characteristics

Your slice is right-sized if:

- ✅ 1-3 days of work
- ✅ One person can own it (with help from others)
- ✅ Adds visible value
- ✅ Can be demoed (even behind feature flag)
- ✅ Doesn't require future slices to be useful
- ✅ Teaches us something important

---

## Slicing Exercise

Practice with these features from our roadmap:

### Exercise 1: "Inventory optimization recommendations"

Try breaking this into 4-5 slices using the techniques above.

<details>
<summary>Click to see suggested slices</summary>

1. User sees hardcoded "optimal inventory level" for one product (1 day)
2. System calculates optimal level using simple rule (e.g., 2x average weekly sales) (2 days)
3. User can see recommendations for any product via dropdown (1 day)
4. System uses optimization algorithm accounting for holding costs (2 days)
5. User sees cost savings from following recommendations (1 day)

</details>

### Exercise 2: "Email alerts for stockouts"

Try breaking this into 3-4 slices.

<details>
<summary>Click to see suggested slices</summary>

1. User sees "low stock" indicator on dashboard (hardcoded threshold) (1 day)
2. System sends manual email when Raul clicks "Send Alert" button (1 day)
3. System automatically sends email when stock goes below threshold (2 days)
4. User can configure alert threshold and frequency per product (2 days)

</details>

---

## Common Mistakes

### Mistake 1: "We need the infrastructure first"

**Wrong**: "First we build the notification service, then we'll add features that use it"

**Right**: "For this feature, we'll send emails via SendGrid directly. If we need notifications elsewhere, we'll extract a service."

**Principle**: Build infrastructure when you feel pain, not in anticipation of pain.

---

### Mistake 2: "But it's not production-ready"

**Wrong**: "We can't ship this without proper error handling, logging, and monitoring"

**Right**: "We'll ship it behind a feature flag, enable for one client, and add robustness based on real issues we see."

**Principle**: Ship to learn, then harden based on real usage.

---

### Mistake 3: "The first version is throwaway code"

**Wrong**: "Let's build a quick prototype, then rebuild it properly"

**Right**: "Let's build the simplest real version, then refactor as needed"

**Principle**: Evolve the code, don't throw it away. Throwaway prototypes never actually get thrown away.

---

### Mistake 4: "We need to design the full API first"

**Wrong**: "Let's spec out all the endpoints before we start coding"

**Right**: "Let's build the first endpoint for the first feature, learn what we need, then design the rest."

**Principle**: Design emerges from usage, not upfront planning.

---

## Slicing Checklist

Before creating an issue, verify:

- [ ] Can be completed in 1-3 days
- [ ] Produces something visible/demoable
- [ ] Works end-to-end (even if with fake data)
- [ ] Delivers value on its own (doesn't depend on future slices)
- [ ] Teaches us something important
- [ ] One person can own it
- [ ] Can be merged to main when complete

---

## Advanced: Slice Planning Session

For complex features, hold a 30-minute slicing session:

1. **Write the big feature** (5 min)
   - "User can X" - the complete vision

2. **Ask "What's the smallest version?"** (5 min)
   - Apply the five techniques
   - Usually reveals first 2-3 slices

3. **Map dependencies** (10 min)
   - Which slices must come first?
   - Which can be parallel?

4. **Validate with magic question** (5 min)
   - "Can we show something after 2 days?"
   - If not, slice thinner

5. **Create issues** (5 min)
   - One issue per slice
   - Assign owners
   - Link them together for context

---

## Questions to Ask When Reviewing Issues

Before assigning or starting work, ask:

1. **Can this be faked first?** (Hardcoded → real)
2. **Can this work for one before many?** (One product → all products)
3. **Can this be manual before automated?** (Human in loop → fully automated)
4. **Can the UI be uglier?** (Table → fancy chart)
5. **Can we skip edge cases?** (Happy path → robust)

If answer to any is "yes", you can probably slice thinner.

---

## Remember

**"If you're not slightly embarrassed by v1, you shipped too late."**

The goal isn't to ship perfect software. The goal is to ship working software, get feedback, and improve quickly.

Every slice should be embarrassingly simple. That's the point.

---

*Last updated: November 2025*  
*Document owner: Raul*
