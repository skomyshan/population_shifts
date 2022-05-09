# Database design

## Country data

Table to store country data including id, name, country code.

## List of wars

Need to store conflicts including countries involved, year or years.

* Could store one record for each year a country was involved in a war, without relating to other countries involved
* Or we could create a table for wars and another table relating wars to countries with years

## Economic indicators

* Country ID
* Year
* Category (e.g. import/export, inflation, military expenditure, agricultural output)
* Value
