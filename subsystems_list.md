# Subsystem Reference #
This is a list of all current subsystems & a quick summary of what they do.

## Air (SSair) ##
ZAS simulation ticks & zone rebuilds.

## Alarm (SSalarm) ##
Tracking and processing of air, fire, and power alarm datums. In-game alarm objects are not processed here.

## Arrivals (SSarrivals) ##
Controls the Odin arrivals shuttle & handles Odin despawn timeout.

## Assets (SSassets) ##
Player asset cache. Handles sending of NanoUI and other HTML assets to players. Does not fire.

## Chemistry (SSchemistry) ##
Handles multi-tick chemical reactions.

## Effects Master (SSeffects) ##
Handles new-style effect ticks. Currently only used by sparks.

## Emergency Shuttle (emergency_shuttle) ##
Handles emergency shuttle movement & calling.

## Events (SSevents) ##
Handles random event scheduling & ticks.

## Explosives (SSexplosives) ##
Handles explosion processing.

## Falling (SSfalling) ##
Handles objects falling down openturfs.

## Garbage (SSgarbage) ##
Garbage collector. Manages qdel'd objects.

## Icon Cache (SSicon_cache) ##
Global holder for icon cache lists. Does not fire.

## Icon Smoothing (SSicon_smooth) ##
Handles queued icon smooth operations.

## Icon Updates (SSicon_update) ##
Handles icon updates queued with `queue_icon_update()`.

## IPIntel (SSipintel) ##
Container for IPIntel cache. Does not fire.

## Jobs (SSjobs) ##
Handles job assignment, spawning, and despawning. Does not fire.

## Law (SSlaw) ##
Container for corporate regulations. Does not fire.

## Lighting (SSlighting) ##
Processes queued lighting engine updates & contains lighting object lists.

## Machinery (SSmachinery) ##
Handles machinery ticks, powernet ticks, and contains the global camera list.

## Mobs (SSmobs) ##
Mob `Life()` processing & container for global mouse list.

## Night Lighting (SSnightlight) ##
Handles automatic night lighting switch over.

## Objects (SSobjects) ##
Handles processing of the `processing_objects` list.

## Open Space (SSopenturf) ##
Handles updates of open turf overlays & turfs, as well as containing the global lists of all openspace overlays + all openturfs.

## Orbit (SSorbit) ##
Handles orbit datum updates.

## pAI (SSpai) ##
Global pAI controller, handles candidate finding & global pAI software list. Does not fire.

## Parallax (SSparallax) ##
Space parallax setup & container for space parallax lists. Does not fire.

## Power (SSpower) ##
Contains powernet lists and manages RCON. Does not fire.

## Radio (SSradio) ##
Communications controller, manages radio frequencies. Does not fire.

## Statistics (SSfeedback) ##
Handles inactivity kick, feedback gathering, and round-end statistics. Cannot be var-edited.

## Sun (SSsun) ##
Solar sun tracking & solar panel updates.

## Sunlight (SSsunlight) ##
Handles surface sunlight illumination. Does not fire.

## Cargo (SScargo) ##
Manages cargo shuttle & supply transactions.

## Ticker (SSticker) ##
Manages game mode & round status.

## Timer (SStimer) ##
Handles timer (addtimer) processing.

## Vote (SSvote) ##
Handles voting. Shocking.

## Wireless (SSwireless) ##
Maintains wireless reciever lists & handles wireless datum pairing.

## Airflow (SSairflow) [Processing] ##
Handles object movement due to air pressure. Does not support `START_PROCESSING()`. 0.1s tickrate.

## Calamity (SScalamity) ##
Generic processor intended for use with blobs, singularities, and other major objects. Supports `START_PROCESSING()`.

## Disease (SSdisease) ##
Generic processor intended for use with diseases. Supports `START_PROCESSING()`.

## Disposals (SSdisposals) ##
Generic processor intended for use with disposal holder objects. Supports `START_PROCESSING()`.

## Processing (Fast) (SSfast_process) ##
Generic multi-purpose processor with a high (0.5s) tick-rate. Supports `START_PROCESSING()`.

## Modifiers (SSmodifiers) ##
Generic processor intended for use with modifier datums. 1s tickrate.

## NanoUI (SSnanoui) ##
Manages & processes NanoUI datums. Supports `START_PROCESSING()`, but should not be used for processing directly.

## Overlays (SSoverlays) ##
Handles addition/removal of overlays from atoms. Does not support `START_PROCESSING()`.

## Pipenet (SSpipenet) ##
Handles atmos pipenet processing. Supports `START_PROCESSING()`.

## Seeds & Plants (SSplants) ##
Maintains global seed lists, plant icon caches, and handles spreading vine processing. Supports `START_PROCESSING()`.

## Processing (SSprocessing) ##
Generic multi-purpose processor. Supports `START_PROCESSING()`. 2s tickrate.

## Shuttles (shuttle_controller) ##
Handles shuttle processing & maintains global shuttle lists. Supports `START_PROCESSING()`.

## Asteroid (N/A) ##
Handles asteroid generation. Does not fire.

## Atoms (SSatoms) ##
Handles atom initialization. Does not fire.

## Early Miscellaneous Init (N/A) ##
Handles miscellaneous server setup steps done early in server boot. Does not fire.

## Late Miscellaneous Init (N/A) ##
Handles miscellaneous server setup steps done late in server boot. Does not fire.

## Xenoarcheology (SSxenoarch) ##
Handles xenoarch find generation at world start. Does not fire.
