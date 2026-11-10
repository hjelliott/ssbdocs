---
layout: home
nav_order: 6
title: Handicapping and Scoring Systems
---
# Handicapping and scoring systems

SailingScoreBoard works out a race result in two steps:

1. **Handicap (time classes only).** Each boat's elapsed time (ET) is converted to a corrected time (CT) using the class's *handicap system*. Boats are ranked by CT, fastest first.
2. **Scoring.** The finishing place becomes race points using the class's *scoring system*. Race points are added up over the series, discards are applied, and ties are broken.

You choose both on the class. A class's **result type** decides whether step 1 applies:

| Result type | How results are entered | Handicap used? |
|---|---|---|
| **Time** | Finish times. Elapsed and corrected times are calculated. | Yes |
| **Place** | Finishing places typed in directly. | No |

All the scoring systems are low-point: the lowest series total wins.

---

## Handicap systems

Elapsed time is measured in seconds from the boat's start (the race start, or the boat's own start time if one is recorded) to its finish. Multi-day races are supported. Corrected times are rounded to the nearest second, except RVPY, which is rounded to 0.1 s.

If two boats have the same corrected time, they share the same place. Each gets the average of the points for the places they occupy.

### Fixed handicaps

The boat's handicap number stays the same for the whole event. Changing a handicap on an entry recalculates all of that boat's races.

| System | Handicap number | Corrected time | Typical use |
|---|---|---|---|
| **Fastest time, no handicap** | none | CT = ET | Scratch results from a Time class |
| **TCF multiplier** | TCF, e.g. 1.025 | CT = ET × TCF | IRC and other time-on-time ratings |
| **HKPN** | HK Performance Number, e.g. 1000 | CT = ET × 1000 / HKPN | Hong Kong dinghy and keelboat fleets |
| **Portsmouth Yardstick (PYC)** | PN, e.g. 1000 | CT = ET × 1000 / PN | Dinghy club racing |
| **Royal Varuna PY (RVPY)** | PN | CT = ET × 1000 / PN, to 0.1 s | As PYC, with times shown to the tenth of a second |
| **Texel (TR)** | Texel rating | CT = ET × 100 / TR | Texel-rated boats |
| **Time subtraction** | Minutes (decimals allowed) | CT = ET − (minutes × 60) | Simple time-on-distance allowances |

Higher TCF means a faster boat. For HKPN, PYC, RVPY and TR a higher number means a slower boat, so a boat with a higher number gets a bigger allowance.

### Dynamic handicaps

The handicap changes as the series goes on. Each race is corrected with the boat's **current** handicap. After each race, the race officer runs **Adjust Handicaps**. That calculates the handicap each boat will use in the *next* race. Boats that did not finish keep their current handicap.

Race 1 uses the entry's starting handicap, which is saved as the boat's *base* TCF. From race 2 on, each race picks up the handicap calculated after the previous race.

If you correct a boat's TCF on the **Edit Result** screen for a race, that race keeps the value you typed (it is not replaced by the starting or previously calculated handicap). Clearing the field, or entering 0, goes back to the calculated one.

#### IRC National Handicapping (`ircnhc`)

Corrected time is ET × TCF. The adjustment is the original (pre-2015) NHC method:

1. Work out the TCF each finisher *achieved*: the TCF that would have made its elapsed time equal to the fleet's, scaled so the finishers' TCFs still add up to the same total.
2. Move the boat's TCF part of the way towards the achieved TCF. Race 1 moves it 60% of the way. From race 2, it moves 60% of the way up and 50% of the way down.
3. Limit the result to within ±10% of the boat's base TCF. Beyond that limit, the overshoot is reflected back.

#### 2015 National Handicapping (`nhc2015`)

Corrected time is ET × TCF. It follows the 2015 NHC method, which takes more account of unusual performances:

1. Work out each finisher's achieved TCF, then compare it with the old TCF to give a *comparison value*.
2. Calculate the mean and standard deviation of the comparison values across the fleet.
3. A boat inside the normal band moves towards its achieved TCF by a set proportion. A boat outside the band is an extreme performer. Its movement is reduced, and it is left out of the benchmark used for the other boats.
4. Scale all the new TCFs so their total equals the total before the race.

The proportions and the number of standard deviations for "extreme" are set per class. The class fields are **NHC OP/UP factor** and **NHC OP/UP count**. Both factors default to 0.3 and both counts to 1.

#### World Sailing Empirical (`wsemp`)

Corrected time is ET × TCF. After a race:

1. Take the corrected times of the finishers. Leave out the fastest 20% and the slowest part of the fleet, and average what is left. This gives the *standard corrected time* (SCT).
2. For each finisher, the TCF it achieved is SCT / ET. The new TCF is `old TCF + PM × (SCT / ET − old TCF)`.
3. PM is the adjustment weight. It is `max(1 / n, 0.2)`, where n is the number of races the boat has finished (never more than the race number). So the first race moves the TCF all the way, and the weight settles at 0.2 from the fifth race. The officer can override PM on the adjust form.

All boats must have finished or been given a code before adjusting.

**Status:** the *Adjust Handicaps* button runs `ircnhc` and `nhc2015` only. The World Sailing Empirical calculation is in the code (`AdjustWSEMP`). It is not offered by the standard adjust action (the `wsemp` case is commented out in `Race::AdjustIRCHandicaps`), so check it is reachable before promising it to an event.

---

## Scoring systems

For every system, a boat that finishes scores its finishing place. Place is by corrected time in a Time class, or the entered place in a Place class. Non-finishers get the system's default points (see the table). The scoring system is set on the class.

| Scoring system | Non-finisher points (DNF, DNS, OCS, DSQ and so on) | Notes |
|---|---|---|
| **Appendix A4 Low** (default) | Boats entered in the class + 1 | The standard low-point system |
| **Appendix A5.2** (RRS 2025–28) | Boats entered + 1 | Same figures as A4 Low |
| **Appendix A5.3** (RRS 2025–28) | **DNC:** boats entered + 1. **Everything else:** (boats entered − DNC boats) + 1 | Scores depend on the other results in the race, so they are recalculated whenever a result is saved |
| **ACYC A9** | Boats that finished + 2 | The ACYC modified A9 |
| **Kiteboard PKC11** | Boats entered + 1 | The winner of a race scores **0.7** points instead of 1. Other places score as normal |
| **Appendix B8** | Boats entered + 1 | Race scoring is as A4. The series tie-break is modified (see below) |
| **Sailing Champions League (SCL)** | Teams paired in that race + 1 | Team racing in supplied boats. Scored by its own rules, set out in [Sailing Champions League scoring](#sailing-champions-league-scoring) below |

**Time limit expired (TLE).** A boat with the TLE code scores finishers + 1, whichever scoring system the class uses. This follows the sailing instructions, not the scoring system.

### Result codes and adjustments

- **Penalty or adjusted scores:** `PEN`, `RDG`, `DPI`, `FPA` and `SCP` can carry a *penalty place* or *penalty points*, which replace the calculated score. A penalty place also pushes the other boats down, so no two boats share it.
- **Non-discardable:** `DNE` and `DGM` can never be discarded.
- **Entrants:** only boats still entered in the class count towards "boats entered".

### Series totals and discards

- **Number of discards.** Either a fixed number, or a drop string made of `races:discards` pairs such as `4:1 8:2`. With a drop string, the number of discards is the one for the largest race count not above the number of races *published* so far. Races that are not published, or are abandoned, are not scored.
- **Total.** Race scores are added up. The worst scores are discarded, up to the number allowed, but non-discardable scores always stay in.
- **Tied totals.** The tie is broken as in RRS A8:
  1. Compare the boats' scores in order, from best to worst, after discards. The lower score at the first difference wins.
  2. Any non-discardable scores are compared next.
  3. If still tied, the boat that scored better in the last race wins.
- **Appendix B8 tie-break.** The comparison also includes the discarded scores. It starts with the best discarded score, then the full list of scores before discards.
- **Place.** Boats with the same total and the same tie-break are shown with the same place. The next place after a tie is the next consecutive number.
- **All DNC.** A boat with DNC in every race is flagged so the results can show it as not competing.

---

## Sailing Champions League scoring

Sailing Champions League (SCL) is a team event sailed in a small fleet of identical boats. A pairing list says which team sails which boat in each short race. The Race Official records only the order in which the boat numbers finish, and the system turns that into team places. SCL classes use their own scoring rules, which differ from the systems above. They are set up and managed from the SCL screens, not from the ordinary class and race screens, and their results are entered in the SCL Scorer rather than on the finish sheet. The Results website, the REST interface and the printed reports show the SCL qualifying table in the usual layout.

**Race points.** A team scores its finishing place. A boat with a code (DNF, DNS, DSQ, OCS, RET or DNC) does not use up a place. Instead it scores **the number of teams paired in that race, plus one**. For example, if boats 3, 5 (OCS), 1 and 2 are recorded in that order in a race with four teams, boat 3 is 1st, boat 1 is 2nd, boat 2 is 3rd, and boat 5 scores 5 points.

**Qualifying series.** Only complete races count. Partial and abandoned races never do. A race that is abandoned can be sailed again as a *re-sail* (for example race 12R), which counts in its place.

**Teams on different numbers of races.** While racing is in progress some teams will have sailed more races than others. Each team counts only as many races as the team with the fewest (among teams that have sailed at least one). A team's most recent extra races are left out and shown in brackets on the Board. The Results website shows every race the team has sailed and the counted total. When every team has sailed the same number of races, nothing is left out.

**Tied totals.** Lowest total wins. Ties are broken as in RRS A8, using only the races that count:
1. Compare the teams' scores in order, from best to worst. The lower score at the first difference wins.
2. If still tied, compare the scores in the last race, then the race before it, and so on.

Teams that are still equal share the place, and the next place after a tie skips the shared places (for example 1, 1, 3).

**Redress and penalties.** An administrator can give a team stated points for a race (redress, shown as RDG) or add penalty points. Both carry a comment, are marked on the displays, and stay in place if the Scorer later corrects the race.

**Finals.** After qualifying, an administrator closes the qualifying series. The leading teams (four by default) go through to a final series. The qualifying leader starts with a head start of one race win (the default). The winner of each final race gets one win, and the first team to reach the number of wins required (two by default) wins the event. The other finalists are then placed by their finish in the deciding final race, followed by the teams that did not reach the finals, in qualifying order. If teams are tied across the last finalist place, or for the lead, the administrator must decide the order before the finals can start. No further final races can be scored once a winner is decided.

**Sub-classes.** A sub-class such as Women is ranked from the main class's results for the teams in it. Boats are not re-placed within the races.
