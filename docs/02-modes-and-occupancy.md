# 02 Modes and occupancy

[← Back to README](../README.md)

## Home modes

| Mode | Set by | Heating | Lights | Security | Notifications |
|---|---|---|---|---|---|
| **Home** | Anyone home and not Night | Evohome schedules | Occupancy and daylight | Disarmed | Normal |
| **Away** | Everyone left (phones + BLE), 10 min confirmation | Economy setback via Evohome; DHW as scheduled | All off except security lighting | Arm prompt (not auto-arm at first) | All to phones |
| **Night** | Bedtime: last bedroom light off after 22:00, or a button | Schedules | Night-path only, low level | Lock check; garage check | P1/P2 only |
| **Holiday** | Manual, with an end date | Holiday mode on both controllers; frost protection; DHW off except a weekly 60 °C cycle | Presence simulation | Armed | Daily summary |
| **Guest** | Manual | Schedules; guest rooms on | Guest dashboard | Unchanged | Hosts only |

Mode changes are logged and shown on the landing view. Manual overrides of the mode always win until the next natural transition.

## Area occupancy

Each area's `binary_sensor.<area>_occupied` combines what's available there:

| Source | Strength | Notes |
|---|---|---|
| Bermuda BLE room (phones, watches) | Who and where; ~30 s latency | Calibration pending (BLE presence repo) |
| Motion (battery Zigbee) | Fast; can't see a still person | Use for "arrived", not for "still here" |
| Media playing, PC active (HASS.Agent) | Strong evidence of presence | Office, lounge, studio |
| Door and lock events | Transitions | Hall and garage |

**Rule:** occupied = any strong source, or motion in the last N minutes (N per area: 2 min in the hall, 15 in the lounge). Vacant only after all sources agree. Bedrooms use a **sleep** state (Night mode + bedroom occupied) that suppresses lighting automations.

## Calendars and exceptions
- **Workday + bank holidays** decide weekday vs weekend behaviour (already integrated).
- **School term** schedule (manual) for morning routines.
- **Bin collection** calendar drives a reminder the evening before (already integrated).
