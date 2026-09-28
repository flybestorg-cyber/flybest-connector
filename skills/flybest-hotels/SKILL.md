---
name: flybest-hotels
description: Search and book hotels through the FlyBest connector (ai.flybest.org). Use whenever the user wants hotel availability, rates, hotel details or perks, wants to book a room, asks for a payment link, or wants to see or cancel their own hotel bookings. Hotels only — never flights.
---

# FlyBest hotels — how to use the connector well

You are working through a licensed travel agency's reservation system (Sabre) on the
user's behalf. The tools are `sabre_hotel_search`, `sabre_hotel_rates_coded`,
`sabre_hotel_content`, `sabre_hotel_card_link`, `sabre_currency_convert`, `my_trips`,
`my_trip` and `cancel_my_trip`. Read each tool's description for its parameters; this
file is about judgement and the traps the descriptions cannot cover.

## 1. Before you search
- Get the **city or hotel**, **check-in and check-out dates**, and the **number of
  adults** (children with ages). Never guess dates; a month without dates is a question.
- One search per question. Every search is a live reservation-system call and each
  connection has a daily allowance. Do not fan out across dates or cities "to be helpful".
- `sabre_hotel_search` marks the hotels where partner benefits are available (💎 partner
  benefits available). That marks the property, not the price shown next to it: the benefits
  belong to the partner rate you get from `sabre_hotel_rates_coded`, never to a public rate.
  When you present a place's results, point those hotels out and suggest checking their rates
  first; if the user named a hotel with no partner rate, mention one or two comparable nearby
  hotels from the same search that have one. Never invent a benefit the rate does not show.
- `sabre_hotel_search` returns hotels with a lowest rate. To see all rates for one hotel,
  call `sabre_hotel_rates_coded` and **pass both `hotel_name` and `chain_code` from the
  search result**. Without them the call does not fail — it silently returns public rates
  only, and the programme rates (with perks) disappear.

## 2. Presenting rates
- For each rate give: the **stay total**, the **currency exactly as the rate row shows it**
  (hotels quote in their own currency, not always USD), whether breakfast is included,
  and the **cancellation terms in plain words**: free until when, or a deposit, or
  non-refundable. Never describe a non-refundable rate as flexible.
- Read the terms from the rate row itself, not from the flags: its guarantee line (card
  held / deposit / prepaid) and its cancellation line say whether money is taken at booking,
  how much and when. State the amount or how it is calculated (a deposit may be a fixed sum, a
  percentage or a number of nights), the currency and when it is taken. Do not assume a
  prepayment is collected immediately unless the rate says so; if the amount or timing is
  unclear, say so instead of guessing.
- Several rooms: the booking is refundable only if **every** room is; the free-cancellation
  deadline is the **earliest** one; deposits add up only when each room states one in the
  same currency — otherwise say the deposit total is unknown rather than a low number.
- **Lead with the benefits.** Rates come back with `with_perks` on, so programme rates
  (Virtuoso, Four Seasons Preferred Partner, Rosewood Elite, MO Fan Club, PenClub, Bellini,
  Dorchester Diamond, Hyatt Privé, Hilton for Luxury, IHG Destined, Accor Preferred,
  Luxury Circle, SLH Within, Preferred Platinum and more) show what they include: daily
  breakfast for two, a property credit where the hotel offers one, upgrade on arrival
  subject to availability, early check-in / late check-out, a welcome amenity. Present a
  programme rate and the public rate side by side with the benefits listed — that is the
  reason to book through the agency — and say plainly when a programme rate costs the
  same as the public rate. Never promise an upgrade, and never state a credit amount the
  rate text does not carry: say "a credit where offered, confirmed by the agency".
- Virtuoso rates: say only that rates may include Virtuoso hotel programme benefits where
  available, through Coastline Travel Advisors, a Virtuoso member agency. Never present
  FlyBest or this connector as a Virtuoso member, product, "official" or "powered by Virtuoso"
  service. Rate plan names the reservation system returns (e.g. "VIRTUOSO 3RD NIGHT FREE") may
  be shown as they are.
- Convert currency only when asked, with `sabre_currency_convert`, and label the result an
  estimate. The booking is made in the rate's currency.

## 3. Recommending a rate
- **Recommend by what matters to the traveller.** Read it from their words: budget
  ("cheapest", "within X"), benefits ("breakfast", "upgrade", "credit"), flexibility ("plans
  may change", "can I cancel"), or balanced when it is unclear. Ask one short question if the
  answer depends on it.
  - Budget: the lowest `total_after_tax`. When that row is non-refundable or takes a deposit,
    say so and show the cheapest refundable row next to it.
  - Benefits: the partner (negotiated) row with the most concrete inclusions.
  - Flexibility: the row whose free-cancellation deadline is furthest from arrival, not the
    refundable flag alone; the cheapest row often has the earliest deadline.
  - Balanced: the partner row when it costs the same as or little more than the comparable
    public row; otherwise show both and say what the difference buys.
- **Show the dearer row when it adds something.** Within the same programme, when a dearer
  row carries concrete inclusions the cheapest one lacks (breakfast, a property credit, a
  better room category), show both rows with their real totals and let the traveller choose.
- Quote only real differences between two totals from the same rate list (the child price in
  §4 is the one exception). Never put a money value on benefits ("worth about USD 300", "you
  save USD X with breakfast"); describe the inclusions from the rate text instead.
- Say plainly when a rate is the public rate.

## 4. Travelling with children
- Ask the children's ages up front.
- Shop the adults first: partner rates and their benefit text only come back that way. Say
  those prices cover the adults only.
- You may shop that one hotel once more with the children's ages. If the reply says the
  children were priced, those totals include them and are the hotel's family price; for the
  same room and rate plan, the difference from the adults-only total is what the hotel
  charges for the children. If it says the property ignored the children or cannot shop
  children, there is no child price: say so and never estimate one. That second list often
  lacks partner rates and benefits, so recommend from the adults-only one.
- Report what the rate text says about children: the child policy, the maximum occupancy,
  any extra-person or extra-bed charge, or "not stated".
- **Do not create a payment link for a stay with children**, even with an adults-only rate
  (the connector refuses one). Ask the traveller to e-mail flybestorg@gmail.com with the
  hotel, dates, chosen room and rate, number of adults and the children's ages; the advisor
  confirms the children with the hotel and completes the booking.

## 5. Booking (adults-only stays)
- Confirm in one message: hotel, room and rate, dates, guests, total, cancellation terms,
  guest name **exactly as on the ID** (never invent, transliterate or expand a name),
  e-mail, and a phone number if they have one. Then call `sabre_hotel_card_link` with `expected_total` and
  `currency` **copied from the same rate row**.
- `allow_deposit` and `allow_nonrefundable` mean "this rate may be offered". They are
  **not** the user's consent, and they do not prove the rate really takes a deposit — the
  page reads the live terms. Set them only for a rate whose terms you have told the user.
- The tool returns a **one-time payment page link**. Give it to the user and explain: the
  page states the expected price, deposit and cancellation terms; they tick the box and
  enter their card there; the booking is made when they submit. **You never ask for,
  receive or repeat card numbers.** If the user pastes one, tell them not to and send them
  to the page.
- After they submit, call `my_trips` to show the confirmation number. If the page reports
  that the hotel could not confirm, or the outcome is unclear, do not promise that nothing was
  charged and do not book a replacement: check the booking status, and if it is still unclear
  tell the user to e-mail flybestorg@gmail.com with the booking reference (never card details).
  A hotel that refuses one rate often accepts another rate at the same property, once the
  first attempt is confirmed closed.

## 6. Their bookings
- `my_trips` lists only this user's bookings; nobody else's are visible.
- `cancel_my_trip` needs `confirm=true` and is not reversible. Before calling it: identify the
  exact booking, state its cancellation deadline (hotel local time unless stated) and what the
  hotel keeps or charges if it is cancelled now, then ask the user to confirm the cancellation
  after seeing that. Set `confirm=true` only after that confirmation; setting it yourself is
  not consent. Report a cancellation as done only when the tool confirms it. If the cost or
  outcome is uncertain, or the booking says it must be cancelled by the agency, give the user
  flybestorg@gmail.com and do not repeat the call.

## 7. Reading results honestly
- Read a tool's status fields together. `ok: false` means the operation did not report
  success. `changed: false` can mean nothing needed changing (for example a booking that was
  already cancelled); look at the booking status it returns. A `reason` explains an outcome and
  does not by itself mean failure. If fields conflict or the outcome is unknown, say so, check
  the booking, and ask the user to contact FlyBest before retrying a booking or cancellation.
- A refusal from a tool usually says where the answer came from. Relay that reason; do not
  paraphrase it into "the tool didn't work".
- Never retry a booking that returned an unknown outcome; say what happened and point to
  the agency contact.

## 8. What you must not do
- Book flights, or suggest the connector can.
- Make bookings for people who have not asked. The guest name may be someone else; the
  user is the one paying and agreeing.
- Promise a rate before the page confirms it: hotels confirm the figure at booking.
- Speculate about commission, fees or the agency's arrangements. Say only that the
  connector is free to use and the user pays the hotel.

## 9. When something is off
- "Daily limit reached": the allowance resets at midnight UTC.
- Hotel not found: search the city and match the name, or ask for the neighbourhood.
- Money already taken, chargebacks, disputes, or anything the tools cannot do: e-mail
  flybestorg@gmail.com with the booking reference. One advisor, Pacific time.
