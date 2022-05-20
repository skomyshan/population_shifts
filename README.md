# Predicting Population Changes
Github Repository URL: https://github.com/skomyshan/wartime_impact


## Segment 1:

### Presentation
#### Selected Topic: Analyzing various country and regional metrics to estimate their correlation to population growth.
- Using a variety of tools, we will look to analyze the factors that correlate to population growth. These factors include: 
	- Inflation: Used to measure the value of a country's (or region's) currancy and possible devaluation of it's population's assets
	- Military Expediture: Used as a proxy to measure the impact of military conflict
	- Exports as a percentage of GDP: Used to measure the interconnectivity and reliance between countries
	- Life expectancy at birth: Used as a proxy to measure the overall heath of a country and the strength of their healthcare system at large
	- GDP (Gross Domestic Product): Used to meaure the overall health of the country's economy
 
#### Reasons why we selected this topic
- The impact of Russia's invasion of Ukraine has been felt across the world and will only continue to cause waves as we move further into the conflict. One huge imact is the expected change in population due to war related deaths and the dispersion of its citizens. This made us curious about what impacts are closely related to changes in population. Are there specific metrics that can be used to predict future population changes? Are some metrics better indicators of future population change than others?

#### Description of the Source Data
- Our data was collected from the World Bank Data Catalog. The data catalog is a project by the World Bank "to provide a more effective means for capture, acquisition, curation, access and use of development-Data Catalog data throughout the World Bank Group." They collect data from various other, credited data catalogs (including, but not limited to the Microdata Library, EnergyData.Info, GFDRR, Finances and World Bank Open Data API) with the goal to "maximize the value and investment in data by increasing the potential for the data to be shared and reused, to minimize transaction costs in finding relevant data and data methodologies, and to prevent duplication." 

From this source, we are have pulled the following metrics from World Developement Indicators (WDI) dataset for use in our predictive modeling:
	- Population, total
	- Inflation, consumer prices (annual %)
	- Military expenditure (% of GDP)
	- Exports of goods and services (% of GDP)
	- Life expectancy at birth, total (years)
	- GDP (current US $)


#### Question we hope to answer with the data
- What are the measurements that strongly correlate to the change in a country's (or region's) population?
	- How does inflation, and variable impacting inflation, affect population?
	- How does military spending forecast military conflicts and ultimately drive population changes?
	- How do changes in a country's exports relate to their dependence on other countries and impact population changes?
	- How does a countries life expectancy impact the their population?
	- How does GDP, a measure of a countries overall economic health, lead to changes in population?
- Does the correlation between these variables and changes in population differ from country to country? Is there a stronger correlation when looking at larger countries? How about when comparing regions? 

### GitHub
#### Communication Protocols
- Group Slack channel will be used for most planning and communication
- We plan to utilize classtime to efficiently discuss our project and work on code as a group
- Additional communication will occur via our phones and the WhatsApp app when necessary

### Machine Learning Model
- The image below will help guide us through the entire project including the machine learning model that we intend to use. At a high level, the model we will be using will be a supervised model that allows us to measure the impact that the independent variables have on population measurements and whcih variables are most impactful. As we become more familiar with the data and our hypothesis developes, we will construct a more comprehensive plan for our machine learning. 

![Roadmap](https://github.com/skomyshan/wartime_impact/blob/main/Group%206%20Project%20Road%20Map.png)

### Database
- Our database will contain a variety of annual, cross-national metrics which should give us a comprehensive view of the health of a country. This data will be summarized by country, by year and will include everything from economic indicators (like import/export and inflation) to military expenditures to agrecultural output. The data will be connected via country codes and an internal country id (primary key), as well as the year for the time series data. Due to the tabular structure of the data sources being used, our data will be organized using SQLite. This will also give us the ability to seamlessly interact with Tableau for the construction of our presentation.

#### Tools
- The following steps of our analysis will require various tools to be used. Our plan is to use the tools listed below to maximize efficiency and produce the best results.
	- Creating Database
  	  - PostgreSQL
	- Analyzing Data
	  - Python in Jupyter Notebook
	- Machine Learning
	  - Python in Jupyter Notebook
	- Dashboard and Presentation
	  - Tableau
	  - Google Sheets

### Visualization
Will be using Tableau to create dashboards to study the impacts of various attributes on population. Google Slides will also be used for presentation purposes.

## Segment 2:

### Presentation
- Please see the Google Slides presentation in our Github repo for a broader overview of our project.

### Machine Learning
#### Preliminary Data Preprocessing
- In order to effectively use a machine learning model, we first needed to perfom steps to combine, clean and organize the data. 
- Before we could combine the data, we needed to re-organize it to better fit our needs. This began by transposing the data so that the years were flipped from the columns to the row inputs. In order to then structure the data so that we could easily be filtered between countries and regions, we need to transpose that data to the rows as well. The final structure of our data has the dependent (population) and independent (inflation, military expenditure, exports, life expectancy, and GDP) variables as the columns of our data. The rows, are a combination of country/region codes and the years that data was available. The final structure has a country/region code and a year indexing each row. Going across the row, you can find the metrics for each variable based on that country/region and the year that was indicated. 

#### Preliminary Feature Engineering and Selection
- Since we are interested in lookig at the impacts of the six variables that we have pulled data for, we will be utilizing all of the features available.
- In order to get the dependent variable, population, ready for machine learning, we needed to have this variable be binary in nature. We are interested in having this variable measure the changes in population growth for a country or region from year to year. Therefore, we calculated the year-over-year percentage change in a country/region's population and then looked to see if this percetage change increased or decreased from the previous year. If it increased, we assigned a value of 1. If it decreased, we assigned it a value of 0.
- For inflation variable, the inputs were already a percentage increase from the previous year. Therefore, we did not feel the need to change how the variable was   