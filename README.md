# BEE2041-FinalProject
BEE2041 Final Project - Web Scraping and Data Analytics
This project investigates the home team advantage to hosting a World Cup and the quantification of this advantage
The intended audience for this project, as outlined in the BEE2041 Project Brief, are people with interest in this topic, but no familiarity with the datasets used

## Project Structure
- data: includes raw and cleaned .csv files of data
- outputs: includes the graphical outputs from the code
- .gitignore
- README.md
- blog.ipynb: includes the code and blog post with outputs are generated the end

## Installation
Install the classic Jupyter Notebook with:
<br>
pip install notebook
<br>
<br>
To run the notebook:
<br>
jupyter notebook

## Usage
- Clone this repository
- Start Jupyter Notebook
- Run blog.ipynb by selecting 'Run' -> 'Run All Cells' from the title bar
- If the above does not work, you may need to run the following separately and try again: !{sys.executable} -m pip install "kagglehub[pandas-datasets]"
- Once run correctly, the blog with outputs is underneath the markdown title 'Blog Post: The Host Nation Advantage? The Process of Creating an Econometric Model of World Cup Performance'
- To find this easier, it is possible to use the toggle on the left of these markdown titles: 'Import Required Libraries and Create Clean Datasets' and 'Graphs and Data Analysis'


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
4. Investigate more variables in the regression, for example:
   - Squad market value
   - Average opponent Elo
   - Confederation status
5. Investigate variables linked to home advantage, for example:
   - Climate similarity
   - Elevation of country

## Blog Markdown
Hosting the World Cup has increasingly been tied to political influence and the projection of soft power, including controversial practices such as ‘sportswashing’, in recent years. These host countries often invest billions into hosting the tournament. As a result, host nations being able to quantitively understand their potential comparative advantage in the tournament has become increasingly important.
<br>
<br>
This blog post uses historical tournament data to analyse whether hosting the World Cup significantly improves host team performance, and if so, to what extent.
<br>
<br>
<img width="260" height="198" alt="image" src="https://github.com/user-attachments/assets/50bac0c4-7040-4f30-b404-f3d6c7aa4fcb" />
<br>
<br>
The above histogram helps us view the distribution of each participating team’s average points per match in each World Cup. Points here are calculated using the ‘three points for a win’ standard where 3 points are awarded to a team for a win, 1 point for a draw, and 0 for a loss.
<br>
<br>
The distribution suggests that host nations tend to achieve a higher average points per match value than non-host nations. The mean difference appears to be almost 1 point per match.
<br>
<br>
However, one must consider that deciding to host the World Cup is partially self-selecting. Host nations tend to be countries that afford the financial costs associated with hosting, which include building new stadiums, having sufficient infrastructure to host hordes of tourists and having developed public services to ensure health and safety practices can be upheld. This all costs a lot. Countries that have the ability to fund this very often also have the ability to devote significant funding to national sporting teams too if sporting presence is a priority. Therefore, stronger World Cup performances by host nations may not be attributed entirely to hosting itself. International team strength should be considered alongside hosting.
<br>
<br>
International team strength has been quantified here by using each country’s Elo rating. Unlike FIFA rankings which were started in 1992, Football Elo ratings take into account all official international matches since 1872, giving a consistent measurement since the first world cup in 1930.
<br>
<br>
By comparing the Elo rating of a country, the year before the World Cup, to avoid using World Cup matches as part of our Elo ‘predictive’ data, and the eventual ranking in the world cup we can observe whether these two factors are correlated in any way.
<br>
<br>
<img width="280" height="206" alt="image" src="https://github.com/user-attachments/assets/896d2d81-8c90-476b-8e66-e16994ef7c21" />
<br>
<br>
Plotting this we observe a negative relationship – as a team’s Elo rating increases their ranking decreases (i.e. gets closer to 1st place). We can also view some significant, but interesting ouliers. This includes France at the 2002 World Cup, who entered as 1998 defending champions before placing last in Group A and scoring no goals. In comparison, Senegal at the 2002 World Cup, placed in group A with France, surpised everyone in their first World Cup appearance by progressing all the way to the quarter finals against Turkiye, where they were knocked out by a ‘golden goal’, a sudden death in extra time.
<br>
<br>
However, ranking is not necessarily the best measure to use to measure team performance, since the number of teams in a world cup has increased from 13 in 1930 to 32 in more modern matches. It has become increasingly competitive to rank First. Average points per match becomes a more reproducible way to measure team performance in the World Cup since it’s value takes into account the number of other participant teams.
<br>
<br>
Plotting this we observe a positive relationship – as a team’s Elo rating increases their average points per match increases (i.e. they perform better each game on average). In this graph, we can also clearly observe the stark difference between France’s performance in the 1998 and 2002 World Cups, where the average points per match for France decreased from just over 2.7 to under 0.4. Interestingly, France hosted the 1998 World Cup.
<br>
<br>
<img width="315" height="230" alt="image" src="https://github.com/user-attachments/assets/3a6d0303-ecdc-4771-8392-81ae10ebed14" />
<br>
<br>
So, moving onwards, does this mean we can use Elo rating as reliable and reproducibile predictor of World Cup performance, where World Cup performance is expressed as average points per match?
<br>
<br>
To determine this, we can run a regression of our current model:
<br>
<br>
average_points_per_match = $α$ + $β$(elo_rating) + $e$
<br>
<br>
From this we obtain:
<br>
<br>
<img width="351" height="229" alt="image" src="https://github.com/user-attachments/assets/2ba7c5cb-9c30-4eac-9605-db226dd6243f" />
<br>
<br>
There are a few values to pay attention to here. To start, Prob (F-statistic) = 0.0000188. This basically means that Elo rating is statistically significant in predicting average points per match at the 1% (0.01), and therefore also at the 5% (0.05), significance levels. The coefficient of rating is 0.0025. that means for every increase in the Elo rating by 1, the average points per match will typically increase by 0.0025. This means that a 400 point increase in Elo rating is typically associated with a 1 point increase in points per match. R-squared has a value of 0.201. This indicates that Elo ratings explain roughly 20.1% of the variation in average points per match. This also means that roughly 80% of variation in average points per match is unexplained in our current model. Overall, Elo is a statistically significant but partial predictor of points per match, so we should look to investigating other variables to explain the rest of the variance in points per match.
<br>
<br>
To investigate variance from the line of best fit, I created a residual term, where ‘residual’ equals the distance between each value and the predicted points per match based off of Elo rating. This redsidual value can be positive if the real value is higher than the predicted value or negative if lower than the predicted value. This quantifies all that is “unexplained” in our current model.
<br>
<br>
By plotting the residuals of hosts and non hosts separately as a box plot, we can observe how the residuals of hosts tends to be more positive than the residuals of non-hosts. Further, the residuals of hosts tend to have more variance than the residuals of non-hosts. This suggests since the model may be suffering from omitted variable bias correlated to hosting since residuals for hosting tend to be underpredicted at a wide variance, compared to non-hosters whoes performance looks to be predicted in a narrower, more accurate range.
<br>
<br>
<img width="366" height="276" alt="image" src="https://github.com/user-attachments/assets/dad188e1-de3b-4946-ac55-a7fa4c55b4a7" />
<br>
<br>
To further investigate it, I created a dummy variable ‘is_host’ which has 2 values. When is_host is equivalent to 0 we are dealing with a non-host and when is_host is equivalent to 1 it indicates that the data refers to a hosting country. This then allowed me to then quantitatively test, through a t-test, whether the average residual between hosts (is_host = 1) and non-hosts (is_host = 0) is actually statistically different (rather than just looking like it).
<br>
<br>
The t-test outputted the following results:
<br>
<br>
t-statistic: -2.37350410888058
p-value: 0.01995873617042853
<br>
<br>
Here, we should pay most attention to the p-value. A p-value of 0.020 (rounded up) means we can reject a null hypothesis that hosts and non-hosts have equal mean residuals at the 5% (0.05) significance level since 0.020 < 0.05. This p-value basically means that if there were no real difference between hosts and non-hosts, we would only expect to see differences between residuals this extreme roughly 2% of the time.
<br>
<br>
Next, I believed it was important to confirm whether the residual remained constant over all levels of Elo rating, our independent variable. If residuals, known as error terms, do remain constant this is known as ‘homoskedasticity’. If not, this is referred to as ‘heteroskedasticity’. It is important to confirm heteroskedasticity since if a model is heteroskedastic, p-values are often considered unreliable since t-tests will often overestimate the significance of results.
<br>
<br>
Plotting a scatter graph of Elo rating of the previous year against our residual can help us visualise whether our current model exhibits homoskedasticity:
<img width="321" height="241" alt="image" src="https://github.com/user-attachments/assets/69d59793-62fe-4a78-abf7-22d9043e8452" />
<br>
<br>
Here, the vertical spread appears relatively constant over the range of Elo ratings, except two extreme outliers in the bottom right. While the spread does slightly widen at the upper end of Elo rating, it is not drastic enough to suggest strong evidence of heteroskedasticity.
<br>
<br>
Although homoskedasticity cannot be confirmed from this graph alone, as running statistical tests would be required, this scatter plot of residuals does not present a picture of heteroskedasticity. Considering the visual evidence available from the scatter plot, the residuals will be assumed to be homoskedastic for the remainder of the blog.
<br>
<br>
Next, I created a new regression model that considered the new variable is_host:
<br>
<br>
average_points_per_match = $α$ + $β$(elo_rating) + $γ$(is_host) + $e$
<br>
<br>
Running a regression of the independent variables elo_rating and is_host on average_points_per_match, the following table was obtained:
<br>
<br>
<img width="385" height="266" alt="image" src="https://github.com/user-attachments/assets/eb651ca9-1890-4f04-91ee-a47364329fc3" />
<br>
<br>
We should pay attention to the is_host value p-value under P > |t|, which is 0.021. This is very similar to the independent t-test that was run on is_host earlier which resulted in a p-value of 0.020. This means that hosting remains a statistically significant predictor of points per match (at the 5% significance level) even after controlling for Elo rating.
<br>
<br>
It is also important to notice that the coefficient (under coef) is for is_host is 0.6989. We discussed earlier how the coefficient of rating (being 0.0025) indicates that for every 1 point increase in Elo_rating, there will typically be a 0.0025 point increase in points_per_match in the model. Here, the coefficient of is_host indicates that a change from 0 to 1 (going from a non-host to a host) is equivalent to a 0.70 (rounded up) increase in points_per_match.
<br>
<br>
This suggests that, in this model, the estimated effect of becoming a host country is similar in magnitude to the estimated effect associated with a 280 point increase in Elo rating. This is roughly equivalent to the difference between Algeria’s and England’s Elo rating (1743 vs 2020, a difference of 277) as of 2026.
<br>
<br>
Re-plotting again the scatter graph of Elo rating against average points per match, the difference in performance between hosts and non-hosts can be observed by plotting two different lines of best fit:
<br>
<br>
<img width="375" height="291" alt="image" src="https://github.com/user-attachments/assets/261ba28e-2fce-463b-abd9-726c62860b34" />
<br>
<br>
It is clear from the lines of best fit that hosts tend to have a higher average points per match at the same Elo rating as non-hosts. The host’s line is roughly 0.7 points above the non-host line, as expected from our regression.
<br>
<br>
Finally, I added an interaction effect to see if the effect of Elo rating differs depending on whether a country is a World Cup host. This modifies the regression model to:
<br>
<br>
average_points_per_match = $α$ + $β$(elo_rating) + $γ$(is_host) + $δ$(elo_rating * is_host) + $e$
<br>
<br>
Where elo_rating * is_host is the interaction effect.
<br>
<br>
Running a regression on this, the following table is obtained:
<br>
<br>
<img width="413" height="291" alt="image" src="https://github.com/user-attachments/assets/50db46ae-75bd-4146-b431-405b26bf849c" />
<br>
<br>
It can be observed that the interaction effect does in fact not improve model performance. With the addition of an interaction variable, neither is_host or interaction are statistically significant at the 5% significance level (0.05) since both of their ‘P > |t|’ values are above 0.05. The interaction effect has likely introduced multicollinearity and is likely highly correlated with is_host.
<br>
<br>
Overall, using the following model:
<br>
<br>
average_points_per_match = $α$ + $β$(elo_rating) + $γ$(is_host) + $e$
<br>
<br>
We can suggest that being the host nation is associated a statistically significant advantage of roughly 0.70 extra points per match. It can also be suggested, in this model, that the estimated effect of becoming a host country is similar in magnitude to the estimated effect associated with a 280 point increase in Elo rating.
<br>
<br>
However, I would be interested in investigating more variables, to potentially reduce the possibility the model is suffering from omitted variable bias. For example, I would look to examine squad market value, average opponent Elo, and confederation status (e.g. CONMEBOL is typically considered the most difficult to qualify in). I could also examine some factors linked to home advantage. For example, climate similarity (e.g. groups from warmer countries may perform better in heat than groups from cooler countries) and average elevation of country (e.g. Bolivia has a significant advantage at home that it loses in many countries due to their experience playing in elevation. This may overpredict their rank in Elo rating when playing abroad).
<br>
<br>
Further, since the dataset web scraped misses some recent World Cup data due to limitations, I would be interested in investigating these too to further add to this model. It will also be exciting to add the upcoming 2026 World Cup to the model and perhaps use this model to create some predictions for it.
