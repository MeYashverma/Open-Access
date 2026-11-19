# OpenAccess

A clean, browser-based web access workspace.

OpenAccess is being built as a transparent, self-hostable project. The first milestone is a lightweight web interface for opening permitted websites, searching the web, and keeping local bookmarks. It does **not** proxy traffic, conceal destinations, or bypass workplace, school, network, or website access controls.

## Current status

This repository is the starting point. The initial frontend is a static site and can be hosted on GitHub Pages. It provides:
- A URL/search bar with basic URL detection
- Quick links to common web destinations
- Locally stored bookmarks and recently opened destinations
- Responsive layout and dark/light appearance

## Important distinction

A static GitHub Pages site cannot run a server-side browser or proxy. Websites opened from OpenAccess are still loaded directly by the user's browser and remain subject to the network and device policies in effect.

A future remote-rendering or server component would need a separately hosted backend, explicit operator-controlled destination policy, abuse protections, and a deployment review. OpenAccess will not be developed as an unrestricted relay for evading network restrictions.

## Run locally

Open `index.html` in a browser, or serve the repository with any static file server.

## Deploy with GitHub Pages

The included GitHub Actions workflow publishes the repository root to GitHub Pages. In the repository settings, set **Pages → Build and deployment → Source** to **GitHub Actions**.

## Privacy

Bookmarks and recent destinations are stored in this browser's local storage. They are not uploaded to an OpenAccess server. Clearing this browser's site data removes them.

## License

No license has been selected yet. Until one is added, the source is not granted an open-source license by default.
