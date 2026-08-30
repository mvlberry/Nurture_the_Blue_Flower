# Meteor Wave Gameplay Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Replace the separate meteor charge bar with a three-blue-star resource loop, mixed bidirectional meteor waves, and a missed-blue-star growth penalty.

**Architecture:** Keep the project framework-free and contained in `index.html`. Store collected and missed blue stars as small integer counters, drive both care-item buttons from the collected counter, and let the existing growth value remain the page's only progress bar. Meteor creation is split into a single-meteor helper and a wave helper so normal play can guarantee mixed red/blue groups while debug verification can still create deterministic cases.

**Tech Stack:** HTML5, CSS, vanilla JavaScript, Canvas 2D, Playwright browser verification.

---

### Task 1: Replace charge UI with a discrete star bank

**Files:**
- Modify: `index.html:388-448`
- Modify: `index.html:739-784`

**Step 1: Define the failing UI checks**

Check that the rendered page has exactly one `.bar`, exposes `BLUE STARS 0 / 3`, and starts with both care-item buttons disabled.

**Step 2: Run the checks and verify they fail**

Run the browser verification script before implementation. Expected: FAIL because the page still contains growth and meteor-charge bars and coffee is available after planting.

**Step 3: Implement the star-bank UI**

Remove the meteor charge bar, add `#star-count` and `#miss-count` text values, and update the legend and item labels to explain that three blue stars buy either care item.

**Step 4: Verify the static UI**

Run the browser check. Expected: one progress bar, readable star counters, and no horizontal overflow at 390×844 and 375×667.

### Task 2: Add mixed bidirectional meteor waves

**Files:**
- Modify: `index.html:1058-1134`

**Step 1: Define deterministic wave checks**

Expose a debug wave-spawn helper and assert that one wave contains blue and red meteors at the same time. Spawn multiple waves and assert that both positive and negative horizontal velocities occur.

**Step 2: Run the checks and verify they fail**

Expected: FAIL because normal spawning creates one right-to-left meteor at a time.

**Step 3: Implement wave spawning**

Create waves of two or three meteors. Every wave begins with one blue and one red meteor, may add a third random color, and distributes launch sides, heights, and delays so the stars remain clickable without forming a rigid line.

**Step 4: Verify movement and cleanup**

Expected: stars move quickly in both directions, their trails point behind their travel direction, and off-screen meteors are removed at either horizontal edge.

### Task 3: Implement three-star spending and penalties

**Files:**
- Modify: `index.html:829-848`
- Modify: `index.html:1151-1171`
- Modify: `index.html:1376-1524`

**Step 1: Define state-transition checks**

Verify: each blue catch adds one star up to three; a red catch removes one stored star; both items unlock at three; either item consumes all three; and every third missed blue meteor subtracts ten growth points and resets the miss counter.

**Step 2: Run the checks and verify they fail**

Expected: FAIL because the current implementation uses a 0–100 charge value, coffee is free, and misses have no effect.

**Step 3: Implement the counters and item gate**

Replace `charge` with `blueStars` and `missedBlueStars`. Centralize button availability in `updateStarHUD()`, require three stars inside `feed()`, and consume three stars before applying coffee or chocolate growth.

**Step 4: Implement missed-star accounting**

When an uncollected blue meteor leaves the play area, increment the miss counter. On the third miss, clamp growth at zero after subtracting ten, reset the counter, flash the scene, and refresh the HUD.

**Step 5: Run interaction verification**

Expected: all deterministic state-transition checks pass.

### Task 4: Update documentation and complete visual QA

**Files:**
- Modify: `README.md`
- Test: `C:/Users/asuspc1/.codex/visualizations/2026/08/25/01a03837-7d2e-7a42-bae6-46cc5ad33e6b/verify-meteor-charge.cjs`

**Step 1: Update player instructions**

Describe mixed bidirectional waves, the `3`-star cost shared by coffee and chocolate, red-star loss, and the `3 misses → -10 growth` rule.

**Step 2: Run syntax and real-browser checks**

Expected: JavaScript parses, wave and resource assertions pass, one progress bar remains, and desktop/iPhone layouts have no horizontal overflow.

**Step 3: Review screenshots**

Inspect desktop, iPhone 14, and iPhone SE screenshots. Expected: the star bank is legible, all buttons fit, and mixed-direction meteors remain visibly distinct.

**Step 4: Commit the completed change**

Run `git add index.html README.md docs/plans/2026-08-30-meteor-wave-gameplay.md` and commit with a focused feature message. Do not add the preserved `index - 副本.html` file.
