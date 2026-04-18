# modpack

Fabric modpack for Minecraft `26.2-snapshot-3`, managed with [packwiz](https://packwiz.infra.link/).

## Layout

```
pack.toml       # packwiz pack manifest
index.toml      # packwiz file index
mods/           # mod metadata (.pw.toml) — added via `packwiz`
config/         # server/client config overrides
```

## Local workflow

Add a mod from Modrinth or CurseForge:

```sh
packwiz mr add <slug>
packwiz cf add <slug>
packwiz refresh
```

Commit and push — the server pulls on restart.

## Server (itzg)

Point the container at the raw `pack.toml`:

```yaml
services:
  mc:
    image: itzg/minecraft-server
    environment:
      EULA: "TRUE"
      TYPE: FABRIC
      VERSION: 26.2-snapshot-3
      PACKWIZ_URL: https://raw.githubusercontent.com/<user>/<repo>/main/pack.toml
    ports:
      - "25565:25565"
    volumes:
      - ./data:/data
```
