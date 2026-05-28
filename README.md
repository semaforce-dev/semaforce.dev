# SemaForce Site Prototype

Local-first static prototype built by Hermes/Codex.

## Context Used

- Current public `semaforce.dev` page: sparse Squarespace-style recruiting message.
- HermesBrain business records around SemaForce marketing, staffing partnerships, Upwork consulting, and data-engineering opportunities.
- Lucas resume source for software leadership, backend/platform, cloud, data, DevOps, observability, and systems competencies.
- Public Semaforce/DevOps-security positioning was treated as directional only, not copied as a verified claim for SemaForce LLC.
- Favicon uses the compact SemaForce SF mark in the site palette until the final source logo package is selected.
- Lumina Teams assets are sourced from the Hermes project at
  `/Users/lucasearl/Hermes/projects/lumina-teams-production-readiness/repos/frontend/public/`
  so future portfolio work uses the project-owned logo instead of a generic external favicon lookup.
- Pago People uses the favicon supplied from
  `/Users/lucasearl/Hermes/projects/pago-people/repos/frontend/public/favicon.ico`.

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

## Production Hosting

The production path is GitHub Pages because this is a static site and can be
hosted for $0 from a public repository.

- Repository: `semaforce-dev/semaforce.dev`
- Production domain: `https://semaforce.dev`
- Deployment: `.github/workflows/deploy-pages.yml`
- Trigger: every push to `main` or `master`, plus manual `workflow_dispatch`

The `CNAME` file binds the Pages deployment to `semaforce.dev`.

Squarespace Domains DNS is pointed to GitHub Pages:

```text
A     @    185.199.108.153
A     @    185.199.109.153
A     @    185.199.110.153
A     @    185.199.111.153
AAAA  @    2606:50c0:8000::153
AAAA  @    2606:50c0:8001::153
AAAA  @    2606:50c0:8002::153
AAAA  @    2606:50c0:8003::153
CNAME www  semaforce-dev.github.io
```

The site is live at `https://semaforce.dev/`; `https://www.semaforce.dev/`
redirects to the apex domain. GitHub Pages HTTPS enforcement is enabled.

The contact form posts over HTTPS to FormSubmit's activated invisible endpoint
for `earl.lucas@gmail.com` and redirects successful submissions to
`/thanks.html`. The public site can still display `lucas@semaforce.dev`, while
the form backend forwards to a mailbox Lucas can receive.

If GitHub Pages gets stuck with `The certificate does not exist yet`, the
recovery path that worked on 2026-05-28 was:

```bash
gh api -X DELETE repos/semaforce-dev/semaforce.dev/pages --silent
gh api -X POST repos/semaforce-dev/semaforce.dev/pages \
  -f build_type=workflow \
  -f 'source[branch]=main' \
  -f 'source[path]=/'
gh api -X PUT repos/semaforce-dev/semaforce.dev/pages \
  -H 'Accept: application/vnd.github+json' \
  -H 'X-GitHub-Api-Version: 2026-03-10' \
  --input - < reconnect-pages.json
gh workflow run deploy-pages.yml --repo semaforce-dev/semaforce.dev --ref main
```

Where `reconnect-pages.json` contains:

```json
{"cname":"semaforce.dev","source":{"branch":"main","path":"/"}}
```

After the Pages API reports `https_certificate.state` as `approved`, enable
enforcement:

```bash
gh api -X PUT repos/semaforce-dev/semaforce.dev/pages \
  -H 'Accept: application/vnd.github+json' \
  -H 'X-GitHub-Api-Version: 2026-03-10' \
  --input - < enforce-https.json
```

Where `enforce-https.json` contains:

```json
{"cname":"semaforce.dev","https_enforced":true,"source":{"branch":"main","path":"/"}}
```

## Next Iterations

- Replace the stock hero image with a SemaForce-owned visual asset or generated brand image.
- Decide whether SemaForce is primarily positioned as technical staffing, consulting, DevOps/security, or a blended delivery partner.
- Add proof: client logos, testimonials, case studies, compliance language, and clear talent intake flow.
- Replace the static form provider with a first-party API endpoint if SemaForce needs CRM routing, stronger spam controls, or private data retention guarantees.
