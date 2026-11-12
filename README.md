# Unraid templates by Tuxxler

Unraid Community Applications (CA) templates for apps made by Tuxxler.

| App | Template | Image | What it does |
|---|---|---|---|
| **NASlab-Agent** | [`templates/nzblab-agent.xml`](templates/nzblab-agent.xml) | `ghcr.io/tuxxler/nzblab-agent:latest` (amd64, arm64) | Read-only monitoring agent for the [NASlab](https://github.com/Tuxxler/nzblab-agent#readme) Android app: temperatures, CPU, GPU, RAM, network, disk spin-ups, file index. Never changes anything on the server. |

## Install

**From Community Applications (once accepted):** Apps › search **NASlab-Agent** › **Install** › **Apply**.

**Without CA (works today):**

1. Unraid › **Docker** › scroll down to **Template repositories** › add the line
   `https://github.com/Tuxxler/unraid-templates` › **Save**.
2. **Add Container** › *Template*: pick **NASlab-Agent**. Check the paths (remove *Cache pool* if you have no pool named `cache`).
   Keep *Data (/config)* → `/mnt/user/appdata/nzblab-agent` (read/write): the agent stores its token and history there.
3. **Apply.** Open the container **Logs**: the line `NZBLab-Agent Token: …` appears once.
4. In the app: *Settings › Server connections › NASlab-Agent* › address `http://<unraid-ip>:8099` › paste the token › **Check**.

All host paths are mounted **read-only**; only `/config` is writable. After start the agent drops root and runs as `PUID`/`PGID` (99/100).
Do not expose port 8099 to the internet; use a VPN (WireGuard, Tailscale) away from home.

## Licenses, stated plainly

- **This repository** (templates, profile, icon): [MIT](LICENSE).
- **The agent** (`ghcr.io/tuxxler/nzblab-agent`, source at <https://github.com/Tuxxler/nzblab-agent>): free and open source, **GNU AGPL-3.0-only** (OSI-approved). You may use it (also commercially), read and modify it; if you distribute a modified version or offer it as a network service, you must publish your changes under the same license.
- **The NASlab app**: separate, closed-source Android app on Google Play (closed test now, public launch planned).

## Support

Forum thread: <<FORUM-LINK>> · Agent code and issues: <https://github.com/Tuxxler/nzblab-agent>
