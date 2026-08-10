---
layout: home
nav_order: 3
title: REST Interface
---


## Overview

SailingScoreboard.com provides a REST interface for those users wishing to develop their own results display systems.

REST Interfaces are described here [REST API Tutorial](http://www.restapitutorial.com/)

The Sailing Scoreboard REST interface implements the HTTP **GET** verb and returns results in JSON format. The Sailing Scoreboard REST implementation follows the standard REST hierarchical URL model for access. The generic form is as follows:

**http://www.rest.sailingscoreboard.com/results/<resource>[/<param1>/<param2>...]**

The resources and parameters are described below.

## Available Resources and Parameters

### EVENTS

Resource Name: EVENTS

Description: Returns one or more events (regattas) managed by Sailing Scoreboard

| Resource URL | Results returned | Example |
|---|---|---|
| results/events | Returns all events | [http://www.rest.sailingscoreboard.com/results/events](http://www.rest.sailingscoreboard.com/results/events) |
| results/events/id/nnn | Returns the event with event id nnn (numeric event id) | [http://www.rest.sailingscoreboard.com/results/events/id/54](http://www.rest.sailingscoreboard.com/results/events/id/54) |
| results/events/id/aaa | Returns the event with event code aaa (alphanumeric event code) | [http://www.rest.sailingscoreboard.com/results/events/id/chncup2013](http://www.rest.sailingscoreboard.com/results/events/id/chncup2013) |

Data Returned

| Field | Details | Example |
|---|---|---|
| EventId | Internal Event identifier. Numeric | 45 |

### CLASSES

Resource Name: CLASSES

Description: Returns a specific class or all classes within a specific event (regatta).

| Resource URL | Results returned | Example |
|---|---|---|
| results/classes | Fails. Must have either Class or Event as minimum parameters | [http://www.rest.sailingscoreboard.com/results/classes](http://www.rest.sailingscoreboard.com/results/classes) |
| results/classes/id/nnn | Returns the class with Class Id nnn (numeric event id) | [http://www.rest.sailingscoreboard.com/results/classes/id/469](http://www.rest.sailingscoreboard.com/results/classes/id/469) |
| results/classes/event/aaa | Returns the classes in the event with event code aaa. Event code can be either the numeric id or the alpha code. | [http://www.rest.sailingscoreboard.com/results/classes/event/chncup2013](http://www.rest.sailingscoreboard.com/results/classes/event/chncup2013) |

Data returned

| Result Element | Description | Example |
|---|---|---|
| ClassId | Internal class identifier (numeric) | 464 |
| className | Class name displayed in results | Beneteau First 40.7 Class |
| classLogo | Class logo file name | icf-f.png |
| classCourse | Course area (string) | A |
| classOrder | Display order in results | 1 |
| classStatus | Status of class (0=Pending, 1=Published, 2=Archived) | 1 |
| classResultType | Type of results. 0=Place, 1=Time Corrected | 0 |
| MaxRaces | Maximum races in the series | 8 |
| MinRaces | Minimum Races needed to constitute a series | 1 |
| PreDropRaces | String representing the discard sequence as n:m = After n races discard m worst scores | 4:1 |
| CompletedRaces | Number of races completed to date | 3 |
| subClassOf | Internal identifier of parent class if this is a subclass | 0 |

### ENTRIES

Resource Name: ENTRIES

Description: Returns a specific entry or all entries within a specific event or class.

| Resource URL | Results returned | Example |
|---|---|---|
| results/entries | Fails. Must have either Class or Event as minimum parameters | [http://www.rest.sailingscoreboard.com/results/entries](http://www.rest.sailingscoreboard.com/results/entries) |
| results/entries/id/nnn | Returns the entry with Entry Id nnn (numeric Entry Id) | [http://www.rest.sailingscoreboard.com/results/entries/id/5329](http://www.rest.sailingscoreboard.com/results/entries/id/5329) |
| results/entries/class/nnn | Returns the entries for Class Id nnn (numeric Class Id) | [http://www.rest.sailingscoreboard.com/results/entries/class/469](http://www.rest.sailingscoreboard.com/results/entries/class/469) |
| results/entries/event/aaa | Returns the entries for event code aaa. Event code can be either the numeric id or the alpha code. | [http://www.rest.sailingscoreboard.com/results/entries/event/chncup2013](http://www.rest.sailingscoreboard.com/results/entries/event/chncup2013) |

Data returned:

| Result Element | Description | Example |
|---|---|---|
| EventId | Internal Id of the event | 54 |
| ClassId | Internal Id of the class | 464 |
| ClassName | Display name of the class | Beneteau First 40.7 Class |
| ClassEntryId | Internal id of the entry | 5245 |
| Boat | Display Name of the boat or team | Vicsail |
| Owner | Display Name of the owner | Robin Hawthorn |
| tcf | Time Correction Factor (float) if the class is a "time" results class otherwise 0 | 1.141 |
| BowNo | Bow number of the boat | 29 |
| Country | Country code of the boat as per RRS Appendix G | AUS |
| SailNo | Sail number of the boat | CHN55029 |
| Club | Club of the boat | RPAYC |

### POINTSCORES

Resource Name: POINTSCORES

Description: Returns the pointscore for a specific class.

| Resource URL | Results returned | Example |
|---|---|---|
| results/pointscores | Fails. Must have either Class or Event as minimum parameters | [http://www.rest.sailingscoreboard.com/results/pointscores](http://www.rest.sailingscoreboard.com/results/pointscores) |
| results/pointscores/class/nnn | Returns the entries for Class Id nnn (numeric Class Id) | [http://www.rest.sailingscoreboard.com/results/pointscores/class/469](http://www.rest.sailingscoreboard.com/results/pointscores/class/469) |

Details of returned data:

| Result Element | Description | Example |
|---|---|---|
| BowNo | Bow number of entry | 574 |
| Boat | Name of boat or team | Hail Beaver |
| Owner | Name of boat owner or skipper | Joseph Wong |
| SailNo | Sail number | HKG2170 |
| Country | Country as a 3 character code as per RRS Appendix G | HKG |
| Club | Club name | RHKYC |
| Racecount | Number of races sailed. | 6 |
| RawPoints | Array of points awarded in each race sailed to date. Array elements are {Race Number : Points Awarded} | {1:5,2:10,3:6,4:10,5:10,6:10} |
| Places | Array of places awarded in each race sailed to date. Array elements are {Race Number : Place Awarded}. Note that place can be a character string as per RRS Appendix A | {1:5,2:DNF,3:6,4:DNS,5:DNS,6:DNS} |
| RawTotalPoints | Sum of all points awarded including discards | 51 |
| TotalPoints | Sum of points less discarded scores | 41 |
| Place | Place in pointscore (numeric) | 1 |
| DNC | Used for circuit events. If True, this competitor has not competed in this event (true/false). | false |

### RACES

Resource Name: RACES

Description: Returns a specific race or all races within a specific event or class.

| Resource URL | Results returned | Example |
|---|---|---|
| results/races | Fails. Must have either Class or Event as minimum parameters | [http://www.rest.sailingscoreboard.com/results/races](http://www.rest.sailingscoreboard.com/results/races) |
| results/races/id/nnn | Returns the race with Race Id nnn (numeric) | [http://www.rest.sailingscoreboard.com/results/races/id/5329](http://www.rest.sailingscoreboard.com/results/races/id/5329) |
| results/races/class/nnn | Returns the races for Class Id nnn (numeric) | [http://www.rest.sailingscoreboard.com/results/races/class/469](http://www.rest.sailingscoreboard.com/results/races/class/469) |
| results/races/event/aaa | Returns the races for event code aaa. Event code can be either the numeric id or the alpha code. | [http://www.rest.sailingscoreboard.com/results/races/event/chncup2013](http://www.rest.sailingscoreboard.com/results/races/event/chncup2013) |

Data returned:

| Result Element | Description | Example |
|---|---|---|
| EventId | Internal id of event | 54 |
| ClassId | Internal id of class | 464 |
| RaceId | Internal id of race | 2574 |
| RaceNo | Race number | 1 |
| RaceName | Display Name of Race | Race 1 |
| RaceDate | Race date as yyyy-mm-dd | 2013-10-25 |
| ScheduledStart | Scheduled race start as hh:mm:ss | 10:05:00 |
| ActualStart | Actual start of race as hh:mm:ss | 10:05:00 |
| LastFinish | Time of last finisher as hh:mm:ss if available otherwise null | 12:44:22 |
| Notification | Notification status. 0=Provisional, 1=Final | 1 |
| Status | Race publication status. 0=Pending, 1=Published, 2=Archived | 1 |

### RACERESULTS

Resource Name: RACERESULTS

Description: Returns a specific raceresult or all raceresults within a specific race or class.

| Resource URL | Results returned | Example |
|---|---|---|
| results/raceresults | Fails. Must have either Class or Event as minimum parameters | [http://www.rest.sailingscoreboard.com/results/raceresults](http://www.rest.sailingscoreboard.com/results/raceresults) |
| results/raceresults/id/nnn | Returns the raceresult with RaceResult Id nnn (numeric) | [http://www.rest.sailingscoreboard.com/results/raceresults/id/5285](http://www.rest.sailingscoreboard.com/results/raceresults/id/5285) |
| results/raceresults/class/nnn | Returns the raceresults for Class Id nnn (numeric) | [http://www.rest.sailingscoreboard.com/results/raceresults/class/469](http://www.rest.sailingscoreboard.com/results/raceresults/class/469) |
| results/raceresults/race/nnn | Returns the races for Race ID nnn. | [http://www.rest.sailingscoreboard.com/results/raceresults/race/2595](http://www.rest.sailingscoreboard.com/results/raceresults/race/2595) |

Data returned

| Result Element | Description | Example |
|---|---|---|
| RaceResultId | Internal id of this race result record | 28658 |
| RaceId | Internal id of race | 2595 |
| RaceDate | Date of race (yyyy-mm-dd) | 2013-10-26 |
| FinishCode | 3 character code of finish status. Refer to FinishCode list for details. | FIN |
| FinishTime | Actual Finish time as "hh"mm:ss" | 12:44:16 |
| ElapsedTime | Elapsed time as (Finish Time minus Race Start Time) in seconds. Null for "place only" classes. | 9256 |
| CorrectedTime | Corrected time = Elapsed Time * TCF in seconds. Null for "place only" classes. | 10561 |
| PenaltyPlace | Place awarded by Jury. Finish Code should be = PEN or RDG | 0 |
| PenaltyPoints | Points awarded by Jury. Finish Code should be = PEN or RDG | 0 |
| Status | Publication status of this race result. 0=Pending, 1=Published | 1 |
| ClassId | Internal Id of class (numeric) | 465 |
| ClassEntryId | Internal id of this boats entry record in this class. | 5285 |
| BoatDisplayName | Name of boat or team to be displayed on results | Alpha Pirates |
| BowNo | Bow number of this boat | 2 |
| OwnerDisplayName | Name of owner or skipper to be displayed on results | Song Xiaqun |
| SailNo | Sail number of this boat (string) | TPE5552 |
| Club | Club of this boat. May be null. | RHKYC |
| Country | Country of this boat. Three character string as per RRS Appendix G | CHN |
| tcf | If the class is a "time" results type, then this contains the time correction factor (float) | 1.141 |
| Points | Points scored in this race | 1 |
| Place | Place awarded in this race. May be numeric (1,2,3...) or 3 character code as per RRS Appendix A | 1 |