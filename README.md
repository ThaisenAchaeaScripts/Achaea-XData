# Achaea-XData

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
