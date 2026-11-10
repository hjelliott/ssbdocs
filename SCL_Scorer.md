---
layout: home
nav_order: 8
title: SCL Scorer app
---

# The SCL Scorer app

The Scorer app is how race officials record Sailing Champions League results on a tablet. It works without an internet connection: results are kept on the tablet and sent when the connection returns.

***Contents***

[toc]

## Install it

Use a tablet in **landscape** (iPad, Android tablet, or a touch laptop with Chrome, Edge or Safari). Open **https://sailingscoreboard.com/scl/scorepad/**, sign in once, then:

- **iPad (Safari):** Share, then *Add to Home Screen*.
- **Android (Chrome):** menu, then *Install app* or *Add to Home screen*.

Install it. An installed app keeps its saved data safely and reopens without a connection. (On an iPad that has not installed it, Safari may clear the data after a week.)

## Sign in

Either type your **username (or email) and password**, or use **Open Scorer** in the workbench: it signs you in without a password. If you can score more than one class you choose a class; the app remembers your choice.

## The screen

- **Top bar:** the event and class, the **sync light**, and the **Menu**.
- **Left:** the results table. One row per race, with the race number, then the boats in the order they finished. Each boat is its number on its colour. A code (such as OCS) shows beneath the number. Abandoned races are struck through, partly scored races say *partial*, and a race waiting to be sent says *pending*.
- **Right:** the keypad and the buttons for the **current race** (the highlighted row).

Tap a race number to make it the current race. When you open the app the current race is the first one that is not complete.

## Scoring a race

1. Tap the boats **in the order they finish**. Each boat you tap is added to the race and its key is dimmed with a tick, so it cannot be tapped twice. Keys for boats that are not racing in this race are disabled.
2. A boat that did not finish gets a **code**: **press and hold** its number (or right-click), or press **Code…** and then tap the number. Choose DNF, DNS, DSQ, OCS, RET or DNC. The boat takes the next place in the order, but a coded boat does not use up a finishing place.
3. Made a mistake? **C** removes the last boat. Press and hold **C**, or use **Reset Race**, to clear the whole race.
4. **DNF Remainder** gives a DNF to every boat that has no entry yet.
5. **Save Race.** If some boats have no result the app asks: *DNF the rest*, *Save as partial*, or *Cancel*. After saving it moves to the next race that is not complete.

Points are worked out by the system, not by the app: a finisher scores its place, and a boat with a code scores one more than the number of teams in the race.

To **change a saved race**, tap its number, change the entries and press Save Race (the app asks you to confirm when you change a complete race). If an administrator has given a redress or penalty in that race, a banner says so and it stays applied.

## The sync light

| Light | Meaning |
|---|---|
| **Synced** (green) | Everything is on the server and the tablet has checked recently. |
| **N pending** (amber) | N races are saved on the tablet and not yet sent. They are sent automatically. |
| **Offline** (amber) | No connection. Keep scoring; results are queued and sent in order when the connection returns. |
| **Error: tap for details** (red) | Something needs attention, for example you have been signed out. Your queued races are kept. Tap for details. |

The app checks the server every 30 seconds and when you return to it.

## Two devices on the same race

If someone else saved a race after you opened it, the app shows both versions side by side when you save: **Yours** and **Server's**. Choose *Keep the server's* to drop yours, or *Overwrite with mine* to replace theirs.

## The menu

- **Sync now:** send anything waiting, then read the latest results.
- **Reload from server:** replace what is on the tablet with the server's copy. It refuses while races are waiting to be sent unless you confirm again.
- **Show team codes:** show each team's code under the boat numbers.
- **Abandon this race / Restore this race:** abandoning keeps the results but does not score the race. This needs a connection.
- **Change class**, **Log out.** Races waiting to be sent stay on the tablet when you log out and are sent when you sign in again as the same person.

## Tips

- Keep the tablet charged and on the same screen while scoring; it is built to be used with wet hands, so the keys are large.
- Before the first race, open the app once with a connection so the class data is on the tablet.
- If you are unsure whether something has reached the server, look at the sync light, or open the **Board** on a phone.
