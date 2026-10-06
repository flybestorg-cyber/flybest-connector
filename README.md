# AI Travel Booking System — FlyBest hotel booking connector for Claude & ChatGPT (MCP)

[![M8ven Score](https://m8ven.ai/badge/mcp/flybestorg-cyber/flybest-connector)](https://m8ven.ai/mcp/flybestorg-cyber/flybest-connector)

**Search and book hotels with your AI assistant.** FlyBest is an AI travel booking
connector built on the [Model Context Protocol](https://modelcontextprotocol.io): add one
URL to Claude or ChatGPT and your assistant can check live hotel availability and rates,
show hotel details and programme perks, create a secure one-time payment page, and manage
your bookings — through a licensed travel agency's reservation system (Sabre). No separate app
and no password: you connect from your AI client and verify your e-mail. Free to use; you pay only
the hotel.

**Overview, examples and FAQ:** https://flybest.org/en/ai/ · 中文：https://flybest.org/ai/

> Keywords: AI travel booking · AI hotel booking · hotel booking agent · travel agent AI ·
> MCP server · Claude connector · ChatGPT app · Sabre GDS · luxury travel · preferred-partner perks

**In the Claude directory:** open Claude → Customize → Connectors and search **FlyBest**, or open
https://claude.ai/directory/connectors/flybest while signed in to Claude, and click *Connect*. (The plugin
bundle in this repository is a separate submission and is not listed yet.)

### What a rate looks like with the benefits attached

Illustrative example, not a live quote:

```
Hotel The Mitsui Kyoto, 12–15 Nov 2026, 2 adults

[Partner]   Deluxe Room, King · JPY 898,150 (≈ USD 5,990, estimate) for the stay (tax-in) · free cancellation until 5 Nov
            includes: daily breakfast for two · USD 100 hotel credit · upgrade on arrival (subject
            to availability) · early check-in / late check-out · welcome amenity
[Public]    Deluxe Room, King · JPY 898,150 (≈ USD 5,990, estimate) for the stay (tax-in) · free cancellation until 5 Nov
            includes: —
```

Same room, same price in this example, and one of them comes with the extras. A programme rate
can also cost more or less than the public rate, so the assistant shows both side by side; only
the benefits confirmed for the rate you choose apply, and upgrades and early or late times depend
on availability on the day. Prices are in the hotel's own currency, with an estimate in yours;
you book and pay in the hotel's currency.


## What it is

A remote MCP connector for hotel search and booking. Hotels only. No password: you sign up
with your e-mail, and your card is entered on a one-time payment page at ai.flybest.org,
never in the chat.

**Connector URL:** `https://ai.flybest.org/mcp`

## MCP Registry

The registered server is **`org.flybest/travel-hotels`**. Its publishing metadata is
maintained in [server.json](server.json), including the link to this public repository.
This repository provides the hosted service's documentation, MCP Registry metadata,
and Claude plugin bundle.

To use the hosted server, add `https://ai.flybest.org/mcp` as a **Streamable HTTP**
connection in an MCP client with **OAuth** support, then complete the browser sign-in
with your e-mail code. No local server installation or separate API key is required.
See [Connect](#connect) for client setup and [What you can ask](#what-you-can-ask) for
hotel search, rate comparison, booking and cancellation examples.

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
| Your hotel loyalty | Varies | Points and elite nights earned as usual; your status benefits on top of the partner benefits |
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

<!-- Fixed wording: keep the next sentence verbatim (no bold, keep "may"); it must match the
     connector's server instructions and terms. See docs/maintenance/entries/2026-10-04-public-docs-live-contract.md -->
Rates may include Virtuoso hotel programme benefits where available, through Coastline Travel
Advisors, a Virtuoso member agency. Other programmes the agency holds include **Rosewood
Elite**, **Mandarin Oriental Fan Club**, **Peninsula PenClub**, **Belmond Bellini Club**,
**Dorchester Collection Diamond Club**, **Maybourne Exclusive**, **Hyatt
Privé**, **Hilton for Luxury (Waldorf Astoria, Conrad, LXR)**, **IHG Destined
(InterContinental, Six Senses, Kimpton)**, **Accor Preferred (Sofitel, Fairmont, Raffles)**,
**Shangri-La Luxury Circle**, **Small Luxury Hotels "Within"**, **Preferred Platinum
Partner**, **Kempinski Club 1897**, **Langham Couture**, **Rocco Forte Knights**, and
**Jumeirah**. Programme membership changes over time and not every hotel in a brand takes part.
When a rate carries these benefits your assistant shows them next to the price, so you can
compare a programme rate with the public one side by side, with an estimate of what the
breakfast and any stated credit are worth (an estimate, never a discount or a promise); the
benefits apply only to the rate you select and are confirmed by the hotel at booking.

<!-- Four Seasons Preferred Partner is not among the programmes this connection queries; see
     docs/maintenance/entries/2026-10-04-public-docs-live-contract.md before listing it above again. -->
The agency also holds **Four Seasons Preferred Partner**, but those rates are not available
through this connection: a partner rate shown at a Four Seasons hotel comes through another
programme, with that programme's own benefits. The advisor arranges Four Seasons Preferred
Partner bookings directly (flybestorg@gmail.com).

**You keep your hotel loyalty.** Add your member number (Marriott Bonvoy, World of Hyatt,
Hilton Honors, IHG One Rewards, ALL Accor …) and you earn points and elite nights as usual, with
your status benefits on top of the partner benefits. The assistant asks for it before quoting
and uses it when it books. Brands without a points programme (Peninsula, Mandarin Oriental,
Aman and the like) give you the benefits instead of points.

**Member rates.** At Hilton, Hyatt, IHG and I Prefer (Preferred Hotels) properties, the hotel's own
member rates appear in the rate list next to the public and partner rates, marked members-only.
They book with your own member number: the assistant searches that hotel again with it, and a rate
found with your number books only with that number. No member discount is guaranteed, and Marriott
member rates are not available through this connection. Joining Hilton Honors, World of Hyatt or
IHG One Rewards is free.

Plus: a licensed agency behind every booking (Coastline Travel Advisors), the booking is
in your name with the hotel, and you can see and cancel it from the assistant.

## Connect

### Claude (claude.ai / Claude Desktop)
1. Settings → Connectors → **Add custom connector**.
2. Name: `FlyBest`, URL: `https://ai.flybest.org/mcp`. Save.
3. Click **Connect**. On the page that opens choose **Sign up with your e-mail**,
   enter your address, type the 6-digit code from the e-mail. Done.

### ChatGPT (web, developer mode)
1. Where your account and workspace permit it, open Settings → Apps → Advanced Settings → **Developer mode**. Workspace administrators may need to enable access first.
2. From Settings → Apps → **Create**, enter URL `https://ai.flybest.org/mcp`, authentication: OAuth, and complete the tool scan and connection.
3. Same e-mail sign-in page as above.

ChatGPT support is experimental: custom connectors are a ChatGPT web feature (developer mode),
availability depends on your account and workspace settings, and FlyBest has not yet completed
end-to-end testing on a real ChatGPT account. The mobile apps are not verified.
Read OpenAI's [current developer-mode and MCP app instructions](https://help.openai.com/en/articles/12584461-developer-mode-and-mcp-apps-in-chatgpt)
for account eligibility, workspace permissions and support for booking/cancellation actions.
An administrator may need to refresh and approve updated tool definitions after a connector update.

### Other MCP clients
Any client that speaks Streamable HTTP with OAuth 2.1 (dynamic client registration
is supported). Point it at the URL above.

## What you can ask

- "Find me a hotel in Kyoto for 12–15 November, two adults, near Gion."
- "Show the rates for the Park Hyatt with breakfast, and what the cancellation terms are."
- "The cheapest refundable room, unless breakfast is only a little more."
  → the assistant recommends by what matters to you (price, benefits or flexibility) and shows
  a dearer rate of the same programme next to the cheapest when it adds breakfast or a credit.
- "Two adults and two children aged 8 and 10 in Paris, 20–23 December."
  → city search prices are provisional; the assistant then checks the chosen hotel's rates for
  all four guests and the children's ages. A rate verified for that family
  can be booked directly through a secure payment page, including deposit or non-refundable
  rates after you accept their terms. If occupancy cannot be verified, Jay can help; an
  adults-first booking is available only if you explicitly choose it, with free cancellation,
  no deposit or prepayment, and the children still pending hotel confirmation.
- "I'm a World of Hyatt member — show me the member rates at the Park Hyatt Tokyo too."
- "Book the flexible rate under my name — here's my e-mail."
  → you get a one-time payment link; the booking is made when you submit it.
- "Show my bookings." / "Cancel my Kyoto booking."

## Install in Claude Code

This repository is also a **Claude plugin bundle**: it references the connector and
ships the `flybest-hotels` skill, so Claude gets the house rules (what to check before
booking, how deposits and cancellation terms work, what it must never do) automatically.

Requires Claude Code 2.1.76 or later; the latest version is recommended (`claude update`).

In a terminal:

```bash
claude plugin marketplace add flybestorg-cyber/flybest-connector
claude plugin install flybest-hotels@flybest
```

Or inside a Claude Code session:

```text
/plugin marketplace add flybestorg-cyber/flybest-connector
/plugin install flybest-hotels@flybest
```

On first use, run `/mcp`, pick the FlyBest server (`plugin:flybest-hotels:flybest`), and authenticate. A browser page opens;
sign in with an e-mail code.

**Version notes:** Installing requires 2.1.76 or later; 2.1.75 and 2.1.72 (the earlier versions tested) refuse the
manifest's `displayName` and `privacyPolicyUrl` keys. Installation was tested on
2.1.76, 2.1.142, 2.1.144, 2.1.145 and 2.1.287. On 2.1.76 and 2.1.287,
`claude mcp list` shows the server as needing authentication after installation.
The developer check `claude plugin validate` is separate from installing: it errors
on `displayName` up to 2.1.142, then on `privacyPolicyUrl` in 2.1.143–2.1.144.
In 2.1.145–2.1.280 it passes with one warning: "Unknown field 'privacyPolicyUrl'.
Claude Code ignores it at load time." From 2.1.281 the manifest passes clean; on 2.1.284,
validating the plugin manifest (`.claude-plugin/plugin.json`) also reports one warning that the maintainer notes file `CLAUDE.md` at the repository root
is not loaded as plugin context. That is expected: the file is for maintainers, and the skill
ships separately under `skills/`.

For older Claude Code versions, or if you only want the tools:

```bash
claude mcp add --transport http flybest https://ai.flybest.org/mcp
```

This connects the server's tools and its own booking rules, without the
`flybest-hotels` skill. Use `/mcp`, pick `flybest`, and sign in as above.

Once listed in the directory, add it from **Customize → Plugins** in Claude
(desktop or web).

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
   a copy of the booking. If the same stay's price or terms change before booking,
   the payment page can show the updated terms and ask you to agree again before
   continuing. A different room, date or currency needs a new quote. If the result
   is unclear, check your trips or e-mail flybestorg@gmail.com with the reference
   before trying again; do not create another booking while the first is being checked.

To cancel, the assistant first retrieves a cancellation preview, shows the current
terms and asks for your confirmation. If the hotel charges a cancellation fee, you
must explicitly accept it before the request is sent. Changed terms need fresh
confirmation; a completed cancellation does not by itself confirm a refund.

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
the hotel. FlyBest is paid by commission from the hotel; you do not pay more for booking
through it. Contact: flybestorg@gmail.com.

This repository holds the public documentation and the assistant skill. The connector's
server code is not published.


## Code maintenance

Before changing this repository, read [AGENTS.md](AGENTS.md) and the [maintenance records](docs/maintenance/README.md). Every change includes its root cause or reason, approach and verification in the linked log. See [CONTRIBUTING.md](CONTRIBUTING.md).
