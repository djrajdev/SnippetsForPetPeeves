## Transitioning from the beautiful R to the slightly annoying Python

This is a ctrl+F friendly doc to keep a track of things I can do blindfolded and drunk in R, but need some googling in python until I get familiar. Mostly `dplyr` to `pandas`.

<u>**Citation**</U><br>
[(Docs) comparison with R libraries.](https://pandas.pydata.org/pandas-docs/stable/getting_started/comparison/comparison_with_r.html)   
Although this quite comprehensive, I find value in documenting it in my words for ease of search.

**Column types or classes for data frame**   
```
# R
sapply(df,class)

# python
df.dtypes
```

**Column names**

```
# R
df %>% names

# python
df.columns
list(df.columns)    # get list of names
```

**Select only specific column types**
```
# R
df %>% select_if(is.numeric)

# python
df.select_dtypes('object').columns
df[df.select_dtypes('object').columns]	# gives back actual dataframe of selected cols
```

**Exclude cols by name**
```
# R 
df %>% select(-c(col1,col2))

# python
df.drop(['col1', 'col2'], axis=1, inplace=True) 	
```
`inplace` has side-effects, it doesn't return df but avoids making a copy

**Get size of data frame**
```
# R
df %>% dim()

# python
df.shape
```

**Count of unique values in each column**
```
# R 
df %>% summarise_all(n_distinct)

# python
df.apply(lambda x:x.nunique())
```

**Select unique values from a column**
```
# R
df %>% distinct('col1')

# python
df['col1'].unique()
```

**Get year of datetime column**
```
# R
library(lubridate)
year(df %>% pull('datecol'))

# python
import datetime as dt
df['datecol'].dt.year
```

**Filter column for values in list variable**
```
# R 
str_list = c('a', 'b')
df %>% filter(col1 %in% str_list)

# python
str_list = ['a', 'b']
df.query("col1 in @str_list")
```

**Multiple aggregation / summarise functions**
```
# R
df %>% group_by(col1) %>% summarise(newcol1 = f1(col2), newcol2 = f2(col2))

# python
df.groupby('col1').agg(newcol1 = ('col2', 'f1'), newcol2 = ('col2', 'f2'))
```
