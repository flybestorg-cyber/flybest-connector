# FlyBest hotel booking plugin — live hotel tools and Skills for Claude

[![M8ven Score](https://m8ven.ai/badge/mcp/flybestorg-cyber/flybest-connector)](https://m8ven.ai/mcp/flybestorg-cyber/flybest-connector)

**Search, compare and book hotels with your AI assistant.** The FlyBest plugin
bundles live hotel tools and the `flybest-hotels` Skill: check rates for your actual
dates and guests, compare rooms, advisor benefits and cancellation terms, create
a secure one-time payment page, and manage your own bookings. The Skill guides
Claude through quote checks, rate selection and booking verification.

The tools connect to a licensed travel agency's reservation system (Sabre) through
[MCP](https://modelcontextprotocol.io). Add the plugin in Claude, then authenticate
with your email code when connecting its hotel tools. Compatible clients can also
connect to the MCP service directly. Free to use; you pay only the hotel.

**Overview, examples and FAQ:** https://flybest.org/en/ai/ · 中文：https://flybest.org/ai/

> Keywords: AI travel booking · AI hotel booking · hotel booking agent · travel agent AI ·
> Claude plugin · hotel Skills · MCP server · Sabre GDS · luxury travel · preferred-partner perks

**Install in Claude:** open the [FlyBest plugin](https://claude.ai/directory/manage/plugins/4c82105c-3ebc-4a9b-b2c4-9916f9566836),
or use **Customize → Plugins** to find FlyBest. Follow Claude's prompts to add it
and connect the hotel tools. The plugin includes the Skill and remote MCP
connection; your email sign-in still authorizes access to your own bookings.

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

A hotel plugin with live tools and a search-and-booking Skill. Hotels only. You
sign in with your email, and your card is entered on a one-time payment page at
ai.flybest.org, never in the chat. The MCP service remains available for clients
that only need the tools.

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
Partner bookings directly (jay@flybest.org).

**Use your own hotel loyalty membership.** Add your member number (Marriott Bonvoy,
World of Hyatt, Hilton Honors, IHG One Rewards, ALL Accor …) when booking. Points,
elite-night credit and status benefits depend on the selected rate and the hotel's
programme rules; they are not guaranteed for every rate. The assistant can quote
public and partner options before you supply a number, then verifies a selected
members-only offer with your own number. Brands without a points programme can
still offer the benefits stated in their selected partner rate.

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
1. Open the [FlyBest plugin](https://claude.ai/directory/manage/plugins/4c82105c-3ebc-4a9b-b2c4-9916f9566836), or find it under **Customize → Plugins**.
2. Add the plugin and follow the prompts to connect its hotel tools.
3. Complete the email-code sign-in when prompted. The Skill and MCP connection
   are included; no separate server installation or manual URL entry is needed.

For a tools-only connection:

1. In Claude's connector settings, choose **Add custom connector**.
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

Use a current Claude Code release. Plugins added to your Claude account can sync
to Claude Code when you sign in with the same account; account sync requires
Claude Code 2.1.273 or later. See [Claude's plugin guide](https://support.claude.com/en/articles/13837440-use-plugins-in-claude).
You can also install this repository directly:

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

**Validation and updates:** `claude plugin validate` checks the package; it does
not install it or complete your hotel-tool authorization. The current Claude
manifest omits the old `displayName` and `privacyPolicyUrl` keys removed in 1.1.6.
The maintainer's root `CLAUDE.md` is not plugin context; the customer Skill ships
under `skills/`. Existing installations need to update the plugin to receive
changed Skill instructions.

For older Claude Code versions, or if you only want the tools:

```bash
claude mcp add --transport http flybest https://ai.flybest.org/mcp
```

This connects the server's tools and its own booking rules, without the
`flybest-hotels` skill. Use `/mcp`, pick `flybest`, and sign in as above.

The [Claude directory entry](https://claude.ai/directory/manage/plugins/4c82105c-3ebc-4a9b-b2c4-9916f9566836)
bundles these tools and the Skill for Claude web and desktop.

Using ChatGPT or another client? The connector sends its core booking rules as server
instructions when you connect (this skill is the fuller version), and you can paste
`skills/flybest-hotels/SKILL.md` together with its linked
`references/quote-integrity.md` into a project or custom instructions. Either way, check the
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
   is unclear, check your trips or e-mail jay@flybest.org with the reference
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
booking, e-mail jay@flybest.org with the booking reference; hotel cancellation deadlines
still apply.

## Terms, privacy, security

- [Terms of use](https://ai.flybest.org/terms) · [Privacy notice](https://ai.flybest.org/privacy)
- Bookings, cancellations the assistant could not complete, charges, privacy requests:
  **jay@flybest.org** with your booking reference (never card details). One advisor,
  Pacific time; replies usually within one business day.
- Found a security problem? See [SECURITY.md](SECURITY.md).

## Who runs this

FlyBest (flybest.org) — an independent luxury travel advisor based in California, USA,
affiliated with Coastline Travel Advisors, a licensed host travel agency. FlyBest operates this
connector and is responsible for its signup and booking data; hotel bookings are placed through
Coastline's reservation system on its accreditation. The connector is free to use; you pay only
the hotel. FlyBest is paid by commission from the hotel; you do not pay more for booking
through it. Contact: jay@flybest.org.

This repository holds the public documentation and the assistant skill. The connector's
server code is not published.


## Code maintenance

Before changing this repository, read [AGENTS.md](AGENTS.md) and the [maintenance records](docs/maintenance/README.md). Every change includes its root cause or reason, approach and verification in the linked log. See [CONTRIBUTING.md](CONTRIBUTING.md).
