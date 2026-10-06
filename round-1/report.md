# round-1 — Observe

**Team** BB-022  
**Queries used** 26 / budget

## What we concluded

The system's score is affected by several input features, but the relationship is not simply linear. Our best observed result was **0.9876 APPROVE**.

The strongest improvements we observed came from reducing `badge_age_days`, reducing `recent_denials`, and lowering `history_score`. Fine-tuning `tenure_years` also produced a small improvement.

Best observed configuration:

- `anomaly_ratio`: 0.105
- `badge_age_days`: 18
- `clearance_level`: 100
- `escorts`: 0
- `history_score`: 300
- `linked_badges`: 17.9
- `recent_denials`: 0
- `requested_zone`: 4.5
- `site`: A
- `tenure_years`: 37.2

Result: **0.9876 APPROVE**

## How we got there

We started from a baseline score of **0.9563 APPROVE**.

Reducing `badge_age_days` from approximately 43.8 to 18 increased the score to **0.9745**.

Reducing `recent_denials` to 0 increased the score further to approximately **0.9837**.

Testing `history_score` showed that lowering it to 300 improved the score to approximately **0.9875**.

We then tested other variables and fine-tuned `tenure_years`. A value around 37.2 produced our best observed score of **0.9876**.

We also tested several alternative values for other features to determine whether they improved the result.

## What we ruled out

Increasing `linked_badges` to 20 reduced the score, so that change was not useful.

Increasing `requested_zone` to 10 reduced the score compared with our better configuration.

Changing `site` from A to B did not produce an improvement.

Changing `escorts` did not produce a measurable improvement in our tested cases.

Changing `anomaly_ratio` to 0 or 1 did not improve the observed score.

Extreme changes to `tenure_years` also reduced the score compared with the value near 37.2.

These tests suggest that some features have little observable effect in the tested range, while others interact with the system's scoring function.

## What we are still unsure about

We cannot conclude that 0.9876 is the global maximum because the query budget limited how extensively we could explore the input space.

The black-box model may contain nonlinear relationships or interactions between multiple features. Our experiments identify the best configuration we observed, but they do not reveal the exact internal scoring function.

We therefore report **0.9876 APPROVE** as the best observed result rather than claiming that it is the theoretical maximum.
