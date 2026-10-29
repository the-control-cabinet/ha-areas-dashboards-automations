# Home Assistant Areas, Dashboards and Automations: the Occupant Layer (Design Stage)

**Design proposals for turning ~110 Home Assistant integrations into a coherent building: an area and zone model, home modes and room occupancy, a BMS-style dashboard hierarchy built to high-performance HMI principles, and a catalogue of around 60 automations across life safety, security, heating and cooling, energy, water, lighting and shading, appliances, information and system health, each with triggers, conditions, safety rules and a status.**

[![YouTube](https://img.shields.io/badge/YouTube-The%20Control%20Cabinet-red?logo=youtube)](https://www.youtube.com/channel/UC5Cupmz7vlfcodpCX7k8iuQ)
[![Portfolio](https://img.shields.io/badge/Portfolio-the--control--cabinet-24292f?logo=github)](https://github.com/the-control-cabinet/the-control-cabinet)
![Domain](https://img.shields.io/badge/BMS-operator%20interface%20%26%20automation-blue)
![Status](https://img.shields.io/badge/Status-Design%20stage-yellow)

> **The short version:**
> - **The gap:** the integrations are in (see the [integration schedule](https://github.com/the-control-cabinet/home-assistant-integration-schedule)), but rooms only have devices assigned, there are a handful of dashboards, and about a dozen automations.
> - **The model:** floors → areas → equipment, with **home modes** (Home, Away, Night, Holiday, Guest) and per-area **occupancy** (Bermuda BLE, phones, motion) as the backbone every automation reads.
> - **The interface:** one landing view, then floors, systems (heating, energy, water, security, plant room) and system health. Grey when normal, colour only when abnormal.
> - **The behaviour:** a numbered automation catalogue ([data](data/automation-catalogue.csv)) built **notify-only first**, then promoted to act, with priorities from the [alarm and trend strategy](https://github.com/the-control-cabinet/alarm-and-trend-strategy).
> - **The split:** Home Assistant runs the occupant-facing automations; Node-RED runs plant supervision ([supervisory layer](https://github.com/the-control-cabinet/ha-node-red-supervisory-layer)).

**Portfolio position:** Management/Automation levels · operator interface and control strategy. Uses: [integration schedule](https://github.com/the-control-cabinet/home-assistant-integration-schedule) · [BLE presence](https://github.com/the-control-cabinet/esp32-ble-presence-network) · [alarm strategy](https://github.com/the-control-cabinet/alarm-and-trend-strategy) · [plant graphics](https://github.com/the-control-cabinet/plant-room-graphics-hmi) · [lighting and shading](https://github.com/the-control-cabinet/lighting-and-shading-control) · [demand-side energy](https://github.com/the-control-cabinet/demand-side-energy-management)

---

## Documents

| Doc | Contents |
|---|---|
| [01 Information model](docs/01-information-model.md) | Floors, areas, zones, labels, naming, helpers |
| [02 Modes and occupancy](docs/02-modes-and-occupancy.md) | Home modes, area occupancy, sleep, guests, calendars |
| [03 Dashboards](docs/03-dashboards.md) | Hierarchy, view-by-view design, card toolkit, HMI rules, wall panel vs phone |
| [04 Automation catalogue](docs/04-automation-catalogue.md) | ~60 automations by domain with triggers, conditions, safety and status |
| [05 Notifications](docs/05-notifications.md) | Priorities, channels, quiet hours, acknowledgement |
| [06 Build and change control](docs/06-build-and-change-control.md) | Packages vs UI, blueprints, testing, shadow mode, naming, backups |
| [07 Roadmap](docs/07-roadmap.md) | Phased delivery |

Data: [area model](data/area-model.csv) · [dashboard map](data/dashboard-map.csv) · [automation catalogue](data/automation-catalogue.csv)

## Design principles
1. **Safety first, comfort second, convenience third:** life-safety automations never depend on the cloud, presence or a mode.
2. **One source of truth per decision:** modes and occupancy are computed once (helpers/templates) and read everywhere.
3. **Fail safe:** if an input is unavailable, the automation does nothing or reverts to the default, and says so.
4. **Notify, then act:** every new automation starts notify-only; it's promoted after a week without false triggers.
5. **Manual always wins:** a manual change suspends the automation for that device until the next mode change.
6. **Exceptions are visible:** anything disabled, overridden or offline appears on the landing view.

## Skills demonstrated (as designed)
| Skill | Evidence |
|---|---|
| Operator interface design | Dashboard hierarchy to high-performance HMI principles |
| Control strategy | Modes, occupancy and interlocks as a written strategy |
| Alarm management | Priorities, routing, suppression and acknowledgement |
| Change control | Shadow mode, promotion criteria, naming and review |
| Systems integration | ~110 integrations mapped into one model |

📺 [The Control Cabinet on YouTube](https://www.youtube.com/channel/UC5Cupmz7vlfcodpCX7k8iuQ)

*Designed and documented by James · part of [The Control Cabinet BMS portfolio](https://github.com/the-control-cabinet/the-control-cabinet). MIT Licence.*
