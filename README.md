# BEE2041-FinalProject
BEE2041 Final Project - Web Scraping and Data Analytics
This project investigates the home team advantage to hosting a World Cup and the quantification of this advantage
The intended audience for this project, as outlined in the BEE2041 Project Brief, are people with interest in this topic, but no familiarity with the datasets used

## Project Structure

## Installation
Install the classic Jupyter Notebook with:
pip install notebook

To run the notebook:
jupyter notebook

## Usage
Clone this repository
Start Jupyter Notebook
Run blog.ipynb by selecting 'Run' -> 'Run All Cells' from the title bar
If the above does not work, you may need to run the following separately and try again:
!{sys.executable} -m pip install "kagglehub[pandas-datasets]"

## Features
- Imports required libraries and creates clean datasets
- Plots graphs, runs regressions and t-tests
- Blog post: contains blog post markdown and outputs

## Data Sources
- Host dataset webscraped from: "https://en.wikipedia.org/wiki/FIFA_World_Cup"
- Elo ratings dataset downloaded from: "saifalnimri/international-football-elo-ratings"
- Names of participant countries webscraped from: https://en.wikipedia.org/wiki/National_team_appearances_in_the_FIFA_World_Cup
- Stats per country per year dataset webscraped from: f"https://en.wikipedia.org/wiki/{year}_FIFA_World_Cup" where each World Cup year was passed through the html

## Things to Note
- I intended to WebScrape Elo ratings data from https://eloratings.net/ as it is a complete source of Elo ratings data. However, the page seems to be built using JavaScript and I was not familiar enough with Selenium to be able to webscrape it. Instead, I downloaded a dataset from this source on Kaggle as I could not find an alternative for obtaining Elo ratings data.
- From this dataset I dropped columns with empty Elo ratings. All columns with empty ratings were Moldova, which has never competed in a World Cup.
- Some DataFrames I webscraped in the 'Stats Per Country Per Year' section online had subheadings within the table. Alongside the data, these were pulled and made into a columns. I deleted columns which did not have a 'Points' column since all columns of data had a 'Points' entry. This deleted unnecessary subheadings from my data.
- In the final DataFrame, I added +1 to the elo_ranking4 column since this is a pre World Cup peformance metric and using the Elo ranking from the year of the World Cup would capture World Cup results. To capture the year before data but align it with World Cup dates, I added +1 to the year.
- On Wikipedia, the World Cup performance data (matches information, rankings, points etc) is formatted very differently for 1994, 2014, 2018 and 2022 (e.g. using a bracket instead of a table to represent match information beyond the group stage) so I could not webscrape this data properly and these years were mostly left out of the project.

## Potential Next Steps
1. See if I can filter use the most previous Elo rankings data before the World Cup (e.g. Using April 2026 data rather than an averaged 2025 Elo rankings for the 2026 World Cup)
2. Webscrape performance data for 1994/2014/2018/2022 properly
3. Use Selenium, rather than KaggleHub, to directly webscrape Elo points data
