# Google Play Apps and Reviews Exploratory Data Analysis 📱📊

This project contains a documented Jupyter notebook for **CSB314 - Exploratory Data Analysis**, Minor Project 02 (CA 03). It studies the supplied Google Play app catalog and user-review files, checks data quality, creates app-level features, aggregates reviews, and explores the available measures.

## 📁 Project files

| File | Description |
| --- | --- |
| `google_play_apps_and_reviews_eda.ipynb` | Main notebook with detailed Markdown, Python code, generated results and plots, observations, and conclusions. |
| `googleplaystore.csv` | App catalog used for app-level analysis. |
| `googleplaystore_user_reviews.csv` | User-review text and sentiment measures, summarized by app before integration. |
| `license.txt` | Licence statement supplied with the dataset. |

## 🎯 Project objectives

- Understand the row grain and key fields in both datasets.
- Check missing values, duplicates, invalid ratings, and sentiment value ranges.
- Create useful features from ratings, review counts, installs, price, size, genres, and update dates.
- Summarize apps by category and compare type and content-rating groups.
- Reshape category summaries using Pandas methods.
- Aggregate the many review rows to one row per app before joining to the app catalog.
- Calculate descriptive statistics and explore distributions, sampling, correlation, and outlier methods.
- Explain the limitations of the supplied historical snapshot.

## 🗃️ Data files and row grain

The app catalog contains one or more metadata rows per app name. The review file contains individual review rows, so an app can have many reviews. The shared field is `App`.

The notebook checks repeated app names and removes exact duplicate catalog rows in a working copy. It excludes a visibly malformed row with a rating outside the expected range and missing category information. For a one-row-per-app analysis table, it retains the row with the most recent parseable `Last Updated` date for each app name.

Review rows with missing text or sentiment, or invalid polarity and subjectivity values, are excluded from sentiment calculations. The notebook reports duplicate review rows and does not silently remove them. It aggregates the remaining reviews by app before joining, which prevents multiple review rows from multiplying the app records.

## ⚙️ Requirements

Use Python 3 with Jupyter Notebook, JupyterLab, or VS Code. The notebook uses Pandas, NumPy, Matplotlib, and Seaborn.

```bash
python -m pip install pandas numpy matplotlib seaborn jupyter
```

## ▶️ How to run

1. Keep all three supplied data files in the same folder as the notebook.
2. Open `google_play_apps_and_reviews_eda.ipynb` in Jupyter Notebook, JupyterLab, or VS Code.
3. Select a Python 3 kernel.
4. Run all cells from top to bottom.

The notebook uses relative file paths and does not depend on a specific computer's folder structure.

## 🧮 Main derived features

The notebook creates these fields in a working copy:

| Feature | Source or formula | Meaning and limit |
| --- | --- | --- |
| `rating_numeric` | Numeric conversion of `Rating` | App rating in the supplied snapshot. |
| `review_count` | Numeric conversion of `Reviews` | Review count recorded in the catalog snapshot. |
| `installs_lower_bound` | Remove commas and plus sign from `Installs` | Lower bound from a rounded install band, not an exact count. |
| `price_usd` | Remove `$` from `Price` | Price in dollars where parsing succeeds. |
| `size_mb` | Convert M to MB and k to MB | `Varies with device` is left missing. |
| `genre_count` | Count semicolon-separated values in `Genres` | Number of genre labels, not number of app categories. |
| `is_free` | `Type` equals `Free` | Boolean app-type feature. |
| `update_year`, `update_month` | Parsed `Last Updated` date | Missing if the date cannot be parsed. |
| Review summary measures | Group valid review rows by `App` | Mean polarity and subjectivity, review count, and sentiment shares. |

## 📚 Notebook sections

1. Problem and objectives
2. Dataset source and description
3. Import libraries and load the data
4. Dataset understanding and row grain
5. Data-quality assessment
6. Feature engineering and app catalog cleaning
7. Grouping, aggregation, and transformation
8. Pivot table and crosstab
9. Data reshaping
10. Data integration and join validation
11. Descriptive statistics
12. Distribution analysis
13. Empirical rule demonstration
14. Sampling and the Central Limit Theorem
15. Correlation and relationship analysis
16. Outlier detection and treatment
17. Findings, limitations, and future scope
18. Conclusion

## 📈 Interpretation notes

- Install values are rounded bands. Their numeric conversion is a lower-bound estimate.
- Ratings are bounded between 1 and 5; install and review counts are highly skewed.
- Review sentiment is calculated only from complete rows with valid numeric sentiment values.
- Review sentiment summaries describe rows in this dataset; repeated review rows are reported and retained.
- The app name is the join key. Name changes and inconsistent spelling can create unmatched records.
- The app catalog is reduced to one row per app name using the most recent parseable update date. This resolves duplicate keys for analysis but may omit older metadata rows.
- Correlation shows association and does not prove causation.
- Simulated examples are marked in the notebook and are not results from the Google Play data.

## ⚠️ Limitations

These files represent a historical dataset snapshot. They do not provide current app listings or exact install counts. The install values are bands, review fields are incomplete, and app names may not always match exactly between tables. Sentiment polarity and subjectivity are derived measures and should not be treated as verified opinions from every user.

The results describe the supplied records only. They do not establish why apps receive a particular rating, number of installs, or sentiment score.

## 📜 Licence and attribution

The supplied `license.txt` states that the work is licensed under the **Creative Commons Attribution 3.0 Unported (CC BY 3.0)** licence. Give appropriate credit, link to the licence, and indicate if changes were made when redistributing material under those terms.

Licence: [Creative Commons Attribution 3.0 Unported](https://creativecommons.org/licenses/by/3.0/)
