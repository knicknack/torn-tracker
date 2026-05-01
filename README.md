# torn-travel-tracker

A single-file browser tool for foreign-shop merching in Torn City. No server, no install, no nonsense — just open the HTML file and go.

Built for two people. If you're not one of them, hello, and good luck.

---

## What it does

- **Live stock** — pulls current foreign shop inventory from YATA, with Torn API market prices layered on top. Sort by profit per hour, filter by country, click a country to open a trip plan.
- **Trip planner** — greedy-fills your slots (paid + flower bonus) with the best available items and tells you exactly what to bring and how much cash to carry.
- **Restock timer** — plug in an estimated restock time, get a departure time. Treat YATA's estimates with appropriate skepticism.
- **Traders** — your personal rolodex of reliable buyers, with direct links to their TornExchange price pages.
- **Shit list** — people who have earned a permanent note in this tool. You know who you are.
- **Collections** — track your plushie and flower museum sets across both accounts.
- **Logbook** — shared field notes, stamped with location and time.

---

## Setup

### 1. Torn API key
Go to `torn.com` → Settings → API Key. Public access level is enough. Paste it in the Settings tab. Required for market prices, item names, and trader lookups.

### 2. Shared data (JSONBin)
The traders list, shit list, collections, and logbook sync between both accounts via JSONBin. Ask Hunka for the secret codes. Paste the Bin ID and Master Key in the Settings tab and hit Save & test.

### 3. Travel preferences
Set your travel method (PI + airstrip), paid slots, and flower bonus slots in Settings. These drive all the trip plan calculations.

---

## Data sources

| Source | Used for |
|---|---|
| [YATA](https://yata.yt) | Foreign shop stock data |
| [Torn API](https://api.torn.com) | Item names, market prices, trader lookups |
| [TornExchange](https://tornexchange.com) | Trader price pages (linked, not scraped) |

---

## Known limitations

- **YATA restock times are fiction.** Treat them as a loose suggestion. The tool will tell you when to leave; the fossils may or may not agree.
- **Market prices are rolling averages.** Good enough for rough math. For actual selling, check your traders on TornExchange like a grown-up.
- **No real-time stock.** YATA data is crowd-sourced and cached. If twelve people just cleaned out Argentina, you won't know until you land.
- **JSONBin is not Fort Knox.** Don't put anything in the logbook you wouldn't want on a sticky note.
- **Trader online status was removed** because it was wrong more often than it was right.

---

## Notes

Everything runs locally in your browser. The only external calls are to YATA, the Torn API, and JSONBin. Nothing is tracked, logged, or phoned home. The HTML file is the whole app.
