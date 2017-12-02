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

### __Process:__ 

Step 1: **Combine the data:** First combine the data from the various files into one sheet, with one row per school. 
 - Crosstab_tool: Unmatched row-numbers, two catagorical fields, Need to transform the structure of either one of the datasets
 - Join_tool: Check the leftover in L/R tabs
 - Union_tool: Stack the data on top of eachother, and remove or rename its fields, using Select_tool
 
Step 2: **Clean the Data:** Next clean the data, which includes addressing duplicate data, missing data, and any other data issues.
 - FieldSummary_tool: Visualize the data first and show missing values in its histograms. Do we delete or impute the missings? 
 - SelectRecords_tool: Delete duplicate rows manually..hopeless
 - Filter_tool: Delete missings'rows by filtering out records that are NULL. ..hopeless

Step 3: **Identify and Deal with Outliers:** Lastly, look for outliers and determine the best way to address them. 
 - Scatterplot_tool: Since there are four predictor variables, we drag in four scatterplot_tools. Then we configure each one with a different predictor variable. The box plots use the interquartile range to determine whether a point is an outlier. 
<img src="https://user-images.githubusercontent.com/31917400/33516276-0f2f2d0c-d768-11e7-8032-44295327200b.jpg" />

 - Sort_tool: Find the obv suspected as outliers..
 - General way to deal with outliers
   - Delete: When data is erroneous or when the outlier hurts the model's’ ability to make prediction (perhaps the value is very unlikely to appear again so keeping it in the model will skew all other predictions).
   - Impute: Also for when data is erroneous, we could use the average or median value in its place.

<img src="https://user-images.githubusercontent.com/31917400/33515497-6ef19394-d75c-11e7-8bcb-ae1210e131cf.png" />


