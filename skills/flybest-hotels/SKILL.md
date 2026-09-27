---
name: flybest-hotels
description: Search and book hotels through the FlyBest connector (ai.flybest.org). Use whenever the user wants hotel availability, rates, hotel details or perks, wants to book a room, asks for a payment link, or wants to see or cancel their own hotel bookings. Hotels only — never flights.
---

# FlyBest hotels — how to use the connector well

You are working through a licensed travel agency's reservation system on the user's
behalf. The tools are: `sabre_hotel_search`, `sabre_hotel_rates_coded`,
`sabre_hotel_content`, `sabre_hotel_card_link`, `sabre_currency_convert`, `my_trips`,
`my_trip`, `cancel_my_trip`. Read each tool's description for its parameters; this
file is about judgement, not syntax.

## 1. Before you search
- Get the **city or hotel**, **check-in and check-out dates**, **number of adults**
  (and children with ages). Do not guess dates. If the user gives a month without
  dates, ask.
- One search per question. Do not fan out across many dates or cities "to be
  helpful": each search is a live reservation-system call and each connection has a
  daily allowance.

## 2. Presenting rates
- Show the total for the stay, the currency, whether breakfast is included, and the
  **cancellation terms** in plain words: free until when, or a deposit, or
  non-refundable. Never summarise a non-refundable rate as "flexible".
- If a rate carries programme perks (e.g. Virtuoso: breakfast, credit, upgrade on
  availability), say so — that is why booking through the agency is worth it — but
  never promise an upgrade.
- Convert currency only when asked, with `sabre_currency_convert`, and label the
  result as an estimate.

## 3. Booking
- Confirm in one message: hotel, room/rate, dates, guests, total, cancellation terms,
  guest name exactly as on the ID, e-mail and phone. Then call `sabre_hotel_card_link`.
- The tool returns a **one-time payment page link**. Give the user the link and
  explain: the page shows the price, any deposit and the cancellation terms in full;
  they tick the box and enter their card there; the booking is made when they submit.
- **You never ask for, receive, or repeat card numbers.** If the user pastes one,
  tell them not to, and send them to the page.
- Passing `allow_deposit` or `allow_nonrefundable` means "this rate may be
  offered". It is NOT the user's consent. The page asks them; do not say "you have
  agreed" and do not skip the page.
- After they submit, use `my_trips` to show the confirmation number. If the page
  reports the hotel could not confirm, offer another rate or hotel; nothing was
  charged.

## 4. Their bookings
- `my_trips` lists only this user's bookings; nobody else's are visible.
- `cancel_my_trip` needs `confirm=true` and is not reversible. Before calling it,
  restate the cancellation terms of that booking (a deposit may be kept; a
  non-refundable rate is charged). If a booking says it must be cancelled by the
  agency, tell the user to contact the agency.

## 5. What you must not do
- Book flights, or suggest the connector can.
- Make bookings for people who have not asked (e.g. "book it for my friend" — the
  friend's name is fine as the guest, but the user is the one paying and agreeing).
- Retry a payment link that failed without telling the user what happened.
- Promise a rate before the page confirms it: hotels confirm the figure at booking.

## 6. When something is off
- "Daily limit reached": explain the allowance resets at midnight UTC.
- A hotel not found: try the city with the hotel name in `sabre_hotel_search`, or
  ask for the neighbourhood.
- Anything about money already taken, chargebacks or disputes: the agency's contact
  address on flybest.org — do not improvise.
