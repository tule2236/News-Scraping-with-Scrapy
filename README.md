# News Scraping with Scrapy
[Scrapy](https://doc.scrapy.org/en/latest/intro/tutorial.html) is a great scraping tool that work great on crawling dynamic websites, especially with those having a well-structured URL links that we can formulized with jQuery. 
  In this project, I choose to scrape financial news data from *http://www.reuters.com*. This website has well-structured URL links that are perfect to analyze the relationship between news and company's performance.

>https://www.reuters.com/finance/stocks/company-news/ + Company Symbol + Date

I decided not to scrape the full article but only the summary displayed on the main pages since it gives good overview of the full content. Moreover, since we will process a big news dataset of 22 companies in the 6-year time span 2011 to 2017, I try to make each data record as compact as possible to speed up the processing time.
## Installation
##### Create a virtual environment

```
pip install virtualenv
```
```
mkvirtualenv samsung
```
##### Install Scrapy and dependencies
```
pip install scrapy service_identity ipython pillow
```
Can check whether we have successfully installed Scrapy by typing command
```
pip freeze
```
## Development Setup 
##### Create the first Spider
To create a Spider project, simply type
```
scrapy startproject samsung
```
This will create a project directory **samsung** and all the neccessary files for the crawler. Now I access the project directory
```
cd samsung 
```
Display all available Scrapy command by
```
scrapy -h
```
Create the first Spider named **samsung_Spider** followed with the link of the news website that I want to scrape data from. 
```
scrapy genspider samsung_Spider www.reuter.com
```
## Running the Test
  I write a script **link_generator.py** to generate all the URL links of Reuters news of 22 companies from January 1, 2011 to December 31, 2017. Each company would have 365 days x 6 years = 2190 links, and I end up with 2190 x 22 = 48180 links stored in **url_list.txt**  
  Then, I construct my Spider in **samsung_Spider.py**.  
  After specifying the crawling rule, I let the Spider crawl the website
```
scrapy crawl samsung_Spider
```
If I want to write the scraped content to csv file and don't display the content in the terminal, I use the command
```
scrapy crawl --nolog --output=export.csv samsung_Spider
```
The source code doesn't contain the date in a clear structure, so I obtained the date from the URL links and then, I write a script **convert_file.py** to extract the date from the URL and re-format them to *MM/DD/YY*
