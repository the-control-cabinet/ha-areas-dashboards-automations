# 04 Automation catalogue

[← Back to README](../README.md)

**58 automations** across 9 domains: 11 live today, the rest proposed or planned. Machine-readable version: [data/automation-catalogue.csv](../data/automation-catalogue.csv). Every proposed automation starts in shadow mode (doc 06).

## Life safety

| ID | Automation | Trigger → action | Priority | Safety / notes | Status |
|---|---|---|---|---|---|
| LS-01 | Fire / CO / fault alert | Aico interface fire/CO/fault on or cleared → Critical push to all phones; persistent notification; resolved message | P1 | Local only; no mode conditions | Live |
| LS-02 | Fire/CO interface offline | Either Shelly unavailable 5 min → P2 alert; back-online message | P2 |  | Live |
| LS-03 | Fire mode response | Fire on → All lights 100 %; blinds open; aircon/purifiers/fans off (don't spread smoke); speaker announcement; pixel display | P1 | Never unlocks doors automatically: an actionable 'unlock front door' button is sent instead | Proposed |
| LS-04 | CO response | CO on → Announcement 'CO alarm: open windows |  leave |  call the gas emergency number'; aircon/purifiers off | P1 |
| LS-05 | Quarterly life-safety test reminder | 1st day of each quarter → Reminder with the test checklist (sound-all via the interface) | P3 |  | Proposed |

## Security

| ID | Automation | Trigger → action | Priority | Safety / notes | Status |
|---|---|---|---|---|---|
| SE-01 | Arm prompt on Away | Home mode → Away · if alarm disarmed → Actionable push 'Arm the alarm?' | P3 | Auto-arm only after a month of reliable presence | Proposed |
| SE-02 | Night lock and garage check | Home mode → Night · if door unlocked or garage open → Push with actions (lock / close) | P2 | Garage close only with a confirmation | Proposed |
| SE-03 | Garage left open | Garage open 15 min · if nobody in garage area → P3 push; P2 after dark | P2 |  | Proposed |
| SE-04 | Doorbell press | Doorbell event → Snapshot to phones; pause media in occupied rooms; announce | P3 |  | Proposed |
| SE-05 | Access control → alarm interlock | (details withheld) |  |  | Live |
| SE-06 | Wireless-button entrance control | (details withheld) |  |  | Live |

## Heating and cooling

| ID | Automation | Trigger → action | Priority | Safety / notes | Status |
|---|---|---|---|---|---|
| HC-01 | Heating/cooling interlock | Aircon cooling while that room's zone has heat demand (or vice versa) → Inhibit the later request; notify once | P3 | FDD F11; dead band ≥ 2 °C | Proposed |
| HC-02 | Away setback | Home mode → Away (confirmed 30 min) → Evohome economy/away mode; restore on return | P4 | Frost protection always kept | Proposed |
| HC-03 | Holiday mode | Home mode → Holiday → Holiday mode on both controllers; DHW off except LG-01 | P4 |  | Proposed |
| HC-04 | Stuck zone / 5 °C override alert | Any zone setpoint ≤ 5.5 °C or the sun-thermometer override · if mode not Holiday → P2 alert with zone name | P2 | From the 5 °C fault case study | Planned |
| HC-05 | Hot water disabled by the timer | DHW calling AND timer output off → P2 alert: return the TS715Si to permanent ON | P2 | FDD F16 | Proposed |
| HC-06 | Cylinder stat or cut-out not passing | Cylinder relay on AND stat-passing off for 10 min · if hot water enabled → P2 alert | P2 | FDD F15; reset the cut-out only after finding why | Proposed |
| HC-07 | Aircon sleep forces cool | Sleep selected → Force Cool mode | P4 | Data-point constraint | Live |
| HC-08 | Room IAQ response | CO2 or PM2.5 above band in an occupied room · if purifier present → Purifier to auto/high; notify if persistent | P3 |  | Proposed |
| HC-09 | Humidity control | Room RH < 35 % (heating season) · if occupied → Humidifier on; off at 45 % | P4 |  | Proposed |
| HC-10 | Window open (when contact sensors are fitted) | Window open 2 min · if zone heating → Zone setback until closed | P4 | Evohome window detection already on | Planned |
| LG-01 | Weekly 60 °C DHW cycle | Weekly (or Holiday mode) → Raise DHW setpoint to 60 °C; confirm the hot-outlet NTC reached 60 °C; alert if not | P3 | Legionella control; after the cylinder NTCs are fitted | Planned |

## Energy

| ID | Automation | Trigger → action | Priority | Safety / notes | Status |
|---|---|---|---|---|---|
| EN-01 | Cheap-window reminder | Tariff cheap window starts · if dishwasher/washer loaded flag → Notify 'cheap window now' | P4 |  | Proposed |
| EN-02 | Flexible loads in cheap windows | Cheap window AND low carbon intensity · if energy-flex device ready → Start the load (smart plug / appliance API) | P4 | Never for tumble dryer unattended at night | Proposed |
| EN-03 | EV plugged-in check | Evening AND car not plugged in · if car home; battery < 50 % → Reminder to plug in | P3 |  | Proposed |
| EN-04 | Peak demand warning | Import above threshold for 5 min → Notify biggest loads | P3 |  | Proposed |
| EN-05 | Carbon-aware heating trim | High carbon intensity · if mode Home → Shadow only: log what a 0.5 °C setback would save | P4 | Comfort always wins | Proposed |

## Water

| ID | Automation | Trigger → action | Priority | Safety / notes | Status |
|---|---|---|---|---|---|
| WA-01 | Steady low flow (drift or leak) | Low steady flow 10 min → Push alert | P2 |  | Live |
| WA-02 | Shower sub-metering | Shower start + humidity confirmation → Usage per shower | P4 |  | Live |
| WA-03 | Washing machine sub-metering | Cycle start → Usage per cycle | P4 |  | Live |
| WA-04 | Leak sensor wet | Any leak sensor wet → P1 push + announcement; pixel display; stopcock reminder | P1 | Auto shut-off only once a mains shut-off valve is fitted | Proposed |
| WA-05 | Tundish discharge | Tundish plate wet → P2 alert; correlate with cylinder pressure | P2 | Unvented cylinder safety discharge | Planned |
| WA-06 | Unexpected flow while Away | Flow > 0 with Home mode Away → P2 alert | P2 |  | Proposed |
| WA-07 | Frost risk on outside pipes | Outdoor < 0 °C forecast → Reminder to protect outside taps | P3 |  | Proposed |

## Lighting and shading

| ID | Automation | Trigger → action | Priority | Safety / notes | Status |
|---|---|---|---|---|---|
| LI-01 | Occupancy lighting | Area becomes occupied · if lux below threshold; not sleep → Lights to the area's scene; off after vacancy delay | P4 | Manual change suspends it until next mode change | Proposed |
| LI-02 | Night path | Motion in hall/landing · if Night mode → Night-path lights at 5 % | P4 |  | Proposed |
| LI-03 | Sunset and sunrise | Sun elevation · if mode Home → Outside lights on/off; blinds by schedule | P4 |  | Proposed |
| LI-04 | Solar-gain shading | Sun on facade AND room > setpoint + 1 °C · if cooling season; room unoccupied or allowed → Blinds to shade position | P4 | Coordinated with HC-01 | Proposed |
| LI-05 | Presence simulation | Holiday mode · if after dusk → Randomised lights in lived-in rooms | P4 |  | Proposed |
| LI-06 | Media scene | TV playing in lounge after dusk → Lights dim; blinds close | P4 |  | Proposed |
| LI-07 | VPin table-aware lighting | Table launched (MQTT) → Room lights to the table's colours | P4 |  | Planned |

## Appliances

| ID | Automation | Trigger → action | Priority | Safety / notes | Status |
|---|---|---|---|---|---|
| AP-01 | Washer / dryer done | Vibration stops 5 min · if cycle was running → Notify the responsible person | P3 |  | Proposed |
| AP-02 | 3D print finished or failed | Printer state change → Notify with a snapshot | P3 |  | Proposed |
| AP-03 | Mower rain hold | Rain forecast or detected → Mower to dock | P4 |  | Proposed |
| AP-04 | Dishwasher sub-metering | Plug power profile → Energy and water per cycle | P4 |  | Planned |

## Information

| ID | Automation | Trigger → action | Priority | Safety / notes | Status |
|---|---|---|---|---|---|
| IN-01 | Bin night reminder | Evening before collection → Notify which bins | P4 |  | Proposed |
| IN-02 | Rain warnings | Several weather sources → Consolidated rain warning | P4 |  | Live |
| IN-03 | Washing-line AI check | Rain coming AND washing out (AI camera check) → Push 'bring the washing in' | P3 |  | Live |
| IN-04 | Commute travel times | Weekday morning · if workday → Travel-time notifications | P4 |  | Live |
| IN-05 | Aurora alert | AuroraWatch amber/red · if after dark; clear sky → Notify | P4 |  | Proposed |
| IN-06 | Met Office warning and flood gauges | Warning issued or gauge above threshold → Notify with severity | P3 |  | Proposed |
| IN-07 | Train disruption | Delay on the usual departure · if workday → Notify | P3 |  | Proposed |

## System health

| ID | Automation | Trigger → action | Priority | Safety / notes | Status |
|---|---|---|---|---|---|
| SH-01 | Device offline | critical-device unavailable 10 min → P3 alert (P2 for gateways and the coordinator) | P2 |  | Proposed |
| SH-02 | Battery low | Any battery-labelled device < 20 % → Weekly list; P3 for locks and leak sensors | P3 |  | Proposed |
| SH-03 | ESPHome reset watch | Uptime drops or reset reason = watchdog → Log and count per board; weekly summary | P4 | Feeds the ESPHome watchdog investigation | Proposed |
| SH-04 | Backup verification | Nightly backup missing or older than 26 h → P3 alert | P3 |  | Proposed |
| SH-05 | HA host resources | Disk > 80 % or CPU high 30 min → P3 alert | P3 |  | Proposed |
| SH-06 | Paused automations reminder | Any automation_pause toggle on 24 h → P3 reminder | P3 | Exceptions stay visible | Proposed |
