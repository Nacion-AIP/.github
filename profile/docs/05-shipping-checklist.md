# Shipping Checklist & Standards

What "done" means and what "shipped" requires.

---

## Definition of Done

A feature is **done** when:
- ✅ Works end-to-end in production
- ✅ Can be enabled for clients
- ✅ Owner can demo it
- ✅ Merged to main

---

## Before Closing an Issue

- [ ] Works end-to-end (tested with real data)
- [ ] Handles happy path + basic errors
- [ ] Merged to main, CI green
- [ ] Owner tested the full flow
- [ ] Can demo it

---

## Thursday: Deploy Checklist

### Before 4 PM
- [ ] All code merged to main
- [ ] Tests passing in staging
- [ ] Feature flags configured (OFF)
- [ ] Know how to rollback

### Deploy Process
1. Run deployment
2. Check health endpoints
3. Verify flags are OFF
4. Monitor for 30 min

### If Something Breaks
- Turn off feature flag (10 sec fix)
- OR rollback deployment
- Communicate to team

---

## Friday: Feature Enablement

**9 AM**: Enable for team → test → monitor  
**11 AM**: Enable for one client → monitor  
**1 PM**: Decide - all clients, or wait?

---

## Feature Flags (Quick Setup)

**Simplest version**:
```typescript
// lib/featureFlags.ts
export const flags = {
  forecastingV2: process.env.NEXT_PUBLIC_ENABLE_FORECASTING === 'true',
}

// In components
const showFeature = flags.forecastingV2
```

**Use them for**:
- Deploy code without releasing features
- Enable for specific users
- Instant rollback (turn flag OFF)

---

## Code Quality

**Python**: Pre-commit hooks handle it
```bash
uv run pre-commit run --all-files
```

**TypeScript**: Lint before pushing
```bash
pnpm lint && pnpm type-check
```

---

## When to Break Rules

Ship fast and dirty if:
- Behind feature flag
- Fix planned for next week
- Team knows what shortcuts were taken

**Done > Perfect**

---

*Last updated: November 2025*
