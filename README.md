# VaR-Simulation

In the financial industry, Value-at-risk (VaR) is a new standard measurement of risk. VaR offers asset managers a better understanding of risk comparing to the simple standard deviation measurement. It tackles the weakness of standard deviations by considering only the downside risk rather than both tails of the distribution. Actual VaR calculation is straight-forward, it is the minimum loss that could occur if an unlikely event happens. However, to effectively manage risk, one should estimate the future VaR rather than using the historical VaR. The three common methods to estimate VaR are Non-Parametric, Parametric (Historical Simulation) and the Monte Carlo Simulation. This research paper introduces a new approach to measure VaR using the replicated portfolio. The replicated portfolio is built using parameters from the regression of the portfolio returns and the performance of 11 equity sectors. The estimated VaRs are then compared to the actual VaR. All four approaches usually yield smaller values than the actual VaR. The parametric and the Monte Carlo Simulation methods yield close estimations. The decomposition method fails to capture all the risks of the actual portfolio; hence, it also fails to deliver a fair estimation. While other methods are only sensitive to the parameters of the distribution (mean and standard deviations), the decomposition method can detect both changes in the shape of the distribution and the parameters.

There are 3 popular methods to estimate VaR: parametric (Historical Simulation), non-parametric, and Monte-Carlo Simulation. This paper also introduces a new approach to measure VaR – decomposition method.
1.	Parametric VaR
The earliest version is parametric VaR. One of the famous parametric VaR method is the RiskMetrics which was introduced by JP.Morgan Chase in 1994 (Longerstaey, 1996). Since then, RiskMetrics became the benchmark for measuring risk and providing clients with a way to effectively manage risks. RiskMetrics calculation is based on the Variance-Covariance method under the normality assumption (Investopedia).
Let P_i be the initial value of the portfolio, μ be the mean of the series, σ be the standard deviation of the return series, and Z be the Z-score related to the confident level under the normality assumption. The Value at Risk of the portfolio’s value under the RiskMetrics framework is:
VaR=P_i*α

Where α=normal.ppf(1-confidence) : the probability density function at (100%-confidence level) of standard normal distribution.
This VaR method was applied widely in both academic fields and businesses. Alexander used Mean-VaR to replace the traditional Mean-Variance of Markowitz to construct the optimal portfolio (Alexander, 2002). The VaR can implement the weakness of variance (similar to standard deviation) as variance considers both sides of the stock movement, while VaR only considers the down-side risks. The variance does not consider the direction of the movement, hence, the optimized portfolio might prevent investors from both gains and losses. On other hand, optimize the portfolio using mean-VaR will only protect investors against the down-side risk (Alexander, 2002).

2. Non- parametric.

Non-parametric VaR is the actual value at risk without the normality assumption. We can calculate VaR directly using left-tail measures (Guojunn Wu, 2002). Given a time-series of assets return: ${r_t }_(t=1)^n$ , VaR is the value such that:
$Pr(r_t≤|VAR_t ||I_(t-1))=1-c$
Where I_(t-1) : information available at time $t$ - 1, c: confident level

3. Monte-Carlo Simulation
Monte-Carlo simulation can be applied differently. Monte Carlo simulation can overcome the drawback of parametric approach since it is able to generate different types of distributions without limited to only normal distribution. Using this approach, one will generate a set of future stock prices, then use it to calculate the set of stock return. The VaR is the α quantile from this distribution. In this paper, we will implement Monte-Carlo Simulation using Python and log-normal distribution. 
Let S_0 be the initial price of the stocks, n be the sample size, c be the confidence level,#{S_i }_(i=1)^n# be the set of future stock paths, ${R_i }_(i=1)^n=({S_i }_(i=1)^n-S_0)/S_0)$ be the set of stock’s return
$P(X≤|VaR|)=α=1-c$
$VAR_α (X)=F_y^(-1) (1-α)$

Given the above framework, there are many models can be used to generate the future stock price such as: the Black-Scholes model, the Herton Model. In this paper, we use the NumPy package in Python to generate the log-normal distribution for the future stocks price directly.

4. Decomposition Approach
An alternative approach to analyze VaR using regression analysis. We decompose the portfolio returns to the performance of 11 equity sectors. The replicated portfolio is formed from the corresponding parameters. The VaR of the actual portfolio can be estimated through the replicated portfolio.

Let y is a time-series of returns of a portfolio y={r_t }_(t=1)^n:
Let $X ⃗={X_i }_(i=1)^11$ are the time-series returns of 11 sectors.
We can decompose the portfolio performances using the multiple regression:
$y=∑_(i=1)^11 α_i  X_i+\ϵ$
The coefficients of the regression are: α ⃗={α_(i=1)^11}
The time-series returns of the replicate portfolio y ̂=X ⃗•α ⃗
The VaR for the replicate portfolio can be estimated using parameters: μ_y ̂  and σ_y ̂  given timeframe and level of confidence: c. We can generate the random numbers that follow log-normal distribution using Monte Carlo Simulation. The VaR is estimated such that:
P(X≤|VaR|)=α=1-c
VAR_α (X)=F_y^(-1) (



To view result please visit.

https://app.powerbi.com/view?r=eyJrIjoiMjU3NjYzY2UtYzM1MC00YjhmLThjNGMtNGJiN2I1MjM1MGVmIiwidCI6ImQ0ZmYwMTNjLTYyYjctNDE2Ny05MjRmLTViZDkzZTgyMDJkMyIsImMiOjN9
