# Analysis of Ad Bids Data

  This report summarizes the key trends and insights from the AdBids metrics view, covering the period from February 26, 2025, to March 26, 2025.

  ## Executive Summary

  The analysis of the AdBids data reveals distinct and recurring patterns in ad spending, impressions, and performance metrics for the top publishers. KrushMedia's
   activity is heavily concentrated on weekdays, while Taboola and Sinclair Broadcasting exhibit massive impression spikes every Tuesday. However, these spikes do
  not always translate to better performance, as Sinclair consistently shows a very low win rate and a near-zero click-through rate (CTR). Taboola, despite a high
  win rate, has a relatively flat CTR. KrushMedia's performance appears to be the most aligned with its spending strategy, showing higher win rates and CTRs during
   its active periods.

  ## Detailed Findings

  1. KrushMedia's Weekday-Focused Spending

  KrushMedia's ad spend and impressions are heavily concentrated on weekdays, with a dramatic drop over the weekends. This suggests a deliberate strategy to target
   users during the work week.

```shell
   1 Mon ██████████
   2 Tue ██████████
   3 Wed ██████████
   4 Thu ██████████
   5 Fri ██████████
   6 Sat █░░░░░░░░░
   7 Sun ░░░░░░░░░░
```

  2. Tuesday Impression Spikes for Taboola and Sinclair

  Both Taboola and Sinclair Broadcasting show massive, recurring spikes in impressions every Tuesday. This suggests a coordinated campaign or a competitive bidding
   war on this day of the week.

  Taboola Impressions:
```shell
   1 Mon    ██░░░░░░░░
   2 Tue    ██████████
   3 Wed    █░░░░░░░░░
   4 Thu    ░░░░░░░░░░
   5 Fri    ░░░░░░░░░░
   6 Sat    █░░░░░░░░░
   7 Sun    █░░░░░░░░░
```
  Sinclair Broadcasting Impressions:
```shell
   1 Mon    ███░░░░░░░
   2 Tue    ██████████
   3 Wed    █░░░░░░░░░
   4 Thu    ░░░░░░░░░░
   5 Fri    ░░░░░░░░░░
   6 Sat    ░░░░░░░░░░
   7 Sun    ░░░░░░░░░░
```
  3. Sinclair's "Heartbeat" Spending Pattern

  Sinclair Broadcasting's spending exhibits a recurring weekly "heartbeat" pattern, with a large spike on Tuesdays, a smaller one on Wednesdays, and then a drop
  for the remainder of the week.

```shell
    1 Spend
    2     ^
    3     |
    4     |      /peak\
    5     |     /      \
    6     |    /        \
    7     |   /          \
    8     |__/            \___________
    9     +---------------------------> Time
   10       Mon Tue Wed Thu Fri Sat Sun
```

  1. Taboola's Consistent Bid Winning, but Flat Engagement

  Taboola consistently achieves a high win rate (around 60-70%) across most days, including during their Tuesday impression spikes. However, their click-through
  rate (CTR) remains relatively low (around 0.05-0.07%) and doesn't significantly increase during these high-volume periods. This suggests that while they are
  successfully getting their ads seen, the content or targeting might not be driving increased user engagement.

  5. KrushMedia's Performance Aligns with Spending Strategy

  KrushMedia's win rate and CTR are notably higher on weekdays, mirroring their increased ad spend and impressions during those periods. Their win rate can reach
  up to 45% on weekdays, while their CTR also sees increases. This suggests that their weekday-focused strategy is effective in both securing ad placements and
  driving user engagement.

  6. Sinclair's Low Engagement Despite Impression Spikes

  Sinclair Broadcasting consistently exhibits a very low win rate (mostly below 1%) and frequently a 0% CTR, even on days with significant impression spikes. This
  indicates a critical issue where their ad placements are not translating into user engagement, suggesting potential problems with ad creative, targeting, or
  overall campaign strategy.

  **Recommendations and Next Steps**

   * For Sinclair Broadcasting: A deep dive into their ad creatives and targeting parameters is highly recommended to address the consistently low win rate and 0%
     CTR.
   * For Taboola: It would be beneficial to investigate factors that could improve CTR during their high-volume impression days. A/B testing ad creatives or refining
      targeting could be valuable.
   * For KrushMedia: Understanding the specific types of ads or campaigns run on weekdays versus weekends could provide further insights into their successful
     strategy.

  Data Source

  All findings are based on the data from the bid_metrics view in Rill. You can explore the data further using the following link: [Rill AdBids Dashboard](https://ui.rilldata.com/demo/rill-api/explore/bid_explore?tr=inf&grain=day&f=pub_name+IN+%28%27KrushMedia%27%2C%27Sinclair+Broadcasting+-+Bally+Sports%27%2C%27Taboola%27%29&measures=win_rate%2Cctr&dims=pub_name&expand_dim=pub_name)
