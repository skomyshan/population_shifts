# Predicting Population Changes
Github Repository URL: https://github.com/skomyshan/wartime_impact


## Segment 1:

### Presentation
#### Selected Topic: Analyzing various country and regional metrics to estimate their potential impact on population growth.
- Using a variety of tools, we will look to analyze the factors that impact population growth. These factors include CPI (Consumer Price Index - to measure inflation), military expediture (used as a proxy to measure the impact of military conflict), exports as a percentage of GDP, life expectancy at birth, and GDP (Gross Domestic Product - to meaure the overall health of the country's economy).
 
#### Reasons why we selected this topic
- The impact of Russia's invasion of Ukraine has been felt across the world and will only continue to cause waves as we move further into the conflict. One huge imact is the expected change in population due to war related deaths and the dispertion of its citizens. This got us curious about what impacts are closely related to changes in population. Are there specific metrics that can be used to possibly predict the impact that certain events will have on population changes. 

#### Description of the Source Data
- Most of our data is coming from the 

#### Question we hope to answer with the data
- How does military spending affect a country's GDP?
- How does military spending affect imports/exports?
- How does military spending affect inflation?
- Do other types of goverment spending have any significant impact on economic growth?

### GitHub
#### Communication Protocols
- Group Slack channel will be used for most planning and communication
- We plan to utilize classtime to efficiently discuss our project and work on code as a group
- Additional communication will occur via our phones and the WhatsApp app when necessary

### Machine Learning Model
- The image below will help guide us through the entire project including the machine learning model that we intend to use. At a high level, the model we will be using will be a supervised model that allows us to measure the impact that one variable (the presence of a war or conflict) has on various other variables, highlighting the variables that are most impacted. As we become more familiar with the data and our hypothesis developes, we will construct a more comprehensive plan for our machine learning. 

### Database
- Our database will contain a variety of annual, cross-national metrics which should give us a comprehensive view of the health of a country. This data will be summarized by country, by year and will include everything from economic indicators (like import/export and inflation) to military expenditures to agrecultural output. The data will be connected via country codes and an internal country id (primary key), as well as the year for the time series data. Due to the tabular structure of the data sources being used, our data will be organized using SQLite. This will also give us the ability to seamlessly interact with Tableau for the construction of our presentation.

### Visualization
Will be using Tableau to create dashboards and study the impacts of war on various attributes across countries.

 the final project deliverable.

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
