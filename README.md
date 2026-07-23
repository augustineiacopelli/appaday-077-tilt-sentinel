# AppADay 077 — Tilt Sentinel

Turn a Tilt hydrometer's Google Sheet into a live fermentation dashboard: current gravity and temperature, a dual-axis chart, and computed OG, attenuation, ABV, and days fermenting with comment markers. Track multiple batches and get phone alerts for stalls, temp swings, and stale readings.

**Category:** Data & Dashboards (D)
**Shipped:** 2026-07-23
**Live:** https://augustineiacopelli.github.io/appaday-077-tilt-sentinel/

## What it does

A Tilt hydrometer floats in the fermenter and logs specific gravity and temperature to a Google Sheet, typically one sheet per brew session. The stock sheet gives you raw rows and a rough graph. Tilt Sentinel reads that same sheet and rebuilds it into a dashboard: current gravity and temperature at a glance, a dual-axis chart of gravity against temperature over the whole fermentation, and the numbers that actually tell you how the batch is going, including apparent attenuation, estimated ABV, and days fermenting. Comments logged from the Tilt app appear as tappable markers on the timeline. You can set the original gravity by hand and add an optional target final gravity, and you can register several batches and switch between them.

## How to use

1. In Google Sheets, share the Tilt sheet as "Anyone with the link can view."
2. Open the app in a normal browser tab and paste the sheet's share link, or just its ID.
3. Set the original gravity and, if you want stall detection, a target final gravity.
4. Leave the tab open near the fermenter for live monitoring, or tap Check Now whenever you want a fresh read.

## Alerts

While the page is open, an alert engine watches for four conditions: no new reading within a set window, temperature outside a range you choose, a rapid temperature swing, and a possible stall when gravity stays flat for a day while still above target. A tripped alert is logged, shown as a toast, and pushed to your phone through ntfy.sh, a free notification app that needs no account, just a topic name you pick.

## Notes

Single-file vanilla HTML, CSS, and JavaScript with no build step and no backend. The sheet is read through Google's gviz endpoint using a script-tag request, so no API key and no server are involved, which is also why the sheet must stay shared as "Anyone with the link can view." Because there is no backend, live monitoring only runs while the page is open somewhere. For alerts that fire even when nothing is open, the durable path is a Google Apps Script time-driven trigger bound to the sheet itself, which runs on Google's servers and pushes the same notifications.

Part of AppADay, one app shipped every day: https://augustineiacopelli.github.io/appaday/
