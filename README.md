# Chameleon Dataset

A dataset of 5,001 contextual psychological profiles from 1,667 Reddit users, enabling analysis of within-person psychological variation across contexts.

## Overview

Chameleon captures how the same user expresses different psychological states across different subreddit contexts. Unlike prior persona datasets that treat psychology as static traits, Chameleon measures users across multiple contexts, revealing that **74% of psychological variance is within-person (state) rather than between-person (trait)**.

## Dataset Statistics

| Metric | Value |
|--------|-------|
| Total posts | 5,001 |
| Unique users | 1,667 |
| Posts per user | 3 |
| Unique subreddits | 645 |
| Psychological dimensions | 26 |
| Extraction methods | 2 (SEANCE, LangExtract) |

## File Description

**chameleon_profiles.csv** contains psychological profiles with the following columns:

### Metadata
- `post_id`: Unique identifier for each post
- `user_id`: Anonymized user identifier (user_0000, user_0001, ...)
- `subreddit`: Subreddit context where the post was made

### Psychological Scales (26 dimensions × 3 variants)

Each scale has three variants:
- `_seance`: Extracted using SEANCE (lexicon-based)
- `_langextract`: Extracted using LangExtract (LLM-based)
- `_combined`: Average of SEANCE and LangExtract

Plus z-normalized versions (`_z` suffix) for each.

**Big Five Inventory (BFI-44)**
- `bfi_extraversion_avg_*`
- `bfi_agreeableness_avg_*`
- `bfi_conscientiousness_avg_*`
- `bfi_neuroticism_avg_*`
- `bfi_openness_avg_*`

**Schwartz Value Survey (SVS-57)**
- `svs_power_avg_*`
- `svs_achievement_avg_*`
- `svs_hedonism_avg_*`
- `svs_stimulation_avg_*`
- `svs_self_direction_avg_*`
- `svs_universalism_avg_*`
- `svs_benevolence_avg_*`
- `svs_tradition_avg_*`
- `svs_conformity_avg_*`
- `svs_security_avg_*`

**Self-Determination Theory (SDT)**
- `sdt_intrinsic_motivation_avg_*`
- `sdt_extrinsic_motivation_avg_*`
- `sdt_competence_avg_*`
- `sdt_autonomy_avg_*`
- `sdt_relatedness_avg_*`

**Domain-Specific Risk-Taking (DOSPERT-40)**
- `dospert_investment_avg_*`
- `dospert_gambling_avg_*`
- `dospert_health_safety_avg_*`
- `dospert_recreational_avg_*`
- `dospert_ethical_avg_*`
- `dospert_social_avg_*`

### Cross-Method Agreement
- `profile_similarity`: Pearson correlation between SEANCE and LangExtract profiles for each post

## Usage

```python
import pandas as pd

# Load dataset
df = pd.read_csv('chameleon_profiles.csv')

# Get all posts for a user
user_posts = df[df['user_id'] == 'user_0000']

# Compute ICC for a scale
from scipy.stats import f_oneway
# ... your analysis code
```

## Scale Interpretation

Raw scores (`_combined`) use the original scale ranges:

| Framework | Scale Range |
|-----------|-------------|
| Big Five (BFI-44) | 1–5 |
| Schwartz Values (SVS-57) | −1–7 |
| Self-Determination Theory (SDT) | 1–7 |
| DOSPERT Risk Attitudes | 1–5 |

Z-scores (`_combined_z`) are standardized per dimension:
- 0: Dataset mean
- ±1: One standard deviation from mean

For cross-scale comparisons, use the z-scored columns.

## Citation

```
[Citation will be added upon publication]
```

## License

CC-BY-4.0

## Source Data

Profiles extracted from the Webis-TLDR-17 corpus (Völske et al., 2017), a publicly available dataset of Reddit posts.

