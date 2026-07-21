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