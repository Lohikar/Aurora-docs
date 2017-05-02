# MC Stat Panel #
StonedMC's status panel is completely different from ProcessScheduler's. It will list subsystems even if they do not fire, and subsystem entries can be clicked to open varedit for that subsystem.

## Byond, Master Controller, and Failsafe entries ##
The `Byond` line has the following values:

| Value     | Description                                                 |
|:---------:|-------------------------------------------------------------|
| TickLag   | The currently configured server tick lag.                   |
| FPS       | The currently configured server framerate. Tied to ticklag. |
| TickCount | How many BYOND ticks have occurred since server boot.       |
| TickDrift | A measure of how far behind the MC is from BYOND's tick. This is a measure of lag, the higher this is the more MC ticks have been delayed.|

The `Master Controller` line has the following values:

| Value    | Description |
|:--------:|-------------|
| TickRate | The MC will tick every this many BYOND ticks. Should usually be 1.|
| Iteration | How many times the MC has ticked since it was created or last restarted. |
| SleepDelta | The higher this is, the more the MC is delaying `CHECK_TICK` sleeps. |

The `Failsafe` line has the following values:

| Value  | Description |
|:------:|-------------|
| Defcon | The current alert level of the failsafe. Should always be 5. If this is lowered, something is wrong.
| Interval | How many deciseconds pass between each Failsafe tick. |
| Iteration | How many times the failsafe has fired since it was created or last restarted. |

## Subsystem Lines ##
This only applies during normal server operation, this changes during Master Initialization.

Example:
`[ ] Disposals    0ms|1%|0    P:0`

The `[ ]` will sometimes have a letter inside it, which indicates a state other than idle.

The following letters can show:

| Letter | Meaning  |
|:------:|----------|
| R      | Running       |
| Q      | Queued to run |
| P      | Paused (`MC_TICK_CHECK`) |
| S      | `fire()` is sleeping. |

The `0ms|1%|0` section gives information about how much CPU time the subsystem used in its last fire.

The `0ms` refers to approximately how much time the last fire took to run.

The `1%` refers to approximately how much of a tick (accumulated over tick-checks) the last fire used.

The `0` refers to how many ticks (accumulated over tick-checks) the last fire used.

### OFFLINE, SUSPEND, and NO FIRE ### 
These lines may show in place of the `0ms|1%|0` performance counters.

| Value   | Meaning |
|:-------:|---------|
| OFFLINE | The subsystem has been disabled by an admin or indirectly by an admin's action. |
| SUSPEND | The subsystem has disabled itself. |
| NO FIRE | The subsystem does not `fire()`. |
