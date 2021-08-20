# GTFS-capabilities

### Goals

Describes the additional capabilities that a service may be able to provide to serve people with disabilities and those who have mobility devices.

GTFS-capabilities builds upon previously developed extension proposals to provide ways for trip planners and analysts to identify how many people could board a vehicle or book a trip. It is composed of three primary themes:

* Information about services available to a rider from a person, such as a driver or other agency-provided human resource.
* Vehicle information, described by the (further extended) [GTFS-VehicleCategories](https://docs.google.com/document/d/156RiBjI6FnWJvO8_XWX11Q9nLdOiBdS_rilA-oamlv8/edit#heading=h.tosuo6e9e0z7) specification. See also the [GTFS-seats](bit.ly/gtfs-seats) draft extension.
* A focus on describing vehicle amenities related to mobility devices, and how boarding with those devices affects capacity for other riders and devices.

### Requirements

**GTFS-VehiclesCategories**. Optionally, **GTFS-VehicleAllocations** may be used to associate multiple vehicle categories with routes.

### Files extended or added

<table>
  <tr>
   <td><strong>File Name</strong>
   </td>
   <td><strong>State</strong>
   </td>
   <td><strong>Defines</strong>
   </td>
  </tr>
  <tr>
   <td><code>routes.txt</code>
   </td>
   <td>Extended
   </td>
   <td>Adds reference to <code>capability_id.</code>
   </td>
  </tr>
  <tr>
   <td><code>trips.txt</code>
   </td>
   <td>Extended
   </td>
   <td>Adds reference to <code>capability_id</code>, which overrides assignment on routes
   </td>
  </tr>
  <tr>
   <td><code>stop_times.txt</code>
   </td>
   <td>Extended
   </td>
   <td>Adds reference to <code>capability_id</code>, which overrides assignment on routes and trips
   </td>
  </tr>
  <tr>
   <td><code>capabilities .txt</code>
   </td>
   <td>Added
   </td>
   <td>Provides fields related to services available to a rider from a person, such as a driver or other agency-provided human resource.
   </td>
  </tr>
  <tr>
   <td><code>vehicle_ categories.txt</code>
   </td>
   <td>Extended
   </td>
   <td>Adds granularity (modifies current extension) for mobility device capacity.
   </td>
  </tr>
  <tr>
   <td><code>mobility_device_spaces.txt</code>
   </td>
   <td>Added
   </td>
   <td>Allows defining the different spaces available for mobility devices on a vehicle group.
   </td>
  </tr>
  <tr>
   <td><code>space_overlaps .txt</code>
   </td>
   <td>Added
   </td>
   <td>Allows areas that can be used for multiple purposes to be identified and associated with seats they would displace.
   </td>
  </tr>
  <tr>
   <td><code>seats.txt</code>
   </td>
   <td>Extended
   </td>
   <td>Adds ability to identify unique seats that are displaced by the use of a mobility device space.
   </td>
  </tr>
  <tr>
   <td><code>urn_sets.txt</code>
   </td>
   <td>Created
   </td>
   <td>Adds ability for a vehicle category or capability to reference URNs for purposes of describing legal compliance
   </td>
  </tr>
  <tr>
   <td><code>urns.txt</code>
   </td>
   <td>Created
   </td>
   <td>Provides additional information related to Uniform Resource Names (URNs)
   </td>
  </tr>
</table>

### File Definitions

#### routes.txt (file extended)

<table>
  <tr>
   <td><strong>Field Name</strong>
   </td>
   <td><strong>Details</strong>
   </td>
  </tr>
  <tr>
   <td><code>capability_id</code>
   </td>
   <td>(ID, <strong>Optional</strong>) Identifies a set of capabilities in effect for the route.
   </td>
  </tr>
</table>

#### trips.txt (file extended)

<table>
  <tr>
   <td><strong>Field Name</strong>
   </td>
   <td><strong>Details</strong>
   </td>
  </tr>
  <tr>
   <td><code>capability_id</code>
   </td>
   <td>(ID, <strong>Optional</strong>) Identifies a set of capabilities in effect for the trip. This overrides any assignment on routes.
   </td>
  </tr>
</table>

#### stop_times.txt (file extended)

<table>
  <tr>
   <td><strong>Field Name</strong>
   </td>
   <td><strong>Details</strong>
   </td>
  </tr>
  <tr>
   <td><code>capability_id</code>
   </td>
   <td>(ID, <strong>Optional</strong>) Identifies a set of capabilities in effect for the stop_time. This overrides any assignment on routes and trips.
   </td>
  </tr>
</table>

#### capabilities.txt (file added)

<table>
  <tr>
   <td><strong>Field Name</strong>
   </td>
   <td><strong>Details</strong>
   </td>
  </tr>
  <tr>
   <td><code>capability_id</code>
   </td>
   <td>(ID, <strong>Required</strong>) Identifies a set of capabilities. A capability is a service available to a rider from a person, such as a driver or other agency-provided human resource.
   </td>
  </tr>
  <tr>
   <td><code>service_level</code>
   </td>
   <td>(Enum, <strong>Required</strong>) Defines the maximum level of service that may be provided to riders by the driver or other staff when picking up or discharging riders.
<p>
0 or blank - Unknown
<p>
1 - Curb-to-curb (assistance at the vehicle only)
<p>
2 - Door-to-door (assistance provided to passenger between the vehicle and the door of their origin or destination)
<p>
3 - Door-through-door (assistance provided to passenger out of and into the rider’s origin or destination)
<p>
4 - Hand-to-hand (rider is assured continuous attendance)
   </td>
  </tr>
  <tr>
   <td><code>assistance_ training</code>
   </td>
   <td>(Enum, <strong>Optional</strong>) Indicates if the driver or other on-board staff has received required training (as defined by national/local regulations) associated with assisting riders at the defined <code>service_level</code>.
<p>
0 or blank - Unknown
<p>
1 - Driver or other on-vehicle staff has not received required training
<p>
2 - Driver or other on-vehicle staff has received required training
   </td>
  </tr>
  <tr>
   <td><code>compliance_ urn </code>
   </td>
   <td>(URN, <strong>Optional</strong>) URN providing a detailed identifier for a law or regulation the capability is intended to comply with. If a value is present, then <code>capabilities.compliance_urn_set_id</code> must be blank.
   </td>
  </tr>
  <tr>
   <td><code>compliance_ urn_set_id</code>
   </td>
   <td>(ID referencing <code>urn_sets.urn_set_id</code>, <strong>Optional</strong>) URN set referencing one or more URNs providing detailed identifiers for laws or regulations the capability is intended to comply with. If more than one URN is provided in the set, the capability complies with all laws or regulations identified by the URNs. If a value is present, then <code>capabilities.compliance_urn</code> must be blank.
   </td>
  </tr>
</table>

#### vehicle_categories.txt (file extended)

<table>
  <tr>
   <td><strong>Field Name</strong>
   </td>
   <td><strong>Details</strong>
   </td>
  </tr>
  <tr>
   <td><code>has_seat_ \
belts</code>
   </td>
   <td>(Enum, <strong>Optional</strong>) Indicates the presence of seat belts on the vehicle.
<p>
0 or blank - Unknown
<p>
1 - There are no seat belts for passengers on the vehicle
<p>
2 - Seat belts are available for seated passengers
<p>
3 - Seat belts are present and must be worn if they are available for use
   </td>
  </tr>
  <tr>
   <td><code>stretcher_ capacity</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) This number denotes the maximum number of riders in a stretcher that the vehicle can carry.
   </td>
  </tr>
  <tr>
   <td><code>vehicle_ramp</code>
   </td>
   <td>(Enum, <strong>Optional</strong>) Indicates if a ramp for boarding is available in the vehicle.
<p>
0 or empty - Unknown
<p>
1 - Not available
<p>
2 - Available
   </td>
  </tr>
  <tr>
   <td><code>ramp_width</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) Width of ramp, in centimeters.
   </td>
  </tr>
  <tr>
   <td><code>vehicle_lift</code>
   </td>
   <td>(Enum, <strong>Optional</strong>) Indicates if a lift for boarding is available in the vehicle.
<p>
0 or empty - Unknown
<p>
1 - Not available
<p>
2 - Available
   </td>
  </tr>
  <tr>
   <td><code>lift_capacity</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) Mass that the lift is capable of raising and lowering, in kilograms.
   </td>
  </tr>
  <tr>
   <td><code>lift_width</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) Width of lift, in centimeters.
   </td>
  </tr>
  <tr>
   <td><code>lift_length</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) Length of lift, in centimeters.
   </td>
  </tr>
  <tr>
   <td><code>vehicle_min_ aisles_width</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) Narrowest width of rider pathways/corridors in vehicle (doorway included), in centimeters.
   </td>
  </tr>
  <tr>
   <td><code>compliance_ urn_set_id</code>
   </td>
   <td>(ID referencing <code>urn_sets.urn_set_id</code>, <strong>Optional</strong>) URN set referencing one or more URNs providing detailed identifiers for laws or regulations the vehicle category is intended to comply with. If more than one URN is provided in the set, the vehicle category complies with all laws or regulations identified by the URNs.
   </td>
  </tr>
</table>

#### mobility_device_spaces.txt (file added)

<table>
  <tr>
   <td><strong>Field Name</strong>
   </td>
   <td><strong>Details</strong>
   </td>
  </tr>
  <tr>
   <td><code>mobility_ device_ space_id</code>
   </td>
   <td>(ID, <strong>Required</strong>) Identifies a mobility device space. A mobility device space describes a designated space onboard a vehicle where a rider using a device may be located while the vehicle is in motion. 
   </td>
  </tr>
  <tr>
   <td><code>vehicle_ category_id</code>
   </td>
   <td>(ID referencing <code>vehicle_categories.vehicle_category_id</code>, <strong>Required</strong>) Identifies the vehicle category the mobility device space applies to.
   </td>
  </tr>
  <tr>
   <td><code>seat_id</code>
   </td>
   <td>(ID referencing <code>seats.seat_id</code>, <strong>Optional</strong>) Identifies a seat if the mobility space corresponds to a single “seat” that is a space whose primary designation is for a rider who uses a mobility device.
   </td>
  </tr>
  <tr>
   <td><code>securement_ method</code>
   </td>
   <td>(Enum, <strong>Optional</strong>) Indicates the method by which mobility devices are secured.
<p>
0 or blank - Unknown.
<p>
1 - There is no equipment in this space to secure mobility devices.
<p>
2 - There is equipment in this space to secure a mobility device, which can be operated by the passenger.
<p>
3 - There is equipment in this space to secure a mobility device, which must be operated by the driver.
   </td>
  </tr>
  <tr>
   <td><code>mobility_ device_ position</code>
   </td>
   <td>(Enum, <strong>Optional</strong>) Indicates the position within the vehicle where the mobility_space is located.
<p>
0 or blank - Unknown
<p>
1 - The mobility device space is near the front door.
<p>
2 - The mobility device space is near the rear door.
<p>
3 - The mobility device space is near the rear of the vehicle, accessed by a separate door or lift.
   </td>
  </tr>
  <tr>
   <td><code>useable_width</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) The number of centimeters of useable clearance along the width of the vehicle for this mobility device space.
   </td>
  </tr>
  <tr>
   <td><code>useable_length</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) The number of centimeters of useable clearance along the length of the vehicle for this mobility device space.
   </td>
  </tr>
  <tr>
   <td><code>seating_capacity_effect</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) The number of seats which cannot be occupied by a rider while this mobility device space is in use.
   </td>
  </tr>
  <tr>
   <td><code>standing_capacity_effect</code>
   </td>
   <td>(Non-negative integer, <strong>Optional</strong>) The approximate number of standing riders who cannot occupy the space while this mobility device space is in use.
   </td>
  </tr>
  <tr>
   <td>storage_allowed
   </td>
   <td>(Enum, <strong>Optional</strong>) Indicates the accommodations available for storing of larger items belonging to riders.
<p>
0 or blank - Unknown
<p>
1 - There is no additional storage beyond the rider’s immediate seat or mobility device space
<p>
2 - There is a storage area separate from the rider’s seat or mobility device space
   </td>
  </tr>
</table>

#### seat_displacements.txt (optional file, added)

<table>
  <tr>
   <td><strong>Field Name</strong>
   </td>
   <td><strong>Details</strong>
   </td>
  </tr>
  <tr>
   <td><code>mobility_ device_ space_id</code>
   </td>
   <td>(ID referencing <code>mobility_device_spaces.mobility_device_space_id</code>, <strong>Required</strong>) Identifies a mobility device space that displaces one or more seats. When a mobility device space displaces more than one seat, then multiple entries in <code>seat_displacements.txt</code> share the same <code>mobility_device_space_id</code>.
   </td>
  </tr>
  <tr>
   <td><code>seat_id</code>
   </td>
   <td>(ID referencing <code>seats.seat_id</code>, <strong>Required</strong>) Identifies a seat that would be displaced to make room for a by a seating area of a vehicle. When a seat may be displaced by more than one mobility device space (due to there being multiple possible vehicle configurations), then multiple entries in <code>seat_displacements.txt</code> share the same <code>seat_id</code>.
   </td>
  </tr>
</table>

#### seat.txt (file extended)

<table>
  <tr>
   <td><strong>Field Name</strong>
   </td>
   <td><strong>Details</strong>
   </td>
  </tr>
  <tr>
   <td><code>mobility_ device_space_ id</code>
   </td>
   <td>(ID referencing <code>mobility_device_spaces.mobility_device_space_id</code>, <strong>Optional</strong>) Provides more detailed information about a “seat” that is a space whose primary designation is for a rider who uses a mobility device.
   </td>
  </tr>
  <tr>
   <td><code>seat_ displacement_ id</code>
   </td>
   <td>(ID referencing <code>seat_displacements.seat_displacement_id</code>, <strong>Required</strong>) Identifies a set of one or more mobility device spaces that, if used, would displace the seat.
   </td>
  </tr>
</table>
