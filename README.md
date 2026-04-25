# Torn Travel Tracker

A small browser-based dashboard for foreign-shop merching in [Torn City](https://www.torn.com). Built for two people, runs anywhere, requires nothing but a Torn API key and a static host.

> *For Hunka & PlyBur — running the routes since 2026.*

---

## What it does

**Live stock.** Reads foreign-shop inventory from the [YATA](https://yata.yt) crowd-sourced database and cross-references it against Torn's market prices to show you, in one table: where things are in stock right now, what they cost to buy, what they sell for, and what your $/hr would be on the round trip. Sortable by profit, stock level, country.

**Traders.** Your own private little black book. Add traders by pasting their Torn profile URL — the tool looks up their username via the Torn API and stores them with your tags, notes, and what they're known to buy. One click to view their TornExchange price list or their Torn profile. A "Check status" button shows who's online, idle, in hospital, abroad, or in the federal pen — so you don't waste time pinging someone who can't trade.

**Shit list.** A running record of buy-muggers, ghosts, and other unsavory characters. Anyone added to "Our traders" gets cross-referenced against this list — you'll get a warning before adding someone who's already burned one of you, and a red flag appears next to their name if they show up in TornExchange's top-30.

**Collections.** Tracks both the Plushie set (13 items) and the Exotic Flower set (11 items) for the Museum exchange. Shows what each of you has in inventory, side-by-side, with a "where to find it now" hint pulled from YATA for anything you're missing. Refreshing your inventory pushes to the shared cloud so your partner sees it too.

---

## Getting started

### 1. Get a Torn API key

In Torn, go to **Settings → API Key**. A *Public*-level key is enough. Copy the 16-character string.

### 2. Open the tracker

Visit the deployed page (whoever set this up will have the URL). Go to **Settings**, paste your API key, click **Save & test**. If it greens up, you're good.

### 3. Hook up the shared lists

In Settings, under **Shared lists (JSONBin)**, paste the Bin ID and Master Key. *Ask Hunka for the secret digits.*

That's it. You and your partner now share a trader directory, a shit list, and your inventory snapshots.

---

## How the data flows

```
                ┌─────────────────────┐
                │   Your browser      │
                │   (this tracker)    │
                └──────────┬──────────┘
                           │
        ┌──────────────────┼──────────────────┐
        ▼                  ▼                  ▼
  ┌──────────┐      ┌──────────┐      ┌──────────┐
  │   YATA   │      │ Torn API │      │ JSONBin  │
  │ (stock)  │      │ (prices, │      │ (shared  │
  │          │      │ traders, │      │  lists,  │
  │          │      │ inventory)│     │ inventory)│
  └──────────┘      └──────────┘      └──────────┘
```

Nothing is stored on a server we don't trust. YATA gives us crowd-sourced foreign stock (the same data TornPDA, TornTools, and torntravel use). The Torn API gives us prices, identities, online status, and your inventory — using your key. JSONBin is a tiny free-tier cloud database where the shared trader list, shit list, and inventory snapshots live — only people with the Master Key can read or write.

Your settings, API key, and a copy of all the shared data live in your browser's localStorage. If you clear your browser, you'll need to re-paste the API key and JSONBin credentials, but the shared list itself is safe in the cloud.

---

## Etiquette

- **YATA caches for 5 minutes** to respect their 10-call-per-hour rate limit. If the chip says "stale," it's still showing you the last good data — clicking refresh hits YATA again only after 5 min.
- **Torn API rate limit is 100/min**. Checking 20 trader statuses is one round-trip per trader; refreshing inventory is one call. You'd need to be hammering the buttons to hit the cap.
- **JSONBin free tier is 10,000 requests/month**. Two people doing normal usage uses a few hundred at most. Don't share the Master Key with anyone you wouldn't trust with a full-load camel haul.

---

## Known limits

- Foreign stock is only as fresh as the most recent traveler's contribution to YATA. If nobody has landed in Switzerland recently, the Switzerland numbers are stale. This is a constraint of the data source, not the tool.
- The TornExchange top-30 list is a static snapshot — trade counts will drift over time. Refresh by editing the file.
- Online-status detection uses Torn's `last_action.status` field, which can lag by a minute or two. Treat "Online" as "probably reachable" rather than "definitely at the keyboard right now."

---

## Stack

Pure single-file HTML — no build step, no dependencies, no framework. Drop into any static host (GitHub Pages works great). Edit in the browser, commit, push, refresh — that's the whole development loop.

---

## License

Personal use. Don't sell it. Don't claim you wrote it. If it's useful to you, that's enough.

---

*Wheels up.*
