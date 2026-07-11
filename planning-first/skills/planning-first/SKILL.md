---
name: planning-first
description: >
  Plan before code. Use whenever the user asks to build, implement, refactor, add a feature,
  fix a non-trivial bug, or "work on" anything that will touch more than a couple of lines or
  more than one file. Before writing or changing any implementation code, produce a short,
  structured plan and show it to the user: the goal, the files you'll touch and why, the
  concrete steps in order, the risks/assumptions, and a verification plan. Only begin
  implementation after the plan is on screen. Trigger even when the user does not explicitly
  ask for a plan — the whole point is to insert planning before coding happens. Skip the plan
  only for single-line fixes, typos, obvious one-shot tweaks, or pure read/research tasks.
---

# Skill: planning-first

## Why this exists

Jumping straight into code on a non-trivial task is the most common cause of wasted work:
the wrong file gets edited, an edge case gets missed, or the approach turns out to conflict
with how the rest of the project works. Spending thirty seconds on a plan — and letting the
user see it before any code is written — catches most of those problems before they cost
anything.

## When to plan

Plan first when the task will touch **more than a couple of lines or more than one file**,
or when there's a real decision to make about approach. Examples:

- "Add a login page"
- "Refactor the user service"
- "Fix the bug where orders sometimes double-charge" (non-trivial bug)
- "Add CSV export to the reports module"

Skip the plan and just do it when the task is trivially small and low-risk:

- A typo fix
- A one-line config value change
- An obvious rename in a single file
- A pure read / research / "where is X?" question

If you're unsure which side a task falls on, plan. The cost of an unnecessary plan is small;
the cost of skipping a needed one is large.

## What the plan contains

Show the plan as a short, scannable block before any code changes. It must include:

1. **Goal** — one or two sentences: what the user wants, in their terms.
2. **Files** — the files you expect to touch, each with a one-line "why". If you'll need to
   create files, say so. If you're not yet sure of a file, list it as a candidate.
3. **Steps** — the concrete, ordered implementation steps. Numbered. Each step should be
   small enough to be obviously correct when done.
4. **Risks / assumptions** — anything you're assuming that, if wrong, changes the plan.
   Unknowns you'll need to resolve along the way. Be honest about what you don't know yet.
5. **Verification** — how you and the user will know it worked. Tests to run, manual checks
   to perform, commands to execute. State this *before* implementing, not after.

Keep the plan tight — its job is to align, not to document. If it's running long, the task
is probably bigger than it looked; say so and propose breaking it up.

## How to run it

1. **Read enough to plan well.** Before drafting, actually look at the relevant parts of the
   codebase — the files you think you'll touch, plus any conventions or patterns nearby.
   A plan built on guesses is worse than no plan. Use search and read tools; fan out then
   converge.

2. **Draft the plan** using the five sections above. Show it to the user in your reply,
   before any tool call that changes files.

3. **Hand off.** End the plan with a clear choice. Either:
   - "Sound good? I'll start on step 1." — proceed on confirmation, or
   - "I'll go ahead unless you want to adjust." — proceed unless the user objects, when the
     task is low-risk and the user has signaled they want speed.

   Pick the first when the plan has real risks or assumptions the user should sign off on.
   Pick the second for routine work where you're confident.

4. **Implement in order**, following your own steps. If reality diverges from the plan
   mid-implementation — you discover the approach won't work, or a file is structured
   differently than expected — **stop and revise the plan** rather than silently going off
   script. A short "plan update: …" message is enough.

5. **Verify** using the verification section you committed to. Report the actual result:
   which tests ran, what passed or failed, what you checked manually. Don't claim success
   without having run the checks.

## When the user says "just do it" or "skip the plan"

Respect that — the user is allowed to opt out. But if the task is genuinely non-trivial and
you see a real risk, say so in one line ("heads up: this touches 4 files and I'm not sure
how the auth middleware will react — want a quick plan first?") and then proceed if they
confirm. Don't force the plan; do flag the risk once.

## Output shape

A reasonable plan looks like:

```
**Goal:** Let users reset their password from the login page.

**Files:**
- src/pages/Login.tsx — add "Forgot password?" link + state
- src/api/auth.ts — add requestPasswordReset() helper
- src/pages/ResetPassword.tsx — new page (create)

**Steps:**
1. Add ResetPassword.tsx with the form + validation
2. Add requestPasswordReset() in auth.ts, hitting POST /auth/reset
3. Wire the link on Login.tsx → navigate to /reset
4. Add the /reset route in App.tsx

**Risks / assumptions:**
- Assuming the backend already exposes POST /auth/reset — need to verify
- Not sure if there's an existing form component to reuse; will check

**Verification:**
- Click "Forgot password?" from login → lands on reset page
- Submit valid email → network call fires, success toast shows
- Submit invalid email → validation error, no call
- Run `npm test` — existing tests still pass
```

Then: "Sound good? I'll start on step 1."
