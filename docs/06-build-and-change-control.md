# 06 Build and change control

[← Back to README](../README.md)

| Topic | Decision |
|---|---|
| Where automations live | **YAML packages** by domain (`packages/life_safety.yaml`, `packages/energy.yaml` …) in git; UI only for drafts, then exported |
| Reuse | Blueprints for repeated patterns (occupancy lighting, battery low, device offline, leak response) |
| HA vs Node-RED | HA for occupant-facing automations; Node-RED for plant supervision and optimum start/stop |
| IDs | Every automation carries its catalogue ID (e.g. `LS-01`) in its alias and description |
| Testing | Trace review after each run; **shadow mode** (notify "would have done X") for at least a week before acting |
| Promotion | Notify-only → acting after 7 days with no false triggers; logged in the catalogue's status column |
| Safety | P1 automations: no cloud dependency, no mode conditions, tested quarterly |
| Change | One domain at a time; backup before; changelog entry after |
| Naming and renames | As doc 01; renames via the fleet runbook so history survives |
| Backups | Before every package change; monthly verified restore; annual DR test |
