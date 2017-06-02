# Lazy List Helpers #
The LAZY* helpers are a set of defines useful for working with lists in a way that only keeps them around when they're actually needed. Lazy list operators should not be used on lists that are passed by reference as they may break the reference.

`LAZYADD(list, item)` - adds `item` to `list`. if `list` is null, it is created.

`LAZYREMOVE(list, item)` - removes `item` from `list`. If `list` is null, nothing is done. If `list` has 0 length after the item is removed, it is nulled out.

`LAZYACCESS(list, index)` - accesses `index` index of `list`. if `list` is null, `null` is returned. If `index` is a number and `index` is greater than `list.len`, `null` is returned. Otherwise, value at `list[index]` is returned.

`LAZYLEN(list)` - gets the length of `list`. If `list` is null, returns `0`.

`LAZYCLEARLIST(list)` - Clears `list` via. `Cut()`. If `list` is null, nothing is done.

`UNSETEMPTY(list)` - If `list` has no length, it is nulled out. Otherwise, nothing is done.

`LAZYINITLIST(list)` - If `list` is null, a new list is created and assigned to `list`.
