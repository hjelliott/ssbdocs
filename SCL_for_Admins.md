---
layout: home
nav_order: 7
title: SCL for Administrators
---

# Sailing Champions League: running an event

This page is for the people who set up and run a Sailing Champions League (SCL) event: the event administrator and the chief scorer. Race officials who enter results use the [SCL Scorer app](SCL_Scorer.html). The scoring rules are explained under [Handicapping and Scoring Systems](handicaps-and-scoring.html).

***Contents***

* TOC
{:toc}

## How an SCL event works

Teams of sailors race in short races in identical boats. A **pairing list** says which team sails which boat in each race. The race officials record only the **order** in which the boats finish, plus a code (DNF, DNS, DSQ, OCS, RET or DNC) for any boat that did not finish. The system works out places, points and standings.

An event has a **qualifying series** and, if the class uses them, a **final series**. Everything is managed from the SCL screens of the workbench.

## Who can do what

| Role | What they can do |
|---|---|
| **SCL Admin** | Everything on this page: boats, classes, teams, pairings, adjustments, finals, access. Can also score. |
| **SCL Scorer** | Enter results in the Scorer app for the classes they have been given. Cannot open the admin screens. |
| Site administrator | Everything, once given access to the event and its classes. |

A person needs two things: to be in the right **group**, and to be **given access to the event and to each class** (Access screen). The person who creates an event or class, the event's chief scorer and the site administrator are given access automatically.

## Set up an event

1. **Create the event.** In the workbench choose *Create Event*, set the event type to **SCL**, and save. Open the event: you land on the SCL **Dashboard**.
2. **Boats.** Enter the boats supplied for the event: number (1 to 8, also the sail number), a colour name, the colour itself and an optional sponsor. These colours appear on the Scorer, the Display and the Board. A class that races six boats needs boats 1 to 6; a class that races eight needs 1 to 8.
3. **Classes.** Create a class (for example *Open*). Choose six or eight boats per race, whether the class has finals, how many finalists (4 is usual), how many wins are needed (2), the leader's head start (1) and whether the class appears on the public Board. You can add a **view** for a division (Women, Youth, Masters or Mixed): it ranks only the teams marked with that division in the team register.
4. **Teams.** The **Team register** holds every team and is reused from event to event: a short code (such as RSYS), name, club, divisions, contact details and a logo. You can import and export teams as CSV. Add teams to a class from the class's **Teams** page. Each team can have a **roster** (first name, family name and role) for the event: the Board shows these names to the public; contact details are never shown.
5. **Pairings.** On the class's **Pairings** page upload the pairing list (below).

## The pairing list

A CSV file with a header and one row per race, a team code in each boat column and a blank for an unused boat:

```
Race,Boat1,Boat2,Boat3,Boat4,Boat5,Boat6
1,RSYS,CYCA,RPYC,RQYS,RYCV,RPAYC
2,SYC,NCYC,GLYC,LMYC,MHYC,RMYS
3,RFBYC,RSAYS,RYCT,CYCSA,,CYCA
```

Qualifying races are numbered 1, 2, 3 ...; final races F1, F2 ... The upload is in two steps: the system **checks** the file and shows every problem with its line number (nothing is saved if there is any), then shows the **balance report** (races per team, how often each team sails each boat, who meets whom, back-to-back races) so you can judge the draw. Only then do you apply it. Races that already have results are left alone unless you tick both confirmation boxes.

You can also swap two boats in a race, replace a team on a boat, and export the list again. Changing the pairing of a race that already has results clears those results, and the system asks you to confirm first.

## During racing

Race officials score in the Scorer app. From the workbench you can:

- **Open Scorer** (Dashboard or Races page) to sign in to the Scorer app without typing a password.
- Look at any race: who was entered, in what order, and the history of changes.
- **Abandon** a race, **restore** it, **clear** its results, or create a **re-sail** of an abandoned race (the re-sail of race 12 is 12R, with the same pairing, counted in its place).
- Give a team a **redress** (RDG: you set the points) or **penalty** (PEN: points added) with a comment. An adjustment stays applied if the scorer saves the race again, and the standings update straight away.
- Watch the **Scoreboard** on the Classes screen, or open the full **Standings** (with a PDF).

The Dashboard shows, for each class, how many races are complete, the last race saved and by whom, and warnings (a race partly scored, a tie that blocks the finals, too few teams for the boats).

## Qualifying Series Completed

While the qualifying series is running, **every race a team has sailed counts** and nothing is dropped. Teams may be on different numbers of races, so the table is provisional.

When the qualifying races are finished, use **Qualifying Series Completed** (Classes screen or the class's Finals page). This:

1. **Normalises** the table: each team counts only as many races as the team that sailed the fewest, and later races are shown in brackets.
2. Fixes the **ranking**: the top teams become the finalists and the leader starts the finals with the head start.

The page shows the normalised table next to each team's total for all races, so you can check before you confirm. It will not complete while a race is only partly scored. If two teams are level across the last finalist place, or for the lead, you must put them in order yourself before it will complete. You can **reopen** the series as long as no final race has been scored.

## Finals

After the series is completed, upload the finals pairing list (final races F1, F2 ...): every finalist must be in every final race. The finals end as soon as one team has won the required number of final races (the leader's head start counts as a win). Finalists are ranked by the **sum of their points in the final races**, with no drops and no tie-breaks; the winner is first. No further final races can be scored once there is a winner.

## Display and Board

- **Display** for a big screen: `https://sailingscoreboard.com/scl/display/<class number>`. See [SCL Display and Board](SCL_Display_and_Board.html).
- **Board** for phones: `https://sailingscoreboard.com/scl/board/`.

Both show only events that are **Published** and classes with the public board switched on, and need no login. The Dashboard has a button for each.

## Giving people access

On the **Access** screen you can see who has access to each class. Use the existing access screen (button on that page) to add or remove people. Put scorers in the *SCL Scorer* group and event administrators in *SCL Admin*.
