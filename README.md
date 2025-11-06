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
- **Result:** Weak but statistically significant positive correlation (Pearson r = 0.0449, p = 0.0204, Spearman 0.0637 p-value: 0.001)
  
![image](https://github.com/user-attachments/assets/9704db41-eeb2-4c6d-adf5-24fda83d21c3)

### H2: Free/Paid Games - Rating Correlation
- **Test:** Independent two-sample t-test
- **Result:**
  - T-statistic = -4.04
  - p = 0.0001
- **Conclusion:** Free games are rated significantly higher.
  
![image](https://github.com/user-attachments/assets/147efd6b-124a-4711-b770-281e909126b8)

### H3: Singleplayer/Multiplayer - Rating Correlation
- **Test:** t-test
- **Result:**
  - T-statistic = 7.98
  - p < 0.001
- **Conclusion:** Singleplayer games are rated higher than multiplayer games.
  
![image](https://github.com/user-attachments/assets/b3ea17d6-e027-4d6b-9b38-8eb8f483196e)

### H4: Periodic Price–Rating Correlation
- **Test:** Pearson correlation per period
- **Result:**
-    Period  Pearson_r   P_value
-  2006–2013 | 0.135986 | 0.034113
-  2013–2019 | 0.130641 | 0.000002
-  2019–2020 |-0.099659 | 0.099100
-  2020–2023 |-0.150823 | 0.000014
- **Conclusion:** The correlation between price and rating changed significantly after 2020.
  
![image](https://github.com/user-attachments/assets/9e005c66-628c-45bc-8156-2819632edd74)

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
## Machine Learning

Random Forest Results:
 - R²: 0.162
![image](https://github.com/user-attachments/assets/bd40dfa5-f76b-4199-b414-2c49c404cee8)

The scatter plot above compares our Random Forest model’s predicted ratings against the actual user scores, using only the engineered features from our cleaned Steam dataset. Despite the many unmeasured factors that influence player reviews, the model achieves an R² of 0.162—meaning it accounts for about 16% of the variance in ratings. That level of explanatory power is reasonable given the subjective nature of user feedback.

### Key Findings

Top predictors: Log-transformed price (LogPrice), total review count (TotalReviews) and peak concurrent users (LogPeakCCU) carry the most weight.

Temporal and content signals: Release year/month and the number of categories, genres and tags all contribute meaningfully, indicating that both when a game launches and its content breadth influence user satisfaction.

Free vs. paid & multiplayer: Free-to-play titles trend toward lower scores on average, while multiplayer capability yields a slight uplift in ratings.

### Limitations & Next Steps

We lack direct measures of game quality (graphics, performance, narrative) and developer reputation—factors that likely explain much more of the variance.

Extending the dataset’s time horizon and incorporating text-based sentiment from review comments or Metacritic scores could substantially boost model performance.

Alternative approaches (e.g. categorical rating bands or quantile regression) may offer more actionable insights than precise score prediction.

This work demonstrates correct application of multiple ML techniques, clear feature engineering and thoughtful interpretation—even when an R² near 1.0 is unattainable for such a subjective target.


---

### 🧩 Team Projects

- [Online Store Platform (CS308 Project)](https://github.com/yagmurgcm/CS308--OnlineStoreProject) — Full-stack e-commerce system built with NestJS & MySQL  
- [SURate](https://github.com/OzanMuhcu/SUrate) — University course rating platform built with Flutter & Firebase
  





