# Alteryx-project-00-BA

-----------------------------------------------------------------------------------------------
##  Data Preparation? cleaning + blending
__Issue:__ Data Source and Type, cleaning, Formatting, Blending 

#### A. Understanding different data types (between strings, integers, doubles, and bytes)
 - Data Sources: transactional(supermarket, etc), devices(TV,phone, etc), collected(weather, census, flight, etc) How to make them available to use? 
 - File Sources: software, database, web
 - From database: https://help.alteryx.com/current/DatabaseConnections.htm
 - From web (API):  https://community.alteryx.com/t5/Engine-Works-Blog/REST-API-In-5-Minutes-No-Coding/ba-p/8137
 - Then Parsing: https://www.alteryx.com/on-demand-training

<img src="https://user-images.githubusercontent.com/31917400/33505159-34580850-d6e2-11e7-8385-9d882a5de3a8.jpg" width="600" height="150" />

 - Data Types(for calculation or blending): str / number / boolean / datetime / others

#### B. Cleaning with dirty dataset (str parsing and replacements, deduping, imputation)
 - issue1: inconsistent delimitors((,-,/), extra characters("str",123str, $123)
 - issue2: **duplicate data**
 - issue3: missing data, remove? or impute? or "multiple imputation + maximum likelihood"-> with R/SAS ?
 - isuue3-1: the fields that have missing datas are "significant predictors"-> with R/SAS ? 
 - issue4: outliers can be suspected via box-plots by eyeballing. or z-score ?

#### C. Formatting - manipulating rows, columns (massaging data)
 - __transposing:__ to combine several columns into one single field (generating two columns: name, value)
 - __aggregation:__ to summarise or pull out new info from manipulating rows, columns
 - __cross tabulation:__ same as aggregation, but taking a two categorical fields from the original than create their own matrix (groupby, groupby, count)

#### D. Blending data
 - __union:__ appending multi-data streams(sharing the same contents) into one unified stream 
 - __join:__ left(scraps) + inner + right(sediments)
 - __fuzzy matching:__ detecting **"non-identical duplicates"** by specifying parameters to match on(using algorithms to score similarity - Jaro:characters in common / Levenshtein:the number of edits (insertions, deletions, or substitutions) ). 
 - __spatial matching & blending:__  



-----------------------------------------------------------------------------------------------
##  Project 00. preparing school data
__Issue:__ A school district wants to predict **the per pupil costs of a school** based on some high level summary data about the school. This way they’ll have a good estimation of how well a school is managing its costs relative to what the model would predict. We are asked to prepare the data for modelling.

### __Data Understanding:__ 
The CSV files contain data for two different school districts.
 - 'DistrictA_Attendance.csv' - It contains average daily attendance, percent attendance, and pupil-teacher ratio data for the 25 schools in district A.
 - 'DistrictA_Finance.csv' - It contains average monthly teacher salary and per pupil cost data for the 25 schools in district A.
 - 'DistrictB_Attendance.csv' - It contains average daily attendance, percent attendance, and pupil-teacher ratio data for the 21 schools in district B.
 - 'DistrictB_Finance.csv' - It contains average monthly teacher salary and per pupil cost data for the 21 schools in district B.

### __Process in Alteryx:__ 

Step 1: **Combine the data:** combine the data from the various files into one sheet, with one row per school. 
 - Crosstab_tool: Unmatched row-numbers, two catagorical fields, Need to transform the structure of either one of the datasets
 - Join_tool: Check the leftover in L/R tabs
 - Union_tool: Stack the data on top of eachother, and remove or rename its fields, using Select_tool
 
Step 2: **Clean the Data:** clean the data, which includes addressing duplicate data, missing data, and any other data issues.
 - FieldSummary_tool: Visualize the data first and show missing values in its histograms. Do we delete or impute the missings? 
 - SelectRecords_tool: Delete duplicate rows manually..hopeless
 - Filter_tool: Delete missings'rows by filtering out records that are NULL. ..hopeless

Step 3: **Identify and Deal with Outliers:** look for outliers and determine the best way to address them. 
 - Scatterplot_tool: Since there are four predictor variables, we drag in four scatterplot_tools. Then we configure each one with a different predictor variable. The box plots use the interquartile range to determine whether a point is an outlier. 
<img src="https://user-images.githubusercontent.com/31917400/33516276-0f2f2d0c-d768-11e7-8032-44295327200b.jpg" />

 - Sort_tool: Find the obv suspected as outliers..
 - General way to deal with outliers
   - Delete: When data is erroneous or when the outlier hurts the model's’ ability to make prediction (perhaps the value is very unlikely to appear again so keeping it in the model will skew all other predictions).
   - Impute: Also for when data is erroneous, we could use the average or median value in its place.

<img src="https://user-images.githubusercontent.com/31917400/33515497-6ef19394-d75c-11e7-8bcb-ae1210e131cf.png" />


# Alteryx-project-01-BA

##  Project 01. Selecting the Location for Next Business of Store
 - __Part 01:__ Data Preparation
 - __Part 02:__ Model Building

> #### Scenario: "Petland" is a leading pet store chain in Wyoming with 13 stores throughout the state. This year, "Petland" would like to expand and open a 14th store. My manager has asked me to perform an analysis to recommend the city for Petland’s newest store, based on predicted yearly sales. 

### Part 01. Data Preparation
My first step in predicting yearly sales is to **format** and **blend** together data from different datasets and **clean** it(deal with duplicates, missings, outliers). I started with the Web Scraped Data from the Wyoming Wikipedia page, and used 'texttocolumns_tool' and 'select_tool' and the Data Cleansing to parse out the City, County, 2010 Census, and 2014 Estimate and remove all of the extra punctuation: 'p2-partially-parsed-wy-web-scrape.csv'. For 'p2-2010-petland-monthly-sales.csv' file, I transposed the data to get City, Month, and Amount, and then summarized by City to get the total amount for each city. For 'p2-wy-demographic-data.csv' file, I used the Auto-field tool to combine all of the numbers labeled as String fields. Before each join, I summarized the amounts by city to ensure that there were no duplicate city names within the data.     

__>Step 1. - Data Understanding:__ My manager has given me the following information to work with:
 - 'p2-2010-petland-monthly-sales.csv' - This file contains all of the monthly sales for all Petland stores for 2010.
 - 'p2-partially-parsed-wy-web-scrape.csv' - This is a partially parsed data file that can be used for population numbers.
 - 'p2-wy-demographic-data.csv' - This file contains demographic data (Households with individuals under 18, Land Area, Population Density, and Total Families) for each city and county in the state of Wyoming. (the US city system: a state contains counties and a county contains one or more cities)
 - 'p2-wy-453910-naics-data.csv' - NAICS data on the most current sales of all competitor stores where total sales is equal to 12 months of sales

<img src="https://user-images.githubusercontent.com/31917400/33517377-32cfd992-d77b-11e7-824c-ce22c8589978.gif" width="400" height="350" />

__>Step 2. - Process in Alteryx:__ Building the training set: 
 - To properly build the model, and select predictor variables, create a dataset with the following columns:
   - City
   - 2010_Census_Population
   - Households_with_Under_18
   - Land_Area
   - Population_Density
   - Total_Families
   - Total_Sales
 - A> **Clean the data**
   - From 'p2-2010-petland-monthly-sales.csv': 
     - Select_tool[int] - Formular_tool[summing monthly up] - Select_tool[City,Total_Sales] 
   - From 'p2-partially-parsed-wy-web-scrape.csv': 
     - TextToColumns_tool[splitting city&county] - Formula_tool[ReplaceChar(), ReplaceFirst(), Left(), FindString()] - Filter_tool[skipping empty] - Select_tool[int]
   - From 'p2-wy-demographic-data.csv':
     - Select_tool[int] 
 - B> **Combine the data**
     - Join_tool[L/R] - the first + the third
     - Join_tool[L/R] - And + the second
<img src="https://user-images.githubusercontent.com/31917400/33520155-2a6b0f24-d7ad-11e7-8951-f97bb83c3823.jpg" /> 

 - C> **Identify and deal with outliers (IQR method)**
   - We use IQR method to determine if there are outlier cities for each of the variables and then justify which city that has at least one outlier value should be removed. To calculate the upper fence and the lower fence:
     - 1 . Calculate 1st quartile and 3rd quartile of the dataset (Excel function QUARTILE.INC or QUARTILE.EXC)
     - 2 . Calculate the Interquartile Range: IQR = Q3 - Q1
     - 3 . Upper Fence = Q3 + 1.5 IQR
     - 4 . Lower Fence = Q1 - 1.5 IQR
     - 5 . Values above the Upper Fence and values below the Lower Fence are outliers
     
   - 2010_Census_Population: Upper(26061.5 + 1.5[26061.5-7917])= 53278, Lower(7917 - 1.5[26061.5-7917])= -19300
   - Households_with_Under_18: Upper(4037 + 1.5[4037-1327])= 8102, Lower(1327 - 1.5[4037-1327])= -2738 
   - Land_Area: Upper(3505 + 1.5[3505-1862])= 5969, Lower(1862 - 1.5[3505-1862])= -602
   - Population_Density: Upper(7.39 + 1.5[7.39-1.72])= 15.9, Lower(1.72 - 1.5[7.39-1.72])= -6.8
   - Total_Families: Upper(7381 + 1.5[7381-2923])= 14068, Lower(2923 - 1.5[7381-2923])= -3764
   - Total_Sales: Upper(312984 + 1.5[312984-226152])= 443232, Lower(226152 - 1.5[312984-226152])= 95904

<img src="https://user-images.githubusercontent.com/31917400/33520874-d3146b5e-d7ba-11e7-9457-0a466433f8cc.jpg" /> 

 - Here, each point indicates each city. 
   - There are two cities – Cheyenne, Gillette – that beyond the upper fence (443232) of Total Sales.  
   - In 2010 Census Population, there is one data point that beyond the upper fence (53278, 443232) which is Cheyenne.
   - In Land Area, there is one data point that beyond the upper fence(5969, 443232) which is RockSprings.
   - In Households with Under 18, there is no data point that beyond the upper fence(8102, 443232) 
   - In Population Density, there is one data point that beyond the upper fence(15.9, 443232) which is Cheyenne. 	
   - In Total Families, there is one data point that beyond the upper fence(14068, 443232) which is Cheyenne.
 - Thus we may consider "Cheyenne" as the outstanding outlier.   

----------------------------------------------------------------------------------------------------------------------------------------
### Part 02. Model Building
My Next step in predicting yearly sales is to check regressors(predictors) and select appropriate predictor variables for our categorical model.
 - Dealing with 'duplicate variable'(representing the same thing as another variable)
 - Dealing with correlations between choosen predictor variables...multicollinearity? Ridge Regression??
 - Modeling with categorical variables because we need to determine the final location for business. When dealing with a categorical response, check - How many levels? - How many freq for each? enough? - What proportion does each take up? 

__>Step 1. - Data Understanding:__ in the training set
 - Check the distribution of each field (continuous, categorical).
<img src="https://user-images.githubusercontent.com/31917400/33528855-e9e119d6-d85f-11e7-9ab0-696ad4d01f36.jpg" />

 - See if each predictor has a linear relationship with our target variable in the training set(scatterplot). I can conclude all predictor variables are good potential predictor variables because they show a linear relationship between sales. 
<img src="https://user-images.githubusercontent.com/31917400/33520874-d3146b5e-d7ba-11e7-9457-0a466433f8cc.jpg" />

 - Detecting multicollinearity b/w predictors in the training set(correlation matrix). 
 - Based on the correlation(b/w predictor va response), we could suspect duplicates because of identical corr-values.  
 - Based on the correlation(b/w predictor vs predictor), we can remove duplicates and inter-correlated variables.

__>Step 2. - Model Building:__
 - Create a linear regression model off our training set to help predict total sales.
 - We can see that 'Household_Under_18', '2010_Census', 'Families', and 'Population Density' have strong correlations which each other. 'Land_area' however, is not as highly correlated. So I started by using 'Land_area' as one predictor and then tested the four variables that are correlated(for deduping). 
<img src="https://user-images.githubusercontent.com/31917400/33529115-e25c8bec-d863-11e7-9eb1-99a795e184f3.jpg" width="600" height="300" />

 - I’ve found out that using **Land_area** and **total_families** as the predictor variables are good fits.
 - The p-values for land area and total families are both below 0.05 and the Multiple R-squared value is at .91 which is close to 1. 
<img src="https://user-images.githubusercontent.com/31917400/33529175-bd628d18-d864-11e7-9547-44fd48904d99.jpg" width="600" height="200" /> 

- We can create the best linear regression equation: Y = 197,330 – 48.42[Land Area] + 49.14[Total Families]

__>Step 3. - Prediction with using testing set:__ 
 - Here are the **criterias** given in choosing the right city:
   - > The new store should be located in a new city. That means there should be **no existing stores** in the new city.
   - > **The total sales for the entire competition** in the new city should be less than $500,000
   - > The new city where we want to build our new store must have a **population** over 4,000 people (based upon the 2014 US Census estimate).
   - > The **predicted yearly sales** must be over $200,000.
   - > The city chosen would have the highest predicted sales from the predicted set.
   
 - Once the model was created, I applied the model to the cities. 
 - I took the competitor data 'p2-wy-453910-naics-data.csv', and joined it, with a formula off of the left join to create a 0 in the Competitor Amount so I could union the cities that have no competitor back into the overall dataset. I don’t want to exclude cities where no competitors are present.  
 - I then applied the filters laid out in the project plan to come up with my list of possible cities, and sorted on the expected revenue to bring the best choice to the top.   
 - I filtered my cities according to the given the criteria in the project and calculated revenue off the population density information using my linear model.


I would recommend the city of Laramie with a predicted sales of $305,014. 
