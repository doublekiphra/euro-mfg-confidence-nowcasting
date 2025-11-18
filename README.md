# Euro Area Manufacturing Confidence Nowcasting with Social Media & LLMs

This repository contains code and experiments for nowcasting the Euro Area Manufacturing Confidence Indicator using
collective intelligence extracted from social media (e.g. Guardian news comments) and Large Language Models (LLMs).

## Main Idea

1. Collect comments from Guardian news articles related to the euro-area economy and manufacturing.
2. Use an LLM classifier to label each comment as UP / DOWN / NEUTRAL with respect to future euro-area manufacturing conditions.
3. Aggregate these labels into a daily high-frequency sentiment index and smooth it with a moving average filter.
4. Use the smoothed index to nowcast the monthly Euro Area Manufacturing Confidence Indicator (FRED series: BSCICP02EZM460S),
   and compare performance against a pure autoregressive (AR) baseline.

## Structure

- `data/`: raw, interim, and processed datasets.
- `notebooks/`: Jupyter notebooks for scraping, labeling, feature construction, and modeling.
- `src/`: reusable Python modules for data processing, feature engineering, and models.
- `scripts/`: pipeline / training scripts.
- `tests/`: unit tests.
