---
layout: home
nav_order: 9
title: SCL Display and Board
---

# SCL Display and Board

Two public pages show a Sailing Champions League class live. They need no login and update by themselves.

***Contents***

[toc]

## The Display (big screen)

Open `https://sailingscoreboard.com/scl/display/<class number>` on the computer that drives the screen, and press the **Full screen** button (it hides itself, and the mouse pointer, after three seconds without movement). The class number is shown in the address of the class's Board page, and the workbench Dashboard has a **Display** button for each class.

It is designed for a 1920 by 1080 screen and scales to fit any screen.

**During qualifying** the left side is the leaderboard: rank, team logo, code and name, the scores of the latest races, the total and the number of races raced. A long leaderboard changes page every ten seconds. The right side shows the **last race** in finishing order, a line for a race that is being scored now, and the **next races** with each boat's team.

**During finals** the leaderboard is replaced by the finals: each finalist with its place, its wins (a diamond marks the leader's head start, filled circles are wins, empty circles are wins still needed) and its points, the final races so far, the next final race, and, once decided, a **winner** banner. The qualifying ranking is shown small beneath.

When a new result arrives the rows that changed are highlighted for five seconds. The small *Updated* time shows when the screen last heard from the server; if it cannot reach the server for a while it says so and keeps showing the last results.

### Options

Add them to the address after a question mark, for example `/scl/display/90001?next=5&theme=light`.

| Option | Effect |
|---|---|
| `next=5` | How many next races to show (1 to 8). |
| `theme=light` | A light background instead of the dark one. |
| `rotate=0` | Do not change pages; stay on the first page of the leaderboard. |

## The Board (phones)

Open `https://sailingscoreboard.com/scl/board/` for the list of published events and their classes, or go straight to a class: `https://sailingscoreboard.com/scl/board/<class number>`. It is made for phones and works on any screen.

- **Standings:** the leaderboard. Tap a team to see its race-by-race scores and its sailors (names and roles only).
- **Races:** every race, newest first, with the finishing order. Tap a race to open or close it.
- **Next:** the race being scored and the next races with each boat's team.
- **Finals:** appears once the qualifying series is completed.

Until the qualifying series is completed the standings are labelled **Provisional**: every race counts, so teams that have sailed more races have more points. Afterwards each team counts the same number of races and the others are shown in brackets.

Every page has its own address, so you can send a link to a class, a tab or a team. The Board checks for new results every ten seconds while the page is open.

## What is shown

Only events that are **Published** and classes with the public board switched on appear. Contact details are never shown.
