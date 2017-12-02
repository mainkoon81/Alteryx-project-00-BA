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
 - issue2: duplicate data
 - issue3: missing data, remove? or impute? or "multiple imputation + maximum likelihood"-> with R/SAS ?
 - isuue3_1: the fields that have missing datas are "significant predictors"-> with R/SAS ? 
 - issue4: outliers can be suspected via box-plots by eyeballing. or z-score ?

#### C. Formatting - manipulating rows, columns (massaging data)
 - __transposing:__ to combine several columns into one single field (generating two columns: name, value)
 - __aggregation:__ to summarise or pull out new info from manipulating rows, columns
 - __cross tabulation:__ same as aggregation, but taking a two categorical fields from the original than create their own matrix (groupby, groupby, count)

#### D. Blending data
 - __union:__ appending multi-data streams(sharing the same contents) into one unified stream 
 - __join:__ left(scraps) + inner + right(sediments)
 - __fuzzy matching:__ detecting "non-identical duplicates" by specifying parameters to match on(using algorithms to score similarity - Jaro:characters in common / Levenshtein:the number of edits (insertions, deletions, or substitutions) ). 
 - __spatial matching & blending:__  



-----------------------------------------------------------------------------------------------
##  Project 00. preparing school data
__Issue:__ A school district wants to predict **the per pupil costs of a school** based on some high level summary data about the school. This way they’ll have a good estimation of how well a school is managing its costs relative to what the model would predict. We are asked to prepare the data for modelling.

__Data Understanding:__ The CSV files contain data for two different school districts.
 - DistrictA_Attendance - It contains average daily attendance, percent attendance, and pupil-teacher ratio data for the 25 schools in district A.
 - DistrictA_Finance - It contains average monthly teacher salary and per pupil cost data for the 25 schools in district A.
 - DistrictB_Attendance - It contains average daily attendance, percent attendance, and pupil-teacher ratio data for the 21 schools in district B.
 - DistrictB_Finance - It contains average monthly teacher salary and per pupil cost data for the 21 schools in district B.

__Process:__ 
> Step 1: **Combine the data:** First combine the data from the various files into one sheet, with one row per school. 
  - issue: Unmatched row-numbers, two catagorical fields, Need to transform the structure of either one of the datasets (we use a crosstab)


> Step 2: **Clean the Data:** Next clean the data, which includes addressing duplicate data, missing data, and any other data issues.

> Step 3: **Identify and Deal with Outliers:** Lastly, look for outliers and determine the best way to address them. 




<img src="https://user-images.githubusercontent.com/31917400/33515497-6ef19394-d75c-11e7-8bcb-ae1210e131cf.png" />























