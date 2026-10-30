# SyncTime

SyncTime is a responsive, browser-only meeting planner for distributed teams. It compares a selected New York meeting time with local times in a customizable set of cities and marks each city as within or outside the 9:00 AM–5:00 PM workday.

## Run it

Open `index.html` in a modern browser. No build step, install, API key, or network connection is required for the planner. Google Fonts are an optional visual enhancement; the app falls back to system sans-serif fonts if they are unavailable.

## What is included

- Responsive desktop and mobile layouts
- Date picker and 15-minute meeting-time slider
- One-tap date choices for today, tomorrow, and the day after tomorrow, plus calendar dates up to one year ahead
- Live local time, weekday/date, and UTC offset for each city
- Searchable city picker, remove and reset controls
- Working-hour overlap timeline and team summary
- Copyable meeting details
- Local persistence of the selected team with `localStorage`
- Slate 900 canvas, Slate 800 surfaces, Slate 700 borders, Slate 50 primary text, Slate 400 secondary text, and the specified Amber 400 active badge palette
- Browser-native `Intl.DateTimeFormat` and IANA time-zone rules for date-aware daylight-saving conversions

## Architecture

This project deliberately has no application server or API. Time conversion, rendering, and saved preferences all run in the browser, which matches the problem statement and avoids maintaining a database for a personal planner. The front end is plain HTML, CSS, and JavaScript. A production team version could add accounts, shared team links, and server-side team preferences if those become product requirements.

## Interview walkthrough

1. Start with `app.js` and the `CITIES` catalog.
2. Explain that a wall-clock time is a different value from an instant. `instantAtMinute` uses the browser's IANA rules to map the selected New York wall time to an instant, and `partsAt` formats that instant in each city's zone.
3. Show how `render` updates the cards and summary from that single instant.
4. Show `drawTimeline`, which samples the day in 15-minute increments to reveal hours when the whole team or part of the team is available.
5. Demonstrate adding a city, changing the date, removing a city, and copying the proposed times.

The chosen meeting anchor is New York. For production scheduling, be aware that a wall time can be ambiguous or nonexistent during the local daylight-saving clock change; a user-facing calendar should explain that edge case explicitly.
