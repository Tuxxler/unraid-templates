# Unraid templates by Tuxxler

Unraid Community Applications (CA) templates for apps made by Tuxxler.

| App | Template | Image | What it does |
|---|---|---|---|
| **NASlab-Agent** | [`templates/nzblab-agent.xml`](templates/nzblab-agent.xml) | `ghcr.io/tuxxler/nzblab-agent:latest` (amd64, arm64) | Read-only monitoring agent for the [NASlab](https://github.com/Tuxxler/nzblab-agent#readme) Android app: temperatures, CPU, GPU, RAM, network, disk spin-ups, file index. Never changes anything on the server. |

## Install

**From Community Applications:** Apps › search **NASlab-Agent** › **Install** › **Apply**.

**Without CA (alternative):**

1. Unraid › **Docker** › scroll down to **Template repositories** › add the line
   `https://github.com/Tuxxler/unraid-templates` › **Save**.
2. **Add Container** › *Template*: pick **NASlab-Agent**. Check the paths (remove *Cache pool* if you have no pool named `cache`).
   Keep *Data (/config)* → `/mnt/user/appdata/nzblab-agent` (read/write): the agent stores its token and history there.
3. **Apply.** Open the container **Logs**: the line `NZBLab-Agent Token: …` appears once, and the certificate fingerprint.
4. In the app: *Settings › Server connections › NASlab-Agent* › address `https://<unraid-ip>:8099` › paste the token › **Check**. The agent uses its own certificate, so a browser warns once; compare the fingerprint with the container log. Set up the app within 30 minutes after the container starts (service keys are only handed out in that window); otherwise restart the container.

Network: the default *Bridge* is enough. Only for the optional home-network device list (`NZBLAB_LAN=1`) switch *Network Type* to *Host* and set *Listen address* to your server address.

All host paths are mounted **read-only**; only `/config` is writable. After start the agent drops root and runs as `PUID`/`PGID` (99/100).
Do not expose port 8099 to the internet; use a VPN (WireGuard, Tailscale) away from home.

## Licenses, stated plainly

- **This repository** (templates, profile, icon): [MIT](LICENSE).
- **The agent** (`ghcr.io/tuxxler/nzblab-agent`, source at <https://github.com/Tuxxler/nzblab-agent>): free and open source, **GNU AGPL-3.0-only** (OSI-approved). You may use it (also commercially), read and modify it; if you distribute a modified version or offer it as a network service, you must publish your changes under the same license.
- **The NASlab app**: separate, closed-source Android app on Google Play (closed test now, public launch planned).

## Support

Support and bug reports (GitHub issues): https://github.com/Tuxxler/nzblab-agent/issues · Agent code: <https://github.com/Tuxxler/nzblab-agent>
