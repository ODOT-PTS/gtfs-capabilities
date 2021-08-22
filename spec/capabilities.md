# GTFS-capabilities

## Goals

Describes the additional capabilities that a service may be able to provide to serve people with disabilities and those who have mobility devices.

GTFS-capabilities builds upon previously developed extension proposals to provide ways for trip planners and analysts to identify how many people could board a vehicle or book a trip. It is composed of three primary themes:

* Information about services available to a rider from a person, such as a driver or other agency-provided human resource.
* Vehicle information, described by the (further extended) [GTFS-VehicleCategories](https://docs.google.com/document/d/156RiBjI6FnWJvO8_XWX11Q9nLdOiBdS_rilA-oamlv8/edit#heading=h.tosuo6e9e0z7) specification. See also the [GTFS-seats](bit.ly/gtfs-seats) draft extension.
* A focus on describing vehicle amenities related to mobility devices, and how boarding with those devices affects capacity for other riders and devices.

## Requirements

**GTFS-VehiclesCategories**. Optionally, **GTFS-VehicleAllocations** may be used to associate multiple vehicle categories with routes.

## Files extended or added

|File Name|State|Defines|
| --- | --- | --- |
|`routes.txt`|Extended|Adds reference to `capability_id`.|
|`trips.txt`|Extended|Adds reference to `capability_id`, which overrides assignment on routes|
|`stop_times.txt`|Extended|Adds reference to `capability_id`, which overrides assignment on routes and trips|
|`capabilities.txt`|Added|Provides fields related to services available to a rider from a person, such as a driver or other agency-provided human resource.|
|`vehicle_categories.txt`|Extended|Adds granularity (modifies current extension) for mobility device capacity.|
|`mobility_device_spaces.txt`|Added|Allows defining the different spaces available for mobility devices on a vehicle group.|
|`space_overlaps.txt`|Added|Allows areas that can be used for multiple purposes to be identified and associated with seats they would displace.|
|`urn_sets.txt`|Created|Adds ability for a vehicle category or capability to reference URNs for purposes of describing legal compliance|
|`urns.txt`|Created|Provides additional information related to Uniform Resource Names (URNs)|

## File Definitions

### routes.txt (file extended)

|Field Name|Details|
| --- | --- |
|`capability_id`|(ID, **Optional**) Identifies a set of capabilities in effect for the route.|

### trips.txt (file extended)

|Field Name|Details|
| --- | --- |
|`capability_id`|(ID, **Optional**) Identifies a set of capabilities in effect for the trip. This overrides any assignment on routes.|

### stop_times.txt (file extended)

|Field Name|Details|
| --- | --- |
|`capability_id`|(ID, **Optional**) Identifies a set of capabilities in effect for the trip. This overrides any assignment on routes and trips.|

### capabilities.txt (file added)

|Field Name|Details|
| --- | --- |
|`capability_id`|(ID, **Required**) Identifies a set of capabilities. A capability is a service available to a rider from a person, such as a driver or other agency-provided human resource.|
|`service_level`|(Enum, **Required**) Defines the maximum level of service that may be provided to riders by the driver or other staff when picking up or discharging riders.<br><br>`0` or blank - Unknown<br>`1` - Curb-to-curb (assistance at the vehicle only)<br>`2` - Door-to-door (assistance provided to passenger between the vehicle and the door of their origin or destination)<br>`3` - Door-through-door (assistance provided to passenger out of and into the rider’s origin or destination)<br>`4` - Hand-to-hand (rider is assured continuous attendance)|
|`assistance_training`|(Enum, **Optional**) Indicates if the driver or other on-board staff has received required training (as defined by national/local regulations) associated with assisting riders at the defined service_level.<br><br>`0` or blank - Unknown<br>`1` - Driver or other on-vehicle staff has not received required training<br>`2` - Driver or other on-vehicle staff has received required training|
|`compliance_urn`|(URN, **Optional**) URN providing a detailed identifier for a law or regulation the capability is intended to comply with. If a value is present, then `capabilities.compliance_urn_set_id` must be blank.|
|`compliance_urn_set_id`|(ID referencing `urn_sets.urn_set_id`, **Optional**) URN set referencing one or more URNs providing detailed identifiers for laws or regulations the capability is intended to comply with. If more than one URN is provided in the set, the capability complies with all laws or regulations identified by the URNs. If a value is present, then capabilities.compliance_urn must be blank.|

### vehicle_categories.txt (file extended)

|Field Name|Details|
| --- | --- |
|`has_seat_belts`|(Enum, **Optional**) Indicates the presence of seat belts on the vehicle.<br><br>`0` or blank - Unknown<br>`1` - There are no seat belts for passengers on the vehicle<br>`2` - Seat belts are available for seated passengers<br>`3` - Seat belts are present and must be worn if they are available for use|
|`stretcher_capacity`|(Non-negative integer, **Optional**) This number denotes the maximum number of riders in a stretcher that the vehicle can carry.|
|`vehicle_ramp`|(Enum, **Optional**) Indicates if a ramp for boarding is available in the vehicle.<br><br>`0` or empty - Unknown<br>`1` - Not available<br>`2` - Available|
|`ramp_width`|(Non-negative integer, **Optional**) Width of ramp, in centimeters.|
|`vehicle_lift`|(Enum, **Optional**) Indicates if a lift for boarding is available in the vehicle.<br><br>`0` or empty - Unknown<br>`1` - Not available<br>`2` - Available|
|`lift_capacity`|(Non-negative integer, **Optional**) Mass that the lift is capable of raising and lowering, in kilograms.|
|`lift_width`|(Non-negative integer, **Optional**) Width of lift, in centimeters.|
|`lift_length`|(Non-negative integer, **Optional**) Length of lift, in centimeters.|
|`vehicle_min_aisles_width`|(Non-negative integer, **Optional**) Narrowest width of rider pathways/corridors in vehicle (doorway included), in centimeters.|
|`compliance_urn_set_id`|(ID referencing `urn_sets.urn_set_id`, **Optional**) URN set referencing one or more URNs providing detailed identifiers for laws or regulations the vehicle category is intended to comply with. If more than one URN is provided in the set, the vehicle category complies with all laws or regulations identified by the URNs.|

### mobility_device_spaces.txt (file added)

|Field Name|Details|
| --- | --- |
|`mobility_device_space_id`|(ID, **Required**) Identifies a mobility device space. A mobility device space describes a designated space onboard a vehicle where a rider using a device may be located while the vehicle is in motion.|
|`vehicle_category_id`|(ID referencing `vehicle_categories.vehicle_category_id`, **Required**) Identifies the vehicle category the mobility device space applies to.|
|`seat_id`|(ID referencing `seats.seat_id`, **Optional**) Identifies a seat if the mobility space corresponds to a single “seat” that is a space whose primary designation is for a rider who uses a mobility device.|
|`securement_method`|(Enum, **Optional**) Indicates the method by which mobility devices are secured.<br><br>`0` or blank - Unknown.<br>`1` - There is no equipment in this space to secure mobility devices.<br>`2` - There is equipment in this space to secure a mobility device, which can be operated by the passenger.<br>`3` - There is equipment in this space to secure a mobility device, which must be operated by the driver.|
|`mobility_device_position`|(Enum, **Optional**) Indicates the position within the vehicle where the mobility_space is located.<br><br>`0` or blank - Unknown<br>`1` - The mobility device space is near the front door.<br>`2` - The mobility device space is near the rear door.<br>`3` - The mobility device space is near the rear of the vehicle, accessed by a separate door or lift.|
|`useable_width`|(Non-negative integer, **Optional**) The number of centimeters of useable clearance along the width of the vehicle for this mobility device space.|
|`useable_length`|(Non-negative integer, **Optional**) The number of centimeters of useable clearance along the length of the vehicle for this mobility device space.|
|`seating_capacity_effect`|(Non-negative integer, **Optional**) The number of seats which cannot be occupied by a rider while this mobility device space is in use.|
|`standing_capacity_effect`|(Non-negative integer, **Optional**) The approximate number of standing riders who cannot occupy the space while this mobility device space is in use.|
|`storage_allowed`|(Enum, **Optional**) Indicates the accommodations available for storing of larger items belonging to riders.<br><br>`0` or blank - Unknown<br>`1` - There is no additional storage beyond the rider’s immediate seat or mobility device space<br>`2` - There is a storage area separate from the rider’s seat or mobility device space|

### seat_displacements.txt (optional file, added)

|Field Name|Details|
| --- | --- |
|`mobility_device_space_id`|(ID referencing `mobility_device_spaces.mobility_device_space_id`, **Required**) Identifies a mobility device space that displaces one or more seats. When a mobility device space displaces more than one seat, then multiple entries in seat_displacements.txt share the same mobility_device_space_id.|
|`seat_id`|(ID referencing `seats.seat_id`, **Required**) Identifies a seat that would be displaced to make room for a by a seating area of a vehicle. When a seat may be displaced by more than one mobility device space (due to there being multiple possible vehicle configurations), then multiple entries in `seat_displacements.txt` share the same seat_id.|
