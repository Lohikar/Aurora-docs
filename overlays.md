# Overlays & SSoverlay #
SSoverlay is a new way to handle `/atom` overlays that allows for automatic overlay caching and reduced appearance churn.

## Usage ##
`/atom/add_overlay(image|text|icon|list(image|text|icon), priority = FALSE)`

Arguments mimic arguments accepted by `atom += `. If argument is a list, all contents of list are added to overlays.
If `priority` is true, the overlay will be added as a priority overlay - it will not be removed by `cut_overlay()` and `cut_overlays()` UNLESS the call to `cut_overlay()` or `cut_overlays()` also has `priority` as true.


`/atom/cut_overlay(image|text|icon|list(image|text|icon), priority = FALSE)`

Removes the matching overlay image if it is present. Same arguments as `add_overlay()`.


`/atom/cut_overlays(priority = FALSE)`

Removes all non-priority overlays from an object UNLESS `priority` is true.


`/atom/copy_overlays(atom/other_atom, cut_old = FALSE)`

Copies another atom's overlays (excluding priority) to this atom. If `cut_old` is true, this atom's existing overlays (excluding priority) will be cut first.
