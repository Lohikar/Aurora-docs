# Initialization & New() #
The `/atom` initialization process has changed dramatically. All `/atom` types including `/turf` and `/area` can use `Initialize()`, and arguments to `New()` are passed along to `Initialize()`.

`New()` and `Initialize()` overrides should not be mixed when possible as one is not guaranteed to occur before the other; their order varies based on when the atom is created.

## Basic Usage ##
Overriding/defining `New()` should be avoided when possible in favor of `Initialize()`.

`Initialize()` always has at least one argument: `mapload`. It is always the first argument. `mapload` is `TRUE` if the atom is being initialized during server startup, `FALSE` otherwise. If any other arguments are passed to `New()`, they will come after mapload. Initialize must return parent.

Example:
```
/obj/myobj/Initialize(mapload)
	. = ..()
	if (mapload)
		world << "[src] initialized at mapload!"
	else
		world << "[src] initialized normally!"
```

## Initialization Hints ##
Initialize can return a hint instead of parent (although parent should still be called), allowing for special post-initialization behavior. The following hints are understood.

`INITIALIZE_HINT_NORMAL` -> Default. Nothing special happens.

`INITIALIZE_HINT_LATELOAD` -> `LateInitialize()` is called.

`INITIALIZE_HINT_QDEL` -> The atom is qdeleted after `Initialize()` returns.

`INITIALIZE_HINT_LATEQDEL` -> The atom is qdeleted after server initialization completes, or immediately after `Initialize()` if the server is already initialized.


## LateInitialize() ##
`LateInitialize()` is another initialization proc that can be defined to do things that require the rest of the objects in the world to be initialized first. It does not need to return anything or call parent.

Example:
```
/obj/myobj/LateInitialize()
	world << "[src] late initialized!"
```

`LateInitialize()` will only be called if `Initialize()` returns `INITIALIZE_HINT_LATELOAD`. If the atom is initialized during server load, it will `LateInitialize()` after all `Initialize()` calls complete. If the atom is initialized later, `LateInitialize()` will be called immediately after `Initialize()`.
