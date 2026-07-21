# Diamond price prediction model
## Dataset source
- **Link**: https://www.kaggle.com/datasets/shivam2503/diamonds
- **Version / date of download (DD.MM.YYYY)**: Version 1 / 17.07.2026
- **Author**: Shivam Agrawal, Danny (Kaggle)
- **License**: Unknown

## Columns explanation
- **carat** – the weight of the diamond (1 carat = 0.2 g); larger carat means a bigger stone
- **cut** – the quality of the diamond's cut, i.e. how well it's been cut (affects how light reflects). Ordered worst to best: Fair → Good → Very Good → Premium → Ideal
- **color** – the diamond's color, graded from D (best, completely colorless) down to Z (yellowish). This dataset ranges from D (best) to J (worst). Less color = more valuable
- **clarity** – how free the diamond is of internal flaws (inclusions). Ordered worst to best: I1 → SI2 → SI1 → VS2 → VS1 → VVS2 → VVS1 → IF
- **depth** – total depth percentage: the diamond's height relative to its average diameter (z ÷ mean(x, y))
- **table** – the width of the diamond's flat top facet as a percentage of its widest point
- **price** – the price of the diamond in US dollars
- **x** – length in mm
- **y** – width in mm
- **z** – depth (height) in mm

> The first four columns (carat, cut, color, clarity) are known as the **"4 Cs"** – the main factors that determine a diamond's value.

## Conclusion

### Aproach
Simple and multiple linear regression were used to predict diamond prices based on physical dimensions 4 Cs (carat, cut, color, clarity). 4 Cs dimensions were ordinal-encoded to preserve their natural ranking (worst -> best).

### Key findings
- **Non-linearity**: Diamond price does not scale linearly with size. Both price and size was log-log transformed to get linear relationship.
- **Omitted variable bias**: Using size as one predictor caused high difference between RMSE and MAE. Adding categorical predictors was required action to improve model accuracy.
- **Data quality**: Rows with zero-valued dimensions (x, y, z = 0) and extreme high-leverage points (size > 1000 mm^3) were removed prior to modeling.

### Final model
- **Predictors**: log(size), cut_encoded, color_encoded, clarity_encoded
- **Target**: log(price)
- **R^2**: 0.977 (train)
- **Train MAE**: 0.116 (log scale) | **Train RMSE**: 0.154 (log scale)
- **Test MAE**: 0.115 (log scale) | **Test RMSE**: 0.147 (log scale)
- Train and test metrics are nearly identical, indicating the model generalizes well and does not overfit.

### Possible next steps
- Compare against non-linear models (e.g. random forest, gradient boosting) as a benchmark