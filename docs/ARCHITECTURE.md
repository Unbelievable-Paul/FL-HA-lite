# Architecture

This setup runs Home Assistant Container locally on a MacBook through Docker
Desktop. It is intended to be lightweight, easy to back up, and simple to move
to another host later.

## Runtime

- Host: macOS with Docker Desktop
- Container: `ghcr.io/home-assistant/home-assistant:stable`
- Web UI: `http://127.0.0.1:8123`
- Config volume: `./config:/config`
- Restart policy: `unless-stopped`

## Resource Limits

The Compose file intentionally caps Home Assistant so it does not dominate the
MacBook:

- CPU: 1.5 cores
- Memory limit: 1536 MB
- Memory reservation: 512 MB
- Swap disabled for this container through `memswap_limit: "1536m"`
- Local Docker logging with rotation

## Device Integration

The working dehumidifier integration is the Frigidaire custom integration:

- Control entity: `humidifier.bathroom_dehumid`
- Humidity sensor: `sensor.bathroom_dehumid_humidity`

The automation turns the humidifier entity on when the bathroom humidity is too
high, sets the target humidity to 35%, and turns the unit off when the humidity
falls below the lower threshold.

## Automation Logic

```text
humidity > 55% for 2 minutes -> turn on dehumidifier, set target humidity to 35%
humidity < 45% for 2 minutes -> turn off dehumidifier
```

The gap between 55% and 45% is intentional. It avoids rapid on/off cycling when
humidity hovers near one threshold.

## What Is Not Committed

The real Home Assistant runtime folder contains private state. Do not commit:

- `.storage/`
- `secrets.yaml`
- `home-assistant_v2.db*`
- logs
- backups
- token/cache files

