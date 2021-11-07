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


xdata comms
- Event raised when a new communication is recieved.
- ARG1 is a table containing information about the communcation.

```javascript
function fancyAlert(arg) {
  if(arg) {
    $.facebox({div:'#foo'})
  }
}
```
