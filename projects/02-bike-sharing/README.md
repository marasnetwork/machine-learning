# Bike sharing prediction model
## Dataset source
- **Link**: https://archive-beta.ics.uci.edu/dataset/275/bike%2Bsharing%2Bdataset
- **Version / date of download (DD.MM.YYYY)**: Year created 2013 / downloaded 21. 07. 2026
- **Author**: Hadi Fanaee-T
- **License**: CC BY 4.0
## Citation
Fanaee-T, H., Gama, J. (2013). Event labeling combining ensemble 
detectors and background knowledge. Progress in Artificial Intelligence.
DOI: 10.24432/C5W894

## Columns explanation
- **instant** - unique record identifier
- **dteday** - date when the data was collected (`YYYY-MM-DD`)
- **season** - season of the year (`1` = spring, `2` = summer, `3` = fall, `4` = winter)
- **yr** - year (`0` = 2011, `1` = 2012)
- **mnth** - month (`1-12`)
- **holiday** - whether the day was a public holiday (`0` = no, `1` = yes)
- **weekday** - day of the week (`0-6`), where `0` = Sunday, `1` = Monday, ...
- **workingday** - whether the day was a working day (`0` = no, `1` = yes)
- **weathersit** - weather conditions:
  - `1` = clear, partly cloudy
  - `2` = fog, cloudy
  - `3` = light rain or snow
  - `4` = heavy rain, storm, or heavy snow
- **temp** - average temperature of the day (normalized: `0-1`)
- **atemp** - perceived ("feels like") temperature (normalized: `0-1`), considering wind and humidity
- **hum** - humidity (normalized: `0-1`)
- **windspeed** - wind speed (normalized: `0-1`)
- **casual** - number of casual users (without registration)
- **registered** - number of registered users
- **cnt** - total number of rented bikes in a day (`cnt = casual + registered`)

## Conclusion

### Approach
Multiple linear regression was used to predict daily bike rental counts based on seasonal, calendar, and weather variables (season, year, month, holiday, weekday, working day, weather situation, temperature, humidity, windspeed).

### Key findings
- **Non-linearity**: Bike rentals do not scale linearly with weather variables. Quadratic terms (atemp², hum², windspeed²) were added, and the target was log-transformed, to capture diminishing/reversing effects (e.g. rentals drop off at very high temperatures, not just low ones).
- **Multicollinearity**: `temp` and `atemp` were near-duplicate predictors (VIF > 1000), so `temp` was dropped in favor of `atemp`. Squared terms also caused artificial collinearity with their linear counterparts (VIF > 1000); centering the variables before squaring resolved this, bringing all VIF values below 4.
- **Residual diagnostics**: Despite a strong R², residuals show non-normality (skew = -1.48, kurtosis = 8.77, Jarque-Bera p ≈ 0), suggesting the presence of outliers or an unmodeled pattern in the data. This is noted as a limitation rather than resolved.

### Final model
- **Predictors**: season, yr, mnth, holiday, weekday, workingday, weathersit, atemp, hum, windspeed, atemp_sq, hum_sq, windspeed_sq
- **Target**: log(cnt)
- **R²**: 0.835 (train) | **Adj. R²**: 0.831
- **F-statistic**: 222.2 (p ≈ 0), model is highly significant overall
- All predictors are statistically significant (p < 0.05) except `windspeed_sq` (p = 0.057)
- Durbin-Watson = 1.885, indicating no meaningful autocorrelation in residuals

### Limitations
- Residuals deviate from normality (Jarque-Bera test), which may slightly affect the precision of confidence intervals, though it does not invalidate the estimated coefficients.
- The condition number (1.09e+03) is elevated due to differing variable scales rather than true collinearity, as confirmed by VIF; standardizing predictors would reduce this cosmetically without changing model conclusions.

### Possible next steps
- Standardize predictors to reduce the condition number for a cleaner diagnostic profile.
- Investigate residual outliers (e.g. extreme weather days, holidays) to understand the source of non-normality.
- Compare against non-linear models (e.g. random forest, gradient boosting) as a benchmark.