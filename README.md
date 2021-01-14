# Playstation 5 Prices - ETL

## Background
The Sony Playstation 5 is an in-demand product that often resells for more than MSRP. This project scrapes pricing info to help sellers and consumers guage the current market pricing trends.

## Extract
BeautifulSoup is used to parse 'Playstation 5' search results on Craigslist and eBay. A for loop extracts information from one listing at a time, places extracted info in a dictionary, then appends each dictionary to a list of dictionaries. The following information is scraped:

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
Finally, SQLAlchemy is used to connect the Jupyter notebook with Postgres. The dataframes are then loaded into 'playstation5_db' database with the following table names:

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
