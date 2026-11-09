---
title: Sub Classes
parent: For Scorers
nav_order: 4
---

## Overview

A subclass gives a second set of results for boats that have already raced in another class (the **parent class**). The boats sail once. The subclass reuses their results.

There are two kinds of subclass. Which one you want depends on what the second set of results is for:

| | Copy subclass | Filter subclass |
|---|---|---|
| **Use it for** | A series scored again among a group of boats, often from only some of the parent's races | A view of the parent's own series, limited to some boats |
| **Examples** | A Club Championship (scratch) from a season handicap series. Girls or Masters results with their own points. | The parent's results for boats from one club or country, with the parent's points |
| **How it's scored** | Its own points, from the boats' positions among themselves. Its own scoring system and discards. | The parent's points, discards and scoring system. Nothing is re-scored. |
| **Has its own entries and races** | Yes | No |
| **Set up by** | **Subclass of** field, left with an empty **Subclass Where clause** | **Subclass of** and a **Subclass Where clause** |

Copy subclasses are by far the most common, so they are described first. Filter subclasses are rarely needed.

## Copy subclasses

### How a copy subclass is scored

A copy subclass is a class in its own right. It has its own entries, races, scoring system, discards and publish status. Its boats must also be entered in the parent class.

It is scored with its own points, based on relative positions. Suppose there are two boats, A and B. In the parent class A scores 3, 5, 7, 4 and B scores 6, 6, 12, 5. In the subclass (with no other boats) A scores 1, 1, 1, 1 and B scores 2, 2, 2, 2.

The subclass's **Results Type** decides how the loaded results are scored:

| Parent | Subclass | Result |
|---|---|---|
| Time | Time | The boats are placed by corrected time, among themselves. |
| Time | **Place** | The boats are placed by **actual finishing order** (elapsed time), with no handicap. This gives scratch results from a handicap fleet. |
| Place | Place | The boats keep their relative finishing order. |

### Example: a Club Championship from a season pointscore

A club scores an all-season pointscore by corrected time. Some of the season's races also count towards a Club Championship, which is scored by elapsed time (scratch).

- The parent class is the season pointscore. It is a **Time** class with a handicapping system, and it has a race for every race of the season.
- The subclass is the Club Championship. It is a **Place** class, with its own scoring system and discards.
- The subclass has **fewer races than the parent**. The two are not matched one to one. You create a subclass race for each championship race, and **Load Parent Results** lets you choose which parent race each one takes its results from.

The same boat can then appear in both pointscores, with a handicap result in the season series and a scratch result in the championship, from the same race.

### Setting up a copy subclass

1. Create the parent class and add all the entries to it. If you are using **Time** results, set its **Handicapping System** as usual.
2. Create the subclass as a new class. In the **Subclass of** field, choose the parent class from the drop-down. Leave **Subclass Where clause** empty. Set the other properties of the subclass:
   - **Results Type** (*Time* or *Place*, see above).
   - **Scoring System** and **Discards**. These belong to the subclass and don't have to match the parent's.
3. Open the subclass's **Entries** screen. It has an **Add from Parent Class** button. Click it. A screen lists the entries in the parent class that are not yet in this class. Select the boats you want and click **Save**.
4. [Create the races](Create_Race.html) in the subclass, one for each race the subclass will score.

<!-- SCREENSHOT 1: class form showing Subclass of drop-down, Subclass Where clause (empty) and Results Type -->
<!-- SCREENSHOT 2: subclass Entries screen showing the Add from Parent Class button -->
<!-- SCREENSHOT 3: the Add from Parent Class selection screen -->

Adding from the parent makes a copy of each entry, linked to the original. The copy is made once. If you later correct a boat's details in the parent class, correct them in the subclass too.

### Loading results into a copy subclass

1. Enter the results in the parent class first, and publish the parent race. Only **published** parent races can be loaded.
2. Open the subclass race (the edit race page) and click **Load Parent Results**.
3. In the **Select Race** dialog, choose the parent race to take the results from, and click **Load Results**. The dialog lists the parent's published races and picks the first one on the same date as the subclass race. The race numbers don't have to match, so a championship's Race 3 can be taken from the season's Race 11.
4. The system copies the results of the boats that are in the subclass and scores them again among themselves. You return to the race page with the results in place.

<!-- SCREENSHOT 4: subclass race edit page showing the Load Parent Results button -->
<!-- SCREENSHOT 5: the Select Race dialog -->

Things to know when loading:

- **Loading replaces.** Any results already in the subclass race are deleted and replaced. Loading the same race twice does no harm.
- **Nothing to load.** If the parent race has no results for the subclass's boats, the subclass race is left as it was.
- **Finish codes come across.** A boat that did not finish (DNF, DNS and so on) scores the subclass's default points for that code, based on the number of entries in the *subclass*.
- **Ties in a scratch subclass.** If two boats have the same elapsed time, they are given consecutive places, in no particular order. Check these and adjust by hand if the order matters.

### When the parent results change

A copy subclass holds a **copy** of the parent's results. It does not change when the parent does. After you correct a finish time or a code, or after a protest, penalty or redress in the parent race, open the subclass race and load the parent results again.

Because loading replaces everything, don't make manual corrections in a subclass race and then reload. Make the correction in the parent race, and reload.

Penalties and redress also come across with the result. A penalty place or penalty points awarded in the parent may not be right for the subclass, so check the loaded results after a protest.

If you delete an entry from a subclass, its results in that class are deleted with it.

## Filter subclasses

A filter subclass shows part of the parent's results. Nothing is copied or re-scored. The results pages take the parent class's pointscore and show only the boats that match a condition. The boats keep the parent's race points, and the totals use the parent's scoring system and discards.

Use it when you want a list of some of the parent's boats, in the parent's order. For example, results for one club or country, or for one age group, without separate points.

### Setting up a filter subclass

1. Create the subclass as a new class. In the **Subclass of** field, choose the parent class.
2. In the **Subclass Where clause** field, enter the condition that picks the boats. See below.
3. Save the class, then publish it as usual. Check it on the public results page.

A filter subclass has no entries or races of its own, so there is nothing to add with **Add from Parent Class** and there is no **Load Parent Results** button. Boats appear and disappear from it as they are added to and removed from the parent.

<!-- SCREENSHOT 6: class form with a Subclass Where clause filled in -->

### Writing the Where clause

The clause is a database condition, applied to the parent's results. The usual use is to pick boats by the **Country** field of the entry, which events have also used for a state or region code. For example:

```
classentry.Country = 'AUS'
classentry.Country = 'NSW'
```

Other entry columns can be used in the same way, such as `classentry.Club`, `classentry.SailNo` and `classentry.BowNo`. Text values go in single quotes. Use `AND` and `OR` to combine conditions.

The clause is typed as text and goes straight to the database, so a mistake gives an error or an empty results page instead of a warning on the form. Always open the public results for the subclass after you save it.

Quick Links: [Scorers Home](For_Scorers.html "For Scorers")
