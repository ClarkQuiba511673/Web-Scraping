# Web Scraping Lab with Python

## 📋 Lab Objectives

By the end of this lab, students will be able to:

- Understand the basic concept of web scraping
- Use Python libraries (requests and BeautifulSoup) to extract data from web pages
- Parse and clean HTML data
- Save extracted data into CSV files

## 🛠 Requirements

- Python 3.x installed
- Libraries: requests, beautifulsoup4, pandas
- Internet connection
- Jupyter Notebook or any Python IDE (e.g., VS Code, PyCharm)

## 📦 Installation

Install dependencies (if not already installed):

```bash
pip install requests beautifulsoup4 pandas
```

## 🚀 Step-by-Step Instructions

### Step 1: Choose a Target Website

Example: http://books.toscrape.com

This is a safe website designed for practicing web scraping.

### Step 2: Fetch the Web Page

```python
import requests

url = 'http://books.toscrape.com/'
response = requests.get(url)
print(response.text)  # HTML content
```

### Step 3: Parse HTML with BeautifulSoup

```python
from bs4 import BeautifulSoup

soup = BeautifulSoup(response.text, 'html.parser')

# Example: Extract book titles
books = soup.find_all('h3')
for book in books:
    print(book.find('a')['title'])
```

### Step 4: Extract Data into a Structured Format

```python
titles = []
prices = []

for book in soup.select('.product_pod'):
    title = book.h3.a['title']
    price = book.select_one('.price_color').text
    titles.append(title)
    prices.append(price)

# Display
for t, p in zip(titles, prices):
    print(f'{t} - {p}')
```

### Step 5: Save to CSV

```python
import pandas as pd

df = pd.DataFrame({
    'Title': titles,
    'Price': prices
})
df.to_csv('books.csv', index=False)
print("Data saved to books.csv")
```

## 📝 Assignment / Deliverables

1. Scrape any data from your chosen website
2. Save the results to a file `book_list.csv`
3. Submit the following:
   - Python script or notebook
   - `book_list.csv` file
   - Screenshot of terminal/output

## 📚 Additional Notes

- Always check a website's `robots.txt` file before scraping (e.g., http://books.toscrape.com/robots.txt)
- Be respectful of website resources - add delays between requests if scraping multiple pages
- Websites may change their structure, which could break your scraper

## 🤝 Ethical Considerations

Web scraping should always be done responsibly:
- Only scrape publicly available data
- Respect the website's terms of service
- Don't overwhelm servers with too many requests
- Use scraped data only for legitimate purposes

Happy scraping! 🕷️
