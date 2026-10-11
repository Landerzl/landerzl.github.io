---
layout: page
title: Focus Up
description: A browser extension and Windows companion for distraction-free work sessions, with a session timer, rest breaks and a calendar.
img: assets/img/cards/focus_up.png
importance: 6
category: non-scientific
github: https://github.com/Landerzl/focus-up
---

<style>
  article p,
  article li,
  .caption {
    text-align: justify;
    hyphens: auto;
  }
</style>

<p style="font-size: 1.1rem">
  <a href="https://github.com/Landerzl/focus-up" target="_blank" rel="noopener"><i class="fa-brands fa-github"></i> <b>Code</b></a>
</p>

I built Focus Up because I wanted a focus mode that actually holds: three tabs, no notifications, and a record of where my time went. It is a Brave/Chromium extension plus an optional Windows companion and desktop app.

## What it does

- **A locked focus window.** Starting a session moves three chosen tabs (Research, Work, Music) into a new window. New tabs and windows close immediately, distraction sites are blocked, the music slot only accepts music sites, and clicking into another browser window snaps focus back. Other apps, like Discord, stay usable.
- **No notifications.** Through a small Windows companion, Windows notification banners are switched off for the duration of the session and restored afterwards, and apps on a blocklist are closed politely.
- **Rest breaks.** By default, after 50 minutes of focus the session pauses itself for 10 minutes, with a longer rest every fourth break. Rest time does not count as focus.
- **Calendar and projects.** Finished sessions go into a month heat-map with weekly stats and streaks, and can be assigned to projects and subprojects with running totals.
- **Ending early has a cost.** If a session had a planned length, ending before it requires typing "I am choosing to end my focus early", and the session is flagged.
- **Sync across computers** through the user's own Supabase project, with row-level security, so the data stays in an account they control.

<div class="row mt-3">
  <div class="col-sm-3 mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/focus-up/popup.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
  <div class="col-sm-9 mt-3 mt-md-0">
    {% include figure.liquid loading="eager" path="assets/img/focus-up/dashboard.png" class="img-fluid rounded z-depth-1" zoomable=true %}
  </div>
</div>
<div class="caption">
  Left: the popup that starts a session. Right: the dashboard with weekly stats and the calendar heat-map (demo data).
</div>

## How it is built

The extension (Manifest V3, plain JavaScript) owns the session and enforces the rules. A Python companion, started by the browser through Native Messaging, handles what an extension cannot do: switching off Windows notifications and closing apps. A desktop app in Python and tkinter mirrors the live session and the calendar, and talks to the companion over a local socket with an HMAC handshake.

Status: the extension works. The companion and desktop app are built and their parts are tested; the full browser-to-desktop chain still has to be run end to end.
