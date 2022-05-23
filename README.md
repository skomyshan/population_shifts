# Predicting Population Changes
Github Repository URL: https://github.com/skomyshan/wartime_impact


## Segment 1:

### Presentation
#### Selected Topic: Analyzing various country and regional metrics to estimate their correlation to population growth.
- Using a variety of tools, we will look to analyze the factors that correlate to population growth. These factors include: 
	- Inflation: Used to measure the value of a country's (or region's) currency and possible devaluation of it's population's assets
	- Military Expnediture: Used as a proxy to measure the impact of military conflict
	- Exports as a percentage of GDP: Used to measure the interconnectivity and reliance between countries
	- Life expectancy at birth: Used as a proxy to measure the overall health of a country and the strength of their healthcare system at large
	- GDP (Gross Domestic Product): Used to measure the overall health of the country's economy
 
#### Reasons why we selected this topic
- The impact of Russia's invasion of Ukraine has been felt across the world and will only continue to cause waves as we move further into the conflict. One huge impact is the expected change in population due to war related deaths and the dispersion of its citizens. This made us curious about what impacts are closely related to changes in population. Are there specific metrics that can be used to predict future population changes? Are some metrics better indicators of future population change than others?

#### Description of the Source Data
- Our data was collected from the World Bank Data Catalog. The data catalog is a project by the World Bank "to provide a more effective means for capture, acquisition, curation, access and use of development-Data Catalog data throughout the World Bank Group." They collect data from various other, credited data catalogs (including, but not limited to the Microdata Library, EnergyData.Info, GFDRR, Finances and World Bank Open Data API) with the goal to "maximize the value and investment in data by increasing the potential for the data to be shared and reused, to minimize transaction costs in finding relevant data and data methodologies, and to prevent duplication." 

- From this source, we are have pulled the following metrics from World Developement Indicators (WDI) dataset for use in our predictive modeling:
	- Population, total
	- Inflation, consumer prices (annual %)
	- Military expenditure (% of GDP)
	- Exports of goods and services (% of GDP)
	- Life expectancy at birth, total (years)
	- GDP (current US $)

#### Question we hope to answer with the data
- What are the measurements that strongly correlate to the change in a country's (or region's) population?
	- How does inflation, and variable impacting inflation, affect the population?
	- How does military spending forecast military conflicts and ultimately drive population changes?
	- How do changes in a country's exports relate to their dependence on other countries and impact population changes?
	- How does a country's life expectancy impact changes in their population?
	- How does GDP, a measure of a country's overall economic health, lead to changes in population?
- Does the correlation between these variables and changes in population differ from country to country? Is there a stronger correlation when looking at larger countries? How about when comparing regions? 


### GitHub
#### Communication Protocols
- Group Slack channel will be used for most planning and communication
- We plan to utilize classtime to efficiently discuss our project and work on code as a group
- Additional communication will occur via our phones and the WhatsApp app when necessary

### Machine Learning Model
- The image below will help guide us through the entire project including the machine learning model that we intend to use. At a high level, the model we will be using will be a supervised model that allows us to measure the impact that the independent variables have on population measurements and which variables are most impactful. As we become more familiar with the data and our hypothesis continues to develope, we will construct a more comprehensive plan for our machine learning. 


### Database
- Our database will contain a variety of annual, cross-national metrics which should give us a comprehensive view of the health of a country. This data will be summarized by country, by year and will include everything from economic indicators (like exports, GDP, and inflation) to military expenditures to life expectancy. The data will be connected via country codes and an internal country id (primary key), as well as the year for the time series data. Due to the tabular structure of the data sources being used, our data will be organized using SQLite. This will also give us the ability to seamlessly interact with Tableau for the construction of our presentation.

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

Link to Google Slides- https://bit.ly/39Kn2Zt


## Segment 2:

### Presentation
- Please see the Google Slides presentation in our Github repo for a broader overview of our project.


### Machine Learning
#### Preliminary Data Preprocessing
- In order to effectively use a machine learning model, we first needed to perform steps to combine, clean and organize the data. 
- Before we could combine the data, we needed to re-organize it to better fit our needs. This began by transposing the data so that the years were flipped from the columns to the row inputs. In order to then structure the data so that we could easily be filtered between countries and regions, we need to transpose that data to the rows as well. The final structure of our data has the dependent (population) and independent (inflation, military expenditure, exports, life expectancy, and GDP) variables as the columns of our data. The rows are a combination of country/region codes and the years that data was available. The final structure has a country/region code and a year indexing each row. Going across the row, you can find the metrics for each variable based on that country/region and the year that was indicated. 

#### Preliminary Feature Engineering and Selection
- Since we are interested in looking at the impacts of the six variables that we have pulled data for, we will be utilizing all of the features available.
- In order to get the dependent variable, population, ready for machine learning, we needed to have this variable be binary in nature. We are interested in having this variable measure the changes in population growth for a country or region from year to year. Therefore, we calculated the year-over-year percentage change in a country/region's population and then looked to see if this percentage change increased or decreased from the previous year. If it increased, we assigned a value of 1. If it decreased, we assigned it a value of 0.
- For the inflation variable, the inputs were already a percentage increase from the previous year. Therefore, we did not feel the need to change how the variable was calculated. Unfortunately, we did notice that the inputs used whole numbers to represent a percentage (i.e. 1.75 was inputted for 1.75%, but this should be 0.0175). We corrected this by dividing each value by 100.
- For military expenditure, the values are as a percentage of GDP. Since we are interested in knowing if a country decides to increase the expenditure as a percentage of GDP, we are simply looking at the difference in the percentages from one year to the next. Similar to the percentage inputs for the inflation variable, we need to divide by 100 to make it a true percentage. 
- Since the exports variable is also a percentage of GDP, we used the same data manipulation techniques as was used for military expenditure.
- For life expectancy, the data is inputted as total years. Therefore, to get the year-over-year change, we simply divided the more recent year by the previous year and subtracted 1 to get the percentage increase. 
- Finally, for the GDP variable, we needed to find the percentage change year-over-year and therefore used a similar technique as was used for life expectancy above.
- After correctly adjusting the data to prepare it for our model, we needed to consider whether or not we needed to scale, or normalize the data.

#### Training and Testing Sets
- Before running the data through the model, we split the data for a particular country/region into training and testing sets. In particular, we decided that 20% of the data would be allocated to a testing data set. The other 80% would be used to train the model.
- We decided not to use any over, or under sampling techniques since we felt the data in both sets properly accounted for 

#### Explanation of Model Selection
- For our machine learning technique, we have decided to use the supervised machine learning technique of logistic regression. Logistic regression is used to predict binary outcomes, like whether or not population growth increased or decreased year over year, using multiple variables. The model will determine, given the inputs for inflation, change in military expenditure, change in exports, change in life expectancy and change in GDP, whether or not the population increase is expected to increase or decrease from the previous year.
- The benefits of using a logistic regression model for our project are as follows:
	- Logistic regression models are easier to interpret than other machine learning models.
	- Logistic regression models provide both a measurement of the appropriateness of a predictor AND a direction of the association between the dependent variable and each of the independent variables.
	- Logistic regression models work well with simple, linear data sets, like the one that we have for each country/region.
	- One can interpret coefficients of the logistical regression model as an indicator of feature importance.
	- Compared to other techniques, logistical regression models are less inclined to overfit datasets.
- The limitations of using a logistic regression model for our project are as follows:
	- The use of a logistic regression model does require the output to be in the form of a binary output (i.e. a discrete function). This means we needed to create a distinction between the binary outputs for population growth.
	- Logistic regression models assume linearity between independent and dependent variables. This relationship may not actually exist in reality.
	- Logistic regression models make it difficult to suss out complex relationships between variables.


### Database
#### Database Contents
- Our database will be responsible for holding the transformed data tables from each of the six variables that we will be utilizing. These tables will then be joined into one file using the country code and year primary keys to make the data file that will be ingested by the machine learning model.

### Dashboard
- As requested, we have included overviews of our potential storyboard in the Google Slides presentation for Segment 2.

#### The Tools Being Used
- For our final presentation we plan to use a mixture of Tableau and Google Slides. Tableau will be used to create dashboards and a storyboard that can then be utilized in the Google Slides we create. We plan to walk the class through the Slides during our presentation. 

#### Interactive Elements
- Our vision is that the dashboard will allow users to select different countries or regions (via a drop-down box) to view the differences in the data, as well as the differences in the output from our machine learning model. All parts of our dashboard will update to reflect the country/region selected.
