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
