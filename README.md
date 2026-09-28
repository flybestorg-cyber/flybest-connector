# AI Travel Booking System — FlyBest hotel booking connector for Claude & ChatGPT (MCP)

**Search and book hotels with your AI assistant.** FlyBest is an AI travel booking
connector built on the [Model Context Protocol](https://modelcontextprotocol.io): add one
URL to Claude or ChatGPT and your assistant can check live hotel availability and rates,
show hotel details and programme perks, create a secure one-time payment page, and manage
your bookings — through a licensed travel agency's reservation system (Sabre). No separate app
and no password: you connect from your AI client and verify your e-mail. Free to use; you pay only
the hotel.

> Keywords: AI travel booking · AI hotel booking · hotel booking agent · travel agent AI ·
> MCP server · Claude connector · ChatGPT app · Sabre GDS · luxury travel · preferred-partner perks

**In the Claude directory:** open Claude → Customize → Connectors and search **FlyBest**, or open
https://claude.ai/directory/connectors/flybest while signed in to Claude, and click *Connect*. (The plugin
bundle in this repository is a separate submission and is not listed yet.)

### What a rate looks like with the benefits attached

Illustrative example, not a live quote:

```
Hotel The Mitsui Kyoto, 12–15 Nov 2026, 2 adults

[Partner]   Deluxe Room, King · JPY 898,150 for the stay (tax-in) · free cancellation until 5 Nov
            includes: daily breakfast for two · USD 100 hotel credit · upgrade on arrival (subject
            to availability) · early check-in / late check-out · welcome amenity
[Public]    Deluxe Room, King · JPY 898,150 for the stay (tax-in) · free cancellation until 5 Nov
            includes: —
```

Same room, same price in this example, and one of them comes with the extras. A programme rate
can also cost more or less than the public rate, so the assistant shows both side by side; only
the benefits confirmed for the rate you choose apply, and upgrades and early or late times depend
on availability on the day.


## What it is

A remote MCP connector for hotel search and booking. Hotels only. No password: you sign up
with your e-mail, and your card is entered on a one-time payment page at ai.flybest.org,
never in the chat.

**Connector URL:** `https://ai.flybest.org/mcp`

## Why I built it

I am a travel advisor. The slowest part of the job was asking hotels, one by one, whether a
rate includes breakfast, whether there is a credit, whether an upgrade is possible, and until
when it can be cancelled. A client says "have a look for me" and I disappear for an hour. So I
handed that work to the assistant: it looks, it explains, and when you have chosen, it books.

## How it differs from other AI travel tools

| | Typical AI assistant / travel AI | FlyBest |
|---|---|---|
| Where prices come from | Usually web search or a third-party feed | Live inventory and rates from the agency's reservation system |
| Can it book? | Usually sends you to a booking site | Books the room, in your name, with the hotel |
| Benefits | Usually cannot show agency-channel benefits | Benefits listed next to each rate, side by side with the public rate |
| Cancellation terms | You read the fine print | Written out in plain words: free until when, deposit, non-refundable flagged |
| After booking | Varies | See and cancel your own bookings in the conversation |

## Why book through FlyBest instead of direct

The rates come from the hotel's own inventory. Programme rates are often the same price as
booking direct, sometimes not, which is why the assistant shows them next to the public rate.
Many come through the agency's **preferred-partner programmes**, which add benefits the hotel
does not normally give guests who book direct. Typical inclusions on those rates:

- **Daily breakfast for two**
- **A property credit** (commonly US$100 per stay, for dining or spa) where the hotel offers one — the exact credit is confirmed by the agency at booking
- **Room upgrade on arrival**, subject to availability
- **Early check-in and late check-out**, subject to availability
- **A welcome amenity**, and often VIP recognition on file

Programmes the agency holds include **Four Seasons Preferred Partner**,
**Rosewood Elite**, **Mandarin Oriental Fan Club**, **Peninsula PenClub**, **Belmond
Bellini Club**, **Dorchester Collection Diamond Club**, **Maybourne Exclusive**, **Hyatt
Privé**, **Hilton for Luxury (Waldorf Astoria, Conrad, LXR)**, **IHG Destined
(InterContinental, Six Senses, Kimpton)**, **Accor Preferred (Sofitel, Fairmont, Raffles)**,
**Shangri-La Luxury Circle**, **Small Luxury Hotels "Within"**, **Preferred Platinum
Partner**, **Kempinski Club 1897**, **Langham Couture**, **Rocco Forte Knights**, and
**Jumeirah**. Programme membership changes over time and not every hotel in a brand takes part.
When a rate carries these benefits your assistant shows them next to the price, so you can
compare a programme rate with the public one side by side; the benefits apply only to the rate
you select and are confirmed by the hotel at booking.

Plus: a licensed agency behind every booking (Coastline Travel Advisors), the booking is
in your name with the hotel, and you can see and cancel it from the assistant.

## Connect

### Claude (claude.ai / Claude Desktop)
1. Settings → Connectors → **Add custom connector**.
2. Name: `FlyBest`, URL: `https://ai.flybest.org/mcp`. Save.
3. Click **Connect**. On the page that opens choose **Sign up with your e-mail**,
   enter your address, type the 6-digit code from the e-mail. Done.

### ChatGPT (web, developer mode)
1. Settings → Security and login → enable **Developer mode**.
2. Add a custom MCP server: URL `https://ai.flybest.org/mcp`, authentication: OAuth. Save and connect.
3. Same e-mail sign-in page as above.

ChatGPT support is experimental: custom connectors are a ChatGPT web feature (developer mode),
availability depends on your account and workspace settings, and FlyBest has not yet completed
end-to-end testing on a real ChatGPT account. The mobile apps are not verified.

### Other MCP clients
Any client that speaks Streamable HTTP with OAuth 2.1 (dynamic client registration
is supported). Point it at the URL above.

## What you can ask

- "Find me a hotel in Kyoto for 12–15 November, two adults, near Gion."
- "Show the rates for the Park Hyatt with breakfast, and what the cancellation terms are."
- "Book the flexible rate under my name — here's my e-mail."
  → you get a one-time payment link; the booking is made when you submit it.
- "Show my bookings." / "Cancel my Kyoto booking."

## Install as a Claude plugin (once listed)

This repository is also a **Claude plugin bundle**: it references the connector and
ships the `flybest-hotels` skill, so Claude gets the house rules (what to check before
booking, how deposits and cancellation terms work, what it must never do) automatically.
Once listed, add it from **Customize → Plugins** in Claude; in Claude Code:

```bash
claude plugin add flybestorg-cyber/flybest-connector
```

Using ChatGPT or another client? The connector sends its core booking rules as server
instructions when you connect (this skill is the fuller version), and you can paste
`skills/flybest-hotels/SKILL.md` into a project or custom instructions. Either way, check the
payment page and the booking confirmation yourself.

## How booking works

1. The assistant asks the connector for a **payment page** for the room you chose.
2. You open the page, read the price, deposit and cancellation terms written out in
   full, **tick the box**, and enter your card. You enter the card only on that page,
   operated by FlyBest at ai.flybest.org; the details are sent to the hotel reservation
   system (Sabre) to make the booking. FlyBest keeps the last four digits, the terms you
   ticked and when you ticked them. Card details are never part of what the assistant
   sends or receives, so never type them in the chat.
3. The hotel confirms; you get a confirmation number in the chat and the agency gets
   a copy of the booking. If the hotel's price at booking differs from the figure on
   the page, the booking is not made and you can ask for a new page. If the page
   reports that the hotel could not confirm, or the outcome is unclear, e-mail
   flybestorg@gmail.com with the booking reference before trying again.

Some rates take a deposit at booking or are non-refundable. The page says so in
plain words before you tick; nothing is charged until you do.

## Limits

Each public connection allows up to 800 searches, 60 payment links and 60 cancellation
requests per day (reset at 00:00 UTC), to keep the reservation system fair for everyone. The
assistant tells you when you hit a limit. If a limit stops you from managing a time-sensitive
booking, e-mail flybestorg@gmail.com with the booking reference; hotel cancellation deadlines
still apply.

## Terms, privacy, security

- [Terms of use](https://ai.flybest.org/terms) · [Privacy notice](https://ai.flybest.org/privacy)
- Bookings, cancellations the assistant could not complete, charges, privacy requests:
  **flybestorg@gmail.com** with your booking reference (never card details). One advisor,
  Pacific time; replies usually within one business day.
- Found a security problem? See [SECURITY.md](SECURITY.md).

## Who runs this

FlyBest (flybest.org) — an independent luxury travel advisor based in California, USA,
affiliated with Coastline Travel Advisors, a licensed host travel agency. FlyBest operates this
connector and is responsible for its signup and booking data; hotel bookings are placed through
Coastline's reservation system on its accreditation. The connector is free to use; you pay only
the hotel. Contact: flybestorg@gmail.com.

This repository holds the public documentation and the assistant skill. The connector's
server code is not published.
