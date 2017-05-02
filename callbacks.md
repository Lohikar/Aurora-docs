# Callbacks #
The callback datum `/datum/callback` represents a proc & the required information to call it. They can be called in a blocking or non-blocking (async) manner.

## General Usage ##
Global proc with no arguments: `CALLBACK(GLOBAL_PROC, /proc/do_the_thing)`

Global proc with arguments: `CALLBACK(GLOBAL_PROC, /proc/do_the_thing, argument1, argument2, argument3)`

Proc belonging to an object, defined on that object's type: `CALLBACK(some_object, .proc/some_proc)` (note that doing it this way instead of an absolute path allows child-types of this type to override the called proc.)

Proc belonging to an object, defined on a parent type: `CALLBACK(some_object, /atom/movable/.proc/some_other_proc)`

## Calling ##
A callback can be manually called using `Invoke()`.

Example:
```
/datum/callback/mycallback = CALLBACK(GLOBAL_PROC, /proc/do_the_thing)`
var/return_val = mycallback.Invoke()
```

Additional arguments may also be passed with invoke, like so:
```
/datum/callback/mycallback = CALLBACK(GLOBAL_PROC, /proc/do_the_thing)`
var/return_val = mycallback.Invoke(some_argument, some_other_argument)
```

`Invoke()` will block until the callback proc returns, and will return that proc's value. If you want to call a proc without waiting for it, use `InvokeAsync()`, but note that it does not return a value.
