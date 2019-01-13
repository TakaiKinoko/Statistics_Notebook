## Why anecdata (anecdotal evidence) normally fail?
* small number of observations
* selection bias
* confirmation bias 
* inaccuracy

## a statistical approach
* data collection 
* descriptive statistics
* exploratory data analysis
* hypothesis testing
* estimation

# Terms
* **cross-sectional** study v.s. **longitudinal study**
    * cross-sectional study captures a snapshot of a group at a point in time. 
        * In general, cross-sectional studies are meant to be representative, which means that every member of the target popu- lation has an equal chance of participatin
    * longitudinal study, which observes a group repeatedly over a period of time
* **population**
    * surveys draw conclusions about a population
    * The people who participate in a survey are called **respondents**; a group of respondents is called a **cohort**
    
* **oversampling**
    * e.g. deliberately recruit three groups—Hispanics, African-Americans and teenagers— at rates higher than their representation in the U.S. population. The reason for oversampling is to make sure that the number of respondents in each of these groups is large enough to draw valid statistical inferences.
    * the drawback of oversampling is that it is not as easy to draw conclusions about the general population based on statistics from the survey. 

# Database Terms
* **record**: information about one respondent
* **fields**: variables that make up a record
* **table**: a collection of records

# data file
* 2002FemPreg.dct is a Stata dictionary file.
    ```
    infile dictionary {
        _column(1)  str12  caseid    %12s  "RESPONDENT ID NUMBER"
        _column(13) byte   pregordr   %2f  "PREGNANCY ORDER (NUMBER)"
    }
    ```
    This dictionary describes two variables: caseid is a 12-character string that represents the respondent ID; pregorder is a one-byte integer that indicates which pregnancy this record describes for this respondent.

* thinkstats2.py includes functions that read the Stata dictionary and the NSFG data file

* nsfg.py uses some functions from thinkstats2.py
    ```
    def ReadFemPreg(dct_file='2002FemPreg.dct',
                dat_file='2002FemPreg.dat.gz'):
        dct = thinkstats2.ReadStataDct(dct_file)
        df = dct.ReadFixedWidth(dat_file, compression='gzip')
        CleanFemPreg(df)
        return df
    ```

# DataFrame, Series, elements
* A DataFrame contains a row for each record, in this case one row per pregnancy, and a column for each variable
* a DataFrame also contains the variable names and their types, and it provides methods for accessing and modifying the data.
* to access a column from a DataFrame, use the column name as a key 
    ```
    >>> pregordr = df['pregordr']
    >>> type(pregorder)
    ```
    of use dot notation 
    ```
    >>> pregordr = df.pregordr
    ```
    the result is a **Series**, yet another pandas data structure. A Series is like a Python list with some additional features. When you print a Series, you get the indices and the corresponding values.
* access the **elements** of a Series using integer indices and slices:
    ```
    >>> pregordr[0]
    1
    >>> pregordr[2:5] 
    2   1
    3   2
    4   3
    Name: pregordr, dtype: int64
    ```

# Transformation 
* **data cleaning**
* nsfg.py includes CleanFemPreg, a function that cleans the variables:
    ```
    def CleanFemPreg(df):
        df.agepreg /= 100.0
        na_vals = [97, 98, 99]
        df.birthwgt_lb.replace(na_vals, np.nan, inplace=True)
        df.birthwgt_oz.replace(na_vals, np.nan, inplace=True)
        df['totalwgt_lb'] = df.birthwgt_lb + df.birthwgt_oz / 16.0
    ```

## statistical significance
Even when an **apparent effect** is derived from some data, there's still no guarantee that the effect is statistically significant.
    * need to see other **summary statistics**, e.g. with a difference in  means, what about median and variance
    * is it possible that the difference occurred by chance?
    * Is it possible that the apparent effect is due to selection bias or some other error in the experimental setup? If so, then we might conclude that the effect is an **artifact**; that is, something we created (by accident) rather than found.