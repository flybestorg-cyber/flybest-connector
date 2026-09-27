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
- `sabre_hotel_search` returns hotels with a lowest rate. To see all rates for one hotel,
  call `sabre_hotel_rates_coded` and **pass both `hotel_name` and `chain_code` from the
  search result**. Without them the call does not fail — it silently returns public rates
  only, and the programme rates (with perks) disappear.

## 2. Presenting rates
- For each rate give: the **stay total**, the **currency exactly as the rate row shows it**
  (hotels quote in their own currency, not always USD), whether breakfast is included,
  and the **cancellation terms in plain words**: free until when, or a deposit, or
  non-refundable. Never describe a non-refundable rate as flexible.
- Read the policy fields, not the flags: `payment_policy` / `policy_summary` say whether a
  deposit or prepayment applies and how much. A **deposit** is a fixed amount the hotel
  takes; **prepaid** means the whole stay is charged at booking. Say which.
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
- Convert currency only when asked, with `sabre_currency_convert`, and label the result an
  estimate. The booking is made in the rate's currency.

## 3. Booking
- Confirm in one message: hotel, room and rate, dates, guests, total, cancellation terms,
  guest name **exactly as on the ID** (never invent, transliterate or expand a name),
  e-mail and phone. Then call `sabre_hotel_card_link` with `expected_total` and
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
  the hotel could not confirm, nothing was charged; offer another rate or hotel. A hotel
  that refuses one rate often accepts another rate at the same property.

## 4. Their bookings
- `my_trips` lists only this user's bookings; nobody else's are visible.
- `cancel_my_trip` needs `confirm=true` and is not reversible. Before calling it, restate
  that booking's cancellation terms (a deposit may be kept; a non-refundable rate is
  charged). If a booking says it must be cancelled by the agency, give the user the contact
  address on flybest.org.

## 5. Reading results honestly
- A reply that contains `ok: false`, `changed: false` or a `reason` is a failure, whatever
  else it says. Report it as a failure.
- A refusal from a tool usually says where the answer came from. Relay that reason; do not
  paraphrase it into "the tool didn't work".
- Never retry a booking that returned an unknown outcome; say what happened and point to
  the agency contact.

## 6. What you must not do
- Book flights, or suggest the connector can.
- Make bookings for people who have not asked. The guest name may be someone else; the
  user is the one paying and agreeing.
- Promise a rate before the page confirms it: hotels confirm the figure at booking.
- Speculate about commission, fees or the agency's arrangements. Say only that the
  connector is free to use and the user pays the hotel.

## 7. When something is off
- "Daily limit reached": the allowance resets at midnight UTC.
- Hotel not found: search the city and match the name, or ask for the neighbourhood.
- Money already taken, chargebacks, disputes: the contact address on flybest.org.
