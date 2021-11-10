# Achaea XData

XData is a mudlet package aimed to make it easier to consume Achaea GMCP data by maintaining local variables and raising additional events.

- afflictions
  - [xdata afflictions](#xdata_afflictions)
  - [xdata afflictions gain](#xdata_afflictions_gain)
  - [xdata afflictions lost](#xdata_afflictions_lost)
  - [xdata afflictions miss](#xdata_afflictions_miss)

- comms
  - [xdata comms](#xdata_comms)

- defences
  - [xdata defences](#xdata_defences)
  - [xdata defences gain](#xdata_defences_gain)
  - [xdata defences lost](#xdata_defences_lost)

- items
  - [xdata items](#xdata_items)
  - [xdata items add](#xdata_items_add)
  - [xdata items remove](#xdata_items_remove)
  - [xdata items update](#xdata_items_update)

- players
  - [xdata players](#xdata_players)
  - [xdata players add](#xdata_players_add)
  - [xdata players remove](#xdata_players_remove)

- rift
  - [xdata rift](#xdata_rift)
  - [xdata rift change](#xdata_rift_change)

- room
  - [xdata room](#xdata_room)

- status
  - [xdata status](#xdata_status)

- time
  - [xdata time](#xdata_time)
  - [xdata time dawn](#xdata_time_dawn)
  - [xdata time noon](#xdata_time_noon)
  - [xdata time dusk](#xdata_time_dusk)
  - [xdata time midnight](#xdata_time_midnight)

- vitals
  - [xdata_vitals](#xdata_vitals)
  - [xdata balance gain](#xdata_balance_gain)
  - [xdata balance lost](#xdata_balance_lost)
  - [xdata equilibrium gain](#xdata_equilibrium_gain)
  - [xdata equilibrium lost](#xdata_equilibrium_lost)
  - [xdata health change](#xdata_health_change)
  - [xdata health full](#xdata_health_full)
  - [xdata mana change](#xdata_mana_change)
  - [xdata mana full](#xdata_mana_full)
  - [xdata endurance change](#xdata_endurance_change)
  - [xdata endurance full](#xdata_endurance_full)
  - [xdata willpower change](#xdata_willpower_change)
  - [xdata willpower full](#xdata_willpower_full)


---
<a name="xdata_afflictions">**xdata afflictions**</a>
- Event raised whenever the Achaea affliction list is recieved on diagnose.
- ARG1 contains xdata.afflications
- xdata.afflictions is a table where the afflictions are keys and the values are the unix time when the affliction was recieved.
- If the affliction isn't in the table or the value is 0 then the affliction is not present.
```lua
Event: xdata afflictions
{
  blindness = 1636558699.754,
  deafness = 1636558699.754,
  paralysis = 1636558699.754
}
```

<a name="xdata_afflictions_gain">**xdata afflictions gain**</a>
- Event raised whenever a new affliction has been gained
- ARG1 is the name of the affliction
- xdata.afflictions contains full list
```lua
Event: xdata afflictions gain
"paralysis"
```

<a name="xdata_afflictions_lost">**xdata afflictions lost**</a>
- Event raised whenever an affliction is lost
- ARG1 is the name of the affliction
- ARG2 is the time in seconds since the affliction was initially gained
- xdata.afflictions contains full list
```lua
Event: xdata afflictions lost
"paralysis"
4.0320000648499
```

<a name="xdata_afflictions_miss">**xdata afflictions miss**</a>
- Event raised whenever an affliction is cured that xdata didn't already know about
- ARG1 is the name of the affliction
- xdata afflictions lost is always raised at the same time
```lua
Event: xdata afflictions miss
"paralysis"
```

---
<a name="xdata_comms">**xdata comms**</a>
- Event raised when a new communication is recieved.
- ARG1 contains xdata.comms
  - ansi: The communication with ANSI color codes, can be used with ansi2deco function in mudlet.
  - channel: The communication channel the message was sent on. ('says','tells','city','house','order',ect)
  - epoch: The unix time that the communction was recieved.
  - talker: The person who sent the message.
  - text: The text of the message with ANSI color codes removed.
  - time: The UTC time that the message was sent.

```lua
Event: xdata comms
{
  ansi = '\27[38;5;014;48;5;237mYour breath sizzles as you say, "Hello."\27[0;37m',
  channel = "says",
  epoch = 1636315829.326,
  talker = "Thaisen",
  text = 'Your breath sizzles as you say, "Hello."',
  time = "11/07/21 20:10:29"
}
```
---
<a name="xdata_defences">**xdata defences**</a>
- Event raised whenever the Achaea defences list is recieved on def.
- ARG1 contains xdata.defences
- xdata.defences is a table where the defences are keys and the values are true or false
- If the defence isn't in the table or the value is false then the defence is not present.
```lua
Event: xdata defences
{
  blindness = true,
  boartattoo = true,
  deafness = true,
  megalithtattoo = true,
  mindseye = true,
  moontattoo = true,
  mosstattoo = true,
  oxtattoo = true
}
```

<a name="xdata_defences_gain">**xdata defences gain**</a>
- Event raised whenever a new defences has been gained
- ARG1 is the name of the defences
- xdata.defences contains full list
```lua
Event: xdata defences gain
"nightsight"
```

<a name="xdata_defences_lost">**xdata defences lost**</a>
- Event raised whenever an defences is lost
- ARG1 is the name of the defences
- xdata.defences contains full list
```lua
Event: xdata defences lost
"softfocusing"
```

---

<a name="xdata_items">**xdata items**</a>
- Event raised whenever an items list is changed
- ARG1 is the location, possible values are 'inv','room','denizens', or 'repXXX' (repXXX is a container where XXX is the container id)
- ARG2 is the table of items where the key is the item id and value is a table of information about the item.
- Tables are stored in xdata.items.LOCATION (e.g. xdata.items.inv or xdata.items.denizens)

```lua
Event: xdata items
"room"
{
  [129601] = {
    icon = "rune",
    id = 129601,
    name = "a runic totem"
  },
  [251212] = {
    icon = "shrine",
    id = 251212,
    name = "a white marble altar"
  },
  [268819] = {
    id = 268819,
    name = "a broken skullbone",
    takeable = true
  },
  [292172] = {
    icon = "lamp",
    id = 292172,
    name = "a logosmas stocking"
  },
  [316094] = {
    icon = "shrine",
    id = 316094,
    name = "a shrine of Neraeos"
  },
  [381143] = {
    icon = "lamp",
    id = 381143,
    name = "a logosmas stocking"
  }
}
```

Item tables can contain the following:
- id: The Achaea item id
- name: The name of the item
- icon: the Achaea icon (used in HTML5 client)
- container: the item is a container and can hold other items
- dead: a denizen that is currently a corpse
- edible: an item that can be eaten
- fluid: a consumable liquid
- groupable: an item that can be grouped together
- loyal: denizens that are loyal to a city (e.g. guards)
- monster: a denizen (these are always in xdata.items.denizens)
- riftable: an item that can be placed in the rift
- takeable: an item on the ground that can be picked up
- wearable: an item that can be worn but currently isn't
- wieldleft: an item that is wielded in the left hand
- wieldright: an item that is wielded in the right hand
- worn: an item that is wearable and currently worn

<a name="xdata_items_add">**xdata items add**</a>
- Event raised whenever an item is removed from a location
- ARG1 is the location, possible values are 'inv','room','denizens', or 'repXXX' (repXXX is a container where XXX is the container id)
- ARG2 is a table containing the item information
- xdata.items.LOCATION is alway updated (e.g. xdata.items.inv or xdata.items.denizens)
```lua
Event: xdata items add
"denizens"
{
  icon = "animal",
  id = 36453,
  monster = true,
  name = "a blackbird"
}
```

<a name="xdata_items_remove">**xdata items remove**</a>
- Event raised whenever an item is removed from a location
- ARG1 is the location, possible values are 'inv','room','denizens', or 'repXXX' (repXXX is a container where XXX is the container id)
- ARG2 is a table containing the item information
- xdata.items.LOCATION is alway updated (e.g. xdata.items.inv or xdata.items.denizens)
```lua
Event: xdata items remove
"inv"
{
  groupable = true,
  icon = "commodity",
  id = 244061,
  name = "a piece of stag's horn",
  riftable = true
}
```

<a name="xdata_items_update">**xdata items update**</a>
- Event raised whenever an item is updated while in inventory
- ARG1 is the location, typically only applies to 'inv'
- ARG2 is a table containing the item information
- xdata.items.LOCATION is alway updated (e.g. xdata.items.inv)
```lua
Event: xdata items update
"inv"
{
  icon = "clothing",
  id = 575794,
  name = "a pair of atavian wings",
  worn = true
}

Event: xdata items update
"inv"
{
  icon = "clothing",
  id = 575794,
  name = "a pair of atavian wings",
  wearable = true
}
```

---

<a name="xdata_players">**xdata players**</a>
- Event raised whenever the players in the current room changes
- ARG1 contains xdata.players
- xdata.players is a table containing the player names
```lua
Event: xdata players
{ "Aeldir", "Ellarose", "Thaisen" }
```

<a name="xdata_players_add">**xdata players add**</a>
- Event raised whenever a new player is added to the room
- ARG1 contains the player name
- xdata.players is always updated
```lua
Event: xdata players add
"Aeldir"
```

<a name="xdata_players_remove">**xdata players remove**</a>
- Event raised whenever a new player is removed from the room
- ARG1 contains the player name
- xdata.players is always updated
```lua
Event: xdata players remove
"Ellarose"
```

---

<a name="xdata_rift">**xdata rift**</a>
- Event raised whenever rift contents is received from the game (typically on INR ALL)
- ARG1 contains the content of xdata.rift
- xdata.rift is a table where the key is the type of item and the value is the amount in the rift

```lua
Event: xdata rift
{
  alchemical_mercury = 2,
  alchemical_salt = 25,
  antimony = 3,
  argentum = 16,
  arsenic = 10,
  ash = 5461,
  aurum = 40,
  azurite = 1,
  bayberry = 5929,
etc...
```


<a name="xdata_rift_change">**xdata rift change**</a>
- Event raised whenever rift contents are added or removed
- ARG1 contains the name of the item
- ARG2 contains the amount added (negative if items removed)
- xdata.rift is always updated with new rift totals

```lua
Event: xdata rift change
"redink"
-10
```

xdata.rift uses a few special naming conventions different from the game
- elixirs are prefixed with "elixir_"
- salves are prefixed with "salve_"
- alchemical ingredients are prefixed with "alchemical_"
- venoms are prefixed with "venom_"
- crystals are prefixed with "crystal_"
- any spaces or non-alpha characters are removed

---


<a name="xdata_room">**xdata room**</a>
- Event raised when room information is received, typically when moving or when you LOOK.
- ARG1 is the contents of xdata.room
- xdata.room is a table containing information about the room
```lua
Event: xdata room
{
  areagame = "Cyrene",
  areaid = 57,
  areamap = "Cyrene, the City of",
  description = "The two main thoroughfares of Cyrene meet here, crossing through an expansive 
plaza surrounding the grassy knoll beneath the city's clocktower. Painted stones of all shapes and 
sizes mesh in an intricate, two-sided mosaic that spans the Crossing. Brightly coloured scenes of 
spring mornings, summer afternoons, and autumn evenings adorn the northern half of the area, 
allowing the clocktower's shadow to mark the passage of time under the light of the sun. To the 
south, scenes of snowy winter nights and rushing rivers adorn the cobbles, marked by large swathes 
of pale whites and chill blues. Broken pillars and chunks of shattered stone, carefully placed and 
smoothed by hand, offer a ring of seating in the grasses beyond the southern edge of the crossing, 
nestled in the shade of several tall, lush trees that border the area. To the south and west, 
bustling rows of shops and other commercial buildings are visible, in stark contrast to the 
picturesque estates lining Bard's way to the north. To the east, the Resistance Bridge rises, 
allowing passage over the Shuun'eludiela.",
  environment = "Urban",
  exitrooms = {
    east = 6297,
    in = 18691,
    north = 6390,
    south = 6391,
    west = 6299
  },
  exits = { "in", "west", "south", "east", "north" },
  harbour = false,
  id = 6298,
  indoors = false,
  name = "Centre Crossing",
  ohmap = false,
  outdoors = true,
  shop = false,
  wilderness = false
}
```

---
<a name="xdata_status">**xdata stats**</a>
- Event raised when status information changes or player requests via STAT
- ARG1 contains xdata.status
- xdata.status is a table containing information about the character
```lua
Event: xdata status
{
  age = 124,
  city = "Cyrene",
  cityrank = 6,
  class = "Serpent",
  credits = { 162, 222 },
  explorerrank = "an Achaean Ranger, 2nd Class",
  gender = "male",
  gold = { 540915, 507894, 1048809 },
  house = "The Grand Merchant Collective",
  houserank = 3,
  lessons = 1249,
  level = 114,
  levelnext = 66.7,
  levelxp = 33.3,
  name = "Thaisen",
  namefull = "Thaisen Vorondil-Lanthe, Merchant Intern",
  nameprefix = "",
  namesuffix = "Vorondil-Lanthe, Merchant Intern",
  order = "(None)",
  race = "Human",
  racefull = "Human Rogue",
  racespec = "Rogue",
  unread_msgs = 0,
  unread_news = 0
}
```
Differences from GMCP
- credits is a table {unbound, bound} (e.g. xdata.status.credits[1] = number of unbound credits)
- gold is a table {inv,bank,total} (e.g. xdata.status.gold[2] = amount of gold in the bank)
- cityrank and houserank are their own variables
- level is split into level, levelxp, and levelnext
- race is split into race, racespec and racefull
- name is split into name, namefull, nameprefix and namesuffix

---

<a name="xdata_time">**xdata time**</a>
- Event raised when time is updated
- XData requests the time from the server every minute
- ARG1 is the contents of xdata.time
- xdata.time is a table contining information about the current date and time

```lua
Event: xdata time
{
  day = 17,
  daynight = 93,
  epoch = 1636567929.65,
  hour = 43,
  mon = 3,
  month = "Aeguary",
  moonphase = "Waxing Gibbous",
  rltime = "11/10/21 18:12:09",
  time = "The shadows have lengthened. It is late afternoon in Achaea.",
  year = 873
}
```
Differences from GMCP
- epoch is Unix time
- rltime is real world UTC time

<a name="xdata_time_dawn">**xdata time dawn**</a>
- Event raised when it is dawn
- No arguments
```lua
Event: xdata time dawn
```


<a name="xdata_time_noon">**xdata time noon**</a>
- Event raised when it is noon
- No arguments
```lua
Event: xdata time noon
```


<a name="xdata_time_dusk">**xdata time dusk**</a>
- Event raised when it is dusk
- No arguments
```lua
Event: xdata time dusk
```


<a name="xdata_time_dawn">**xdata time midnight**</a>
- Event raised when it is midnight
- No arguments
```lua
Event: xdata time midnight
```

---

<a name="xdata_vials">**xdata vitals**</a>
- Event raised when vitals are received, typically every prompt
- ARG1 contains contents of xdata.vitals
- xdata.vitals is important information about characters current vitals
```lua
Event: xdata vitals
{
  balance = true,
  balance_duration = 0.97000002861023,
  balance_gain = 1636568310.427,
  balance_lost = 1636568309.457,
  bleed = 0,
  endurance = 5793,
  endurance_change = 0,
  endurance_max = 5793,
  endurance_pct = 1,
  endurance_pct_change = 0,
  equilibrium = true,
  equilibrium_duration = 2.9739999771118,
  equilibrium_gain = 1636566976.415,
  equilibrium_lost = 1636566973.441,
  health = 6053,
  health_change = 0,
  health_max = 6053,
  health_pct = 1,
  health_pct_change = 0,
  mana = 5793,
  mana_change = 0,
  mana_max = 5793,
  mana_pct = 1,
  mana_pct_change = 0,
  rage = 0,
  venom = "",
  willpower = 5793,
  willpower_change = 0,
  willpower_max = 5793,
  willpower_pct = 1,
  willpower_pct_change = 0
}
```
- balance: variable if you currrently have balance, true or false
- balance duration: time in seconds it took to gain balance last time
- balance gain: Unix time when balance was last gained
- balance lost: Unix time when balance was last lost
- same varaibles exist for equilibrium
- health: current health
- health_max: current maximum health
- health_change: change in health from last time vitals were received
- health_pct: current health percentage of maximum health
- health_pct_change: health change in terms of percentage points
- same variables exist for mana, endurance and willpower
- rage: current battlerage amount
- bleed: current rate of bleeding
- class specific varaibles (e.g. above in serpent shows the current venom secreted)

<a name="xdata_balance_gain">**xdata balance gain**</a>
- Event raised when balance is regained
- ARG1 is the Unix Time that balance was regained
- ARG2 is the duration it took to regain balance in seconds
```lua
Event: xdata balance gain
1636569145.312
0.80299997329712
```

<a name="xdata_balance_lost">**xdata balance lost**</a>
- Event raised when balance is lost
- ARG1 is the Unix Time that balance was lost
```lua
Event: xdata balance lost
1636569144.509
```

<a name="xdata_equilibrium_gain">**xdata equilibrium gain**</a>
- Event raised when equilibrium is regained
- ARG1 is the Unix Time that equilibrium was regained
- ARG2 is the duration it took to regain equilibrium in seconds
```lua
Event: xdata equilibrium gain
1636569632.598
1.9500000476837
```

<a name="xdata_equilibrium_lost">**xdata equilibrium lost**</a>
- Event raised when equilibrium is lost
- ARG1 is the Unix Time that equilibrium was lost
```lua
Event: xdata equilibrium lost
1636569630.648
```

<a name="xdata_health_change">**xdata health change**</a>
- Event raised when health is changed
- ARG1 is the amount of health lost/gained
- ARG2 is the percent of health lost/gained
```lua
Event: xdata health change
-83
-0.013712208822072
```

<a name="xdata_health_full">**xdata health full**</a>
- Event raised when health is full
- No arguments
```lua
Event: xdata health full
```

<a name="xdata_mana_change">**xdata mana change**</a>
- Event raised when mana is changed
- ARG1 is the amount of mana lost/gained
- ARG2 is the percent of mana lost/gained
```lua
Event: xdata mana change
23
0.0039703089936131
```

<a name="xdata_mana_full">**xdata mana full**</a>
- Event raised when mana is full
- No arguments
```lua
Event: xdata mana full
```

<a name="xdata_endurance_change">**xdata endurance change**</a>
- Event raised when endurance is changed
- ARG1 is the amount of endurance lost/gained
- ARG2 is the percent of endurance lost/gained
```lua
Event: xdata endurance change
200
0.0075131480090158
```

<a name="xdata_endurance_full">**xdata endurance full**</a>
- Event raised when endurance is full
- No arguments
```lua
Event: xdata endurance full
```

<a name="xdata_willpower_change">**xdata willpower change**</a>
- Event raised when willpower is changed
- ARG1 is the amount of willpower lost/gained
- ARG2 is the percent of willpower lost/gained
```lua
Event: xdata willpower change
-300
-0.012931034482759
```

<a name="xdata_willpower_full">**xdata willpower full**</a>
- Event raised when willpower is full
- No arguments
```lua
Event: xdata willpower full
```
