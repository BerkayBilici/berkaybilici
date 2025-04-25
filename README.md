# Analysis of the Relationship Between Game Prices and Player Ratings on Steam

## Motivation
As someone who has been playing games for many years and regularly uses Steam, I’ve always been curious about what influences how players rate a game. Prices on Steam vary widely, and I often wondered whether higher-priced games truly offer better experiences or whether budget and free-to-play games are equally appreciated. Steam is also a platform with an enormous user base and vast amounts of publicly available data. Thanks to this data richness, I knew I could dive into real-world statistics to answer meaningful questions with accessible and well-structured datasets. That made it the perfect environment for both exploring my interest and sharpening my data analysis skills.

## Overview
This project investigates the relationship between game prices and player ratings using a dataset of over 93,000 games published on the Steam platform. As the number of available games grows and player feedback becomes more prominent in purchasing decisions, understanding how price interacts with user ratings has become a relevant issue for both developers and gamers. Our analysis covers not only this core relationship but also explores how player ratings vary by game type (e.g., singleplayer vs. multiplayer), by payment model (free vs. paid), and across different release periods (e.g., pre-pandemic vs. post-pandemic).

Throughout the project, we perform data cleaning, exploratory data analysis (EDA), and hypothesis testing. Each hypothesis is examined using statistical tests such as Pearson correlation and t-tests, and findings are visualized with bar charts, box plots, and correlation heatmaps.

### Key Research Questions:
1. Does price correlate with player ratings?
2. Are free games rated more positively than paid ones?
3. Are multiplayer or singleplayer games rated more positively?
4. Has the price-rating relationship changed across different periods (e.g., COVID period)?

## Dataset
**Source:** [93182 Steam Games](https://www.kaggle.com/datasets/joebeachcapital/top-1000-steam-games?utm_source=chatgpt.com)
# Steam Games: Price vs Rating Analysis

## Data Cleaning

The original dataset had 39 columns. We selected only the relevant ones:

- AppID
- Name
- Release date
- Price
- Positive
- Negative
- Categories
- Genres
- Tags

Further steps:
- Removed games with fewer than 200 total ratings.
- Removed games priced above $100.
- Created a new `Rating` column as:

```python
Rating = Positive / (Positive + Negative)
```

The resulting clean dataset was saved as `clean_steam.csv`.

## Exploratory Data Analysis (EDA)

We visualized various aspects of the dataset:
- Scatter plots and box plots to show price-rating distribution.
- Bar charts showing average ratings across price ranges and periods.
- Correlation heatmaps to compare free vs. paid games.
- Periodic analysis using custom bins: 2006–2013, 2013–2019, 2019–2020, 2020–2023.

## Hypothesis Testing

### H1: Price ↔ Rating Correlation
- **Test:** Pearson and Spearman correlation
- **Result:** Weak but statistically significant positive correlation (Pearson r = 0.0449, p = 0.0204)

### H2: Free vs Paid Games
- **Test:** Independent two-sample t-test
- **Result:**
  - T-statistic = -4.04
  - p = 0.0001
- **Conclusion:** Free games are rated significantly higher.

### H3: Singleplayer vs Multiplayer
- **Test:** t-test
- **Result:**
  - T-statistic = 7.98
  - p < 0.001
- **Conclusion:** Singleplayer games are rated higher than multiplayer games.

### H4: Periodic Price–Rating Correlation
- **Test:** Pearson correlation per period
- **Result:**
  - 2013–2019: r = 0.1306 (p < 0.001)
  - 2020–2023: r = -0.1508 (p < 0.001)
- **Conclusion:** The correlation between price and rating weakened significantly after 2020.

## Summary of Insights

- Free games tend to receive better ratings than paid games.
- Singleplayer games receive higher ratings compared to multiplayer titles.
- The correlation between price and user rating shifted notably after the pandemic.
- Data cleaning choices (like filtering out low-rating-count games and overpriced outliers) were critical to achieving reliable results.

## Tools Used

- Python
- Pandas
- Matplotlib
- Seaborn
- SciPy
- Google Colab

## Files in This Repository

- `clean_steam.csv` — Cleaned dataset used in the project
- `EDA_+_Hypothesis_.ipynb` — Jupyter notebook with all code
- `README.md` — Project summary and methodology


