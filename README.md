Web Scraping and Data Cleaning Project
Overview
This project is a Python-based web scraping tool that extracts tabular data from websites using BeautifulSoup and requests. The script includes robust error handling, data extraction capabilities, and data cleaning functionality to transform raw HTML tables into structured pandas DataFrames.

Features
Web Scraping: Extracts data from HTML tables on web pages

Error Handling: Comprehensive exception handling for network issues

Data Extraction: Parses table headers and row data

Data Cleaning: Processes and structures raw HTML data into clean DataFrames

Pandas Integration: Converts scraped data into structured datasets

Code Structure
1. Web Scraping with Error Handling
python
from bs4 import BeautifulSoup
import requests 

# Set headers with a proper User-Agent
headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36'
}

try:
    response = requests.get(url, headers=headers, timeout=10)
    response.raise_for_status()  # Raises an HTTPError for bad responses
    
    # If we get here, the request was successful
    soup = BeautifulSoup(response.content, 'html.parser')
    print(soup)
    
except requests.exceptions.ConnectionError:
    print("Error: Failed to connect to the server. Check your internet connection.")
    
except requests.exceptions.Timeout:
    print("Error: The request timed out. Server took too long to respond.")
    
except requests.exceptions.HTTPError as e:
    print(f"Error: HTTP error occurred: {e}")
    
except requests.exceptions.RequestException as e:
     print(f"Error: An unexpected error occurred: {e}")
2. Table Extraction
python
# Extract the third table from the page
table = soup.find_all('table')[2]
print(table)

# Find wikitable class tables
soup.find('table', class_ = 'wikitable')

# Extract table headers
headers = table.find_all('th')

if headers:
    header_text = [header.get_text(strip=True) for header in headers]
    print("Headers found:", header_text)
else:
    print("No <th> elements found")
3. Data Cleaning and DataFrame Creation
python
import pandas as pd

# Create DataFrame with cleaned headers
headers = [header.get_text(strip=True) for header in headers]
df = pd.DataFrame(columns=headers)

# Data Cleaning: Extract and structure row data
for row in column_data[1:]:  # Skip header row
    row_data = row.find_all('td')
    individual_row_data = [data.text.strip() for data in row_data]
    
    # Add cleaned data to DataFrame
    length = len(df)
    df.loc[length] = individual_row_data
Data Cleaning Process
The project includes comprehensive data cleaning functionality:

Text Cleaning: Removes whitespace and extracts clean text from HTML elements

Header Processing: Extracts and cleans table column names

Row Data Extraction: Processes individual table cells and removes HTML artifacts

DataFrame Structuring: Organizes cleaned data into a structured pandas DataFrame

Incremental Data Addition: Efficiently adds new rows to the growing dataset

Error Handling
The script handles various network and scraping scenarios:

Connection failures

Request timeouts

HTTP errors (4xx, 5xx status codes)

General request exceptions

Dependencies
beautifulsoup4 - HTML parsing and web scraping

requests - HTTP requests with custom headers

pandas - Data manipulation and DataFrame operations

Usage
Set the target URL

Run the script to scrape table data

The script automatically handles data extraction and cleaning

Results are stored in a pandas DataFrame for further analysis

Output
Cleaned and structured tabular data

Properly formatted DataFrame with appropriate column names

Error logs for troubleshooting failed requests

This project demonstrates end-to-end web scraping with professional-grade error handling and data cleaning capabilities suitable for data analysis and machine learning pipelines.
