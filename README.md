## Project_2: ETL

**Team Red XIII**: Kristina Swanson, Mel Runser, Dante Dillahunt, Rufin Perez

**Due**: Tuesday, December 12, 2023

**PROJECT REPORT**

## Project Proposal

We thought it would be interesting to see food waste to income on a global scale.
Our team will find 2 sources of data reviewing the Kaggle (https://www.kaggle.com) website and will perform, among other procedures, a merging of the datasets as part of the ETL process.

## Finding the Data

We obtained 2 datasets (datasets) from Kaggle related to:
* Global Food Waste (File name: [‘Food Waste data and research - by country.csv’](https://www.kaggle.com/datasets/joebeachcapital/food-waste); File Type: CSV)
* Global Salary Data (File name: [‘salary_data.csv’](https://www.kaggle.com/datasets/zedataweaver/global-salary-data); File Type: CSV)

Based on review of the 2 datasets, we determined that we will use the country as the column to join the datasets. 

## Data Cleanup & Analysis

We created a Jupyter Notebook file (file) to document the code for this project. We performed the following Extract-Transform-Load (ETL) procedures:

EXTRACT
* Obtained the datasets from Kaggle.com and saved them on our local drive
  
* Read in the datasets into the file as separate Pandas DataFrames

TRANSFORM
* Obtained and reviewed the index data types (column names) in the datasets to determine if any format conversion was warranted (e.g., to string or integer)

* Renamed the following column in the Global Salary dataset to match that of the Global Food Waste dataset:
‘country_name’: ‘Country’

* Discrepancies of country names between the datasets:
These discrepancies were preventing the ‘join’ from working as intended. For example, the ‘United States’ was not properly included in the results of the join because it had been named, ‘United States of America’, in one dataset, and ‘United States’ in the other. 

We performed procedures to identify the countries to be renamed by converting the ‘Country’ columns in both DataFrames to sets to find the countries unique to both the Global Food Waste and Global Salary DataFrames. Additionally, we found those countries common to both DataFrames.

We created a dictionary (‘rename_dict’) to rename and replace the country names in the Global Food Waste DataFrame. 

* Performed a ‘left join’ to merge the food waste and salary data of each country (a combined DataFrame):
As a result of the renaming procedures above, this allowed the join to properly work as intended - displaying the salaries for the countries that had been ‘mis-named’ before.

* Converted the combined DataFrame to a list of dictionaries (‘foodWaste_DICT’) to prepare it for import into MongoDB Compass.

## LOAD
* Our team decided to prepare the file for loading into MongoDB Compass (non-relational database) since initially the datasets did not include the same ‘records’ of information.

* Created an instance of MongoClient.

* Created a variable as a reference to a new database (‘Project2_DB’) and its related collection (‘Project2_collection’).

* Used ‘.insert_many’ to insert data from the ‘foodWaste_DICT’ list of dictionaries.

* Verified MongoDB Compass to ensure that the Project2_DB and Project2_collection were properly created.

* Used ‘.find_one()’ to query one record to verify that the piping coding is working as intended.

* Queried the Project2_collection and converted it to a DataFrame to be able to export it to a CSV file.

* Exported the Project2_collection (‘foodWasteDF’) to a CSV file.   

## CONCLUSIONS 

**Project ETL**:
Our team extracted 2 CSV files for this project, performing ETL procedures to get the data into a usable format for use in a non-relational production database. We created a GitHub repository named Project_2, which includes our Jupyter Notebook file, the 2 dataset CSV files, and this Project Report (markdown file). Each team member will copy the GitHub url into our individual Bootcampspot / Canvas for submission.

**Data Analysis**:
The data shows that the higher the income, the lower the food waste. For example, one part of Europe has an average income of $4096 monthly with 1971 tonnes of waste. While another part of Europe has an average income of $956 with 79,651 tonnes of food waste. Africa has an average income of $314 monthly with 87,9908 tonnes of food waste. I reached out to several buyers of local companies and here are some of the takeaways.

* Higher Income
  - Places with high incomes tend to purchase food daily and eat what was purchased.
  - The food that is purchased is of higher quality and has a longer shelf life at time of purchase.

*Low Income
  - Places with low income tend to purchase food by paycheck to paycheck.
  - Low incomes tend to purchase food looking for deals which in most cases is a lower quality of food. 
