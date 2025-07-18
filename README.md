Myntra Scraper
Overview
The Myntra Scraper is a Python-based project designed to scrape product details from Myntra for items like "Anouk Kurta" and perform data analytics on the extracted data. Using Selenium for navigating dynamic web pages and BeautifulSoup for parsing HTML, the scraper extracts product prices and review links. The collected data is then used for analytics tasks, such as price trend analysis or summarizing review accessibility.
Features

Web Scraping: Extracts product details (e.g., prices, review links) from Myntra’s search and product pages.
Error Handling: Robust checks for dynamic content and missing elements, addressing issues like the NoneType error on review link extraction.
Data Analytics: Processes scraped data for insights (e.g., price distribution, review link availability).
Dynamic Page Handling: Uses explicit waits to ensure reliable scraping of JavaScript-loaded content.

Prerequisites

Python 3.8+
Chrome Browser (compatible with ChromeDriver)
ChromeDriver: Download from chromedriver.chromium.org and add to system PATH.

Required Python Libraries
Install dependencies using pip:
pip install selenium beautifulsoup4 pandas numpy matplotlib

Installation

Clone the Repository:
git clone https://github.com/your-username/myntra-scraper.git
cd myntra-scraper


Set Up a Virtual Environment (recommended):
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate


Install Dependencies:
pip install -r requirements.txt


Install ChromeDriver:

Download the ChromeDriver version matching your Chrome browser.
Add it to your system PATH or specify its path in the script.



Usage

Configure the Search Query:

Edit scraper.py to set the product query (default: "anouk kurta"):product = "anouk kurta"




Run the Script:
python scraper.py


Output:

Scraped data (prices, review links) is printed to the console and can be saved to a CSV file for analysis.
Example output:Price: Rs. 999
Reviews link: https://www.myntra.com/reviews/123456
Price Analytics: Average price = Rs. 1050





Data Analytics
The project includes basic data analytics on scraped data, such as:

Price Analysis: Calculates statistics (e.g., mean, median) of product prices using Pandas.
Review Link Processing: Counts valid review links and identifies products without reviews.
Visualization: Generates plots (e.g., price distribution) using Matplotlib.

Example analytics code:
import pandas as pd
import matplotlib.pyplot as plt

# Load scraped data into a DataFrame
data = pd.DataFrame({"Price": prices, "Review_Link": review_links})
# Calculate average price
print(f"Average Price: Rs. {data['Price'].mean()}")
# Plot price distribution
data['Price'].plot.hist(title="Price Distribution")
plt.show()

Code Structure

scraper.py: Core script for web scraping and data analytics.
requirements.txt: Lists required libraries.
README.md: This documentation file.

Key Code Snippets

Search Page Navigation:product = "anouk kurta"
driver.get(f"https://www.myntra.com/kurta?rawQuery={product}")


Review Link Extraction (Error Fix):Reviews = proResponse_html.find("a", {"class": "detailed-reviews-allReviews"})
if Reviews:
    t2 = Reviews['href']  # Line 24
    Review_link = 'https://www.myntra.com' + t2
else:
    print("Error: Reviews link not found.")


Price Extraction:price_elements = proResponse_html.find_all("span", {"class": "product-discountedPrice"})
for i in price_elements:
    price_value = i.text.strip()



Troubleshooting

Error on Line 24: 'NoneType' object is not subscriptable:
Cause: The find method returns None for the reviews link (detailed-reviews-allReviews).
Solution: Added a check (if Reviews:) to handle cases where the link isn’t found. Verify the class name using Chrome Developer Tools.
Example fix:Reviews = proResponse_html.find("a", {"class": "detailed-reviews-allReviews"})
if Reviews:
    t2 = Reviews['href']
    Review_link = 'https://www.myntra.com' + t2
else:
    print("Reviews link not found. Check class name.")




Dynamic Content Issues:
Use WebDriverWait to ensure the reviews section loads:WebDriverWait(driver, 10).until(EC.presence_of_element_located((By.CLASS_NAME, "detailed-reviews-allReviews")))




CAPTCHA Blocks:
Add a user-agent:options = webdriver.ChromeOptions()
options.add_argument("user-agent=Mozilla/5.0 (Windows NT 10.0; Win64; x64) Chrome/91.0.4472.124")





Notes

HTML Changes: Myntra’s class names (e.g., results-base, detailed-reviews-allReviews) may change. Inspect the website using Chrome Developer Tools to update selectors.
Legal Considerations: Scraping may violate Myntra’s terms. Review https://www.myntra.com/robots.txt and their policies. Use responsibly or explore official APIs.
Analytics Expansion: Add more analytics (e.g., price trends over time, sentiment analysis of reviews) by extending the Pandas/Matplotlib code.

Contributing

Fork the repository.
Create a branch (git checkout -b feature-name).
Commit changes (git commit -m "Add feature").
Push to the branch (git push origin feature-name).
Open a pull request.

License
MIT License. See LICENSE for details.
Contact
For issues or suggestions, open a GitHub issue or email deveshrathod15@gmail.com