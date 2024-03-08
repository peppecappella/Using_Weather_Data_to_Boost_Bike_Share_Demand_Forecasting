# Using_Weather_Data_to_Boost_Bike_Share_Demand_Forecasting 

Author: Giuseppe Cappella

This project merges data from bike share stations in Washington DC with meteorological data over a time span that covers 10 years. The goal is to develop an extensive MongoDB dataframe suitable for subsequent analyses. Furthermore,this data will be employed to analyze and understand the impact of weather conditions on bike share usage, enhancing the dataset's richness and the accuracy of demand forecasting. 

The project specifically compares two approaches using **Prophet**: one that incorporates weather regressors and one that does not, to evaluate their effectiveness in improving service demand predictions within the forecasting model.

## Data Sources

For the bike sharing station data, this project utilizes CSV files made available by Capital Bikeshare, covering Washington DC from 2013 to 2023. These files will be integrated to create a singular, comprehensive CSV file that consolidates bike share usage data over the specified period. As for the meteorological data, the source is OpenWeatherMap, which provides detailed weather information for Washington DC.

**NB: the Capital bike share data can be downloaded at the following link : https://capitalbikeshare.com/system-data in the "Trip History Data" section. The 10 years Weather data are present in the repo as a csv file (2d8242457dbe0baa13874aac40efb970.csv)** 

## Architecture and Technologies:

**MongoDB:** A NoSQL database used to store and manage processed data. MongoDB is chosen for its flexibility in handling variable data schemas, horizontal scalability, and its indexing features, including Time-To-Live (TTL) indexes, which automate the removal of outdated data.

**Docker:** An open-source platform for developing, shipping, and running applications in containers. Containers allow a developer to package up an application with all of the parts it needs, such as libraries and other dependencies, and ship it all out as one package. In our system, MongoDB are hosted on Docker a docker container. This approach enhances the system's scalability and ensures a consistent environment across different stages, from development to production.

**Prophet:** Prophet is a powerful, open-source tool developed by Facebook for time series forecasting. It is designed to handle the complexity of seasonal effects, holidays, and changes in trends, making it highly suitable for predicting activities like station departures that are likely to be influenced by these factors.

more at: https://facebook.github.io/prophet/

## Installation and Configuration Steps

Follow these steps to set up the environment and get the system up and running.

**0. Install Docker**:

https://www.docker.com/

**1. Docker Network Creation:**

Start by creating a network in Docker. This will allow your containers to communicate with each other. Open your terminal and run the following command:

docker network create kafka-network

**2. MongoDB container Creation: this will serve as your database for storing processed data. Open a Teminal and run:**

docker run -d --name mongodb -p 27017:27017 mongo:latest

**3. Installing Facebook Prophet for forecasting: open a Teminal and run:**

   python -m pip install prophet

**4. Setting JAVA_HOME Environment Variable:**

Java Installation:

If Java is not installed, you can download and install it from the official Oracle Java site (link) or use OpenJDK (link). Choose the version of Java that best suits your needs (for example, Java 8, 11, or later versions are commonly used with Spark).

Setting the JAVA_HOME environment variable:
On Windows:

    a. Search for "Environment Variables" in the Start menu and select "Edit the system environment variables".
    b. In the "System Properties" window, click on "Environment Variables".
    c. Click on "New" under "System variables" and enter JAVA_HOME as the variable name and the path of the Java installation folder (for example, C:\Program Files\Java\jdk-11.0.1) as the value.
    d. Modify the Path variable by adding %JAVA_HOME%\bin to the existing value.

On Linux/Mac:

    a. Open your shell's configuration file (for example, ~/.bashrc, ~/.zshrc, etc.) with a text editor.
    b. Add the following lines at the end of the file (replacing /path/to/your/jdk with the actual path of your JDK installation):

export JAVA_HOME=/path/to/your/jdk export PATH=$JAVA_HOME/bin:$PATH

    c. Save the file and execute source ~/.bashrc (or the name of your shell's configuration file) to apply the changes.

Check the configuration:

After setting JAVA_HOME, reopen the terminal or command prompt and type java -version again to verify that Java is correctly installed and recognized by the system.

## Running the code:

After completing these steps, your environment will be configured, and you should be able to run the code:

Open a jupyter notebook on the main folder and execute:

pipeline.ipynb

## Project Results

### Mongo collections:

A first result of the project is the creation of three MongoDB collections:

- The "Weather_history" collection contains 10 years of hourly aggregated meteorological data in Washington DC.
- The "Sales_history" collection contains the count of the number of hourly departures from the Thomas Circle stations.
- The "integrated data" collection contains enriched data from the Weather_history collection and Sales_history collection.

A separate Sales_history collection has been created by simply removing the filter on Thomas Circle to show hourly departures for all stations.

### Tableau Dashboard:

These collections have been utilized for the development of a **dashboard in Tableau**. This dashboard visualizes the relationships and insights derived from the aggregated and enriched data, providing an interactive and user-friendly interface for exploring patterns in weather conditions and their impact on station departures. It allows users to filter data based on specific criteria, offering a comprehensive tool for analysis.

**Here is a link to my dashboard for direct access to the interactive analysis tool:**

**https://public.tableau.com/views/CapitalBikeshareDemandAnalysis/Weather-IntegratedAnalysisofBikeSharingDemand3?:language=en-US&:sid=&:display_count=n&:origin=viz_share_link**

Additionally, below is a preview of the dashboard:

<img width="428" alt="Schermata 2024-03-08 alle 19 59 52" src="https://github.com/peppecappella/Using_Weather_Data_to_Boost_Bike_Share_Demand_Forecasting/assets/124899610/601a68da-dc94-4b66-8f32-8baf45de031b">

### Consistent forecasting outcomes: 

#### Metrics comparison
Consistent forecasting outcomes emerge as a notable result of the project, underscored by a comparative analysis between models with and without the integration of meteorological data as regressors. This distinction underscores the significant role weather data plays in enhancing the precision of forecasts.

<img width="761" alt="Schermata 2024-03-08 alle 18 56 49" src="https://github.com/peppecappella/Using_Weather_Data_to_Boost_Bike_Share_Demand_Forecasting/assets/124899610/49af08ab-9ecb-4e1e-8125-b3849667414f">

**For the model incorporating meteorological data:**

- RMSE (Root Mean Square Error) stands at 20.75, signifying the predictions' deviation from actual values. A lower RMSE indicates closer accuracy.
- MAE (Mean Absolute Error) is 15.94, reflecting the average magnitude of errors in the predictions, which, in this context, is comparatively lower.
- Both R² and r (Pearson's correlation coefficient) value at 0.94, pointing to a robust positive correlation between the forecasted and actual data, suggesting a high degree of reliability in the predictions.
- Rho (Spearman's rank correlation coefficient) at 0.95, further confirms a strong monotonic relationship, echoing the findings of Pearson's coefficient.
- MAPE (Mean Absolute Percentage Error) is 14.98%, indicating predictions, on average, diverge from actual values by this margin, which is relatively modest.

**Contrastingly, the model excluding meteorological data reveals:**

- An RMSE increase to 32.50, highlighting reduced precision in forecasts.
- An elevated MAE of 24.38, indicating larger average prediction errors.
- A decrease in both R² and r to 0.85, suggesting a lesser positive correlation between predicted and actual values, thus a drop in predictive reliability.
- A corresponding rho value that aligns with the reduced R² and r, underlining a weaker correlation.
- A MAPE escalation to 45.37%, demonstrating a significant deterioration in prediction accuracy.

In essence, integrating meteorological data as regressors markedly enhances forecasting accuracy. This is evidenced by lower MAPE and higher R² and rho values, signifying a potent correlation between forecasts and actual outcomes. 

#### Forecast comparison
As can be seen from the images below, the forecasts made with meteorological data (with some exception due to outliers) closely follow the actual observed trends more than the predictions made without incorporating meteorological data. This observation aligns with the previously discussed metrics, highlighting a more accurate forecast when meteorological regressors are included.

<img width="695" alt="Schermata 2024-03-08 alle 20 11 00" src="https://github.com/peppecappella/Using_Weather_Data_to_Boost_Bike_Share_Demand_Forecasting/assets/124899610/c8a0eda4-e739-4882-bf23-0b0106a8d115">

#### Scatterplot comparison
Finally, as illustrated by the following scatterplots, the predictions utilizing meteorological data show a tighter cluster around the regression line. This indicates a higher level of accuracy compared to the more dispersed points from the model without meteorological data.

<img width="798" alt="Schermata 2024-03-08 alle 18 55 47" src="https://github.com/peppecappella/Using_Weather_Data_to_Boost_Bike_Share_Demand_Forecasting/assets/124899610/0a96694c-8d6a-4d8f-a6a4-75e726ed13eb">

**In conclusion this analysis confirms the critical impact of meteorological data in refining the precision of predictive models.**
