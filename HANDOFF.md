# CG Staff Handoff

Updated 10/24/2026 for version **1.26.1** (built from live 1.26). Check the raw files for merge markers after each upload.

- Live: [https://cgstaff.northcountryems.org/](https://cgstaff.northcountryems.org/)
- Upload: [https://github.com/emaildougb/cg-staff/upload/main](https://github.com/emaildougb/cg-staff/upload/main)
- Repo: [https://github.com/emaildougb/cg-staff](https://github.com/emaildougb/cg-staff)
- Demo, no sign in: [https://emaildougb.github.io/cg-staff/?demo=1](https://emaildougb.github.io/cg-staff/?demo=1) (add `&as=dennis`, `&as=derek`, `&as=bryce`, `&as=nick` or `&as=chuck` to see it as someone else)

Owner: Doug Boyce, BC / Training, North Country EMS (d.boyce@northcountryems.org).

## What it is

The command staff front door. One Microsoft sign in, then a dashboard with live numbers from every admin area, plus the Shift Briefing Notes board (the old Shift Ops board) built in. Chiefs use it to see the whole agency on one screen and jump straight into whatever needs them.

Across the top (1.21): the crews strip, who is on M51, M52, M53 and M54 now and tomorrow. Dashboard boxes, top to bottom: Scheduling, Shift Briefing Notes, Incident Reports, Vehicle Checks, Grounds, Facilities. Tap any box, tile or row and it opens that thing.

Other views:
- `?view=board` the Shift Briefing Notes board
- `?view=brief` the shift briefing
- `?veh=<check ref>` straight to one vehicle issue

## Who gets in

Six people: Doug, Derek Langdon, Dennis Madler, Bryce Shirley, Chuck Andrus, Kim Reid. (Nicholas Stafford was removed from the Command Staff Entra app 10/21; his email is still in `CONFIG.staff`, harmless since Microsoft blocks him, trim it in a later version.)

Two locks, both have to match:
1. **Microsoft (the real lock).** Entra app **NCEMS Command Staff**, client id `f758d1fe-91b7-4bd5-92a9-1324d8bf0826`, tenant `153dc089-095e-4a20-8d10-39321a0aca09`. Assignment required = Yes, only those six assigned. Anyone else gets turned away by Microsoft before the app loads
2. **The app's own list.** `CONFIG.staff` in index.html. Anyone signed in but not on it sees "CG Staff only" and a link to the hub

To add a chief: Entra > Enterprise applications > NCEMS Command Staff > Users and groups > Add, then add their email to `CONFIG.staff` and bump the version. They also need access to the CG Staff and Facilities and Grounds SharePoint sites or the numbers won't load.

Forms shares this same Entra app.

## How it's built

- One file, `index.html` (about 2,400 lines), plain HTML, CSS and JavaScript. No build step, no framework
- Microsoft sign in through MSAL (redirect flow). Graph calls for SharePoint use the access token; the Workers get the ID token
- Hosted on GitHub Pages from the `cg-staff` repo under `emaildougb`, custom domain `cgstaff.northcountryems.org`
- Everything you'd change lives in the `CONFIG` block near line 606: list ids, URLs, the staff list, vehicle rules (day starts 0700, 2 ambulance minimum, red after noon if short, 45 days kept on screen)
- Refreshes every 60 seconds

Files in the repo (upload all of them every version): `index.html`, `logo.png`, `apple-touch-icon.png`, `icon-512.png`, `manifest.json`, `README.md`, `HANDOFF.md`.

## Where the data comes from

| Box | Source | Notes |
|---|---|---|
| Shift Briefing Notes | SharePoint list "Shift Ops" on the CG Staff site (BattalionChiefLocal), list id `a74e70d7-2646-4ba7-9b7a-8cc11b1d6dba` | Read and write. Fed by the Claude email sweep through the "Shift Ops Drop (do not delete)" folder and Power Automate flows "Shift Ops: drop folder to list", "Shift Ops: completed stamp" and "Shift Ops: reminders" (steps in README) |
| Vehicle Checks | `ncems-checks` Worker, https://ncems-checks.d-boyce.workers.dev (North Country Cloudflare, D1 `ncems-checks-db`, photos in R2 `ncems-check-photos`) | Read checks, write out of service, Fixed and Shift Ops links. Unit list from https://checks.northcountryems.org/units.json |
| Vehicle check records | CG Staff SharePoint, `App Data/Vehicle Checks/YYYY-MM/` | CG Staff copies every check and its photos there in the background whenever a chief has it open, 40 per refresh. Crew phones can't write to that site, so this is how they get there |
| Facilities, Grounds | Facility Work Orders, Facility Services, Grounds Tracker lists on the FacilitiesandGrounds SharePoint site | Read only |
| Incident Reports | `ncems-api` Worker, https://ncems-api.d-boyce.workers.dev/bin/incident-reports | Read only, counts and types only, no names. Worker only answers its ADMINS list |
| Crews strip (1.21) | `ncems-schedule-crews` Worker, https://ncems-schedule-crews.d-boyce.workers.dev/crews (North Country Cloudflare). It holds Doug's key for Derek's Schedule API as secret `NCEMS_SCHEDULE_KEY` and returns names and seats only | Read only. Key, Derek's prompt and API Usage Guide saved on the CG Staff site at `App Data/Schedule API (Derek)/`. The key never goes in index.html (public repo) |
| Scheduling | Derek's Open Shifts feeds: Crew 1 `ncems-ot.d-langdon.workers.dev/dashboard`, Crew 2 `ncems-c2.d-langdon.workers.dev/dashboard` | Read only. **Derek's app, Derek's accounts. Leave it alone** |

Firebase (`ncems-hub-9111d`) and Cloudinary are retired as of 10/21. Old notes about them in the README are history only.

## Why it's built this way

- **Single file on GitHub Pages:** free, nothing to keep running, Doug can upload from his phone
- **Microsoft sign in:** everyone already has an NCEMS account, so no new passwords, and Entra decides who gets in
- **Own Entra app (since 1.20):** CG Staff used to share "NCEMS Grounds Tracker" with F&G and Reports, which meant anyone signed into those could read the same feeds. Splitting it off locked it to seven people
- **SharePoint for anything chiefs keep:** standing rule. All data CG Staff touches ends up on the CG Staff SharePoint site so chiefs can search it and rebuild reports in one spot
- **Cloudflare for vehicle checks:** crews on any phone need to write checks without SharePoint access. The Worker checks the Microsoft token, and it's on the agency Cloudflare, not a personal one

## Open items

0. **Reminders (done 10/24):** Shift Ops list has AlsoAssigned, RemindOn, RemindEvery. Flow "Shift Ops: reminders" runs daily 7:00 AM Pacific from Doug's Power Automate (details in README). If a chief says a reminder never came, check that flow's run history first
1. **Crews strip:** the `ncems-schedule-crews` Worker was made 10/23 with its code and plain settings. Doug still pastes the key as the Secret `NCEMS_SCHEDULE_KEY` (Settings > Variables and Secrets). Until then the strip says "Schedule data is unavailable right now"
2. **Derek:** add `f758d1fe-91b7-4bd5-92a9-1324d8bf0826` to the allowed audiences on `ncems-ot` and `ncems-c2`. Until he does, the Scheduling box says it's waiting on him. Leave `254c214f` in for now
3. **Later:** once Derek confirms, drop the old Grounds Tracker id (`254c214f...`) from anything on the Command Staff side
4. **Shift Ops acknowledgment build:** each item acknowledged by its owner (Training Doug, Logistics Dennis, Operations Derek, Chief Bryce), owners reminded of new items, no duplicates across the BCs' email sweeps
5. **Unit issue history view** (in next-build-queue.md)
6. **CITYBUS.md** for this repo still hasn't been made. This file covers most of it
7. **README cleanup:** the old Firebase rules block and Cloudinary photo note at the bottom are stale. Trim them next version

## Rules for the next version

- Haptics (1.25): `haptic()` runs on every tap of a button, card, link or tab (one capture listener). iPhone uses the hidden `<input type="checkbox" switch>` trick (iOS 18+), Android uses `navigator.vibrate`. Doug wants the same in every NCEMS app as each is rebuilt
- Anything fixed to the bottom edge must be `visibility:hidden` when idle, or iPhone Safari tints its bottom bar with that color

- Start from the live files: `https://raw.githubusercontent.com/emaildougb/cg-staff/main/index.html` (and README.md). Never an old local copy
- Bump `const VERSION` in index.html and the version line plus changelog in README.md. Version shows in the (i) panel
- Deliver one zip named `cg-staff-v<version>.zip` with every file inside
- Upload through the website upload page, not GitHub Desktop. After upload, check the raw file for `<<<<<<<` merge markers
- After a deploy, delete and re-add the home screen icon on iPhones (iOS caches hard). On a computer, Ctrl+Shift+R
- Never call `history.replaceState()` or clean the address bar before MSAL's `handleRedirectPromise()` runs. It wipes the sign in code and causes a sign in loop (bit the Forms app once)
- Reminders (1.23): `CONFIG.reminders` near the top of index.html. Each has id, who (email names before the @), mode once or daily, text, and a link (go) or the board (act). Done marks are files in `App Data/Reminders` on the CG Staff site: `<id> <email>.txt` for once, `<id> <email> <YYYY-MM-DD>.txt` for daily (day flips at 0600). Delete a file there to make a reminder show again
- Header look (1.21, Doug's standing rule for every NCEMS app): Derek's Open Shifts style. White bar, system font, "NCEMS" in black and "CG Staff" in green #2d6a2d at 18px weight 800, a thin line, then "North Country EMS" in gray. Crews strip uses the same look; tabs and boxes below still have the old style
- Home button to hub.northcountryems.org stays on top, iOS bottom bar flush with the bottom, search stays at the bottom of the dashboard
- Doug's writing rules apply to app text and the README: plain words, no em dashes, no hyphens as punctuation
- Test in demo mode (`?demo=1`) before shipping. The old pattern was a Playwright smoke test: dashboard boxes render, board drag works, briefing opens, phone layout, no page errors

## Starting a new AI chat on this app

Paste this, then say what you want changed:

```
I'm Doug Boyce, BC at North Country EMS. I need to work on my CG Staff app, a single file HTML command staff dashboard on GitHub Pages. Repo: github.com/emaildougb/cg-staff. Live: cgstaff.northcountryems.org. Before doing anything, pull the live index.html and README.md from raw.githubusercontent.com/emaildougb/cg-staff/main/ and read HANDOFF.md from the same place. Work from those, not memory. Sign in is Microsoft Entra app NCEMS Command Staff (f758d1fe-91b7-4bd5-92a9-1324d8bf0826). Data: Shift Ops SharePoint list on the BattalionChiefLocal site, vehicle checks on the ncems-checks Cloudflare Worker, incident reports on ncems-api, scheduling is Derek Langdon's feed (don't touch his side), crews at the top come from the ncems-schedule-crews Worker, which holds the Schedule API key (never put the key in index.html). When you build, bump the version, update the README changelog, and give me one zip named cg-staff-v<version>.zip with every file inside. Write plain, no em dashes, no hyphens as punctuation.
```
