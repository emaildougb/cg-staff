# NCEMS CG Staff

Command staff dashboard for North Country EMS. One sign-in, live counts for every admin area, the Shift Ops board built in, and today's ambulance checks.

**Version 1.28.1**

## Links

- Live: [https://cgstaff.northcountryems.org/](https://cgstaff.northcountryems.org/)
- Upload: [https://github.com/emaildougb/cg-staff/upload/main](https://github.com/emaildougb/cg-staff/upload/main)
- Live (dashboard, GitHub address): [https://emaildougb.github.io/cg-staff/](https://emaildougb.github.io/cg-staff/)
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
- `icon-512.png` : large app icon
- `HANDOFF.md` : how the app is built and how to start a new chat on it
- `README.md` : this file

## Page layout

**Top tabs:** Dashboard (default) | Shift Ops
**Header buttons:** home (NCEMS hub) · Briefing · Refresh · (i) info (shows version)

**Crews strip (1.21), above the boxes:** who is on M51, M52, M53 and M54 today, with the date in a big pill next to it so it's obvious which day you're looking at (M53 and M54 only when someone is on them). PM is the C1 paramedic, EMT is C2, AC shows on M54 when someone is in it. Split shifts show each piece with times, an empty seat shows OPEN in red, and trade, cover and OT tags come from Aladtec. On a computer, tomorrow's crews show on one line under it. On a phone every unit is one tight row, all on screen at once (no swiping), with a Today / Tomorrow switch. The day flips at 0600. "Schedule data as of" shows when Derek last rebuilt the data, and turns yellow when it is 4 or more days old. Tap a unit to open Aladtec.

**Dashboard sections:**

| Section | Live numbers | Button goes to |
|---|---|---|
| Vehicle Checks | Ambulances checked today vs the 2 minimum, open issues, problems left by the prior crew, out of service. Tap Open issues or Left by prior to jump straight to that ambulance. Tap a unit chip to open it. A camera icon shows on units with a photo today | Open vehicles (detail for every ambulance), [EP Checker](https://checks.northcountryems.org/) |
| Shift Ops | Open, new in 48 hrs, mine, 14+ days, items needing a group | Shift Ops tab, Briefing |
| Facilities | Open jobs, critical, waiting, overdue services | [fng.northcountryems.org/?view=dash](https://fng.northcountryems.org/?view=dash), Report a problem |
| Grounds | This week, done, late, not completed | [fng.northcountryems.org](https://fng.northcountryems.org/) |
| Incident Reports | New, reviewed, last 30 days (type, date, status only, no names) | [reports.northcountryems.org](https://reports.northcountryems.org/) |
| Scheduling | Open shifts in the next 7 and 30 days, minimum staffing shifts (sorted to the top, red when nobody is interested), filled this week, an 8 week filled chart, and who's next up on the long and short lists | [overtime.northcountryems.org](https://overtime.northcountryems.org/) |

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

## Fleet Health (1.27)

The **Fleet Health** button on the Vehicle Checks card (1.27.1, where the EP Checker button was) opens the **Fleet Health** page, and so does a button at the top of the vehicle sheet. "Open vehicles" opens the vehicle sheet as before. In 1.27 "Open vehicles" opened the page (full screen, "&#8592; CG Staff" to go back). Also opens from cgstaff.northcountryems.org/#fleet (the EP Checker's i links there for CG Staff). Data comes from the ncems-checks Worker 1.3 (`/fleet/summary`, admins and readers only) plus Derek's schedule, which the Worker saves every hour.

- Range: Today, Last 7 days (default), 14 days, **Month in review** (calendar month with arrows for earlier months; 1.28) or Custom (up to 92 days). Check days run 0730 to 0730
- **Counting starts Fri 10/23/2026** (1.28, Doug): nothing before that shows or counts, so test days don't drag the numbers down. Nothing was deleted; change `FH_START` in index.html to move it
- Top numbers: ambulance rig days checked (75% or more counts), other units due and checked, crew days with every rig checked, open problems, out of service
- Every rig, every day grid (green checked, yellow partial, red missed, brown out of service, blank not due) and a bar chart of ambulances checked each day
- Problems by rig, with a button to the old vehicle sheet for Fixed and out of service (that sheet is also the new **Problems** button on the card)
- Crews: who was on each crew from the schedule, the rigs, and a dot for each person (green signed in and checked, yellow signed in only, red did not sign in). The whole crew gets credit for a done day
- Providers: everyone on the schedule except CG Staff, with Shift compliance (crew got it done) and Hands on (they checked themselves) for the last 30 days, and a strip of their last 30 days of shifts. Tap a column title to sort, Find to search
- Weekly report (copy or print) and Export CSV
- The Vehicle Checks card title now reads like "Sun Oct 25 · Ambulances 2/4 · Other units 1/2" and shows who signed in to the Checker today
- Demo: ?demo=1#fleet shows sample data without signing in

## Who gets in

Emails in `CONFIG.staff`: Doug, Derek, Dennis, Bryce, Chuck, Nick, K. Reid. Anyone else who signs in sees "CG Staff only" and a link to the hub. Each person also needs access to the CG Staff and Facilities and Grounds SharePoint sites for numbers to load.

## Where the data lives

- **Shift Ops:** "Shift Ops" SharePoint list in the CG Staff team. Fed by the Claude email sweep (every 4 hours) through the "Shift Ops Drop (do not delete)" folder and the Power Automate flows "Shift Ops: drop folder to list" and "Shift Ops: completed stamp". The list also has `Triage` (Choice: Red, Yellow, Green) and `Briefing` (Yes/No) columns, added for v1.2. If they're ever missing, the app still works but triage and flags show a note instead of saving.
- **Facilities / Grounds:** Facility Work Orders, Facility Services and Grounds Tracker lists on the Facilities and Grounds site (same data as the F&G app, read only here).
- **Vehicle Checks (1.19):** the `ncems-checks` Worker on Doug's NCEMS Cloudflare, `https://ncems-checks.d-boyce.workers.dev` (D1 database `ncems-checks-db`, photos in R2 `ncems-check-photos`). Same lists as before (checks, vehicleStatus, vehicleResolved, vehicleLinks). Older notes: it used to be Firebase project `ncems-hub-9111d`. Since 1.6, `vehicleLinks/{check ref}` holds the link between a vehicle issue and its Shift Ops card (card id, status, latest note) so the EP Checker can show the chiefs' latest note to crews. The EP Checker (v2.14.0 and up) writes one doc per submitted check to `vehicleChecks`. Out of service marks go to `vehicleStatus`, Fixed marks go to `vehicleResolved`. The dashboard reads the last 45 days.
- **Vehicle check records on SharePoint (1.18):** every check, with its photos, is copied to the CG Staff site under `App Data/Vehicle Checks/YYYY-MM/` as a text file named `YYYY-MM-DD HHMM UNIT (Crew).txt` (unit, crew, fuel, DEF, O2, mileage, problems, narc counts, section notes, photo list, full check detail and the raw data for reports). Photos go to `App Data/Vehicle Checks/YYYY-MM/Photos/`. Crew phones can't write to this site, so CG Staff does it in the background whenever a chief has it open, up to 40 checks per refresh, skipping files already there. Photos are downloaded from Cloudinary in the browser; if one can't be copied, the text file says so and keeps the original link. This is the stopgap until the Cloudflare nightly copy (claude/firebase-to-cloudflare-plan.md step 6)
- **Incident Reports:** Cloudflare Worker `ncems-api.d-boyce.workers.dev/bin/incident-reports`, read only. Since v1.3 the dashboard sends the Microsoft sign-in token, and the Worker only answers for chiefs on its ADMINS list.
- **Crews (1.21):** Doug's Worker `ncems-schedule-crews` on the North Country Cloudflare, `https://ncems-schedule-crews.d-boyce.workers.dev/crews`. It holds Doug's key for Derek's Schedule API (`ncems-schedule.d-langdon.workers.dev`) as the secret `NCEMS_SCHEDULE_KEY`, checks the Microsoft ID token (Command Staff app, CG Staff emails only), and hands back only names and seats for M51 to M54, now and next shift. No time off reasons, hours, phones or requests reach the browser. The key is never in this repo. A copy of the key, Derek's prompt and the API Usage Guide are on the CG Staff site under `App Data/Schedule API (Derek)/`. Refreshes every 10 minutes; the Worker only downloads Derek's file again when his `generated_at` changes.
- **Scheduling (1.12):** two of Derek's Worker feeds, Crew 1 `https://ncems-ot.d-langdon.workers.dev/dashboard` and Crew 2 `https://ncems-c2.d-langdon.workers.dev/dashboard`, same ID token, cgstaff site only. Older notes: Derek's Worker feed, `GET https://ncems-ot.d-langdon.workers.dev/dashboard`, read only. CG Staff sends the Microsoft ID token (`Authorization: Bearer <idToken>`), the same way it reads incident reports. Derek's Worker only answers the cgstaff site, NCEMS staff only, no guests. The feed has no start time or position, so shift rows show date, type, unit and how many people are interested.

## Also assigned and reminders (1.9)

Add three columns to the **Shift Ops** list (List settings, Create column). The names must match exactly:

| Column | Type |
|---|---|
| `AlsoAssigned` | Single line of text |
| `RemindOn` | Date and time (date only) |
| `RemindEvery` | Number, 0 decimal places, default 0 |

Until they exist, the card shows the fields greyed out with a note, and everything else works.

**Power Automate flow "Shift Ops: reminders"** (built 10/24/2026 in Doug's Power Automate, Default environment, flow id 8de26877-6ea9-4b3a-b2a2-1728e8e5c6c0, runs as Doug, emails come from Doug's mailbox). Tested 10/24 on SO-016 (Once): email sent, RemindOn cleared, nothing else on the card changed. Scheduled cloud flow, every day at 7:00 AM Pacific:
1. SharePoint **Get items**: site BattalionChiefLocal, list Shift Ops, Filter Query `Status ne 'Completed' and RemindOn le '@{addHours(utcNow(), 12)}'`. The 12 hours matter: the app saves reminder dates at 15:00 UTC, so a plain "now" would skip today's reminders until tomorrow
2. **Apply to each** item:
   - **Compose** (the chief's email): looks up the card's AssignedTo (Doug, Derek, Dennis, Bryce, Tyler, Nick) in a small name to email table. Unassigned or anyone else falls back to Doug
   - Outlook **Send an email (V2)**: To = the email inside AlsoAssigned (`Name <email>`), or the chief if nobody is set. CC = the chief. Subject `Reminder: <ItemID> <Title>`. Body: owner, status, details, the newest note line, and a link to https://cgstaff.northcountryems.org/?view=board
   - SharePoint **Update item**: only Id, Title and RemindOn are filled in. Leave every other field out (Show all fills Category with a default and would overwrite cards). Id and Title from the card, RemindOn moved forward by RemindEvery days (kept at 15:00 UTC like the app does), or cleared when RemindEvery is 0 (Once)

## Changelog

### v1.28.1 (10/25/2026)
- Providers table shows Crew 1 or Crew 2 (the seat from the schedule) instead of Paramedic or EMT. Someone with no scored shift yet gets the seat from today's schedule (Garrett Long showed as Paramedic)

### v1.28 (10/25/2026)
- Fleet Health counts from Fri 10/23 (FH_START); earlier days are left out of every range, the 30 day provider columns, the report and the CSV. Nothing deleted
- New Month in review range (calendar month, previous and next arrows) with a Monthly report; it replaces 30 days. Last 7 days stays the default

### v1.27.1 (10/25/2026)
- Vehicle Checks card: the EP Checker button is now **Fleet Health** (opens the full page). Open vehicles and tapping the card open the vehicle sheet again, and the extra Problems button is gone
- Fleet Health, full page button at the top of the vehicle sheet

### v1.27 (10/25/2026)
- Fleet Health page: Open vehicles on the Vehicle Checks card opens it (also cgstaff.northcountryems.org/#fleet). Range picker, top numbers, every rig every day grid, daily bar chart, problems by rig, crews with who signed in and checked, providers with Shift compliance and Hands on (30 days), weekly report, CSV export
- Vehicle Checks card: title shows today's counts (Ambulances x/y, Other units x/y), a line for who signed in to the EP Checker, and a new Problems button for the old vehicle sheet (Fixed, out of service)
- iPhone status bar meta set to default so the clock shows on the white bar
- Needs ncems-checks Worker 1.3

### v1.26.2
- Dashboard button on the iPhone no longer drops you out of CG Staff to a blank page. It used to "go back" in the browser history, and after a relaunch or a sign in the step back left the app. Now it only steps back over pages CG Staff itself added. Same fix for closing the shift briefing

### v1.26.1
- Home button (house, top left) opens the NCEMS Hub in Safari instead of inside the CG Staff home screen app. On an iPhone, leaving a home screen app for another site showed a blank page and dropped you out of CG Staff. Now CG Staff stays open behind it; switch back with the app switcher

### v1.26
- Shift Briefing Notes on a phone: tapping a group tab (Operations, Chief) no longer snaps the tab row back to the start. The row stays put and slides just enough to keep the tab you picked in view
- Swipe left or right on the board to slide to the next group. The column follows your finger and slides over, with a tick. A short or slow swipe snaps back, and a swipe never opens the card under your finger
- (i) panel has a Haptics check: shows what this phone supports (iOS version) and a Test haptic button

**iPhone haptics checklist:** iOS 18 or newer (Settings, General, About, iOS Version); Settings, Sounds & Haptics, System Haptics on; Settings, Accessibility, Touch, Vibration on. Low Power Mode can mute them. Then open the (i) panel and tap Test haptic.

### v1.25
- The "Set them up now" button for the Also assigned and reminder columns only shows for Doug, the site owner. Everyone else sees "waiting on a one time setup by Doug." Derek hit a No permission error on that button 10/23 because only an owner can add list columns
- The three columns (AlsoAssigned, RemindOn, RemindEvery) were added to the Shift Ops list 10/24, so Also assigned and reminders are on for every chief
- The "Shift Ops: reminders" Power Automate flow was built 10/24 (see Also assigned and reminders above), so reminder emails now go out at 7:00 AM
- One click or tap anywhere on a Shift Briefing Notes card opens it, on a computer too. No more click to preview, then Open card
- Fixed the dark green band at the bottom of the screen on iPhone. The hidden Undo bar and message pop up were parked dark at the bottom edge, so Safari tinted its bottom bar to match and the Undo button peeked out. Both are now fully hidden until they're needed
- Haptics: a light tick when you tap a button, tab or card. Android phones vibrate. iPhones need iOS 18 or newer and System Haptics on (Settings, Sounds & Haptics); Safari has no vibrate, so the app flips a hidden switch, which iOS answers with a tick

### v1.24
- Shift Briefing Notes: every card no one has rated yet shows an amber **Needs triage** tag. Tap the tag (or the dot) to rate it; any CG Staff member can. The first rating adds a note line with who triaged it and when
- Any rated card with no change in 6 or more days shows a blue **Update status · Nd** tag. Tap it to open the card and add a note; any change clears it. The 6 days is `CONFIG.updateDays`
- New order in each column: briefing items, then Red, then Needs triage, then Yellow, then Green, so untouched items sit right under the urgent ones
- Filter row cut to All, Mine and Needs triage (plus search). Getting old, Waiting, Briefing and Red chips are gone: the card colors and the Briefing button already cover those
- Dashboard tile renamed Need triage, amber when above 0. The Red tile opens the whole board (Red items are on top)

### v1.23.1
- New reminder for Dennis and Derek: run the retro personnel notes search with Retro-October-Input-Directions-v2.md from Doug's 10/19 email "Retro personnel notes, plus check out Forms". Open Outlook button, stays until they tap Done

### v1.23
- Reminders at the top of the dashboard, only for the person they're meant for (set in `CONFIG.reminders`):
  - Dennis and Derek: "Upload your forms with Doug's Forms app" with an Open Forms button. Stays until they tap Done
  - Dennis and Derek: "Look over Shift Briefing Notes. Update your items and add anything for shift briefing." Comes back every day at 0600 until they tap Done for today
  - Dennis only: "Update the Facilities and Grounds site" with an Open F&G button. Stays until he taps Done
- Done marks are small text files on the CG Staff site in `App Data/Reminders` (who, when), so they follow the person to any device and Doug can open that folder to see who has done what. To add or change a reminder, edit `CONFIG.reminders` (id, who, once or daily, text, link)
- Vehicle Checks shows the check day's date instead of just "today": the box reads "Ambulances Fri Oct 23", the green banner says "checked Fri Oct 23", and the vehicles screen title has the date. The check day still starts at 0700
- Demo: add `&as=dennis` or `&as=derek` to see the reminders

### v1.22
- Header no longer shows the open count, update time and name under North Country EMS. That line only appears if something goes wrong (it shows "Offline" with the reason), and says Demo in demo mode

### v1.21
- New crews strip at the top of the dashboard: who is on M51, M52, M53 and M54 now and tomorrow, from Derek's Schedule API
- Flips to the new day at 0600. Today's date sits in a big pill next to the crews
- Computer: unit cards across the top, tomorrow on one line under them
- Shows split shifts with times, OPEN in red, and trade, cover and OT tags. "Schedule data as of" time on the strip, yellow when 4 or more days old
- Reads through the new `ncems-schedule-crews` Worker, which keeps the API key off this public repo
- Demo mode has sample crews
- Phone: no swiping. Each ambulance is one tight row, all units on screen at once, with a Today / Tomorrow switch
- New look matched to Derek's Open Shifts app: white header reading **NCEMS CG Staff** | North Country EMS (NCEMS in black, CG Staff in green, a thin line, then North Country EMS in gray), system font, his green #2d6a2d, light green borders, square cornered buttons. The crews strip uses the same look. The tabs and boxes below keep the old style for now. Every NCEMS app gets this header as it's rebuilt

### v1.20.1
- Scheduling: when Derek's feed answers "wrong audience" (it hasn't been given the new app ID yet), the card says that instead of "sign in again"

### v1.20
- Signs in with the new **NCEMS Command Staff** Entra app (`f758d1fe-91b7-4bd5-92a9-1324d8bf0826`). Only the 7 CG Staff are assigned, so Microsoft turns everyone else away before the app loads. Everyone signs in once more after this update
- Scheduling card says so plainly if Derek's Open Shifts feed hasn't accepted the new app yet

### v1.19
- Vehicle Checks moved off Firebase: checks, out of service, Fixed and Shift Ops links all live on the `ncems-checks` Worker (Doug's NCEMS Cloudflare, `https://ncems-checks.d-boyce.workers.dev`), read and written with the Microsoft ID token
- Who can change out of service and links: the Worker's ADMINS and READERS lists (Nick is a reader). Anyone else gets "not on the vehicle checks list"
- The SharePoint copy (App Data/Vehicle Checks) keeps working; photos now come from the Worker
- Firebase history (11 checks, 1 photo, 5 Fixed, 1 out of service, 2 links) was copied to Cloudflare on 10/21 with matching counts

### v1.18
- Photo button. Any vehicle with a photo on today's check gets a "📷 Photo" button joined to its chip. Narc below par rows and issue rows on the dashboard, and issue rows on the vehicle sheet, get the same button when that check has a photo. The issue's own photo (EP Checker 2.22 and up) shows first, then the rest of that check's photos
- Photo viewer opens on top of whatever you're on: big picture, swipe or arrows for more, Full size link, Esc or ✕ to close
- Issue detail has a big "See the photo of this problem" button above the thumbnails, or says "No photo on this check"
- Every check and its photos are saved to the CG Staff SharePoint site, App Data/Vehicle Checks (see Where the data lives)
- Demo (?demo=1): M19 Brake lights has a sample problem photo

### v1.17
- The Shift Briefing Notes tab no longer shows the open count, just the words. The count is still in the header line and the Open tile

### v1.16
- Forms button in the top bar opens NCEMS Forms (forms.northcountryems.org): write ups, quick notes, SOG drafts and personnel search

### v1.15
- The Shift Ops tab and dashboard box are now called Shift Briefing Notes (same board, same SharePoint list)
- Tap anywhere on a dashboard box to open that area: Scheduling opens Open Shifts, Shift Briefing Notes opens the board, Incident Reports opens Reports, Vehicle Checks opens the vehicles page, Grounds and Facilities open Facilities and Grounds. The buttons, number tiles and rows inside each box still go to their own spot

### v1.14
- Sign-in page has a red "CG Staff only" box above the Microsoft button with a Back to the NCEMS Hub button, so crews can leave before trying to sign in (the hub shows the CG Staff button to everyone since hub 2.0)

### v1.13
- New phone icon: NCEMS green and maroon split corner to corner with three crossed bugles, bells down like the division chief collar pin, NCEMS across the bottom (matches the Open Shifts icon). `apple-touch-icon.png` is the new icon and `icon-512.png` is the big one Android uses for the icon and the launch screen. Delete the old icon from the home screen and add it again to see it

### v1.12
- Scheduling card rebuilt for Derek's NCEMS Open Shifts (shifts.northcountryems.org), the app that replaced Overtime. Reads two feeds with the same Microsoft ID token: Crew 1 paramedic overtime (`ncems-ot.d-langdon.workers.dev/dashboard`) and Crew 2 EMT open shifts (`ncems-c2.d-langdon.workers.dev/dashboard`)
- Next up pills open the app straight to the long list or short list
- Big number: shifts left this month, Crew 1 (green) plus Crew 2 (blue)
- Three tiles: Min staffing (red when above 0), Next 7 days, Filled this week. Uses the feeds' own counts and min staffing flags
- Day strip from today to the end of the month: stacked bar per day, Crew 1 green on the bottom, Crew 2 blue on top, red ▲ on any day with a min staffing shift. Tap a day for the count
- Needs attention: top 4 open shifts from both crews, min staffing first then soonest, with a C1 or C2 chip, interest (Crew 1) or offers (Crew 2), and today / tomorrow / in N days. Tapping opens Open Shifts
- Buttons: Open Shifts (replaces Open OT) and Open Aladtec
- The feeds refresh every 5 minutes. If one crew's feed fails, the other still shows with a note, and the missing crew shows ? instead of a fake 0
- Dates are handled as Pacific calendar days, never shifted by time zone

### v1.11
- The number tiles click through too: Shift Ops Open (board), Briefing (opens the Briefing), Red (board showing Red only), Not triaged (board filtered); Vehicle Checks tiles open the vehicles screen or the issue list; Scheduling tiles open OT; Facilities, Grounds and Incident Reports tiles open their apps
- New Red filter on the board

### v1.10
- Every row on the dashboard opens what it's about: Shift Ops rows open the card, vehicle rows open that issue (like M19 Compartment 2: Hurst battery), short narcs open the rig, Facilities, Grounds, Incident Reports and open shifts open their apps
- Scheduling card has two buttons: Open OT and Open Aladtec (secure2.aladtec.com/northcountryems)
- Also assigned searches your Microsoft people as you type (needs People.Read, Microsoft asks once). The fixed list still works without it
- If the Shift Ops list doesn't have the AlsoAssigned, RemindOn and RemindEvery columns yet, the card shows a "Set them up now" button that adds them (site owner, so Doug)
- Take it now says what it does: makes you the chief / owner of the card

### v1.9
- Dashboard order: Scheduling, Shift Ops, Incident Reports on top; Vehicle Checks, Grounds, Facilities below (3 across on a computer, 2 on a tablet, 1 on a phone)
- Scheduling card: who's next on the long list and short list sits at the top as big name pills (tap opens scheduling). The 8 week chart is gone
- Shift Ops cards and vehicle issues: big "Yes, save changes" box at the bottom. Complete and Fixed are smaller, need two taps, and give 6 seconds to Undo before anything saves. Completed cards are still under Done this week with Reopen
- Also assigned to: hand any card or vehicle issue to someone besides the group's chief (type a name, like Stephen Schutts; the chiefs, Chuck, Stephen, Nick and Tyler are suggested)
- Email reminders: pick a date and Once, Every day, Every 3 days or Every week. A Power Automate flow sends them (setup below)
- Back button from the Briefing or the board goes to the dashboard, not out of the app
- Sign in once: the hub passes who you are, CG Staff tries a quiet sign in, then one hop through Microsoft without typing if you're already signed in. Links from CG Staff to Facilities and Grounds, Overtime and the hub pass it along too

### v1.8
- Vehicle Checks card flags any narc below par on today's latest check (red at half par or less, amber otherwise). Before, short narcs only showed in the Briefing and the rig detail

### v1.7
- Scheduling section now shows live numbers from Derek's overtime app: open shifts, minimum staffing, filled this week, 8 week chart, next up
- Demo has sample scheduling data

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
