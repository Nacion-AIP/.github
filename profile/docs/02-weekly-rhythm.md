# How We Work: Weekly Rhythm

Our weekly cadence optimizes for fast feedback loops and regular shipping. This document defines what happens when and what's expected.

---

## Meeting Schedule

| Day | Time | Meeting | Duration | Purpose |
|-----|------|---------|----------|---------|
| Monday | 9:00 AM | Weekly Planning | 30 min | Define what ships Thursday |
| Mon-Thu | 9:00 AM | Async Standup Update | 2 min | Written status in Slack |
| Mon-Thu | 9:15 AM | Sync Standup | 15 min | Coordinate & unblock |
| Thursday | 4:00 PM | Pre-Deploy Check | 30 min | Final review & deploy |
| Friday | 9:00 AM | Feature Enablement | 1 hour | Turn on features & monitor |
| Friday | 3:00 PM | Demo + Retro | 1 hour | Show work & improve |

**Total structured meeting time**: ~3.5 hours/week

---

## Weekly Checklist

Use this to stay on track:

### Monday
- [ ] **9:00 AM**: Weekly Planning meeting
  - [ ] Review last week's retro action items
  - [ ] Define the ONE thing we're shipping Thursday
  - [ ] Break it into vertical slices (see [Slicing Guide](./03-breaking-down-work.md))
  - [ ] Assign owners and collaborators
  - [ ] Create issues in Linear/Jira
  - [ ] Schedule any needed pairing sessions

### Tuesday - Thursday
- [ ] **By 9:00 AM**: Post async standup update in Slack
- [ ] **9:15 AM**: Sync standup (15 min hard stop)
- [ ] **Throughout day**: 
  - [ ] Merge to main at least once
  - [ ] Pair on integration points
  - [ ] Update issue status

### Thursday
- [ ] **By 3:00 PM**: All code merged and tested in staging
- [ ] **4:00 PM**: Pre-Deploy Check
  - [ ] Review shipping checklist (see [Shipping Checklist](./05-shipping-checklist.md))
  - [ ] Confirm everything is ready
  - [ ] Deploy to production
  - [ ] All feature flags configured (off by default)

### Friday
- [ ] **9:00 AM**: Feature Enablement
  - [ ] Enable features for internal team first
  - [ ] Monitor for 1-2 hours
  - [ ] Enable for beta client (if applicable)
  - [ ] Document any issues
- [ ] **3:00 PM**: Demo + Retro
  - [ ] Demo what we shipped
  - [ ] Retro: What went well? What slowed us down?
  - [ ] One action item for next week

---

## Async Standup Update (Daily)

Post this in `#daily-standups` Slack channel **by 9:00 AM** every day (Mon-Thu).

### Template

Copy-paste this template and fill it out (takes 2-3 minutes):

```
**Daily Update - [Your Name] - [Date]**

**✅ Yesterday I shipped/merged:**
- [PR #123]: Brief description + link
- [PR #124]: Brief description + link
- Or: "Nothing merged - still working on X"

**🎯 Today I'm shipping/merging:**
- [Specific task]: Expected completion time
- [Another task]: Expected completion time

**🤝 I need:**
- [ ] Pairing with [Name] on [specific thing] - [proposed time]
- [ ] Code review on [PR link]
- [ ] Input from [Name] on [specific decision]
- Or: "Nothing - I'm unblocked"

**🚧 Blockers/Concerns:**
- [Specific blocker]: What I've tried, what I need
- Or: "None"

**📊 Status for this week's goal:**
- On track / Slightly behind / Need help
```

### Example

```
**Daily Update - Sofia - Nov 12**

**✅ Yesterday I shipped/merged:**
- PR #234: Added forecast chart component with mock data
- PR #235: Fixed auth redirect bug

**🎯 Today I'm shipping/merging:**
- Integrate forecast API (pairing with Mateo at 2pm)
- Add loading states and error handling

**🤝 I need:**
- [x] Pairing with Mateo at 2 PM to integrate forecast API
- [ ] Quick review of PR #234 from Raul before I merge

**🚧 Blockers/Concerns:**
- None

**📊 Status for this week's goal:**
- On track to ship Thursday
```

---

## Sync Standup (Daily 15 min)

**9:15 AM, Monday - Thursday**

This is NOT for reading updates (everyone already read them). This is for:

1. **Quick Clarifications** (3 min)
   - Answer questions about async updates
   - Confirm pairing times

2. **Real-Time Coordination** (5 min)
   - Identify dependencies
   - Resolve conflicts (two people touching same file)
   - Adjust priorities if needed

3. **Problem-Solving** (5 min)
   - Someone is stuck → quick brainstorm
   - Feature scope too big → decide what to cut
   - Architecture decision → timebox to 15 min, then move to separate call

4. **Vibe Check** (2 min)
   - Is anyone struggling but not saying it?
   - "You've been 'almost done' for 3 days - need help?"

**Hard stop at 15 minutes.** Longer discussions → schedule separate call.

---

## Monday: Weekly Planning (30 min)

**Goal**: Define what we're shipping Thursday

### Agenda

1. **Review last week** (5 min)
   - Did we ship what we planned?
   - Action items from retro - did we do them?

2. **This week's goal** (10 min)
   - What's the ONE thing we're shipping Thursday?
   - Why is this the priority? (client need, dependencies, etc.)

3. **Break it down** (15 min)
   - Use [Slicing Guide](./03-breaking-down-work.md) to create vertical slices
   - Assign owners (see [Ownership Guide](./04-issue-ownership.md))
   - Identify collaborators
   - Schedule pairing sessions
   - Create issues in Linear/Jira

### Output

By end of meeting:
- Clear goal for the week
- 3-6 issues created with owners assigned
- Pairing sessions scheduled
- Everyone knows what they're working on

---

## Thursday: Pre-Deploy Check (30 min)

**Goal**: Ensure we're ready to deploy

### Checklist

Go through [Shipping Checklist](./05-shipping-checklist.md) together:

- [ ] All features merged to main
- [ ] Tested in staging environment
- [ ] No broken tests
- [ ] Feature flags configured
- [ ] Rollback plan documented
- [ ] Client communication prepared (if needed)

### If Not Ready

**Option 1**: Cut scope - disable incomplete features via feature flags, ship what's done

**Option 2**: Extend to Friday - but this should be rare

**Option 3**: Ship with known issues - document them, plan fix for next week

### Deploy Process

1. **Run deployment**:
   ```bash
   # Example - adjust for your setup
   ./scripts/deploy.sh production
   ```

2. **Verify deployment**:
   - Check health endpoints
   - Verify feature flags are OFF
   - Smoke test critical paths

3. **Monitor**:
   - Watch CloudWatch/logs for 30 minutes
   - Be ready to rollback if needed

---

## Friday: Feature Enablement (1 hour)

**Goal**: Turn on features safely and incrementally

### Process

1. **Enable for internal team** (9:00 AM)
   - Turn on feature flags for team email addresses only
   - Test all functionality
   - Fix any obvious issues

2. **Monitor** (9:30 AM - 11:00 AM)
   - Watch logs, error rates, performance
   - Check that everything works as expected

3. **Enable for beta client** (11:00 AM) - if applicable
   - Turn on for one selected client
   - Inform them it's available
   - Ask for feedback

4. **Decision point** (1:00 PM)
   - Everything good? Enable for all clients
   - Issues found? Keep feature flag off, plan fix for next week
   - Document decision and reasoning

### Rollback Plan

If something breaks:
1. Turn off feature flag immediately (10 second fix)
2. Assess impact - who was affected?
3. Decide: quick fix or wait until next week?
4. Communicate with affected clients

---

## Friday: Demo + Retro (1 hour)

**Goal**: Celebrate wins and improve continuously

### Part 1: Demo (30 min)

- **Owner demonstrates** the feature we shipped
- Pretend we're the client - show it like you would to them
- Others ask questions, give feedback
- Celebrate! We shipped something.

### Part 2: Retro (30 min)

Use this format:

**1. What went well this week?** (10 min)
- What helped us ship faster?
- What should we keep doing?

**2. What slowed us down?** (10 min)
- Where did we get stuck?
- What took longer than expected?
- What surprised us?

**3. One improvement for next week** (10 min)
- Pick ONE thing to change
- Make it specific and actionable
- Assign someone to own it
- Write it down

**Example action items**:
- ❌ "Better communication" (too vague)
- ✅ "Schedule pairing sessions on Monday instead of ad-hoc" (specific)

---

## Ad-Hoc: Pairing Sessions

Schedule these as needed throughout the week.

### When to Pair

- Integrating two services/components
- Debugging complex issues
- Making architectural decisions
- Onboarding someone to new codebase
- When someone is stuck for >2 hours

### How to Pair Effectively

1. **Schedule it** - don't just "try to find time"
2. **Time-box it** - usually 1-2 hours
3. **One person drives** - shares screen, writes code
4. **Other person navigates** - suggests approach, catches bugs
5. **Switch roles** - every 30 minutes
6. **End with plan** - what's next, who does what

---

## Red Flags

If you see these, raise them in standup:

- 🚨 Same task in "Today I'm shipping" for 3+ days
- 🚨 "Nothing merged" for 2+ days
- 🚨 Vague blockers ("having some issues")
- 🚨 Status: "Need help" but no specific ask
- 🚨 Thursday arrives and we can't deploy

---

## Remote Work Guidelines

We're a remote team. These practices keep us aligned:

### Async First
- Default to written communication (Slack, Linear comments)
- Don't block on synchronous responses
- Document decisions in issues/PRs

### Sync When Needed
- Complex discussions → video call
- Integration points → pairing session
- Stuck for >2 hours → ask for help immediately

### Working Hours
- Core hours: 9 AM - 5 PM (your timezone)
- Be available for daily standup at 9:15 AM
- Thursday deploys at 4 PM - be available

### Communication
- Slack for quick questions
- Linear for work tracking
- GitHub for code discussions
- Loom for async demos/explanations

---

## Questions?

If something in this process isn't working, bring it up in Friday retro. We iterate on our process just like we iterate on our product.

---

*Last updated: November 2025*  
*Document owner: Raul*
