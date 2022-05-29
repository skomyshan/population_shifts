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
- Can the variables of inflation (and variables impacting inflation), military spending (forecast proxy for military conflicts), exports and GDP (economic measures), and a country's life expectancy (a measure of a country's overall economic health) be used to effectively model population change from year to year in a country or across the world. 
- Is there a grouping (of either countries or years) that would allow us to better predict population change and, if so, what are the groupings? What does this tell us about the variables that impact population. 


### Machine Learning Model
- The image below will help guide us through the entire project including the machine learning model that we intend to use. At a high level, the model we will be using will be a supervised model that allows us to measure the impact that the independent variables have on population measurements and which variables are most impactful. As we become more familiar with the data and our hypothesis continues to develop, we will construct a more comprehensive plan for our machine learning. 

<img width="1092" alt="Group 6 Project Road Map (2)" src="https://user-images.githubusercontent.com/95661553/169725733-44c389c4-c5ee-4d8d-a6e0-7abf88910934.png">

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



## Segment 2:

### Presentation
Please see the Google Slides presentation in our Github repo for a broader overview of our project.

Link to Google Slides- https://bit.ly/39Kn2Zt


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
- For now, have copied all the six excels as data source. Have created placeholder Worksheets demonstrating correlations between:
	* Inflation with Population
	* Military Expenditure with Population
	* Exports with Population
	* Life Expectancy with Population
	* GDP with Population
- Since we have run the data using Machine Learning models now in segment 2, will be using that data further in next segment to create visualizations.
- **Next Step(s)** shall be to create Dashboards and story highlighting correlation between these variables and changes in population differ from country to country using data in excel sheets and machine learning models.

Link to Tableau Dashboard: https://tabsoft.co/388OwYf

#### The Tools Being Used
- For our final presentation we plan to use a mixture of Tableau and Google Slides. Tableau will be used to create dashboards and a storyboard that can then be utilized in the Google Slides we create. We plan to walk the class through the Slides during our presentation. 

#### Interactive Elements
- Our vision is that the dashboard will allow users to select different countries or regions (via a drop-down box) to view the differences in the data, as well as the differences in the output from our machine learning model. All parts of our dashboard will update to reflect the country/region selected.



## Segment 3:

### Presentation
Please see the Google Slides presentation in our Github repo for a broader overview of our project.

Link to Google Slides- https://bit.ly/39Kn2Zt


### Machine Learning
- Please see the Machine Learning subsection found in the Segment 2 section of the README for an overview of the following: 
	- The data processing steps
	- The feature engineering and selection process
	- The splitting of the training and testing data
	- The Explaination of our intitial model choice

#### Explanation of Model Changes and Model Training Techniques
- In an effort to try and increase the accuracy score of our model and to try and suss out additional insights, we decided to introduce an unsupervised machine learning component to our model to try and group the individual data points in the master data set into groups. The technique chosen was k-means clustering.
- Before performing the unsupervised learning, we needed to prepare the data to better visualize and work with the data. Therefore, we decided to reduce the data dimentionality of our database using PCA. PCA was used after standardizing the data with a Standard Scaler methodology to reduce the data to three principal components; PC 1, PC 2, and PC 3.
- Next, we needed to determine the number of clusters to use for our k-means model. In other words, it helps us decide the number of unique groupings that will be best to separate the data into. To do this we ran and ploted the data's inertia (a multivariate measure of the amount of variation in a data set) when clustering in a range of groups from 1 to 11. The result can be found in the image below which is refered to as an elbow curve. To select the best number of clusters, we want t find the inflection point in the elbow curve. For this data that was particularly difficult with no obvious point where the rediuction in inertia significantly slows. We felt that k=5 and k=6 were the best points and decided to move forward with k=5. 

<img width="1092" alt="k-means Elbow Curve" src="https://github.com/skomyshan/predicting_population_change/blob/main/resources/k-means_elbow_curve.png">

- After deciding on k=5, we are able to build and fit the k-means model to predict the 5 clusters within the data. Once the model runs, we appended the class number onto the original dataset and created the visual below to review the groupings based on the three PCA components. 
	- Reviewing the visual, it is clear that the clustering resulted in two large groups (labeled Class 0 and Class 1) and three smaller groupings consisting of 1 or two data points. Reviewing the results when run with k=6 and k=4, we see similar results with 2 main groupings.

<img width="1092" alt="Clusters" src="https://github.com/skomyshan/predicting_population_change/blob/main/resources/cluster_results.png">

- Downloading the data into an Excel file, we reviewed the classes in more detail to try and find a connection between the points that is more intuitive. First, we looked at each country and the split of the available data points to see if there are some countries that are almost exclusively in one class or another. Our hope was that the groupings would split the data by region or by economic standing (i.e., first vs third world countries), but there didn't seem to be any split like that. Our next review was of the years to see if there was a difference in the grouping based on year of the datapoint. Reviewing this, we did find that points were consistantly more likely to fall into Class 0 for more modern years (1990's through to 2020) with early years (prior to the 1970's) were more likely to call into Class 1. Unfortunately, we did not feel as thought these splits were significant enough for us to say that the groupings had a connection to the year of the data.
	- For a review of the clusters, please see the file at the following link: 
		- https://github.com/skomyshan/predicting_population_change/blob/main/resources/Cluster_Review.xlsx 

#### Description of Current Accuracy Score
- When running the initial supervised machine learning model, we were able to generate a accuracy score of .6143. In addition, please see the image below for confusion matrix and classification report. 

<img width="1092" alt="Results from Initial ML" src="https://github.com/skomyshan/predicting_population_change/blob/main/resources/Machine_Learning_v1.png">

- While the accuracy score was reasonable, we introduced the unsupervised machine learning technique in hopes that the groups created by k-means clustering could be run sereately and generate more accurate models.

- Before running the models for the classes created, we needed to review the data to see which classes could be run through our model. Due to the sizes of classes 2, 3, and 4 being under ten data points in total, we knew that it would be fruitless to run the model as the training and testing sets would not be large enough to create a model that could be used in future years. Therefore, we only re-ran the model for classes 0 and 1. For reference, Class 0 contained 4,394 data points and Class 1 contained 2,880.

- The results of the model for Class 0 can be found below. Although the accuracy score increased to a reasonable .6706, this accuracy score is driven by the fact that the model only produces a Population_Change output of 0, as one can see from the confusion matrix and the classification report for the output of 1. This measn that the model is useless for predictive purposes. 

<img width="1092" alt="ML Results for Class 0" src="https://github.com/skomyshan/predicting_population_change/blob/main/resources/Machine_Learning_wClustering_Class0.png">

- For the Class 1 model, the results are below. While this model did a better job in creating a model that predicts a Population_Change indicator of 0 and 1, it has a worse accuracy score than the original model at .5889. This is not accurate enough on its own to be used as a model and is worse than the original model, therefore, we would not choose to use this model over the oringinal model. 

<img width="1092" alt="ML Results for Class 1" src="https://github.com/skomyshan/predicting_population_change/blob/main/resources/Machine_Learning_wClustering_Class1.png">

#### Issues
- Based on the results of the various supervised machine learning runs, it is clear that the data that we have makes it difficule to predict changes in population year-over-year. There are many reasons why this could be and we have listed these reasons below for review. 
	- The original data for population change is tough to measure on its own due to the fact that more most countries, especially established ones like the US, it is rare that the population ever decreases. For less developed countries, who are more likely to see both population increases and decreases, data is less readibly available and the accuracy of data is more suspect. Missing data led us to remove many years of datapoints associated with these types of countries. 
		- We used the change in population percentage increase as our year-over-year indicator for the Population_Change variable. In reality, it may have been better to have created a more sophisticated measurement. One that looked at changes in the speed of the increases may have been more accurate.
	- We used many variables that


### Dashboard
- 

Link to Tableau Dashboard: https://tabsoft.co/388OwYf