# Describing Data Sources
### An explanation of the work plan underlying data
See: https://github.com/Colsai/scott_data606/blob/main/Project_Proposal.md
  
- HHS OIG displays all public projects, which can be found at https://oig.hhs.gov/reports-and-publications/workplan/.
- The primary challenge is in finding a way to scrape the data. I've initially scraped the paragraphs by writing an initial scraper: 
- https://github.com/Colsai/scott_data606/blob/main/HHSOIG_WP_Scrapers.ipynb

This scrapes for two data sources:
#### Aggregate-level data
- https://github.com/Colsai/scott_data606/blob/main/Data_Sources/HHS_OIG_Reports.csv
![image](https://user-images.githubusercontent.com/70355052/172527208-be0283b0-512e-49b7-bf5a-820226907e39.png)

#### Reports data
- https://github.com/Colsai/scott_data606/blob/main/Data_Sources/HHS_OIG_workplans.csv
![image](https://user-images.githubusercontent.com/70355052/172527255-2f155ac1-1d6c-4be7-8be7-1c0334cbf247.png)

#### Example of a report (scraped data)
*Data is as it currently is, before cleanup*
![image](https://user-images.githubusercontent.com/70355052/172527504-e34cc318-9858-49fc-b9b8-8d37499ecb9a.png)

These are not large files (1-2mb), but contain full summary-level data of all reported attributed projects connected to publically-available projects from HHS OIG.
The major issue with this data is that there is a lot of cleanup and standardization needed. Many of the data elements need to be expanded, such as agency, where acronyms are used- ex. *Food and Drug Administration for one item, FDA for another'.
  
Additionally, reports data need several steps of cleanup to make them usable:
- Remove HTML tags
- Standardize and clean stop words
- Remove any common but unhelpful words here (ie: OIG, etc.)
