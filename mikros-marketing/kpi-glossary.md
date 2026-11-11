# MIKROS Marketing KPI Glossary

These definitions describe how MIKROS Marketing campaign metrics are calculated.

## How Clicks and Visits Are Measured

Campaign links are tracked links. When someone clicks one:

1. the click is recorded;
2. the visitor is redirected to the game destination, such as a store page, website, or community;
3. if the system confirms the visitor reached the destination, a destination visit is recorded.

Not every recorded click becomes a confirmed visit. For example, a visitor may close the page before it loads. Ad impressions are reported by the paid advertising platforms, not by MIKROS tracking.

The measurement infrastructure is proprietary. This page describes it only at a high level.

## Metrics

| Metric | Definition | Formula |
|---|---|---|
| Ad Impressions | Times campaign ads were shown, as reported by the paid advertising platforms | Reported by the platforms |
| Total Clicks (Redirects) | Recorded clicks that were routed to the game destination through tracked links | Count |
| Confirmed Destination Visits | Visits the MIKROS measurement system confirmed reached the game destination after a tracked redirect | Count |
| Total Generated Content | Qualifying promotional items submitted by the Tatum Games internal team and MIKROS Network Partners for the campaign | Count |
| CTR (Click-Through Rate) | Share of ad impressions that led to a recorded ad click | Recorded ad clicks ÷ ad impressions × 100 |
| CPC (Cost Per Click) | Average spend per recorded click | Campaign spend ÷ recorded clicks |
| CPV (Cost Per Visit) | Average spend per confirmed destination visit | Campaign spend ÷ confirmed destination visits |
| Average Cost Per Generated Content | Average spend per qualifying content item | Campaign spend ÷ qualifying content count |

## Calculation Rules

- **Missing or zero denominators:** when a denominator is missing or zero, the metric is shown as **N/A**, not as 0 or infinity.
- **Consistent spend basis:** CPC, CPV, and Average Cost Per Generated Content all use the same campaign spend figure for the same reporting period.
- **Clicks and visits are different:** CPC uses recorded clicks. CPV uses confirmed destination visits. CPV is usually higher than CPC.
- **No invented results:** metrics come from recorded campaign data. Projections and estimates are not reported as results.

## Related

- [How MIKROS Marketing Works](how-it-works.md)
- [Campaign Lifecycle and Benefits](campaign-lifecycle.md)
