# Breaking Down Work: The Slicing Guide

Break big features into small, shippable slices. This is the most important skill for fast delivery.

---

## The Core Principle

**Build the thinnest possible slice that delivers value and teaches us something.**

Each slice should:
- ✅ Work end-to-end (UI → API → algorithm → database)
- ✅ Take 1-3 days
- ✅ Be demoable
- ✅ Teach us something

---

## Five Slicing Techniques

**1. Fake It Before You Make It**  
Hardcoded → Simple → Real → Optimized

**2. One Before Many**  
Single case → Any one → Multiple → All (optimized)

**3. Manual Before Automated**  
Human does it → Semi-automated → Fully automated

**4. Ugly Before Pretty**  
Plain table → Basic chart → Interactive → Beautiful

**5. Happy Path Before Edge Cases**  
Perfect data → Validation → Error handling → Robustness

---

## Real Example: User Sees Demand Forecast

**❌ Wrong (2 weeks, nothing until end)**

One issue: "Build demand forecasting feature"

**✅ Right (5 slices, 1-2 days each)**

**Slice 1** (1 day): "User sees hardcoded forecast for Product X"
- Just UI: `<div>Predicted: 150 units</div>`
- **Value**: Validate placement & format
- **Deploy**: Feature flag OFF

**Slice 2** (2 days): "User sees real forecast for Product X"
- Backend: Simple 7-day moving average
- Frontend: Call API
- **Value**: End-to-end works
- **Deploy**: Internal team only

**Slice 3** (2 days): "User selects product from dropdown"
- Add selector (reuse product list)
- API takes product_id
- **Value**: Client can actually use it
- **Deploy**: One beta client

**Slice 4** (2 days): "Forecast uses CatBoost model"
- Replace simple algorithm
- API contract stays same
- **Value**: Actually accurate
- **Deploy**: All clients

**Slice 5** (1 day): "User sees confidence interval"
- Add confidence range
- Show on chart
- **Deploy**: Full release

---

## The Magic Question

**"What could we show the client after 2 days that gets us 10% of the value and 90% of the learning?"**

That's your first slice.

---

## Red Flags: Slice Too Big

- ❌ Can't complete in 3 days
- ❌ Requires parallel work from multiple people
- ❌ Can't demo anything visible
- ❌ Depends on something that doesn't exist
- ❌ Words like "complete", "full", "proper"

---

## Common Mistakes

**"We need infrastructure first"**  
→ Build it when you feel pain, not before

**"It's not production-ready"**  
→ Ship behind feature flag, harden based on real issues

**"This is throwaway code"**  
→ Evolve the code, don't throw it away

**"We need to design the full API first"**  
→ Build first endpoint, learn, then design the rest

---

*Last updated: November 2025*
