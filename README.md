# IKEA MYGGBETT — door/window contact blueprint (Home Assistant)

Home Assistant automation blueprint for the IKEA **MYGGBETT** door/window contact sensor
(or any contact `binary_sensor`). Bind **open** and **close** independently to lights and/or
any actions (notifications, scenes, scripts), with optional debounce, an open-only condition,
and an **open-too-long** reminder.

The sensor shows up in HA as a `binary_sensor` (device_class `door` / `window` / `opening` /
`garage_door`): **`on` = open, `off` = closed.**

## Install

[![Import blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fgithub.com%2Fk0nsta%2Fha-myggbett-sensor-blueprint%2Fblob%2Fmaster%2Fblueprints%2Fmyggbett_contact.yaml)

Or **Settings → Automations & Scenes → Blueprints → Import Blueprint** and paste:

```
https://github.com/k0nsta/ha-myggbett-sensor-blueprint/blob/master/blueprints/myggbett_contact.yaml
```

## Inputs

| Section | Input | What it does |
|---|---|---|
| 1 · Sensor | Door/window sensor | The contact `binary_sensor` to watch |
| 2 · When OPENED | Lights to turn on | Optional lights switched on when opened |
| | Actions to run | Any actions (notify, scene, script…) on open |
| 3 · When CLOSED | Lights to turn off | Optional lights switched off when closed |
| | Actions to run | Any actions on close |
| 4 · Behaviour | Open / Close debounce | Seconds the state must hold before the branch runs |
| | Only run OPEN actions when… | Condition(s) gating the OPEN branch (close always runs) |
| 5 · Reminder | Enable / after / repeat / actions | Re-fire actions while the door stays open |

## Notes

- **Notifications** use free-form *action* fields — drop in a `notify.mobile_app_*` call,
  `persistent_notification.create`, etc. Nothing is hardcoded to a device.
- `mode: restart` — closing the door cancels any pending reminder loop immediately.
- The OPEN condition gates only the open branch (e.g. "only when dark"); the close branch
  always runs so lights reliably turn off.

## License

MIT — see [LICENSE](LICENSE).
