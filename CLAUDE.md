# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A zero-dependency, single-file top-down car racing game using HTML5 Canvas. All game logic, rendering, and styles live in `index.html`.

## Running

Open `index.html` directly in a browser — no build step or server required.

## Architecture

Everything is in one `<script>` block inside `index.html`:

- **Game states**: `gameState` string (`"start"`, `"playing"`, `"gameover"`) controls flow; Space key transitions between states
- **Road**: 3-lane vertically scrolling road drawn on a 400x600 canvas; lane dividers scroll via `lineDashOffset` tied to `roadOffset`
- **Player**: blue car near the bottom, moves left/right with arrow keys or A/D, clamped to road boundaries
- **Obstacles**: colored cars spawn at the top in random lanes, scroll downward at 70% of road speed; spawn rate and speed increase over time for progressive difficulty
- **Collision**: AABB check with 4px inset hitboxes for fairness
- **Scoring**: increments each frame while playing; session high score tracked in memory
- **Lane fairness**: `spawnObstacle()` filters out lanes blocked near the top to prevent impossible situations
