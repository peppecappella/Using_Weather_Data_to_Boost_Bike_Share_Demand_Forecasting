# Using_Weather_Data_to_Boost_Bike_Share_Demand_Forecasting 

Author: Giuseppe Cappella

This project merges data from bike share stations in Washington DC with meteorological data over a time span that covers 10 years. The goal is to develop an extensive MongoDB dataframe suitable for subsequent analyses. Furthermore,this data will be employed to analyze and understand the impact of weather conditions on bike share usage, enhancing the dataset's richness and the accuracy of demand forecasting. The project specifically compares two approaches using Prophet: one that incorporates weather regressors and one that does not, to evaluate their effectiveness in improving service demand predictions within the forecasting model.

## Data Sources

For the bike sharing station data, this project utilizes CSV files made available by Capital Bikeshare, covering Washington DC from 2013 to 2023. These files will be integrated to create a singular, comprehensive CSV file that consolidates bike share usage data over the specified period. As for the meteorological data, the source is OpenWeatherMap, which provides detailed weather information for Washington DC.

**NB: the Capital bike share data can be downloaded at the following link : https://capitalbikeshare.com/system-data in the "Trip History Data" section. The 10 years Weather data are present in the repo as a csv file (2d8242457dbe0baa13874aac40efb970.csv)** 

## Installation and Configuration Steps

Follow these steps to set up the environment and get the system up and running.

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

<div class='tableauPlaceholder' id='viz1709924098565' style='position: relative'><noscript><a href='#'><img alt='Weather-Integrated Analysis of Bike Sharing Demand (3) ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Ca&#47;CapitalBikeshareDemandAnalysis&#47;Weather-IntegratedAnalysisofBikeSharingDemand3&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='CapitalBikeshareDemandAnalysis&#47;Weather-IntegratedAnalysisofBikeSharingDemand3' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;Ca&#47;CapitalBikeshareDemandAnalysis&#47;Weather-IntegratedAnalysisofBikeSharingDemand3&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='language' value='en-US' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1709924098565');                    var vizElement = divElement.getElementsByTagName('object')[0];                    if ( divElement.offsetWidth > 800 ) { vizElement.style.width='1420px';vizElement.style.height='1887px';} else if ( divElement.offsetWidth > 500 ) { vizElement.style.width='1420px';vizElement.style.height='1887px';} else { vizElement.style.width='100%';vizElement.style.height='3827px';}                     var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>

