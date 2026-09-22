# AmbitionBox Indian Companies Data Scraper

A Python-based web scraping project that collects company-related information from AmbitionBox and converts it into a structured dataset using **Requests, BeautifulSoup, Regular Expressions, and Pandas**.

## About the Project

This project was created as a learning/practice project to understand how web scraping works in Python.

The notebook starts with a simple request to an AmbitionBox company-listing page, handles the `403 Forbidden` response using request headers, parses the HTML using BeautifulSoup, extracts the required company information, and finally scrapes multiple pages to build a larger dataset.

The final dataset contains **10,000 company records**.

## What I Collected

For each company, the scraper collects information such as:

- Company name
- Company rating
- Industry
- Headquarters
- Number of other locations
- Areas where the company is highly rated
- Areas where the company is critically rated
- Number of reviews
- Number of salary entries
- Number of interview entries
- Number of job listings
- Number of benefits entries

## Project Workflow

```text
AmbitionBox Company Listing
            ↓
       HTTP Request
            ↓
   Handle 403 / User-Agent
            ↓
      HTML Response
            ↓
     BeautifulSoup Parser
            ↓
   Extract Company Details
            ↓
       Data Cleaning
            ↓
      Pandas DataFrame
            ↓
       CSV Dataset
```

## Technologies Used

| Technology | Purpose |
|---|---|
| Python | Main programming language |
| Requests | Sending HTTP requests |
| BeautifulSoup | Parsing HTML pages |
| Regular Expressions | Extracting and cleaning values |
| Pandas | Creating and exporting the dataset |
| Jupyter Notebook | Development and experimentation |

## Repository Structure

```text
.
├── DAY 18.ipynb
├── indian_companies_dataset.csv
├── README.md
└── .gitignore
```

### `SCRAPING.ipynb`

The notebook contains the complete scraping process, including:

1. Making an initial request to AmbitionBox
2. Handling a `403` response using a User-Agent header
3. Parsing HTML with BeautifulSoup
4. Inspecting the company card structure
5. Extracting company names and ratings
6. Extracting industry and headquarters information
7. Extracting review, salary, interview, job, and benefit counts
8. Handling missing values
9. Cleaning values using regular expressions
10. Scraping company-listing pages from page 1 to page 500
11. Creating a Pandas DataFrame
12. Exporting the final dataset to CSV

### `indian_companies_dataset.csv`

The final scraped dataset contains **10,000 rows** and the following meaningful fields:

| Column | Description |
|---|---|
| `name` | Name of the company |
| `rating` | Company rating |
| `industry` | Industry/category of the company |
| `headquarter` | Company headquarters |
| `other_locations` | Number of additional locations |
| `highly_rated_for` | Area(s) where the company is highly rated |
| `critically_rated_for` | Area(s) where the company is critically rated |
| `reviews` | Number of reviews |
| `salaries` | Number of salary entries |
| `interviews` | Number of interview entries |
| `jobs` | Number of job entries |
| `benefits` | Number of benefit entries |

The CSV also contains the Pandas index column generated during CSV export.

## Scraping Approach

The final implementation uses a browser-like User-Agent while making requests:

```python
headers = {
    'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) '
                  'AppleWebKit/537.36 (KHTML, like Gecko) '
                  'Chrome/120.0 Safari/537.36'
}
```

The scraper then loops through the company-listing pages:

```python
for j in range(1, 501):
    url = f'https://www.ambitionbox.com/list-of-companies?page={j}'
```

For every successful page, the company cards are parsed and the required information is extracted.

A one-second delay is also used between requests:

```python
time.sleep(1)
```

This was included to keep the request rate lower and reduce the chance of sending requests too quickly.

## Data Cleaning

The project also includes a small cleaning step using Regular Expressions.

For example, values such as:

```text
1.1L
70.4k
9k
```

are extracted from the text using a regular expression so that the useful numeric-unit part can be stored in the dataset.

## How to Run the Project

### 1. Clone the repository

```bash
git clone <your-repository-url>
cd <your-repository-folder>
```

### 2. Install the required libraries

```bash
pip install pandas requests beautifulsoup4 lxml jupyter
```

### 3. Start Jupyter Notebook

```bash
jupyter notebook
```

Open:

```text
DAY 18.ipynb
```

### 4. Run the notebook

Run the cells in order.

The final section of the notebook performs the multi-page scraping and saves the result as:

```text
indian_companies_dataset.csv
```

## Learning Outcomes

Through this project, I practiced:

- Sending HTTP requests using Python
- Understanding and handling HTTP `403` responses
- Using request headers
- Parsing HTML with BeautifulSoup
- Finding elements using HTML tags and CSS classes
- Extracting structured information from webpages
- Handling missing HTML elements
- Using Regular Expressions for data extraction
- Working with Pandas DataFrames
- Exporting scraped data to CSV
- Building a simple multi-page web scraper

## Limitations

This is a learning project and the scraper depends on the current HTML structure of AmbitionBox.

If the website changes its:

- HTML structure
- CSS classes
- page layout
- request restrictions

the scraper may need to be updated.

The project also does not implement advanced features such as automated retries, proxy rotation, concurrent requests, database storage, or a scheduled scraping pipeline.

## Future Improvements

Some improvements I would like to make in the future:

- Add better exception handling and retry logic
- Add logging for failed pages
- Prevent duplicate company records
- Convert values such as `1.1L` and `70.4k` into proper numeric values
- Add exploratory data analysis and visualizations
- Save the data directly to a database
- Make the number of pages configurable
- Add a `requirements.txt` file
- Improve the scraper so it can adapt more safely to changes in webpage structure

## Note

This project is intended for **educational and learning purposes**.

When using or modifying the scraper, please respect the target website's terms, policies, and applicable rules regarding automated access and data collection.

## Author

**Manikarnika Yadav**

A student project created while learning Python, web scraping, and data handling.
