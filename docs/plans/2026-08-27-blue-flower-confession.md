# Blue Flower Confession Game Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Turn the existing vertical clicker into a horizontal, five-chapter pixel confession game built around a tea restaurant meeting, playing Switch together, and watching meteors.

**Architecture:** Keep the project as a single static `index.html`. Use a finite-state chapter controller for DOM copy and interactions, a Canvas renderer for all scenes, and a small validated localStorage payload for unlocked chapter and collected memories.

**Tech Stack:** HTML5, CSS Grid, Canvas 2D, vanilla JavaScript, Pointer Events, localStorage.

---

### Task 1: Horizontal story shell

**Files:**
- Modify: `index.html`

**Step 1:** Build a desktop grid with `minmax(520px, 1.7fr)` for the scene and `minmax(300px, .8fr)` for the letter panel.

**Step 2:** Add a compact header, a bottom petal chapter trail, and a single-column breakpoint below 780px.

**Step 3:** Add visible focus styles, semantic buttons, live dialogue regions, pointer-friendly controls, and reduced-motion behavior.

**Step 4:** Verify at 1440x900 that the scene and letter share one row without clipping.

### Task 2: Chapter controller and persistence

**Files:**
- Modify: `index.html`

**Step 1:** Define chapter IDs `prologue`, `seed`, `restaurant`, `switch`, `meteor`, `bloom`, and `confession` in an ordered configuration.

**Step 2:** Implement `goToChapter`, `completeChapter`, `saveProgress`, `loadProgress`, and `resetProgress` with schema validation and storage error fallbacks.

**Step 3:** Centralize editable story strings and expose a clearly named `FINAL_CONFESSION` constant.

**Step 4:** Expose `window.__BLUE_FLOWER_DEBUG__` methods for state inspection and deterministic chapter navigation during browser checks.

### Task 3: Seed and restaurant interactions

**Files:**
- Modify: `index.html`

**Step 1:** Make the seed draggable with Pointer Events and clickable as an accessible fallback.

**Step 2:** Accept a drop inside the flowerpot, then ask the player to choose coffee or chocolate before completing the chapter.

**Step 3:** Draw the tea restaurant and register three hit areas for the menu, warm drink, and opposite seat.

**Step 4:** Reveal one line per found item and unlock the next chapter only after all three are collected.

### Task 4: Switch cooperation interaction

**Files:**
- Modify: `index.html`

**Step 1:** Generate a fixed 12-step left/right prompt sequence and render the active prompt in Canvas and DOM.

**Step 2:** Support `A`/`D`, arrow keys, and two large touch buttons.

**Step 3:** Advance on every input, count matches, never fail, and reveal a bonus memory at 9 or more matches.

**Step 4:** Complete automatically after the sequence and show a continue button.

### Task 5: Meteor and bloom finale

**Files:**
- Modify: `index.html`

**Step 1:** Spawn one clickable meteor at a time across deterministic paths and provide a large hit radius for touch users.

**Step 2:** Add each caught meteor to the flower bud and finish after five catches.

**Step 3:** Run a staged bloom animation that brings every collected memory icon back into the garden.

**Step 4:** Reveal the editable confession panel only after the bloom animation completes.

### Task 6: Verification

**Files:**
- Test: `index.html`

**Step 1:** Extract the inline script and run `node --check` against it; expect exit code 0.

**Step 2:** In a real browser, traverse every chapter through debug navigation and through representative user inputs.

**Step 3:** Reload after progress changes and verify continuation; reset and verify the prologue returns.

**Step 4:** Capture and inspect desktop and mobile screenshots, fix clipping or accidental desktop stacking, then re-run checks.
