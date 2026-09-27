# AI Travel Booking System — FlyBest hotel booking connector for Claude & ChatGPT (MCP)

**Search and book hotels with your AI assistant.** FlyBest is an AI travel booking
connector built on the [Model Context Protocol](https://modelcontextprotocol.io): add one
URL to Claude or ChatGPT and your assistant can check live hotel availability and rates,
show hotel details and programme perks, create a secure one-time payment page, and manage
your bookings — through a licensed travel agency's reservation system (Sabre). No app to
install, no account to manage, free to use.

> Keywords: AI travel booking · AI hotel booking · hotel booking agent · travel agent AI ·
> MCP server · Claude connector · ChatGPT app · Sabre GDS · luxury travel · Virtuoso perks


## What it is

A remote MCP connector for hotel search and booking. Hotels only. No account, no password:
you sign up with your e-mail, and your card is entered on a one-time page the
assistant never sees.

**Connector URL:** `https://ai.flybest.org/mcp`

## Connect

### Claude (claude.ai / Claude Desktop)
1. Settings → Connectors → **Add custom connector**.
2. Name: `FlyBest`, URL: `https://ai.flybest.org/mcp`. Save.
3. Click **Connect**. On the page that opens choose **Sign up with your e-mail**,
   enter your address, type the 6-digit code from the e-mail. Done.

### ChatGPT
1. Settings → Connectors (or Apps) → **Create** / add a custom MCP server.
2. URL: `https://ai.flybest.org/mcp`, authentication: OAuth. Save and connect.
3. Same e-mail signup page as above.

### Other MCP clients
Any client that speaks Streamable HTTP with OAuth 2.1 (dynamic client registration
is supported). Point it at the URL above.

## What you can ask

- "Find me a hotel in Kyoto for 12–15 November, two adults, near Gion."
- "Show the rates for the Park Hyatt with breakfast, and what the cancellation terms are."
- "Book the flexible rate under my name — here's my e-mail and phone."
  → you get a one-time payment link; the booking is made when you submit it.
- "Show my bookings." / "Cancel my Kyoto booking."

Install the skill in `skills/flybest-hotels/` to give your assistant the house
rules (what to check before booking, how deposits work, what it must never do).

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
