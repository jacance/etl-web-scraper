# Craigslist and eBay - ETL
![Alt text](ebay-craiglist.jpg?raw=true "Title")

## Background
The goal of this project is to extract, transform, and load data from multiple sources. To accomplish this, I created my own datasets by scraping two popular online marketplaces: Craigslist and eBay. I chose PlayStation 5 listings because the PlayStation 5 is currently in high demand and is regularly listed above retail price.

## Extract
BeautifulSoup is used to parse 'PlayStation 5' search results on Craigslist and eBay. A for loop extracts information from one listing at a time, places extracted info in a dictionary, then appends each dictionary to a list of dictionaries. The following information is scraped:

#### Craigslist
- Title
- Price
- Location
- Link

#### eBay
- Title
- Price
- Shipping
- Link

## Transform
Once all the desired information is extracted into two separate lists (craigslist_all, ebay_all), the lists of dictionaries are then converted into separate dataframes using Pandas: craigslist_df and ebay_df. The dataframes are then transformed as follows:

- 'New Listing' tags are removed from 'title'
- Currency symbol and commas are removed from 'price' column
- 'Free shipping' is changed to 0
- Both 'price' and 'shipping' columns datatypes are converted to float
- New column 'total' is added for eBay dataframe as a sum of price + shipping
- Duplicates are dropped according to 'link'

## Load
Finally, SQLAlchemy is used to connect the Jupyter notebook with pgAdmin 4. The dataframes are then loaded into 'playstation5_db' as two tables to maintain their own columns and structure from the transformation process. 

- 'craigslist_df' dataframe imported as 'craigslist' 
- 'ebay_df' dataframe imported as 'ebay'

## Technologies
- Pandas
- Python
- HTML
- BeautifulSoup
- Jupyter Notebook
- SQLAlchemy
- Postgres
- pgAdmin 4
