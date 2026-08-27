# Competitive Blue Flower Challenge Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Replace the passive vertical prototype with a responsive horizontal 90-second score challenge that runs directly on GitHub Pages.

**Architecture:** Keep the project dependency-free and encapsulate all markup, styles, rendering, state, timing, persistence, and input handling in `index.html`. Drive the game from one explicit state object and one animation loop; render the arena to Canvas and mirror competitive state into accessible DOM meters and text.

**Tech Stack:** HTML5, CSS Grid, Canvas 2D, vanilla JavaScript, localStorage.

---

### Task 1: Horizontal competition shell

**Files:**
- Modify: `index.html`

**Step 1:** Replace the 460px vertical frame with a viewport-sized shell containing an arena, an action console, and a scoreboard.

**Step 2:** Set the desktop grid to `minmax(420px, 1.55fr) minmax(220px, .72fr) minmax(230px, .76fr)` and reserve stacking for the `760px` mobile breakpoint.

**Step 3:** Add keyboard-visible focus states, responsive type sizes, reduced-motion handling, and live status regions.

**Step 4:** Open the page at 1440x900 and verify the three primary panels share one horizontal row without viewport overflow.

### Task 2: Deterministic game state and actions

**Files:**
- Modify: `index.html`

**Step 1:** Define a single state object containing `phase`, `timeLeft`, `growth`, `health`, `energy`, `heat`, `score`, `combo`, `cooldowns`, `event`, and result counters.

**Step 2:** Implement `startGame`, `performAction`, `updateGame`, and `finishGame` so each action has an explicit energy cost, cooldown, stat delta, and score value.

**Step 3:** Clamp all meters to `0..100`, end immediately at zero health, and award the bloom bonus only once.

**Step 4:** Expose a read-only `window.__BLUE_FLOWER_DEBUG__.snapshot()` plus `start`, `act`, `advance`, and `finish` helpers for browser verification.

### Task 3: Events, combo, scoring, and persistence

**Files:**
- Modify: `index.html`

**Step 1:** Schedule frost, moth, and storm events every 6-10 seconds; associate them with coffee, chocolate, and comfort respectively.

**Step 2:** Resolve a correct response with score and combo gains; resolve a wrong or expired response with damage and combo reset.

**Step 3:** Calculate final score from earned points plus growth, health, energy, bloom, and event performance. Map scores to C/B/A/S ranks.

**Step 4:** Read and write a validated top-five array under `blueFlowerLeaderboardV1`, swallowing storage errors without interrupting the game.

### Task 4: Canvas feedback and verification

**Files:**
- Modify: `index.html`

**Step 1:** Draw the sky, plot, plant stages, event weather, particles, combo flashes, and bloom effects from the current state.

**Step 2:** Run a JavaScript syntax check by extracting the inline script and evaluating it with Node's parser.

**Step 3:** Drive start, all three actions, an event success, an event timeout, bloom, and finish through a real browser; assert visible state and disabled-button behavior.

**Step 4:** Capture desktop and mobile screenshots, inspect them, and fix any clipping, stacking, contrast, or alignment problem before delivery.
