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

<img src="https://user-images.githubusercontent.com/31917400/33272708-df02ba9c-d382-11e7-914e-7cd34298c857.jpg" width="600" height="300" />

 - Data Types(for calculation or blending): str / number / boolean / datetime / others

#### B. Cleaning with dirty dataset (str parsing and replacements, deduping, imputation)
 - issue1: inconsistent delimitors((,-,/), extra characters("str",123str, $123)
 - issue2: duplicate data
 - issue3: missing data, remove? or impute? or "multiple imputation + maximum likelihood"-> with R/SAS ?
 - isuue3_1: the fields that have missing datas are "significant predictors"-> with R/SAS ? 
 - issue4: outliers 


#### C. Manipulating rows and columns of data (transposing, aggregation, cross tabulation)

#### D. Blending data through joins and unions (fuzzy matching, spatial blending to help with spatial analysis)
