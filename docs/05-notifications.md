# 05 Notifications

[← Back to README](../README.md)

Priorities follow the [alarm and trend strategy](https://github.com/the-control-cabinet/alarm-and-trend-strategy):

| Priority | Examples | Channels | Quiet hours | Acknowledge |
|---|---|---|---|---|
| **P1 Life safety** | Fire, CO, major leak | Critical push to all phones (bypasses silent), speaker announcement, pixel display, all lights on | **Ignored** | Required; repeats every 2 min |
| **P2 Urgent** | Intruder alarm, plant fault, cylinder cut-out tripped, garage open at night | Push to all adults; persistent notification | Ignored | Required |
| **P3 Action today** | Low battery, device offline, filter due, washing done | Push to the responsible person; persistent | Held until morning | Optional |
| **P4 Information** | Bin day, aurora, rain coming, train delays | Pixel display or dashboard; push only if subscribed | Held | No |

**Rules:** one message per event (no repeats unless P1/P2); every message says what, where and what to do; cleared conditions send a short "resolved"; a weekly digest lists nuisance alarms for review.
