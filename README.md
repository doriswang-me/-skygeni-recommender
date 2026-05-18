# SkyGeni Sequential Recommender

A hybrid Markov + Association Rules recommender that predicts the next product
a B2B account will buy. Built as a Practicum project at Santa Clara University
in partnership with SkyGeni.

🔗 **Live site**: https://doriswang-me.github.io/skygeni-recommender/

## Headline Results

- **68% Hit@1** — for two-thirds of accounts, the model's #1 pick is exactly the next product purchased
- **86% Hit@3** — top-3 recommendations contain the correct product
- **98% Hit@10** — top-10 nearly always contains it
- Evaluated on 3,510 accounts with leave-last-out protocol

## Approach

Seven-signal hybrid combining:
- Four orders of Markov chains (orders 1–4)
- Association rules (confidence + lift)
- Stage-aware popularity
- Cascading fallback for unseen higher-order states

## Team

- Doris Wang
- Liwen Chen
- Zenning He
- Faculty Advisor: Sami Najafi

Santa Clara University · May 2026
