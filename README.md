# Calculate-Hurst-Index  
The Hurst exponent is used as a measure of long-term memory of time series. Detailed explanation can be found [here](https://en.wikipedia.org/wiki/Hurst_exponent). The mathematical  expression  is  $$\mathbb{E} \left [ \frac{R(n)}{S(n)} \right ]=C n^H  \text{  as } n \to \infty$$
where
* $R(n)$ is the range of the first <math>n</math> cumulative deviations from the mean
* $S(n)$ is the series (sum) of the first n standard deviation
* $\mathbb{E} [x]$ is the expected value
* $n$ is the time span of the observation (number of data points in a time series)
* $C$ is a constant.
