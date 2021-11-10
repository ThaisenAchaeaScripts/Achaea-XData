# Achaea-XData

XData is a mudlet package to make it easier to consume Achaea GMCP data by maintaining local variables and raising additional events.

Modeules
- afflictions


---
**xdata afflictions**
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

**xdata afflictions gain**
- Event raised whenever a new affliction has been gained
- ARG1 is the name of the affliction
- xdata.afflictions contains full list
```lua
Event: xdata afflictions gain
"paralysis"
```

**xdata afflictions lost**
- Event raised whenever an affliction is lost
- ARG1 is the name of the affliction
- ARG2 is the time in seconds since the affliction was initially gained
- xdata.afflictions contains full list
```lua
Event: xdata afflictions lost
"paralysis"
4.0320000648499
```

**xdata affliction miss**
- Event raised whenever an affliction is cured that xdata didn't already know about
- ARG1 is the name of the affliction
- xdata afflictions lost is always raised at the same time
```lua
Event: xdata afflictions miss
"paralysis"
```




---
**xdata comms**
- Event raised when a new communication is recieved.
- ARG1 contins xdata.comms
- Variables
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
