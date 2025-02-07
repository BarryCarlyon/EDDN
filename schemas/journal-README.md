# EDDN Journal Schema

## Introduction
Here we document how to take data from miscellaneous ED Journal
events and properly structure it for sending to EDDN.

This is the historical "all Journal events" schema that will be deprecated 
in the future.  Please check for a schema specific to the journal event 
under consideration to see if data should be sent on that event specific 
schema instead.

Please consult [EDDN Schemas README](./README-EDDN-schemas.md) for general
documentation for a schema such as this.

## Senders
The primary data source for this schema is the ED Journal events:

  - `Docked`
  - `FSDJump`
  - `Scan`
  - `Location`
  - `SAASignalsFound`
  - `CarrierJump`
  - `CodexEntry` - But see the separate
    [codexentry schema](./codexentry-README.md) documentation.

### Key Renames
Many of the key names have a different case defined in this schema, make
sure you are renaming them as appropriate.

### Elisions
#### Remove _Localised key/values
All keys whose name ends with `_Localised`, i.e. the `Name_Localised`
key/values in Items.

#### Personal data in `Docked` events
The following keys+values should be removed from `Docked` event data:

  - `Wanted`
  - `ActiveFine`
  - `CockpitBreach`

#### Personal data in `FSDJump` events
The following keys+values should be removed from `FSDJump` event data:

- `Wanted`
- `BoostUsed`
- `FuelLevel`
- `FuelUsed`
- `JumpDist`
- `HappiestSystem` from within the list of `Factions`.
- `HomeSystem` from within the list of `Factions`.
- `MyReputation` from within the list of `Factions`.
- `SquadronFaction` from within the list of `Factions`.

####  Personal data in `Location` events
The following keys+values should be removed from `Location` event data:

- `Wanted`
- `Latitude`
- `Longitude`
- `HappiestSystem` from within the list of `Factions`.
- `HomeSystem` from within the list of `Factions`.
- `MyReputation` from within the list of `Factions`.
- `SquadronFaction` from within the list of `Factions`.

### Augmentations
#### horizons flag
You SHOULD add this key/value pair, using the value from the `LoadGame` event.

#### odyssey flag
You SHOULD add this key/value pair, using the value from the `LoadGame` event.

#### StarSystem
You MUST add a `StarSystem` key/value pair representing the name of the 
system this event occurred in.  Source this from either `Location`, 
`FSDJump` or `CarrierJump` as appropriate.

#### SystemAddress
You MUST add a `SystemAddress` key/value pair representing the numerical ID 
of the system this event occurred in.  Source this from either `Location`,
`FSDJump` or `CarrierJump` as appropriate.

#### StarPos
You MUST add a `StarPos` array containing the system co-ordinates from the
last `FSDJump`, `CarrierJump`, or `Location` event.
