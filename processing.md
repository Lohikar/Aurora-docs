# Processing Subsystems #
`processing_objects` is now considered obsolete and should be avoided whenever possible.

`process()` is now defined at the `/datum` level, as such any variable can be made to process with a processing subsystem.

To register an object with a processing subsystem, use `START_PROCESSING(the_processing_subsystem, your_object)`, generally you want to use `SSprocessing`. 

`START_PROCESSING(SSprocessing, your_object)` is equivalent to `processing_objects += your_object`.

To stop an object processing, use `STOP_PROCESSING(the_processing_subsystem, your_object)`.

An object may only be in one processing list at a time, and it may only be in the list once. `START_PROCESSING()` and `STOP_PROCESSING()` will automatically enforce this for you.

Valid processing lists: `SScalamity`, `SSdisposals`, `SSprocessing`, `SSfast_processing`, `SSdisease`, `SSmodifiers`. Generally only `SSprocessing` (2 seconds) and `SSfast_processing` (0.5 seconds) should be used.
