# round-2 - Investigate

**Team:** BB-022  
**Queries used:** 31

## What we concluded

Round 2 experiments were performed using controlled LOW/HIGH combinations of selected parameters. The objective was to identify which parameters affected the BLACKBOX score and which parameter combinations showed meaningful relationships.

The recorded experiments showed that the highest-impact parameters were:

- `linked_badges`
- `requested_zone`
- `history_score`
- `recent_denials`
- `badge_age_days`

The following parameters showed no meaningful score change in the recorded experiments and were therefore treated as low priority:

- `anomaly_ratio`
- `clearance_level`
- `escorts`

## How we got there

### 1. anomaly_ratio + clearance_level

The following four combinations were tested:

| anomaly_ratio | clearance_level | Result |
|---|---|---:|
| 0 | 0 | 0.9876 |
| 1 | 100 | 0.9876 |
| 1 | 0 | 0.9876 |
| 0 | 100 | 0.9876 |

No score change was observed across the four combinations.

Conclusion: `anomaly_ratio` and `clearance_level` were deprioritized.

### 2. history_score + recent_denials

The recorded results were:

| history_score | recent_denials | Result |
|---:|---:|---:|
| 300 | 0 | 0.9876 |
| 900 | 5 | 0.7638 |
| 900 | 0 | 0.8658 |
| 300 | 5 | 0.9458 |

Increasing `history_score` from 300 to 900 decreased the score:

- With `recent_denials = 0`: 0.9876 → 0.8658

Increasing `recent_denials` from 0 to 5 decreased the score:

- With `history_score = 300`: 0.9876 → 0.9458

The combination `history_score = 900` and `recent_denials = 5` produced a score of 0.7638.

Conclusion: both `history_score` and `recent_denials` have negative effects on the score. Their combination is an important relationship observed during the investigation.

### 3. badge_age_days + escorts

The recorded results were:

| badge_age_days | escorts | Result |
|---:|---:|---:|
| 18 | 0 | 0.9458 |
| 75 | 6 | 0.8974 |
| 18 | 6 | 0.9458 |
| 75 | 0 | 0.8974 |

Increasing `badge_age_days` from 18 to 75 decreased the score from 0.9458 to 0.8974.

Changing `escorts` from 0 to 6 did not change the observed score.

Conclusion: `badge_age_days` has a moderate negative effect. `escorts` showed no meaningful effect.

### 4. linked_badges + requested_zone

The recorded results were:

| linked_badges | requested_zone | Result |
|---:|---:|---:|
| 20 | 100 | 0.8583 |
| 0 | 0 | 0.5920 |
| 20 | 0 | 0.8944 |
| 0 | 100 | 0.4475 |

Controlled comparison of `linked_badges`:

- At `requested_zone = 0`:
  0.5920 → 0.8944 when `linked_badges` increased from 0 to 20.
- At `requested_zone = 100`:
  0.4475 → 0.8583 when `linked_badges` increased from 0 to 20.

Therefore, `linked_badges` has a strong positive effect on the score.

Controlled comparison of `requested_zone`:

- At `linked_badges = 0`:
  0.5920 → 0.4475 when `requested_zone` increased from 0 to 100.
- At `linked_badges = 20`:
  0.8944 → 0.8583 when `requested_zone` increased from 0 to 100.

Therefore, `requested_zone` has a negative effect on the score.

The negative effect of `requested_zone` was smaller when `linked_badges` was high. This suggests a compensating relationship between `linked_badges` and `requested_zone`.

### 5. history_score + linked_badges + requested_zone

The recorded three-parameter experiment included the following combinations:

| history_score | linked_badges | requested_zone | Result |
|---:|---:|---:|---:|
| 300 | 0 | 0 | 0.5920 |
| 900 | 20 | 100 | 0.4672 |
| 900 | 0 | 0 | 0.2088 |
| 300 | 20 | 0 | 0.8944 |
| 300 | 0 | 100 | 0.4475 |

These observations support the importance of all three parameters, but the complete three-way interaction cannot be conclusively established from these five recorded combinations because all eight LOW/HIGH combinations were not recorded.

## What we ruled out

Based on the recorded controlled experiments:

- `anomaly_ratio` showed no meaningful score change.
- `clearance_level` showed no meaningful score change.
- `escorts` showed no meaningful score change.

These parameters were therefore treated as low priority for further investigation.

## What we are still unsure about

The experiments provide clear evidence that:

- `linked_badges` increases the score.
- `requested_zone` decreases the score.
- `history_score` decreases the score.
- `recent_denials` decreases the score.
- `badge_age_days` decreases the score moderately.

The strongest observed two-parameter relationship was between `linked_badges` and `requested_zone`.

The recorded three-parameter experiment involving `history_score`, `linked_badges`, and `requested_zone` provides useful evidence, but the complete three-way interaction is not claimed because all eight controlled combinations were not recorded.
