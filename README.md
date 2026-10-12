# NCEMS CG Staff

Command staff dashboard for North Country EMS. One sign-in, live counts for every admin area, and the Shift Ops board built in.

**Version 1.0**

## Links

- Live (dashboard): [https://emaildougb.github.io/cg-staff/](https://emaildougb.github.io/cg-staff/)
- Live (Shift Ops board): [https://emaildougb.github.io/cg-staff/?view=board](https://emaildougb.github.io/cg-staff/?view=board)
- Live (shift briefing): [https://emaildougb.github.io/cg-staff/?view=brief](https://emaildougb.github.io/cg-staff/?view=brief)
- Demo (sample data, no sign-in): [https://emaildougb.github.io/cg-staff/?demo=1](https://emaildougb.github.io/cg-staff/?demo=1)
  - See it as someone else: add `&as=dennis`, `&as=derek`, `&as=bryce`, `&as=nick` or `&as=chuck`
- Repo: [https://github.com/emaildougb/cg-staff](https://github.com/emaildougb/cg-staff)
- Upload: [https://github.com/emaildougb/cg-staff/upload/main](https://github.com/emaildougb/cg-staff/upload/main)
- Shift Ops list (SharePoint): [https://northcountryemsorg.sharepoint.com/sites/BattalionChiefLocal/Lists/Shift%20Ops/AllItems.aspx](https://northcountryemsorg.sharepoint.com/sites/BattalionChiefLocal/Lists/Shift%20Ops/AllItems.aspx)

## Files (upload ALL of these)

- `index.html` — the whole app (dashboard + Shift Ops board)
- `logo.png` — NCEMS round logo (header)
- `apple-touch-icon.png` — iOS home-screen + tab icon
- `manifest.json` — standalone app-mode config
- `README.md` — this file

## Page layout

**Top tabs:** Dashboard (default) | Shift Ops
**Header buttons:** back to NCEMS hub · Briefing · Refresh · (i) info

**Dashboard sections:**

| Section | Live numbers | Button goes to |
|---|---|---|
| Shift Ops | Open, new in 48 hrs, mine, 14+ days, items needing a group | Shift Ops tab, Briefing |
| Facilities | Open jobs, critical, waiting, overdue services | [fng.northcountryems.org/?view=dash](https://fng.northcountryems.org/?view=dash), Report a problem |
| Grounds | This week, done, late, not completed | [fng.northcountryems.org](https://fng.northcountryems.org/) |
| Incident Reports | New, reviewed, last 30 days (type, date, status only, no names) | [reports.northcountryems.org](https://reports.northcountryems.org/) |
| Overtime | Link only for now | [overtime.northcountryems.org](https://overtime.northcountryems.org/) |

**Shift Ops tab:** one column per group (Needs Triaged, Training, Logistics, Operations, Chief, plus Fire Dept, Admin, General when used). Drag a card to move it; the owner follows the group's default person (Training Doug, Logistics Dennis, Operations Derek, Chief Bryce). Tap a card for details, status, notes, Take it, and Complete. Done this week, filters (All, Mine, Getting old, Waiting), search, and Add item. On a phone it shows one group at a time with tabs and swipe.

## Who gets in

Emails in `CONFIG.staff`: Doug, Derek, Dennis, Bryce, Chuck, Nick. Anyone else who signs in sees "CG Staff only" and a link to the hub. Each person also needs access to the CG Staff and Facilities and Grounds SharePoint sites for numbers to load.

## Where the data lives

- **Shift Ops:** "Shift Ops" SharePoint list in the CG Staff team. Fed by the Claude email sweep (every 4 hours) through the "Shift Ops Drop (do not delete)" folder and the Power Automate flows "Shift Ops: drop folder to list" and "Shift Ops: completed stamp".
- **Facilities / Grounds:** Facility Work Orders, Facility Services and Grounds Tracker lists on the Facilities and Grounds site (same data as the F&G app, read only here).
- **Incident Reports:** Cloudflare Worker `ncems-api.d-boyce.workers.dev/bin/incident-reports`, read only.
- **Overtime:** Derek's Worker (`ncems-ot.d-langdon.workers.dev`) with its own sign-in. Live numbers need a read endpoint shared with this app.

## Microsoft sign-in setup

1. Uses the existing Entra app "NCEMS Grounds Tracker" (client id `254c214f-bfe2-4ebb-9294-99815e167ab0`), Sites.ReadWrite.All already consented
2. Entra > App registrations > NCEMS Grounds Tracker > Authentication > Single-page application > add `https://emaildougb.github.io/cg-staff/`
3. Save. No new consent needed

## Changelog

### v1.0
- First build: Dashboard tab with Shift Ops, Facilities, Grounds, Incident Reports and Overtime sections
- Shift Ops board built in (replaces the standalone shift-ops app, which was never deployed)
- Login gate by email for CG Staff
- Playwright smoke test (demo mode): dashboard sections, board drag, briefing, phone layout, no page errors

## Notes

- Hosted in `cg-staff` repo — never touches root URL
- iOS home-screen caches hard — delete and re-add icon after every deploy
- Back button goes to `https://hub.northcountryems.org/`
- Add to the hub's Operations tab under BC / Chief when it's live
