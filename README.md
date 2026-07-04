# Health Data Analytics

A statistical health-data analysis of dietary aflatoxin exposure from wheat, rice, and milk consumption. The project turns 192 survey responses into estimated daily intake (EDI), margin of exposure (MOE), and a cancer-risk proxy, then evaluates how those measures vary across demographic groups.

## Project at a glance

| Area | Implementation |
|---|---|
| Data source | Excel survey data, 192 responses and 17 source columns |
| Data preparation | Category mapping, missing-value handling, frequency normalization, filtering |
| Feature engineering | Daily food intake, EDI, MOE, cancer-risk proxy, height, BMI, BMI category |
| Exploratory analysis | Descriptive statistics, demographic group summaries, correlation analysis |
| Statistical analysis | Independent two-sample t-tests, one-way ANOVA, 95% confidence intervals |
| Visualization | Heatmap, scatter plots, bar charts, histograms, kernel density estimates |
| Environment | Python in Google Colab / Jupyter Notebook |

## Tools and concepts demonstrated

- **Python** for the end-to-end analytical workflow
- **pandas** for Excel ingestion, tabular transformations, grouping, binning, and descriptive statistics
- **NumPy** for numerical operations and summary-statistic calculations
- **SciPy** for t-tests, one-way ANOVA, and Student's t-distribution
- **Matplotlib and Seaborn** for statistical visualization
- **Google Colab and Google Drive** for notebook execution and data access
- **Health-risk analytics** using EDI, MOE, and a potency-weighted cancer-risk proxy
- **Survey-data engineering** by translating categorical portions and consumption frequencies into estimated daily quantities
- **Inferential statistics** to compare demographic groups and quantify uncertainty

## Analysis pipeline

```text
Excel survey
    -> portion categories mapped to grams/millilitres
    -> consumption frequency normalized to daily intake
    -> food-specific and total EDI calculated
    -> MOE and cancer-risk proxy derived
    -> height and BMI features engineered
    -> demographic summaries and visual exploration
    -> t-tests, ANOVA, and 95% confidence intervals
```

The analysis uses food-specific concentration constants and respondent body weight to calculate EDI. It then derives MOE as `400 / EDI` and calculates the risk proxy using a weighted average potency factor. Fresh and packaged milk use different concentration constants in the notebook.

## Selected notebook results

After excluding four records with zero daily milk intake, the analysis contains 188 observations:

| Measure | Mean | 95% confidence interval |
|---|---:|---:|
| Total EDI | 45.7361 | 42.4432–49.0289 |
| Total MOE | 13.1429 | 9.4368–16.8490 |
| Total cancer-risk proxy | 0.9216 | 0.8552–0.9879 |

The recorded notebook outputs also show:

- Total cancer-risk proxy differs by gender in the independent t-test (`p = 0.0018`).
- Total MOE differs by gender (`p = 0.0077`).
- Cancer-risk proxy differs across BMI categories in the one-way ANOVA (`p = 0.0001`).
- The notebook does not find statistically significant BMI-category differences for total MOE, or age/location differences for either outcome at the 0.05 level.
- Wheat EDI has the strongest recorded correlation with the total cancer-risk proxy (`r = 0.829`) among the three food-specific EDI measures.

These are analytical outputs from this sample, not clinical conclusions.

## Repository structure

```text
health_data_analytics/
├── data/
│   └── SMM - Survey Responses.xlsx
├── docs/
│   └── Report.pdf
├── notebooks/
│   └── Statistical_Data_Analysis.ipynb
└── README.md
```

## Run the analysis

The notebook was authored for Google Colab:

1. Upload or clone this repository to Google Drive.
2. Open `notebooks/Statistical_Data_Analysis.ipynb` in Google Colab.
3. Update the Excel path in the data-loading cell to the location of `data/SMM - Survey Responses.xlsx`.
4. Run the cells in order.

The required Python packages are:

```python
pandas
numpy
scipy
matplotlib
seaborn
openpyxl
```

For local Jupyter use, remove the Google Drive mount cell and replace the hard-coded Colab path with a local relative path such as:

```python
smm = pd.read_excel("../data/SMM - Survey Responses.xlsx")
```

