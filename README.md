# Homelab Camera Dashboard

A self-hosted camera dashboard using [go2rtc](https://github.com/AlexxIT/go2rtc) with Tailscale networking for secure remote access to RTSP camera streams.

## Setup

1. Copy the example env file and fill in your values:

   ```sh
   cp .env.example .env
   ```

   - `CAM_USER` / `CAM_PASS` — credentials for your camera/NVR
   - `CAM_HOST` — IP address of the NVR
   - `TS_AUTHKEY` — Tailscale auth key ([generate here](https://login.tailscale.com/admin/settings/keys))

2. Start the stack:

   ```sh
   docker compose up -d
   ```

3. Open the dashboard at `http://localhost:1984/dashboard.html`

## Architecture

- **Tailscale sidecar** — joins your tailnet so go2rtc can reach cameras on a Tailscale-routed subnet
- **go2rtc** — streams RTSP from 5 camera channels and serves a WebRTC-based dashboard
- The dashboard auto-discovers streams and renders them in a responsive grid layout

## Ports

| Port | Protocol | Purpose     |
|------|----------|-------------|
| 1984 | TCP      | Web UI      |
| 8554 | TCP      | RTSP        |
| 8555 | TCP/UDP  | WebRTC      |
