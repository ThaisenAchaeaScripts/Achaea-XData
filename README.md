# Achaea-XData

XData is a mudlet package to make it easier to consume Achaea GMCP data by maintaining local variables and raising additional events.

Modeules
- comms
- status
- vitals
- room
- players
- items
- time
- afflictions
- defenses


---
**xdata comms**
- Event raised when a new communication is recieved.
- ARG1 is a table containing information about the communcation.

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
