# Shipping Checklist & Standards

This document defines what "done" means and what "shipped" requires. Use these checklists to ensure quality while maintaining speed.

---

## Our Definition of Done

A feature is **done** when:
- ✅ Works end-to-end in production
- ✅ Can be enabled for clients (even if behind feature flag)
- ✅ Owner can demo it successfully
- ✅ Basic error handling in place
- ✅ Code is merged to main

A feature is **NOT done** if:
- ❌ Only works locally
- ❌ Only works in staging
- ❌ Has broken tests
- ❌ Requires manual intervention to work
- ❌ Sits in a long-lived branch

---

## Before Marking Issue Complete

Use this checklist before closing any issue:

### Functionality
- [ ] Works end-to-end (UI → API → algorithm → database → back)
- [ ] Tested with real data (not just mock/seed data)
- [ ] Handles the happy path successfully
- [ ] Basic error handling in place (doesn't crash on common errors)
- [ ] Owner has personally tested the full flow

### Code Quality
- [ ] Code merged to `main` branch
- [ ] All tests passing (CI is green)
- [ ] Pre-commit hooks pass (Python projects)
- [ ] No console errors or warnings in production
- [ ] TODO comments cleaned up or converted to issues

### Integration
- [ ] Integrated with collaborators' work
- [ ] API contracts match between frontend/backend
- [ ] Database migrations run successfully
- [ ] Environment variables documented (if new ones added)

### Demo-Ready
- [ ] Owner can demo it to the team
- [ ] Screenshots/recording available (for async review)
- [ ] Feature flag configured (if applicable)

### Documentation
- [ ] README updated (if setup changed)
- [ ] API docs updated (if endpoints changed)
- [ ] Comments added for complex logic

---

## Thursday: Pre-Deploy Checklist

Go through this as a team before deploying to production.

### Code Readiness
- [ ] All planned features merged to `main`
- [ ] No open PRs blocking the release
- [ ] CI/CD pipeline passing
- [ ] All tests green (unit, integration, E2E)

### Staging Verification
- [ ] Features tested in staging environment
- [ ] Smoke tests completed:
  - [ ] User can log in
  - [ ] Critical paths work (orders, forecasts, etc.)
  - [ ] New features work as expected
- [ ] Performance acceptable (no obvious slowdowns)
- [ ] No console errors

### Feature Flags
- [ ] All new features behind feature flags
- [ ] Feature flags default to OFF
- [ ] Flag configuration tested in staging
- [ ] Team knows how to enable/disable flags

### Deployment Plan
- [ ] Deployment commands ready:
  ```bash
  # Next.js app
  cd dp-app && pnpm deploy:production
  
  # API services
  cd dp-api && ./deploy.sh production
  
  # Python services (example)
  cd dp-forecast-engine && ./deploy.sh
  ```
- [ ] Person assigned to monitor deployment
- [ ] Rollback plan documented (see below)

### Risk Assessment
- [ ] Database migrations are reversible (or tested)
- [ ] No breaking API changes (or handled gracefully)
- [ ] External dependencies checked (APIs, third-party services)
- [ ] High-risk changes identified and discussed

### Communication
- [ ] Team knows deployment is happening
- [ ] Clients informed (if user-facing changes)
- [ ] Support team briefed (if applicable)

### Monitoring
- [ ] CloudWatch dashboards ready
- [ ] Error tracking configured (Sentry, etc.)
- [ ] Performance monitoring active (APM, if available)
- [ ] Log aggregation working

---

## Thursday: Deployment Process

Follow these steps during deployment:

### 1. Pre-Flight (15 min before)
- [ ] Team on Slack/call and available
- [ ] Staging final smoke test complete
- [ ] All checklists above reviewed

### 2. Deploy (30 min)
- [ ] Run deployment commands
- [ ] Verify deployment succeeded (check CI/CD logs)
- [ ] Confirm services are running:
  ```bash
  # Check health endpoints
  curl https://api.nacion-aip.com/health
  curl https://app.nacion-aip.com/api/health
  ```
- [ ] Check CloudWatch metrics (CPU, memory, errors)

### 3. Smoke Test Production (15 min)
- [ ] Log in as test user
- [ ] Navigate through critical paths:
  - [ ] Dashboard loads
  - [ ] Can view forecasts
  - [ ] Can generate reports
  - [ ] Can upload data
- [ ] Check browser console (no new errors)
- [ ] Check server logs (no unexpected errors)

### 4. Feature Flags Still OFF (5 min)
- [ ] Verify new features not visible to users
- [ ] Confirm flags are configured correctly
- [ ] Test flag enablement/disablement

### 5. Monitor (30 min)
- [ ] Watch error rates in Sentry/CloudWatch
- [ ] Check API response times
- [ ] Monitor database connections
- [ ] Verify background jobs running

### 6. All Clear or Rollback
- [ ] If everything looks good → document completion, done for today
- [ ] If issues found → execute rollback plan (see below)

---

## Rollback Plan

If deployment fails or causes issues:

### Quick Rollback (Feature Flags)
1. **Disable feature flags immediately**:
   ```bash
   # Access feature flag admin
   # Turn problematic features OFF
   ```
2. **Verify issue is resolved**
3. **Debug offline, plan fix for next week**

### Full Rollback (Code)
1. **Revert to previous deployment**:
   ```bash
   # Example - adjust for your setup
   ./rollback.sh production [previous-version]
   ```
2. **Verify services are running**
3. **Communicate to team and clients (if needed)**
4. **Post-mortem: what went wrong, how to prevent**

### When to Rollback
- 🚨 Critical functionality broken
- 🚨 Error rate spike (>5% of requests)
- 🚨 Performance degradation (>2x slower)
- 🚨 Data integrity issues
- 🚨 Authentication broken

### When NOT to Rollback
- ✅ Minor UI bug (fix with feature flag + quick patch)
- ✅ Single client affected (disable for that client)
- ✅ Non-critical feature has issue (disable feature flag)

---

## Friday: Feature Enablement

Follow this process to safely enable new features.

### 9:00 AM: Enable for Internal Team

1. **Turn on feature flags for team emails**:
   ```javascript
   // Example feature flag config
   {
     forecasting_v2: {
       enabled: true,
       users: ['raul@nacion-aip.com', 'sofia@nacion-aip.com', ...]
     }
   }
   ```

2. **Test all functionality**:
   - [ ] Each team member tests their part
   - [ ] Integration points verified
   - [ ] Happy path works
   - [ ] Error cases handled

3. **Document any issues found**:
   - Create issues for bugs
   - Decide: fix now or disable feature?

### 10:00 AM - 12:00 PM: Monitor

- [ ] Watch logs for errors
- [ ] Check performance metrics
- [ ] Verify no unexpected behavior
- [ ] Team discusses any concerns

### 12:00 PM: Decision Point

**If everything works:**
- ✅ Proceed to beta client enablement

**If issues found:**
- ❌ Disable feature flag
- ❌ Plan fix for next week
- ❌ Document learnings in retro

### 1:00 PM: Enable for Beta Client (if applicable)

1. **Select one friendly client** (someone who gives good feedback)

2. **Enable feature for them**:
   ```javascript
   {
     forecasting_v2: {
       enabled: true,
       users: [...team, 'client@example.com']
     }
   }
   ```

3. **Inform them**:
   - Brief email or message
   - "We've enabled [feature] for you. Please try it and let us know what you think."

4. **Monitor closely** (2-4 hours):
   - Watch their usage
   - Check for errors
   - Be ready to respond to questions

### 3:00 PM: Final Decision

**Option A: Enable for all clients**
- Everything working great
- Beta client had positive experience
- No issues found

**Option B: Keep beta for another week**
- Works but want more feedback
- Minor issues to fix
- Want to see more usage

**Option C: Disable and fix**
- Issues found
- Needs more work
- Plan fix for next week

---

## Feature Flag Setup

### Using Environment Variables (Simplest)

**In your Next.js app**:
```typescript
// lib/featureFlags.ts
export const featureFlags = {
  forecastingV2: process.env.NEXT_PUBLIC_ENABLE_FORECASTING_V2 === 'true',
  aiAgent: process.env.NEXT_PUBLIC_ENABLE_AI_AGENT === 'true',
  optimizationEngine: process.env.NEXT_PUBLIC_ENABLE_OPTIMIZATION === 'true',
}

export function useFeatureFlag(flag: keyof typeof featureFlags) {
  return featureFlags[flag] ?? false
}
```

**Usage in components**:
```typescript
import { useFeatureFlag } from '@/lib/featureFlags'

export function Dashboard() {
  const showForecastingV2 = useFeatureFlag('forecastingV2')
  
  return (
    <div>
      <SalesChart />
      {showForecastingV2 && <NewForecastingWidget />}
    </div>
  )
}
```

**In your .env files**:
```bash
# .env.local (development)
NEXT_PUBLIC_ENABLE_FORECASTING_V2=true

# .env.production (production)
NEXT_PUBLIC_ENABLE_FORECASTING_V2=false
```

### Using Database (Better)

Store flags in database for dynamic control:

```sql
CREATE TABLE feature_flags (
  flag_name VARCHAR(255) PRIMARY KEY,
  enabled BOOLEAN DEFAULT false,
  allowed_users TEXT[], -- array of email addresses
  created_at TIMESTAMP DEFAULT NOW()
);
```

**Benefits**:
- Change flags without re-deploying
- Enable for specific users
- Audit trail of changes

### Using a Service (Best for scale)

When you have >5 flags or >10 users:
- [LaunchDarkly](https://launchdarkly.com) (paid, enterprise)
- [Flagsmith](https://flagsmith.com) (open source)
- [PostHog](https://posthog.com/feature-flags) (includes analytics)

---

## Code Quality Standards

### Python Projects

**All checks run automatically via pre-commit hooks:**
- Black (formatting)
- Ruff (linting)
- MyPy (type checking)
- Bandit (security)
- Pytest (tests)

**Before pushing**:
```bash
# Run all checks
uv run pre-commit run --all-files

# If checks fail, fix them
# Most formatting issues are auto-fixed
git add .
git commit -m "your message"
```

### TypeScript/Next.js Projects

**Linting**:
```bash
pnpm lint
pnpm lint:fix
```

**Type checking**:
```bash
pnpm type-check
```

**Tests**:
```bash
pnpm test
```

### Database Migrations

**Before merging**:
- [ ] Migration runs successfully locally
- [ ] Migration is reversible (has `down` migration)
- [ ] Migration tested with production-like data
- [ ] Migration won't lock tables for >30 seconds

**After deploying**:
- [ ] Verify migration ran in production
- [ ] Check data integrity
- [ ] Monitor for issues

---

## Security Checklist

Before shipping features that handle sensitive data:

- [ ] Authentication required for all endpoints
- [ ] Authorization checks in place (user can only see their data)
- [ ] Input validation on all user inputs
- [ ] SQL injection prevention (use parameterized queries)
- [ ] XSS prevention (sanitize outputs)
- [ ] CSRF protection (for state-changing operations)
- [ ] Secrets not in code (use environment variables)
- [ ] API keys not exposed to frontend
- [ ] Error messages don't leak sensitive info

---

## Performance Checklist

For features that might have performance impact:

- [ ] Database queries optimized (use indexes)
- [ ] N+1 query problems avoided
- [ ] Large responses paginated
- [ ] Images optimized (Next.js Image component)
- [ ] Heavy computations cached
- [ ] API response time <500ms (target)
- [ ] Page load time <2s (target)

---

## Monitoring & Alerts

### What to Monitor

**Application**:
- Error rate (% of requests failing)
- Response time (p50, p95, p99)
- Request volume
- Memory usage
- CPU usage

**Business**:
- User sign-ups/logins
- Features usage
- Key actions (forecasts generated, POs created)

**Infrastructure**:
- Database connections
- Disk space
- Network latency

### When to Alert

Set up alerts for:
- 🚨 Error rate >5%
- 🚨 Response time >2 seconds (p95)
- 🚨 Memory usage >80%
- 🚨 Database connections >80% of max
- 🚨 Disk space <20%

---

## Common Shortcuts to Avoid

These seem faster but slow you down:

### ❌ "We'll add tests later"
**Problem**: Later never comes, bugs accumulate  
**Do instead**: Write tests for critical paths before merging

### ❌ "We'll fix that after launch"
**Problem**: Creates technical debt  
**Do instead**: Fix before enabling feature, or don't ship

### ❌ "It works on my machine"
**Problem**: Won't work in production  
**Do instead**: Test in staging, which mirrors production

### ❌ "We don't need error handling for this edge case"
**Problem**: That edge case will happen to a client  
**Do instead**: Handle at least with graceful error message

### ❌ "We'll document this later"
**Problem**: Knowledge gets lost  
**Do instead**: Document as you build (takes 5 min)

---

## When to Break the Rules

Sometimes you need to ship fast and dirty. That's okay if:

1. **Behind feature flag** - Easy to disable if needed
2. **Explicitly documented** - Team knows what shortcuts were taken
3. **Fix planned** - Issue created for proper implementation
4. **Time-boxed** - "This is our 2-day version, we'll improve next week"

**Example**:
- Ship with hardcoded data → OK if flag off, plan to fix
- Ship without tests → Only if creating test in next PR
- Ship with quick hack → Only if refactor planned

---

## Remember

**Done is better than perfect.**

These checklists ensure quality without slowing you down. 

If a checklist item doesn't make sense for your feature, skip it. But if you skip many items, ask yourself: "Are we cutting corners or being pragmatic?"

Ship working software. Ship it safely. Ship it Thursday.

---

*Last updated: November 2025*  
*Document owner: Raul*
