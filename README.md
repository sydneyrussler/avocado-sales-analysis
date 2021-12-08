# Avocado Sales Volume and Price Analysis
## by Sydney Russler


## Dataset

This dataset was download from Kaggle at the link https://www.kaggle.com/neuromusic/avocado-prices and originally sourced from the Hass Avocado Board website in May of 2018 at this link http://www.hassavocadoboard.com/retail/volume-and-price-data.

As described by Hass:
> The table below represents weekly 2018 retail scan data for National retail volume (units) and price. Retail scan data comes directly from retailers’ cash registers based on actual retail sales of Hass avocados. Starting in 2013, the table below reflects an expanded, multi-outlet retail data set. Multi-outlet reporting includes an aggregation of the following channels: grocery, mass, club, drug, dollar and military. The Average Price (of avocados) in the table reflects a per unit (per avocado) cost, even when multiple units (avocados) are sold in bags. The Product Lookup codes (PLU’s) in the table are only for Hass avocados. Other varieties of avocados (e.g. greenskins) are not included in this table.

Some relevant columns in the dataset:

* Date - The date of the observation
* AveragePrice - the average price of a single avocado
* type - conventional or organic
* year - the year
* Region - the city or region of the observation
* Total Volume - Total number of avocados sold
* 4046 - Total number of avocados with PLU 4046 sold
* 4225 - Total number of avocados with PLU 4225 sold
* 4770 - Total number of avocados with PLU 4770 sold

According to the Hass Avocado Board website, the Product Lookup codes are assigned as follows:

> Small/Medium Hass Avocado (~3-5oz avocado) | #4046 Avocado

> Large Hass Avocado (~8-10oz avocado) | #4225 Avocado

> Extra Large Hass Avocado (~10-15oz avocado) | #4770 Avocado


### Preliminary Wrangling
* Reformat column names for easier coding (replace spaces with _ and change all letters to lowercase).
* Rename PLU number columns to descriptive names {'4046':'small_medium', '4225':'large', '4770':'extra_large'}.
* Drop extra index column 'unnamed:_0'
* Date column changed to 'datetime' with to_datetime function.
* Year column changed to 'object' type with astype function.
* Convert 'type' column to dummies, with 1 representing organic and 0 representing conventional, using get_dummies function. Drop the orginal type column and the new conventional column to leave one organic column where 1 indicates organic and 0 indicates not organic (or conventional).
* Create column 'season_name' to categorize each observation by season based on the date. Convert to ordered categorical type.


## Summary of Findings

* Volume has a long-tailed distribution, with the majority of units sold weekly at the smaller end and very few sold at the larger end. When plotted on a log-scale histogram, the volume distribution looks roughly trimodal. There are peeks between 3k and 30k units, 100k and 1 million units, and a small peek around 3 million units. There is also a fourth very small peek between 10 and 30 million.
* Roughly half of all observations are of conventional avocados and the other half is organic as shown by a countplot.
* The majority of the total volume is conventional avocados with around 4 million sold and less than 500k sold of organic as shown by a bar chart.
* Average unit price is normally distributed with a peak between 1 and 1.25 dollars as shown through a histogram.

#### Correlation plot findings
* There are very strong correlations between total volume and the volume of each subset (small_medium, large, and extra_large, as wells as total_bags).
* There is not an extremely strong correlation between price and volume; however, a negative correlation does exist. The negative correlation is strongest between the small/medium avocados and the price.
* There is a negative correlation present between the number of bags sold and the total price of the avocados.

#### Box plots
* The price of organic avocados is consistently higher than the price of conventional. The median average price for organic avocados is above the third quartile for the conventional avocados. This shows that consumers are consistently paying more for organic!
* The average price also varies by season, though not as drastically. Autumn had the highest median price for avocados, while winter had the lowest. However, all of the medians were within 25 cents of each other.

#### Bar charts
* The average price and total volume both vary by month, with a negative correlation between the two when assessing monthly trends.

#### Scatter plots
* There is a weak negative correlation between average price and total volume seen.
* For organic avocados, we see a cluster of data points at a lower volume (between 1k and 30k units) and higher price (between 1.5 and 2 dollars).
* For conventional avocados, we see a less defined cluster. However, most of the data falls into a much higher range of volume (between 100k and 1 million units) and lower price (between 50 cents and 1.5 dollars).
* There is a negative correlation between price and number of bags sold. As more bags are sold, the average price per unit decreases, matching the prediction.

### Multivariate Exploration

#### Plot of prices by date
* For both conventional and organic avocados, prices did not fluctuate dramatically over time. However, the trend of prices increasing during autumn months is visible for both.

#### Point plots of average price and volume by month
* The negative correlation between average price and total volume is strongest for conventional avocados.

#### Line plot of volume by date
* During the three years observed, the decrease in total volume in very evident. This trend also exists for the small/medium and large avocados, which make up the vast majority of avocados sold.


## Key Insights for Presentation

The average price and total volume both vary by month, with a negative correlation between the two when assessing monthly trends. To show this relationship, I will isolate the visualization that focus only on the price, volume, and months. I will also take the line plot of rolling averages for the volume over time and include only the line for total volume, and add a line for the rolling average for average price to make one concise concluding visual.
