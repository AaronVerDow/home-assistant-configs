## Mode
his sets some default attributes for lights like brightness and color.  All or none can be set.  These are grouped in lists and the settings will cascade if active.

Examples: (instances of Mode)
* Cool lights
* Warm lights
* Bright
* Dim
* Sleeping 
* Watching TV
* Playing video games
* Colorful
* Emergency
* Empty
* Night Vision
Options:
* primary lights
    * value(s) to apply to primary lights
* accent lights
    * value(s) to apply to accent lights
States:
* active
    * Is this mode active or not?

## Room 
Controls transisions between states 
Examples:
* Bedroom
* Kitchen 
* etc...

Options:
* Active modes
* Active timeout
* Idle modes
* Idle timeout
* Inactive modes
* Expectant modes
* Expectant timeout
* Neighboring rooms
    * Instances of rooms connected to this one.
* Sensors
    * Motion sensors for the rooms
* Primary Lights
    * Lights in ceiling fixtures or visible lamps
* Accent Lights
    * Lights under furniture
* Optional Devices
    * Don't turn these on when active, let the user do it.  Turn off when inactive.
    * Turn off when state transitions to inactive
    * Examples:
        * Fans
        * Soldering iron
        * Hair straightener
        * TVs
* Manditory Devices:
    * Things that should always be on when the room is active
    * Turn on when state transisitions to active (or expectant?)
    * Turn off when state transitions to inactive
    * Examples:
        * Computer monitors
* Ghost Devices:
    * Things that should only be on when the room is inactive
    * Turn on when state transitions to inactive
    * Turn off when state transitions to expectant or active
    * Examples:
        * Air filters
States:
* Status:
    * Active
    * Idle
    * Inactive
    * Expectant
* Primary Light Value
* Accent Light Value
* Alarmed
    * Something unexpected happened.  Not really used in this class but will be picked up by other automation.
* Armed 
    * Trigger alarmed state if something unexpected happened.  (Transition from inactive to active without going through the expectant state.)
    * This will be turned on by other automation.
    * Rooms will turn off neighbors once they go inactive.

Events:
* Motion detected:
    * Set status to "active"
    * Notify neighbors of pending activity
* Inactivity detected:
    * Start active timer
* Status changed:
    * Calculate new light values
* Status turned to active:
    * Turn on manditory devices
    * Cancel idle timer
    * Cancel expectant timer
* Mode changed:
    * Calculate new light values
* Light values changed:
    * Write values to lights
* Active timer finished
    * Set status to idle
    * Start idle timer
* Idle timer finished
    * Set status to inactive
    * Disarm neighbors
    * Turn off optional devices
    * Turn on ghost devices
* Notification of pending activity 
    * If status is not inactive do nothing
    * set mode to expectant
    * Start expectant timer
* Expectant timer finished
    * Set status to inactive 
