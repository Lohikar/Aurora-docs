# SStimer and addtimer #
SStimer is a system that replaces spawn() and Scheduler. **Timers are faster than spawn() and it is preferred to use addtimer instead of spawn whenever possible.**

Timers cannot fire before master controller initialization completes at server startup.

## Arguments ##

`addtimer(datum/callback/callback, time, flags)`

`flags` is optional, `callback` and `time` are not. `time` can be zero.

SStimer will invoke `callback` after `time` ds have passed. The callback will not block further timers from processing.

Generally the first argument should be a `CALLBACK()` call, like `addtimer(CALLBACK(src, .proc/something), 15)`.

## Flags ##
The following flag are understood by addtimer:

`TIMER_UNIQUE` -> Do not run timer if an identical timer is already running.

`TIMER_OVERRIDE` (used with `TIMER_UNIQUE`) -> If an identical timer is already running, stop it and run this one instead.

`TIMER_CLIENT_TIME` -> Calculate time with more accurate client time. More expensive to track, should only be used to sync things with events that happen client-side, such as animations or sounds.

`TIMER_STOPPABLE` -> `addtimer()` will return a value that can be used to stop the timer with `deltimer()`.

`TIMER_NO_HASH_WAIT` -> The timer's `time` variable will not be used to check if a timer is unique.

## General Usage ##
The most common way to use addtimer is:


`addtimer(CALLBACK(src, .proc/some_proc), 15)`

This will call a proc named `some_proc` defined on the current object in `15` ds.
