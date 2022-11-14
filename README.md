# Calculate-Hurst-Index  
The Hurst exponent is used as a measure of long-term memory of time series. Detailed explanation can be found [here](https://en.wikipedia.org/wiki/Hurst_exponent). The mathematical  expression  is  $$\mathbb{E} \left [ \frac{R(n)}{S(n)} \right ]=C n^H  \text{  as } n \to \infty$$
where
* $R(n)$ is the range of the first <math>n</math> cumulative deviations from the mean
* $S(n)$ is the series (sum) of the first n standard deviation
* $\mathbb{E} [x]$ is the expected value
* $n$ is the time span of the observation (number of data points in a time series)
* $C$ is a constant.  


A value between $0.5-1$ indicates a positive autocorrelation-'high' followed by  'high', 'low' followed  by 'low'. $0-0.5$ switching between  'high' and 'low'.  $0.5$  no correelation. The python code is as  follows
 
 ```{python}
 def hurst(df, max_days_one_period):
    RSlist = []
    nList = range(30,max_days_one_period)
    for j in nList:
        num_of_rets = df.shape[0]
        n = j
        ret = df['rets'].tolist()
        periods = []
        for i in range(num_of_rets//n):
            periods.append([ret[i*n : (i+1)*n]])

        L = []
        for period in periods:
            m = np.mean(period)
            Xta = pd.Series(map(lambda x: x-m, period)).cumsum()
            Xta = Xta.tolist()[0]
            Ra = max(Xta) - min(Xta)
            Sa = np.std(period)
            rs = Ra / Sa
            L.append(rs)
        RS = np.mean(L)
        RSlist.append(RS)

    log_RSlist = np.log(RSlist)
    log_nList = np.log(nList)
    x = log_nList.reshape(-1,1)
    fit = LinearRegression().fit(x, log_RSlist)
    return fit.coef_[0]
 ```
