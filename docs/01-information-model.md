# 01 Information model

[← Back to README](../README.md)

Home Assistant's **floors, areas, labels and zones** are the equivalent of a BMS site/building/floor/zone hierarchy. Getting them right first means every card, automation and report can find things by *where* and *what*, not by entity name.

## Hierarchy

| Level | HA object | Examples |
|---|---|---|
| Site | Home zone | Home (with a radius that suits arrival automations) |
| Other places | Zones | Work, school, station, family (generic; drive arrival and travel logic) |
| Floor | Floor | Ground, First, Second, Outside |
| Area | Area | Lounge, Family room, Kitchen, Dining, Hall, Utility, Play room, Office, Bedrooms, En-suites, Bathroom, Landings, Studio, Plant room, Understairs, Garage, Driveway, Garden |
| Equipment | Device | Boiler, cylinder L, UFH manifold, aircon, purifier, EV charger |
| Point | Entity | Flow temperature, zone setpoint, occupancy |

The full table, with heating zone, presence receiver and typical devices per area, is in [data/area-model.csv](../data/area-model.csv).

## Labels (cross-cutting)
Labels group things across areas, the way BMS points carry tags ([Haystack repo](https://github.com/the-control-cabinet/haystack-semantic-tagging)):

| Label | Used for |
|---|---|
| `life-safety` | Fire/CO and anything that must never be disabled casually |
| `security` | Alarm, lock, garage, cameras |
| `plant` | Boiler, cylinders, valves, pumps, plant sensors |
| `battery` | Every battery device (feeds the battery report) |
| `critical-device` | Things whose loss is alarmed (gateways, coordinators, the HA host) |
| `energy-flex` | Loads that can shift in time (EV, dishwasher, washer, dryer) |
| `night-path` | Lights used for low-level night lighting |
| `guest-safe` | Controls exposed on the guest dashboard |

## Naming convention
`<domain>.<area>_<equipment>_<point>`, all lower case, for example `sensor.plant_room_boiler_flow_temperature`, `light.kitchen_ceiling`, `binary_sensor.utility_leak`. Friendly names drop the area when the card already shows it. Renames follow the [ESPHome fleet runbook](https://github.com/the-control-cabinet/esphome-fleet-standards) so history is kept.

## Helpers (the shared state)
| Helper | Type | Purpose |
|---|---|---|
| `input_select.home_mode` | Select | Home / Away / Night / Holiday / Guest |
| `binary_sensor.<area>_occupied` | Template | Area occupancy (doc 02) |
| `input_boolean.automation_pause_<domain>` | Toggle | Pause a whole domain for maintenance (shown on the landing view) |
| `input_boolean.quiet_hours` | Schedule-driven | Suppresses P3/P4 announcements |
| `schedule.school_days`, `binary_sensor.workday` | Schedule / Workday | Exception schedules (bank holidays) |
| `binary_sensor.cheap_electricity` | Template | True during the tariff's cheap windows (doc 04, energy) |
