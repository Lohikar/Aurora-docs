# qdel, Destroy, and SSgarbage #
A new garbage collector has been introduced with the SMC PR, this comes with new features for Destroy() as well as a requirement to return parent in Destroy().

This is how most Destroy() procs should look:
```
/obj/mything/Destroy()
    some_global_list_of_mythings -= src
	return ..()
```

SSgarbage also accepts deletion hints. Most of the time you should not need these. These are the hints that are understood:

`QDEL_HINT_QUEUE` -> Handle deletion normally. This is the default, you shouldn't need to manually specify this.

`QDEL_HINT_LETMELIVE` -> Do not delete on *non-forced* qdel. If you use this hint, you *must* respect force deletions. The GC will ignore this hint and complain on force-delete.

`QDEL_HINT_IWILLGC` -> This object will handle GC itself and the GC should leave it alone. Functionally the same as LETMELIVE.

`QDEL_HINT_HARDDEL` -> Hard-delete this object instead of attempting to GC it. Has a negative performance cost. Avoid usage if possible.

`QDEL_HINT_HARDDEL_NOW` -> Hard-deletes this object *ASAP*. Has a negative performance cost. Avoid usage if possible.

`QDEL_HINT_FINDREFERENCE` -> Functionally identical to `QDEL_HINT_QUEUE`, except the GC will run find-references on del if `TESTING` is defined.

`QDEL_HINT_POOL` -> The GC will return this object to the pool instead of deleting it on non-forced deletes. Objects that use this hint must respect force-deletion.

To use a hint, return it instead of returning parent. You must still call parent. If you're using `QDEL_HINT_POOL` or `QDEL_HINT_LETMELIVE`, you *must* respect the force parameter. If you do not respect the force parameter, the GC will delete you anyways on force delete. Admin-delete uses force-delete.

Example of a Destroy() with a hint:
```
/obj/mything/myotherthing/Destroy()
    some_global_list_of_myotherthings -= src
	..()
	return QDEL_HINT_HARDDEL
```

Example of a Destroy() with a force-respecting hint:
```
/obj/mything/myotherotherthing/Destroy(force = FALSE)
	if (!force)
		world << "Something tried to delete [src]!"
		return QDEL_HINT_LETMELIVE

	// force-deletion
	world << "[src] force-deleted."
	return ..()
```

Additionally, `qdel()` has a new parameter: `force`. `/proc/qdel(datum/the_thing, force = FALSE)`. If force is `TRUE`, the object is force-deleted.
