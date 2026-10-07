# Quote integrity

Read this before comparing or presenting hotel prices. Use the fields or sentences
actually returned by the connected role; an omitted field is unknown, not evidence
of a favourable term.

- City availability is discovery only. Formal quotes come from
  `sabre_hotel_rates_coded`. A discovery price or partner-property badge does not
  prove a selected rate's price, availability or benefits.
- Quote the selected row's `total_after_tax` and its own currency, never
  `total_after_tax_excl_fees` or a converted display estimate. State nights,
  rooms and guests per room. A multi-room total already covers all quoted rooms.
  Identify separately any mandatory fees excluded from the total, and any fees
  whose inclusion or amount is unknown. Do not label a total all-inclusive when
  the returned terms do not establish that.
- Compare the same property, dates, room/product, bed arrangement, room count,
  adults, children's ages and currency. Show differences in breakfast, benefits,
  cancellation or payment terms beside the real price difference. Different
  room categories or conditions are alternatives, not equivalent-price savings.
- Partner benefits belong to the selected negotiated row and its own rate key.
  A public breakfast/package rate can include what its own terms state; it does
  not acquire another row's partner benefits. Empty benefit text is unverified,
  not proof of no benefits and not permission to copy another row's inclusions.
- Group by returned room/product identity and full description. Do not merge
  rows merely because their displayed plan names match. Keep different benefits,
  bed types, deadlines and payment conditions distinguishable. Unknown bed type
  means bed type to confirm; keep an otherwise priced option visible.
- Use the selected row's exact cancellation date, time and stated hotel timezone.
  If the timezone or deadline is missing, say what is unknown. A refundable flag
  or a plan called flexible does not prove cancellation is free now. State deposit
  amount/basis and collection timing from the live terms, without guessing.
- Before saying no matching room/rate exists, check visible truncation, warnings,
  request refusals and occupancy verification. If the schema supports them, use
  `room_contains`, a larger `max_rows` or `cheapest_first=false` for a targeted
  suite/villa search. Use `negotiated_only` only for a targeted partner search,
  preserving the comparable public row from a complete matching quote. Describe
  coverage as the returned options, not every rate in the market.
- Keep the selected row's price, currency, room, party, benefits and payment/
  cancellation terms in the working context for the link and confirmation check.
  Copy opaque rate keys and family tokens unchanged from that same row. A changed
  room, dates, currency or party needs a matching new quote; changed liabilities
  need the live page's fresh agreement.
