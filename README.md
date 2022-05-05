### Final Project - Group 6 - Wartime Impact 

Github Repository URL: https://github.com/skomyshan/wartime_impact

This README is a proposal for our final project and the various components included. It starts with the topic that we will be exploring, including an overview of the main goals and hypotheses that we intend to answer. In order to explore this topic we devised a plan to utilize machine learning. As an overview of this plan we provide an outline of the database we plan to construct and the machine learning techniques that will be used to process this data. Finally, we end with our team members and the roles for each, understanding that these roles will shift throughout the life of the project.

### Presentation
- Our selected topic: Impact of War on Countries Across the World

- Reason why we selected their topic: The impact of Russia's invasion of Ukraine has been felt across the world and will only continue to cause waves as we move further into the conflict. We want to know how past wars and conflicts have affected the countries involved, as well as those who are not, as we try to predict the impact across the world in the years to come. 

- Description of our source of data: For our data we will be using a variety of data sources including, but not limited to, the FAO, World Bank, and OCED. For more detail regarding the data and its purpose please see the Database section below.

- Questions we hope to answer with the data: How does war and other military conflicts impact the countries involved as well as those who are not?


### Database

Our database will contain a variety of annual, cross-national metrics which should give us a comprehensive view of the health of a country. This data will be summarized by country, by year and will include everything from economic indicators (like import/export and inflation) to military expenditures to agrecultural output. The data will be connected via country codes and an internal cuntry id (primary key), as well as the year for the time series data. Due to the tabular structure of the data sources being used, our data will be organized using SQLite. This will also give us the ability to seamlessly interact with Tableau for the construction of our presentation.


### Machine Learning Model

The image below will help guide us through the entire project including the machine learning model that we intend to use. At a high level, the model we will be using will be a supervised model that allows us to measure the impact that one variable (the presence of a war or conflict) has on various other variables, highlighting the variables that are most impacted. As we become more familiar with the data and our hypothesis developes, we will construct a more comprehensive plan for our machine learning. 


### Team Members, Roles, and Communication Protocols

- Bhavna Aggarwal: Viz
- Jack Eisenreich: Triangle
- Suzanna Komyshan: Square
- Kurt Minges: X
- Sophie Xue: Circle

Square: The team member in the square role will be responsible for the repository.

Triangle: The member in the triangle role will create a mockup of a machine learning model. This can even be a diagram that explains how it will work concurrently with the rest of the project steps.

Circle: The member in the circle role will create a mockup of a database with a set of sample data, or even fabricated data. This will ensure the database will work seamlessly with the rest of the project.

X: The member in the X role will decide which technologies will be used for each step of the project.

Viz: The member in the Viz role will be responsible for the visualization techniques that will be used and ultimately integrated into the final project deliverable.

***Description of the communication protocols - Not sure what this is suposed to be***
