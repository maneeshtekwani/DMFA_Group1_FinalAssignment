# DNSC 6305: Data Management for Analytics Final Project- Group 1

## Ask 1 - Searching and Identifying a Dataset to Analyze
* Identify and describe your dataset
* Identify dataset source
* Why is important and what appeals to you about it
* Acquire data and perform initial exploration to make sure it is suitable for dimensional modeling and analytical analysis
* Describe the analytical questions you want to answer with the data. (3+ major questions are required)
* Describe any concerns with the data and changes you expect to overcome

### Identify and describe your dataset
For the final project, Group 1 decided to examine a dataset on oil spill incidents that took place in the state of New York. The dataset provides administrative information about each spill that occurred in their DEC region, with a unique seven-digit spill number. Additionally, the dataset also provides information on the program facility name and location, the categorical entities responsible for the spill, the spill date, location, cause, material, material type, quantity spilled, quantity recovered, units measured, affected waterbody, and the close date of the incident (the date when the cleanup activity is complete and all the paperwork for the incident is processed). The dataset is accessible for download in CSV format through the data.gov link here: https://data.ny.gov/api/views/u44d-k5fk/rows.csv. The size of the dataset is 97 MB and was last updated on 12/10/2023, according to Data.gov. The dataset has 500,000+ transactional records and 20 variables. Each record represents a unique spill incident that occurred in the state of New York.

### Identify dataset source
This dataset provides information to help monitor spill incidents that cause environmental damage in New York State, their causes, and their environmental impact. The goal of this dataset is to help the New York Department of Environmental Conservation work alongside
their goals to Protect public health, the environment, and improving the health, safety, and welfare of their people. The dataset is extracted from data.ny.gov, which is a website where NY State publishes open source datasets for the purpose of visualization and analysis.


#### Why is important and what appeals to you about it
Our group decided to choose this dataset for two reasons:
  
__1.__ Firstly, our group wanted to conduct an analysis that would derive valuable insights on a significant topic, such as Environmental Change. Environmental Change is a critical issue that continues to impact us, and we believe that by conducting this analysis, we can identify ways that data and its analysis can be used for the greater good. Specifically, our analysis would help the New York State Department of Environmental Conservation in identifying leading causes of spill incidents, regions with the most environmental contamination, and which areas that require more remediation support. This information would enable the department to conduct more suitable remediation programs or enhance related regulations to benefit the overall environment in New York State.

__2.__ Secondly, our group selected this dataset because we felt it was suitable for dimensional modeling and analysis. With more than 500,000 unique spill records and over 50 years of data, we believe there is enough transactional data for us to analyze and interpret spill occurrences. Furthermore, with specific columns like contributing_factor, waterbody, source, material_type, and county, we can zoom into specifics to truly understand spill incidents in NY.

#### Analytical questions we want to analyzie with this data
__1.__ Analyze the top 5 waterbodies most significantly impacted by spill quantity and present details regarding the spilled materials and the recovery rate for each waterbody to give more insights into the effectiveness of remediation efforts

__2.__ Analyze the top 5 sources responsible for spill incidents based on spill quantity and provide an in-depth breakdown of contributing factors associated to each source
   
__3.__ Analyze the top and bottom 5 sources based on spill recovery rates to assess their efficiencies in resolving matter and identify the counties with better performance in cleaning spills by evaluating resolution rates and recovery rates

#### Concerns with the data and limits we expect to overcome

In examining the dataset, we identified a few issues that we decided to address before working with the data and analyzing relationships.

__1. Using csvkit to remove the zip_code: The Zip Code column is empty for a majority of records (90.55%, 491,824/543,133 rows):__ it was acknowledged as a gap in the data by the data dictionary. We have ample other location-based columns in the data to analyze and determine patterns, including Street Intersections of the location (via street 1 and 2), Locality, Country, State-Wide Information System (SWIS) Code, and Department of Environmental Correction (DEC) code 1-7. Additionally, Our analysis is on a state level, hence, the granualarity for Zip Code is not needed, instead, its better for us to examine spill incidents on a County Level.
   
__2. Dropping and Removing Data from prior to 1978 up until 1996 using SQL (Analyzing 25 Years of Data, from 1997 up until 2023/present):__ We discovered records of spill dates prior to 1978, which raised concerns. According to the sponsor, the New York State Department of Environmental Conservation, the NY State Spill Fund began operating in 1978, but some spills in the dataset occurred before that year, rendering these spills more as estimates. Furthermore, we observed inconsistencies, such as quantities spilled or recovered with null values and different units for the same materials, in the dataset beyond 1978, up until 1996. We attribute these inconsistencies to advancements in technology and incident recording systems. Therefore, our group decided to remove all data from before 1978 until 1996, narrowing our focus to incidents that took place within the past 25 years only.
   
__3. Addressing Null Values within our Data Columns using SQL:__ Among the 20 columns in our dataset. we have NULL values for street_2, locality, waterbody, and units. We want our want to uniquely identify null values, we decide to change null values as zero for our analysis to ensure that the data would be consistent when running queries and doing visualizations.

__4. Addressing Test Records with our data using SQL:__ We remove records that have "TEST" or "TEST SPILL" within the Program Facility Name as these are clearly test records based on the information within their remaining columns. The number of records of "TEST" or "TEST SPILL" within the Program Facility Name is 15 records. We decided to drop this to avoid inconsistencies when running our queries.

__5. Concerns with the Received and Close Date Columns within the spills table:__ While we were wrangling the data, we discovered NULL values in both the Received Date and Close Date columns. We decided to drop these NULL values. Firstly, NULL values for "Close Date" can indicate either that spills hasn't been cleared yet or that the information is not available. Based on this, We believe we cannot be reasonably sure how to replace these NULL, hence we decided not to. Additionally, in terms of the Received Date the replacing NULL Values would also be merely on assumption rather than reasonable certainity, hence we decided not to drop the NULLs for received date as well.
