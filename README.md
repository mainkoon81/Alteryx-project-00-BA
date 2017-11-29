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
 - issue4: outliers can be suspected via box-plots by eyeballing. or z-score ?

#### C. Formatting - manipulating rows, columns (massaging data)
 - __transposing:__ to combine several columns into one single field (generating two columns: name, value)
 - __aggregation:__ to summarise or pull out new info from manipulating rows, columns
 - __cross tabulation:__ same as aggregation, but taking a two categorical fields from the original than create their own matrix (groupby, groupby, count)

#### D. Blending data
 - __union:__ appending multi-data streams(sharing the same contents) into one unified stream 
 - __join:__ left(scraps) + inner + right(sediments)
 - __fuzzy matching:__ detecting "non-identical duplicates" by specifying parameters to match on(using algorithms to score similarity - Jaro:characters in common / Levenshtein:the number of edits (insertions, deletions, or substitutions) )
 - __spatial matching, blending:__  
