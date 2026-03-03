# Close the Loop Tracker Server

## What this is
This is the production server for Close the Loop, a 30-day behavioral execution tracker sold by @stoicmind. The tracker is a single-page static site served at tracker.stoicmind.org.

## Critical Rules (NEVER ignore these)
- NEVER modify index.html content without explicit instruction
- NEVER install Node.js, Python, or any runtime for this site
- NEVER set up a reverse proxy. This is purely static.
- NEVER expose any other ports or services through the nginx config
- NEVER create a database or any server-side storage
- NEVER make changes beyond the scope of the current task
- BEFORE making any change, understand the existing structure first

## Server
- Provider: DigitalOcean
- OS: Ubuntu 24.04.4 LTS
- IP: 159.203.109.157
- Domain: tracker.stoicmind.org (A record pointing to this IP)
- Web server: nginx (serving static files)
- SSL: certbot / Let's Encrypt

## Site Structure
All static files live in /var/www/tracker/:

/var/www/tracker/
  index.html            -> The entire tracker app (single file, vanilla JS/CSS/HTML)
  favicon.ico
  favicon-16x16.png
  favicon-32x32.png
  apple-touch-icon.png

There is no build step. No framework. No dependencies. One self-contained HTML file with inline CSS and JavaScript.

## How the Tracker Works
- Gate screen: user enters access code (discipline) from purchase email
- Start screen: user clicks begin, sets Day 1 to today
- Tracker screen: 30-day grid, one entry per day via 4-step protocol modal
- Protocol sequence: the priority, the obstacle, the lie, the schedule
- All data persists in browser localStorage (key: ctl_data)
- Completion screen: screenshottable proof card after 30 days
- No backend. No database. No server-side logic.

## Brand
- Colors: Green #294036, Off-white #F5F0E8, Gold #C9A84C, Black #0D1F17
- Typography: Outfit (300/400/600/700), DM Mono (400) from Google Fonts
- Voice: all lowercase in content. direct. no fluff.

## Nginx Config Rules
- Serve static files from /var/www/tracker/
- Listen on port 80 (HTTP) and 443 (HTTPS after certbot)
- Server name: tracker.stoicmind.org
- Set appropriate cache headers for static assets
- Set X-Content-Type-Options: nosniff
- Set X-Frame-Options: DENY (tracker should not be iframed)
- Gzip HTML, CSS, JS

## SSL
Use certbot with nginx plugin. Domain: tracker.stoicmind.org. Auto-renew via certbot default systemd timer.

## Deployment
1. Replace /var/www/tracker/index.html with new version
2. No restart needed. Nginx serves static files directly.

## Conventions
- All content text: lowercase. direct. no fluff.
- CSS: inline in index.html. No external stylesheets beyond Google Fonts.
- JS: inline in index.html. No external scripts.
- Colors: only use brand palette (#294036, #F5F0E8, #C9A84C, #0D1F17)
- Typography: only Outfit and DM Mono

## Workflow
1. Understand the task. Ask questions if anything is unclear.
2. Review current index.html before making changes.
3. Make targeted changes only. Do not refactor unrelated code.
4. Test in browser after changes.
5. Verify mobile responsiveness.
