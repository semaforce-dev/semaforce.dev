# SemaForce Site Prototype

Local-first static prototype built by Hermes/Codex.

## Context Used

- Current public `semaforce.dev` page: sparse Squarespace-style recruiting message.
- HermesBrain business records around SemaForce marketing, staffing partnerships, Upwork consulting, and data-engineering opportunities.
- Lucas resume source for software leadership, backend/platform, cloud, data, DevOps, observability, and systems competencies.
- Public Semaforce/DevOps-security positioning was treated as directional only, not copied as a verified claim for SemaForce LLC.
- Favicon uses the compact SemaForce SF mark in the site palette until the final source logo package is selected.

## Run Locally

```bash
cd /Users/lucasearl/HermesProjects/semaforce-site
python3 -m http.server 5081 --bind 127.0.0.1
```

Then open:

```text
http://127.0.0.1:5081/
```

## Share Preview

```bash
cloudflared tunnel --url http://127.0.0.1:5081
```

Use the generated `https://*.trycloudflare.com` URL for phone/device preview.

Current verified quick tunnel:

```text
https://chemicals-responsible-cedar-expansys.trycloudflare.com
```

The current durable local preview is managed by LaunchAgents:

```bash
launchctl print gui/$(id -u)/dev.semaforce.preview.server
launchctl print gui/$(id -u)/dev.semaforce.preview.tunnel
```

Logs are written under:

```text
~/Library/Logs/HermesPreview/
```

## Next Iterations

- Replace the stock hero image with a SemaForce-owned visual asset or generated brand image.
- Decide whether SemaForce is primarily positioned as technical staffing, consulting, DevOps/security, or a blended delivery partner.
- Add proof: client logos, testimonials, case studies, compliance language, and clear talent intake flow.
- Replace `mailto:` with a real form provider before production.
