### Means and average
* the **mean** of a sample is the summary statistic computed with the mean formula
* an **average** is one of many summary statistics you might choose to describe the **typical value** or the central tendency of a sample

* example to help differentiate means from average
    * Suppose I grow several varieties in my garden, and one day I harvest three decorative pumpkins that are 1 pound each, two pie pumpkins that are 3 pounds each, and one Atlantic Gi- ant® pumpkin that weighs 591 pounds. The mean of this sample is 100 pounds, but if I told you “The average pumpkin in my garden is 100 pounds,” that would be wrong, or at least misleading.
    * In this example, there is **no meaningful average because there is no typical pumpkin**.

### Variance
If there is **no single number** that summarizes pumpkin weights, we can do a little better with two numbers: **mean and variance**.

* mean is intended to describe the central tendency
* variance is intended to describe the spread
    * it is the (mean (squared deviation)), denoted σ2

* The square root of variance, σ, is called the **standard deviation**.

### Distributions -- an alternative to summary stats
Summary statistics are concise, but dangerous,because they obscure the data. An alternative is to look at the distribution of the data, which describes how often each value appears.

* a common representation: **histogram**, a graph that shows the frequency **or** probability of each value
    * frequency --  the number of times a value appears in a dataset
    * probability -- frequency expressed as a fraction of the sample size n

* Python 
    * an efficient way to compute frequencies is with a dictionary
    ```
    # given a sequence of values t
    hist = {}
    for x in t: 
    hist[x] = hist.get(x, 0) + 1   #get(key[, default]) return the value for key if key is in the dictionary, else default.
    # The result is a dictionary that maps from values to frequencies
    ```

    * To get from frequencies to probabilities, we divide through by n, which is called **normalization**:
    ```
    n = float(len(t))
    pmf = {}
    for x, freq in hist.items(): # items() returns a new view of the dictionary’s items ((key, value) pairs)
        pmf[x] = freq / n
    ```
    The normalized histogram is called a **PMF**, which stands for “probability mass function”; that is, it’s a function that maps from values to probabilities

