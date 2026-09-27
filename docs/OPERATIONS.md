# Operations

## Start

```bash
cd homeassistant
docker compose up -d
```

Open:

```text
http://127.0.0.1:8123
```

## Stop

```bash
cd homeassistant
docker compose down
```

## Restart

```bash
cd homeassistant
docker compose restart
```

On this Mac, Docker's bundled binary can also be used if `docker` is not on
the shell PATH:

```bash
/Applications/Docker.app/Contents/Resources/bin/docker compose restart
```

## Update Home Assistant Image

```bash
cd homeassistant
docker compose pull
docker compose up -d
```

## Backup

Use Home Assistant's built-in backup feature for real operational backups.
For a light config archive, exclude runtime state and secrets:

```bash
tar \
  --exclude='./home-assistant_v2.db*' \
  --exclude='./home-assistant.log*' \
  --exclude='./*.log' \
  --exclude='./deps' \
  --exclude='./tts' \
  -czf homeassistant-config-backup.tar.gz \
  -C homeassistant/config .
```

Store backups somewhere outside the live config folder.

## Restore

1. Install Docker Desktop.
2. Clone this repo.
3. Restore the private Home Assistant config backup into `homeassistant/config`.
4. Start Home Assistant with Docker Compose.
5. Confirm the Frigidaire integration and entities still match:
   - `humidifier.bathroom_dehumid`
   - `sensor.bathroom_dehumid_humidity`

