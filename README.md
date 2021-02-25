# Surfs_Up
## Overview of the analysis

The purpose of this analysis is to see the temperature statistics for the months of June and December to find out if running a surf shop is sustainable year around. We will sort the data and perform analysis by running two seperate queries, one for June and the other for December. We run our queries and store the temperatures in a list then convert them to a dataframe. By using the .describe() method on the dataframe, we can retrieve the summary statistics.

## Results

* The minimum temperature for June is 64 and for December, it is 56. The June weather looks more favorable for the business.
* The max temperature for June is 85 and for December, it is 83. This does not seemm to be a huge difference and hence, December can also be considered as a fair season for the business.
* The inter quartile range for June is 73 to 77 with a mean of 74.94 while the inter quartile range for December is 69 to 74 with a mean od 71.04.


![Image](https://github.com/Vaishali715/surfs_up/blob/main/Resources/june_temps.png)
![Image](https://github.com/Vaishali715/surfs_up/blob/main/Resources/dec_temps.png)

Looking at the overall statistics for the month of June, it is a good warm month for surf and ice cream while December looks little cold and may be challenging for the surf and ice cream business.

## Summary

### Analysis of temperature data for the month of June and December

The data is imported from SQLite to pandas DataFrame and we can access the data to get the statistical information for the analysis. Using the describe() method we get the statistical data like mean, std, min, max, percentiles and based on the analysis, we can suggest that June looks nice warm month and is perfect for the surf and ice cream business.

The following steps explain how the data is accessed, filtered and visualized.
1. The following dependencies are imported

```
import numpy as np
import pandas as pd

# Python SQL toolkit and Object Relational Mapper
import sqlalchemy
from sqlalchemy.ext.automap import automap_base
from sqlalchemy.orm import Session
from sqlalchemy import create_engine, func
```

2. Creating engine function - Used to query a SQLite database.
```
engine = create_engine("sqlite:///hawaii.sqlite")
```
3. automap_base() function - to reflect our existing database in SQLite into a new model.
```
Base = automap_base()
```
4. prepare() function - reflect the schema of our SQLite tables into our code and create mappings.
```
Base.prepare(engine, reflect=True)
```
5. Reference the measurement and station classes by assigning variables measurement and station.
```
Measurement = Base.classes.measurement
Station = Base.classes.station
```
6. Use an SQLAlchemy Session to query our database.
```
session = Session(engine)
```
7. Using session.query we can now get the June and December temperatures from the SQLite database and save it to a variable. Code showing only June temperatures.
```
temp_june = session.query(Measurement.tobs).filter(extract('month', Measurement.date) == 6)
```
8. We then convert this data to a list.
```
june_list = []
for t in temp_june:
    june_list.append(t)
```
9. Next we convert the data to a pandas DataFrame so we can perform functions and use statistical models.
```
june_temp_df = pd.DataFrame(june_list)
```
10. Using describe() method we can now get the interquartile range.
```
june_temp_df.describe()
```

![Image](https://github.com/Vaishali715/surfs_up/blob/main/Resources/june_temps.png)

### Additional query 1 - Precipitation data for the month of June.
We have the query data saved in a variable called precip_june, then we convert this variable to a list named precip_june_list and finally convert this list to a pandas DataFrame called precip_june_df to get statistical and visulaziation data.

```
precip_june = session.query(Measurement.prcp).filter(extract('month', Measurement.date) == 6)
precip_june_list = []
for p in precip_june:
   precip_june_list.append(p)
#print(precip_june_list)
precip_june_df = pd.DataFrame(precip_june_list)
precip_june_df.describe()
```

![Image](https://github.com/Vaishali715/surfs_up/blob/main/Resources/june_prcip.png)

### Additional query 2 - Precipitation data for the month of December.
We have the query data saved in a variable called precip_dec, then we convert this variable to a list named precip_dec_list and finally convert this list to a pandas DataFrame called precip_dec_df to get statistical and visulaziation data.

```
precip_dec = session.query(Measurement.prcp).filter(extract('month', Measurement.date) == 12)
precip_dec_list = []
for p in precip_dec:
   precip_dec_list.append(p)
#print(precip_dec_list)
precip_dec_df = pd.DataFrame(precip_dec_list)
precip_dec_df.describe()
```

![Image](https://github.com/Vaishali715/surfs_up/blob/main/Resources/dec_prcip.png)

