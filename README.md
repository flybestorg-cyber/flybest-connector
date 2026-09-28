# AI Travel Booking System — FlyBest hotel booking connector for Claude & ChatGPT (MCP)

**Search and book hotels with your AI assistant.** FlyBest is an AI travel booking
connector built on the [Model Context Protocol](https://modelcontextprotocol.io): add one
URL to Claude or ChatGPT and your assistant can check live hotel availability and rates,
show hotel details and programme perks, create a secure one-time payment page, and manage
your bookings — through a licensed travel agency's reservation system (Sabre). No app to
install, no account to manage, free to use.

> Keywords: AI travel booking · AI hotel booking · hotel booking agent · travel agent AI ·
> MCP server · Claude connector · ChatGPT app · Sabre GDS · luxury travel · Virtuoso perks

**Now in the Claude directory:** open Claude → Customize → Connectors, search **FlyBest**, or go to
https://claude.ai/directory/connectors/flybest and click *Connect*.

### What a rate looks like with the benefits attached

```
Hotel The Mitsui Kyoto, 12–15 Nov, 2 adults

[Virtuoso]  Deluxe Room, King · JPY 898,150 for the stay (tax-in) · free cancellation until 5 Nov
            includes: daily breakfast for two · USD 100 hotel credit · upgrade on arrival (subject
            to availability) · early check-in / late check-out · welcome amenity
[Public]    Deluxe Room, King · JPY 898,150 for the stay (tax-in) · free cancellation until 5 Nov
            includes: —
```

Same room, same price, one of them comes with the extras. That is the point of booking
through a preferred-partner agency, and the assistant shows it every time.


## What it is

A remote MCP connector for hotel search and booking. Hotels only. No account, no password:
you sign up with your e-mail, and your card is entered on a one-time page the
assistant never sees.

**Connector URL:** `https://ai.flybest.org/mcp`

## Why book through FlyBest instead of direct

The rates are the hotel's own rates — usually the same price you would pay booking
direct — but many of them come through the agency's **preferred-partner programmes**,
which add benefits the hotel does not give walk-up guests. Typical inclusions on those
rates:

- **Daily breakfast for two**
- **A property credit** (commonly US$100 per stay, for dining or spa) where the hotel offers one — the exact credit is confirmed by the agency at booking
- **Room upgrade on arrival**, subject to availability
- **Early check-in and late check-out**, subject to availability
- **A welcome amenity**, and often VIP recognition on file

Programmes the agency holds include **Virtuoso**, **Four Seasons Preferred Partner**,
**Rosewood Elite**, **Mandarin Oriental Fan Club**, **Peninsula PenClub**, **Belmond
Bellini Club**, **Dorchester Collection Diamond Club**, **Maybourne Exclusive**, **Hyatt
Privé**, **Hilton for Luxury (Waldorf Astoria, Conrad, LXR)**, **IHG Destined
(InterContinental, Six Senses, Kimpton)**, **Accor Preferred (Sofitel, Fairmont, Raffles)**,
**Shangri-La Luxury Circle**, **Small Luxury Hotels "Within"**, **Preferred Platinum
Partner**, **Kempinski Club 1897**, **Langham Couture**, **Rocco Forte Knights**, and
**Jumeirah**. When a rate carries these benefits your assistant shows them next to the
price, so you can compare a programme rate with the public one side by side.

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
3. Same e-mail sign-in page as above. Custom connectors are a ChatGPT web feature for now; the mobile apps may not show them.

### Other MCP clients
Any client that speaks Streamable HTTP with OAuth 2.1 (dynamic client registration
is supported). Point it at the URL above.

## What you can ask

- "Find me a hotel in Kyoto for 12–15 November, two adults, near Gion."
- "Show the rates for the Park Hyatt with breakfast, and what the cancellation terms are."
- "Book the flexible rate under my name — here's my e-mail and phone."
  → you get a one-time payment link; the booking is made when you submit it.
- "Show my bookings." / "Cancel my Kyoto booking."

## Install as a Claude plugin (recommended)

This repository is also a **Claude plugin bundle**: it references the connector and
ships the `flybest-hotels` skill, so Claude gets the house rules (what to check before
booking, how deposits and cancellation terms work, what it must never do) automatically.
Once listed, add it from **Customize → Plugins** in Claude; in Claude Code:

```bash
claude plugin add flybestorg-cyber/flybest-connector
```

Using ChatGPT or another client? The connector sends the same rules as server
instructions when you connect, and you can paste `skills/flybest-hotels/SKILL.md` into
a project or custom instructions.

## How booking works

1. The assistant asks the connector for a **payment page** for the room you chose.
2. You open the page, read the price, deposit and cancellation terms written out in
   full, **tick the box**, and enter your card. The card goes straight to the hotel's
   reservation system; the assistant, the chat provider and this connector never see
   it (only the last four digits are kept).
3. The hotel confirms; you get a confirmation number in the chat and the agency gets
   a copy of the booking.

Some rates take a deposit at booking or are non-refundable. The page says so in
plain words before you tick; nothing is charged until you do.

## Limits

Each connection has a daily allowance (searches, payment links, cancellations) to
keep the reservation system fair for everyone. The assistant tells you when you hit it.

## Terms, privacy, security

- [Terms of use](https://ai.flybest.org/terms) · [Privacy notice](https://ai.flybest.org/privacy)
- Found a security problem? See [SECURITY.md](SECURITY.md).

## Who runs this

FlyBest (flybest.org) — an independent luxury travel advisor affiliated with Coastline
Travel Advisors, a licensed host travel agency. Hotel bookings are placed through Coastline's
reservation system on its accreditation. The connector is free to use; you pay only the hotel.

This repository holds the public documentation and the assistant skill. The connector's
server code is not published.
