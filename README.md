# OpenAccess

OpenAccess is a self-hostable, browser-based **restricted web reader**. It fetches pages through a server you operate and displays rewritten HTML inside the app instead of redirecting the user to the destination.

## Functional MVP

- Server-side HTTP/HTTPS fetching for operator-approved hostnames
- HTML pages, stylesheets, images and common font resources
- Rewritten page links and static assets so navigation stays inside OpenAccess
- URL/search interface and in-app page view
- Host allowlist, public-IP checks, redirect validation, timeout and response-size limits

## Limitations

This is a first functional proxy milestone, not a full Chromium remote browser like Rammerhead. For safety and reliability, the reader removes page scripts, forms, embedded frames and active content. Login flows, interactive web apps, streaming, WebSockets, downloads and many modern sites will not work. Only GET requests are supported. Sites that depend on JavaScript may fail.

OpenAccess is intentionally **not an unrestricted proxy** and must not be used to evade school, employer, device, network, or website access controls. The backend only fetches hostnames explicitly configured by its operator.

## Deploy the backend

A Render Blueprint is included in `render.yaml`.

1. In Render, create a new Blueprint and select this repository.
2. Deploy the `open-access-proxy` service.
3. Copy its public service URL (for example, `https://open-access-proxy.onrender.com`).
4. Open the GitHub Pages frontend, choose **Settings**, and paste the backend URL.

Free Render services may sleep when idle; first requests can be delayed and free-plan limits may change.

### Configure allowed destinations

Set `ALLOWED_HOSTS` to a comma-separated list of hostnames you are authorized to serve, for example:

```
ALLOWED_HOSTS=example.com,www.wikipedia.org,en.wikipedia.org,developer.mozilla.org
```

A rule also allows its subdomains. Keep this list narrow. Set `FRONTEND_ORIGIN` to your exact GitHub Pages origin after deployment rather than `*`.

## Deploy the frontend

The included GitHub Actions workflow publishes `index.html` to GitHub Pages. Set **Repository Settings → Pages → Build and deployment → Source** to **GitHub Actions**.

## Run locally

Requires Node.js 20+.

```sh
npm install
ALLOWED_HOSTS=example.com,www.wikipedia.org npm start
```

The health check is available at `http://localhost:3000/health`. Configure the frontend backend URL as `http://localhost:3000`.

## Security notes

- Only explicitly allowlisted hostnames are fetched.
- DNS answers are checked and non-public IP ranges are blocked; redirects are revalidated.
- Only GET is exposed; there is no arbitrary method/body forwarding.
- Responses are capped by `MAX_RESPONSE_BYTES` (default 5 MB) and `REQUEST_TIMEOUT_MS` (default 12 seconds).
- HTML scripts, forms, frames, refresh redirects and active content are removed.
- This is an MVP, not yet hardened for unrestricted public operation. Before wider public use, add authentication, rate limiting, quotas, robust DNS pinning and stricter CORS settings, then security-test it.

## Privacy

The frontend stores the backend URL in local storage. The backend does not intentionally store browsing history.
