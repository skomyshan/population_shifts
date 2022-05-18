# Database design

## Country data

Table to store country data including:
* ID
* Name
* Country code (2-character)
* Country code (3-character).

Source: [ISO country codes](https://www.iso.org/obp/ui/#search)

1. Copy data to CSV file
2. Load into Pandas
3. Save to SQLite database

## Country statistics

Data used for normalization.
* Country ID
* Year
* Population

## List of wars

Need to store conflicts including countries involved, year or years.

* Could store one record for each year a country was involved in a war, without relating to other countries involved
* Or we could create a table for wars and another table relating wars to countries with years

## Economic indicators

* Country ID
* Year
* Category (e.g. import/export, inflation, military expenditure, agricultural output)
* Value
