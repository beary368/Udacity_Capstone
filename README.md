
# Commodity Super- & Agriculutre-Cycles

Udacity Capstone project utilizing price time series data from a few different sources, transforming the data, implementing a Band-Pass (BP) Filter, and plotting the cyclical components versus the real price data.

# Motivation

### At Mars, we are a commodity conversion company. As a company heavily involved in the purchases of various agriculture and energy commodities we want to gain insights in order to manage our risk and deliver value to the business. If these signals indicate a recession or growth (Super-Cycles) and supply shocks or demand destruction (Ag-cycles), they could be a factor we look at when we buy.

# Libraries

These are the following libraries I used.

```python
numpy==1.16.2

matplotlib==3.0.3

pandas==0.24.2

statsmodels==0.9.0

scipy==1.2.1
```
My import statement was as follows...
```python

import pandas as pd
import numpy as np
from statsmodels.tsa.filters.cf_filter import cffilter
import matplotlib.pyplot as plt
from matplotlib.ticker import PercentFormatter,NullFormatter
from scipy.interpolate import interp1d

```

# Files

There are 2 main excel files.

1. CMOHistoricalDataAnnual.xlsx - Contains 6 tabs, we use 2. Use tab 'Annual Prices (Nominal)' to bring in all price data dating back to 1960 in Nominal terms. Use tab 'Annual Prices (Real)' to import column BT which is the MUV Index which we will use to deflate the Nominal Prices to Real.


2. GY_Table_Reweighted.xlsx - Contains 2 tabs, we will use both. On first tab 'GY_Table', we will import columns A - C as this is the [Grilli-Yang Commodity Price Index Table](https://editorialexpress.com/cgi-bin/conference/download.cgi?db_name=SECHI2018&paper_id=61), which is used to weight the indexed real prices. Columns H & I is the MUV Index from 1900 - 1959 allowing us to reindex the rest of price data. The second tab, 'GY_Price_Data_1900-2010' houses all commodities price data from 1900 - 2010 (we will only be using 1900 to 1959).

The rest of the files are either images for Ipython Notebook or README file. 

# Summary/Results

## Conclusions

Super-cycles: 

1. What are the super cyles within that last 120 years?
    
    - Since we defined super cycles as they did in the paper, [Super-cycles of commodity prices since the mid-nineteenth century](https://www.un.org/esa/desa/papers/2012/wp110_2012.pdf), we saw 4 distinct supercycle periods in all 4 of the commodity baskets.

2. What defines the super cycles during these periods?
    
    - While the exact time periods vary, it seems to show the US expansion before WW1 as the first cycle, Europe's reconstruction and WW2 as the second, the expanding Global Economy mixed with shorter term events such as wars and oil crisis as the third, and China's rapid industrialization and expansion as the fourth.

Ag-Cycles:

1. Are there commodities which have a similar length of cycle?
    
    - See improvements section on attacking this with Fourier Transforms in future. But, by looking at these graphs you can see some similarities in row crops (or those that feed off row crops such as Beef or Lamb) have a generally shorter cycle (2-3 years) than the tree crops (cocoa, coffee, palm oil, etc.) which are about 4-6 years on average.
    
2. Are notable Supply Shocks (1970s Oil Crisis, 2007 Farm Crisis, etc.) able to be seen coincidentally as a peak in the ag-cycle component?

    - As stated above in findings, there are a few noted especially on Oil and Farm Crisis. There is also one about the migration from the Gros Michel Banana to the Cavendish which was the cause of its ag-cycle and price spike around 1950.
    
## Did we achieve what we set out to do? (Metrics)

1. Is each of the super-cycles we evaluate, representative of a particular economic expansion/recession? Also do each of the cycles meet the minimum requirements of a super-cycle (i.e > 20 years but < 70 year periods)?

    - The food and total had a clear expansion and recession component in each of the 4 delineated super-cycles. 
    
    - However, Non-Food shows only an expansionary period during the second and a contractionary period in the third. While these periods both meet the 20 minimum it may be a better estimation to show them as a long super-cycle with a period approaching 70 years. We had added this to future work/improvements discussion below.
    
    - Metals has an interesting first 2 super-cycle periods. It meets the time constraint as non-foods does but there is a clear downward trend between the first two periods. It appears to have peaks during war preparation/war-time as metal is in high use for these materials but the downtrend is unexplained by this. I have also added this to the future work/improvements.

2. Do major supply shocks in agriculture products show a distinct reflection on the price? Is there a negligible correlation between the agriculture cycle and real prices?

    - Yes major supply shocks show a distinct reflection on price as stated above (there are more notable examples, but we will save you from boredom). Cocoa is one for example...you can see that [explanation here](https://medium.com/@chuckmorris1621/commodity-super-cycles-agriculture-cycles-what-causes-them-and-their-impact-on-price-7a7d33033f7a).
    - The correlations between agriculture-cycles and real prices are quite larger than I originally expected especially in softs commodities (cocoa, coffee, sugar) than in grains or fruits. In softs, the correlation was upwards of 30% as opposed to 10 - 20% for livestock and annual crops.
    
## Future Work

1. With Super-cycles, make the entire process a function so it can be callable and give more personalized information to stakeholders when they want to know what next instance of commodity supercycle they are in. 

2. With Ag-cycles figure out a method to find maximum, minimum, and average period of cycle rather than estimating by looking at the charts

3. Find a way to empirically explain the consistent downtrend of metals basket between 1900 and 1950. Also evaluate if the non-food super-cycle should be expanded from 2 small cycles to 1 large from 1935 to 2000. Both would fit the length of time stipulation.

## Improvements

1. More dynamic shading of the super cycle regions, currently hard-coded through trial and error.

2. Clean code into functions to transform this into a callable ETL pipeline for more 'data at your fingertips' for stakeholders.

3. Incorporate a more interactive chart style by plotly to more accurately compare timeframes of cycles versus real prices.

communicates the libraries used, the motivation for the project, the files in the repository with a small description of each, a summary of the results of the analysis, and necessary acknowledgements.

# Acknowledgements

### 1. I would like to thank Udacity for giving me the opportunity to explore this topic through Python. I do not believe I would have had the skills to generate this analysis if it wasn't for the skills gained throughout the course.


### 2. I would like to thank the Commercial Applied Research Team (CART) at Mars for encouraging me to attempt this analysis and providing suggestions for future work to make this project truly impactful.

### 3. Lastly, I would like to thank the World Bank for providing this data to the public so I could make this project possible.
