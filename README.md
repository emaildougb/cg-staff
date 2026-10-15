# NCEMS CG Staff

Command staff dashboard for North Country EMS. One sign-in, live counts for every admin area, the Shift Ops board built in, and today's ambulance checks.

**Version 1.6**

## Links

- Live (dashboard): [https://emaildougb.github.io/cg-staff/](https://emaildougb.github.io/cg-staff/)
- Live (Shift Ops board): [https://emaildougb.github.io/cg-staff/?view=board](https://emaildougb.github.io/cg-staff/?view=board)
- Live (shift briefing): [https://emaildougb.github.io/cg-staff/?view=brief](https://emaildougb.github.io/cg-staff/?view=brief)
- Demo (sample data, no sign-in): [https://emaildougb.github.io/cg-staff/?demo=1](https://emaildougb.github.io/cg-staff/?demo=1)
  - See it as someone else: add `&as=dennis`, `&as=derek`, `&as=bryce`, `&as=nick` or `&as=chuck`
- Repo: [https://github.com/emaildougb/cg-staff](https://github.com/emaildougb/cg-staff)
- Upload: [https://github.com/emaildougb/cg-staff/upload/main](https://github.com/emaildougb/cg-staff/upload/main)
- EP Checker (crew vehicle checks): [https://checks.northcountryems.org/](https://checks.northcountryems.org/)
- Shift Ops list (SharePoint): [https://northcountryemsorg.sharepoint.com/sites/BattalionChiefLocal/Lists/Shift%20Ops/AllItems.aspx](https://northcountryemsorg.sharepoint.com/sites/BattalionChiefLocal/Lists/Shift%20Ops/AllItems.aspx)

## Files (upload ALL of these)

- `index.html` : the whole app (dashboard + Shift Ops board)
- `logo.png` : NCEMS round logo (header)
- `apple-touch-icon.png` : iOS home-screen + tab icon
- `manifest.json` : standalone app-mode config
- `README.md` : this file

## Page layout

**Top tabs:** Dashboard (default) | Shift Ops
**Header buttons:** home (NCEMS hub) · Briefing · Refresh · (i) info (shows version)

**Dashboard sections:**

| Section | Live numbers | Button goes to |
|---|---|---|
| Vehicle Checks | Ambulances checked today vs the 2 minimum, open issues, problems left by the prior crew, out of service. Tap Open issues or Left by prior to jump straight to that ambulance. Tap a unit chip to open it. A camera icon shows on units with a photo today | Open vehicles (detail for every ambulance), [EP Checker](https://checks.northcountryems.org/) |
| Shift Ops | Open, new in 48 hrs, mine, 14+ days, items needing a group | Shift Ops tab, Briefing |
| Facilities | Open jobs, critical, waiting, overdue services | [fng.northcountryems.org/?view=dash](https://fng.northcountryems.org/?view=dash), Report a problem |
| Grounds | This week, done, late, not completed | [fng.northcountryems.org](https://fng.northcountryems.org/) |
| Incident Reports | New, reviewed, last 30 days (type, date, status only, no names) | [reports.northcountryems.org](https://reports.northcountryems.org/) |
| Scheduling | Link only for now (Derek's overtime app) | [overtime.northcountryems.org](https://overtime.northcountryems.org/) |

**Vehicle Checks detail (Open vehicles):** one card per ambulance from the EP Checker's `units.json`. Shows who checked it today and when, percent done, fuel and mileage, open problems (Could not fix in red, Open in yellow) with a Fixed button, and "Left by the prior crew" for anything the crew fixed on the spot at their check, with the crew who had it before. Type a reason and tap Out of service to take a unit out of the count; tap Back in service to put it back. Last 7 days line shows how many days it was checked and how many handoff fixes.

**Vehicle day and colors:** the check day starts at 0700. Green banner when at least 2 in service ambulances are checked. Yellow before noon if short, red after noon if short.

**Shift Ops tab:** one column per group (Needs Triaged, Training, Logistics, Operations, Chief, plus Fire Dept, Admin, General when used). Drag a card to move it; the owner follows the group's default person (Training Doug, Logistics Dennis, Operations Derek, Chief Bryce). Tap a card for details, status, notes, Take it, and Complete. Done this week, filters (All, Mine, Getting old, Waiting), search, and Add item. On a phone it shows one group at a time with tabs and swipe.

**Triage and briefing flag:** every card has a dot (tap to set Red urgent, Yellow soon, Green routine; white means not triaged yet) and a flag (tap to put it on the shift briefing). The card's left edge shows the triage color. Flagged cards float to the top of their group, then Red, Yellow, not triaged, Green. Filters: Briefing and Not triaged. On a computer the cards are compact. Click a card to show its details and last note right on the board, click again to close it, and click Open card (or double click) for the full card. On a phone, tap opens it. The item sheet has the same Triage buttons and a Mention at shift briefing switch.

**Vehicle issues (1.6):** tap Open issues or Left by prior on the dashboard. One issue opens straight to it, several open a list. Tapping any issue (dashboard list, Open vehicles, or search) opens its detail: crew notes, who reported it and when, how many days it's been open, crew confirmations from later checks, photos, a Fixed button and Full check. **Add to Shift Ops** makes a Logistics card for Dennis with everything filled in and a "Vehicle check ref" line at the bottom of the details that links the two. Notes added on the card (from the issue screen or the board) show on the issue and on the next crew's EP Checker. Completing the card marks the issue fixed; tapping Fixed on the issue completes the card; a crew tapping Now fixed on the next check does both.

**Carry over:** open problems stay open every day until someone marks them fixed. Checks from before EP Checker 2.16 keep the old rule (open items from the latest check only, could not fix from the last 6 checks). Low fuel and DEF only count from the latest check.

**Full check:** each check line in Open vehicles has a Full check button with the whole check as the crew saw it (EP Checker 2.16 and up). Older checks show just the problems.

**Search:** at the bottom of the dashboard. Searches every Shift Ops item ever put on (title, details, notes, assigned, completed by, group, SO number) and every vehicle check issue from the last 45 days. All, Open and Done chips. Every word you type has to match. Tap a result to open it.

**Photos and notes on checks:** in Open vehicles, each check shows its walk-around and fridge photos as thumbnails (tap for full size), anything typed in the Other notes boxes, and narc counts that came in short.

**Briefing:** has a "Rig checks for Logistics (Dennis)" block with everything today's checks turned up: could not fix, open, left by the prior crew, short narcs, notes, and out of service units. It also (and flagged items finished in the time window) by default. Tap Everything for new, being worked, other done, and getting old.

## Who gets in

Emails in `CONFIG.staff`: Doug, Derek, Dennis, Bryce, Chuck, Nick, K. Reid. Anyone else who signs in sees "CG Staff only" and a link to the hub. Each person also needs access to the CG Staff and Facilities and Grounds SharePoint sites for numbers to load.

## Where the data lives

- **Shift Ops:** "Shift Ops" SharePoint list in the CG Staff team. Fed by the Claude email sweep (every 4 hours) through the "Shift Ops Drop (do not delete)" folder and the Power Automate flows "Shift Ops: drop folder to list" and "Shift Ops: completed stamp". The list also has `Triage` (Choice: Red, Yellow, Green) and `Briefing` (Yes/No) columns, added for v1.2. If they're ever missing, the app still works but triage and flags show a note instead of saving.
- **Facilities / Grounds:** Facility Work Orders, Facility Services and Grounds Tracker lists on the Facilities and Grounds site (same data as the F&G app, read only here).
- **Vehicle Checks:** Firebase project `ncems-hub-9111d` (same one the hub uses). Since 1.6, `vehicleLinks/{check ref}` holds the link between a vehicle issue and its Shift Ops card (card id, status, latest note) so the EP Checker can show the chiefs' latest note to crews. The EP Checker (v2.14.0 and up) writes one doc per submitted check to `vehicleChecks`. Out of service marks go to `vehicleStatus`, Fixed marks go to `vehicleResolved`. The dashboard reads the last 45 days.
- **Incident Reports:** Cloudflare Worker `ncems-api.d-boyce.workers.dev/bin/incident-reports`, read only. Since v1.3 the dashboard sends the Microsoft sign-in token, and the Worker only answers for chiefs on its ADMINS list.
- **Scheduling:** Derek's Worker (`ncems-ot.d-langdon.workers.dev`) with its own sign-in. Live numbers need a read endpoint shared with this app.

## Microsoft sign-in setup

1. Uses the existing Entra app "NCEMS Grounds Tracker" (client id `254c214f-bfe2-4ebb-9294-99815e167ab0`), Sites.ReadWrite.All already consented
2. Entra > App registrations > NCEMS Grounds Tracker > Authentication > Single-page application > add `https://emaildougb.github.io/cg-staff/`
3. Save. No new consent needed

## Changelog

### v1.6
- Open issues and Left by prior open the issues: straight to it if there's one, a list if there are more
- Issue detail screen with crew notes, days open, crew confirmations, photos, Fixed and Full check
- Add to Shift Ops on any vehicle issue (Logistics, Dennis). The card and the issue stay linked both ways: notes, completing and Fixed
- Open problems carry over until fixed (2.16 checks)
- Full check button on every check
- Search bar at the bottom of the dashboard for every Shift Ops item, open or done, plus vehicle check issues
- Briefing shows how long a rig problem has been open and its Shift Ops status and latest note
- Link straight to an issue with ?veh= plus the check ref

### v1.5
- Photos from the EP Checker show as thumbnails on each check, with a camera icon on the dashboard chip
- Other notes, short narc counts, DEF and O2 readings show on each check
- Tapping Left by prior (or Open issues) jumps right to that ambulance's list
- Unit chips open that ambulance
- Shift briefing has a Rig checks block for Dennis with what today's checks turned up
- Overtime renamed Scheduling
- Held email note now says 1100 (EP Checker 2.15 rule)

### v1.4
- Added k.reid@northcountryems.org to CG Staff access (hub button shows for them too in hub v1.14)

### v1.3
- Shift Ops cards on a computer open with a click instead of hover. Second click closes, Open card or double click for the full card
- Incident Reports numbers now load with your Microsoft sign-in (goes with Incident Report v3.0 and the new Worker)

### v1.2
- Shift Ops cards get a triage dot (Red / Yellow / Green) and a shift briefing flag, both one tap from the card
- Flagged cards float to the top, then by triage color
- Briefing view shows only flagged items by default, with an Everything button for the full list
- Compact cards on desktop, hover to see details and the last note
- Dashboard Shift Ops card: Open, Briefing, Red, Not triaged, with flagged items listed first
- New filters: Briefing, Not triaged

### v1.1
- New Vehicle Checks section, first on the dashboard: daily check status for every ambulance, 2 ambulance minimum, open issues, handoff problems left by the prior crew
- Open vehicles detail: per unit checks, Fixed button on open problems, Out of service with reason, Back in service, 7 day look back
- Header back arrow is now a home button to the hub

### v1.0
- First build: Dashboard tab with Shift Ops, Facilities, Grounds, Incident Reports and Overtime sections
- Shift Ops board built in (replaces the standalone shift-ops app, which was never deployed)
- Login gate by email for CG Staff
- Playwright smoke test (demo mode): dashboard sections, board drag, briefing, phone layout, no page errors

## Notes

- Hosted in `cg-staff` repo : never touches root URL
- iOS home-screen caches hard : delete and re-add icon after every deploy
- Back button goes to `https://hub.northcountryems.org/`
- Vehicle Checks needs EP Checker v2.14.0 live before any checks show up. Checks submitted before that are email only
- Firebase rules (Firebase console > Firestore > Rules). The whole thing, as published for EP Checker 2.16 / CG Staff 1.6:

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /notices/{doc} { allow read: if true; allow write: if false; }
    match /usage/{doc} { allow read, write: if true; }
    match /vehicleChecks/{id} { allow read: if true; allow create, update: if request.resource.data.unit is string && request.resource.data.atMs is number && request.resource.data.issues is list; }
    match /vehicleStatus/{unit} { allow read: if true; allow create, update: if request.resource.data.oos is bool && request.resource.data.by is string; }
    match /vehicleResolved/{id} { allow read: if true; allow create, update: if request.resource.data.checkId is string && request.resource.data.by is string; }
    match /liveChecks/{id} { allow read: if true; allow create, update: if request.resource.data.unit is string && request.resource.data.date is string && request.resource.data.updatedAt is number; }
    match /vehicleLinks/{id} { allow read: if true; allow create, update: if request.resource.data.checkId is string && request.resource.data.label is string; }
  }
}
```
