## Transitioning from the beautiful R to the slightly annoying Python

This is a ctrl+F friendly doc to keep a track of things I can do blindfolded and drunk in R, but need some googling in python until I get familiar. Mostly `dplyr` to `pandas`.

**Column types or classes for data frame**   
```
# R
sapply(df,class)
```

```
# python
df.dtypes
```

<br />

**Column names**

```
# R
df %>% names
```

```
# python
df.columns
list(df.columns)    # get list of names
```
