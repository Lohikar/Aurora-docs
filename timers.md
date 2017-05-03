# SStimer and addtimer #
SStimer is a system that replaces spawn() and Scheduler. **Timers are faster than spawn() and it is preferred to use addtimer instead of spawn whenever possible.**

Timers cannot fire before master controller initialization completes at server startup.

## Arguments ##

`addtimer(datum/callback/callback, time, flags)`

`flags` is optional, `callback` and `time` are not. `time` can be zero.

SStimer will invoke `callback` after `time` ds have passed. The callback will not block further timers from processing.

Generally the first argument should be a `CALLBACK()` call, like `addtimer(CALLBACK(src, .proc/something), 15)`.

## Flags ##
Flags is a bitfield, and as such these values can be OR'd to combine them.
The following flags are understood by addtimer:

`TIMER_UNIQUE` -> Do not run timer if an identical timer is already running.

`TIMER_OVERRIDE` (used with `TIMER_UNIQUE`) -> If an identical timer is already running, stop it and run this one instead.

`TIMER_CLIENT_TIME` -> Calculate time with more accurate client time. More expensive to track, should only be used to sync things with events that happen client-side, such as animations or sounds.

`TIMER_STOPPABLE` -> `addtimer()` will return a value that can be used to stop the timer with `deltimer()`.

`TIMER_NO_HASH_WAIT` -> The timer's `time` variable will not be used to check if a timer is unique.

## General Usage ##
The most common way to use addtimer is:

`addtimer(CALLBACK(src, .proc/some_proc), 15)`

This will call a proc named `some_proc` defined on the current object in `15` ds.


## Stoppable Timers ##
The `TIMER_STOPPABLE` flag allows you to stop the timer before it completes.

When this flag is supplied, `addtimer()` will return a value used to identify the timer which can be stored in a variable.

To delete a timer, use `deltimer(the_return_value_of_addtimer)`. Deltimer will return `TRUE` if the timer was successfully deleted, `FALSE` otherwise. 

It is safe to re-delete a timer already deleted, or a null variable. Deltimer will do nothing and return `FALSE` in this case.

Example:
```
/proc/my_proc()
	world << "my_proc invoked!"
  
var/mytimer

/proc/start_timer()
	mytimer = addtimer(CALLBACK(GLOBAL_PROC, /proc/my_proc), 2 SECONDS, TIMER_STOPPABLE)
    
/proc/stop_timer()
	if (deltimer(mytimer))
		world << "Successfully deleted mytimer!"
	else
		world << "Unable to delete mytimer!"
```

All timers associated with an object are automatically deleted when the object is qdeleted, regardless of flags.

## Unique Timers ##
The `TIMER_UNIQUE` flag allows you to specify that a timer should only run if another identical timer is not running on the same object.

The values used to check if a timer is unique are: `callback` (incl. source object), `flags`, `wait` (if `TIMER_NO_HASH_WAIT` is not specified).

If `TIMER_OVERRIDE` is specified, the timer will overwrite the other timer instead of not running.

If `TIMER_NO_HASH_WAIT` is specified, a timer's set time will not be considered when checking if a timer is unique or not.
