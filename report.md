# Group Assignment 1.7: I'm BLUE dabadidabada

*[CEGM1000 MUDE](http://mude.citg.tudelft.nl/)*

*Written by: `Sandra Verhagen, Lina Hagenah`*

*Due: Friday, October 17, 2025.*


## Part 1

**1. Give a short explanation about the data and the models we created. Include brief statements about the data and the differences between the two datasets. (1 pt)**
_Your answer should only be a few sentences long, and be sure to use quantitative information! You do not need to reproduce the model, but at least specify model parameters (physical meaning), observation types, redundancy, etc. You can use bullet lists to summarize and state interesting information._

% solution_start
`Two data sets were used. We had heights based on InSAR and GNSS observations (both satellite observations of the ground surface). InSAR- and GNSS-derived heights were used as observations, and for each the functional model was set up.

InSAR has 53 observations and GNSS 365. There are 3 unknowns, so redundancy is 50 and 362
The standard deviation of each InSAR and GNSS measurement is assumed to be 2 mm and 15 mm, respectively.

The model has three parameters, each of which are linear with respect to the computed displacement of the ground surface:

- initial displacement, $d_0$ m (or mm if you converted the observations to mm as well)

- rate of displacement as a function of time, $v$ m/day (or mm/day)

- amplitude of seasonal (annual) variations (m or mm)`


$$

d = d_0 + vt + A\sin(\frac{2\pi t}{365} - \phi),

$$

Note in particular the differences between each term: $d_0$ in independent of time, the other terms are dependent on time.

% solution_end

% solution_start

- 0.25 points for redundancies (50 for InSAR and 362 for GNSS)
- 0.5 for description of model parameters and observations (-0.2 if they forget units)
- 0.25 for mentioning differences: number observations, precision

% solution_end

## Part 2

**2. Assess the precision (include values!) and significance of the estimated parameters. (2 pt)**
_To include in your answer: What information is contained in the covariance matrix? How to interpret the values (given the physical meaning of the parameters)?_ 

% solution_start

The covariance matrix $\Sigma_Y$ contains information on the quality of the observations, where an entry on the diagonal represents the variance of one observation at a particular epoch. If there is an indication that for instance the quality for a particular time interval differs, different $\sigma$ values can be put in the stochastic model for these epochs.

The off-diagonal in the matrix represents the covariance between observations or estimated values. A zero value on the off-diagonal indicates zero correlation.

The dimension of the covariance matrix of Y is 53x53 for InSAR and 365x365 for GNSS.

The standard deviations of the estimated parameters are equal to the square root of the diagonal elements of the covariance matrix of $\hat{x}$. Compared with the estimated values, the standard deviations seem quite small, meaning on the one hand that the uncertainty due to data quality is quite small and also that the estimated values are significant.

The off-diagonal elements show the covariances between the estimated parameters, which are non-zeros since the estimates are all computed as function of the same vector of observations and the same model.

The standard deviation for the GNSS-estimated initial height is 1.574 mm

The standard deviation for the GNSS-estimated velocity is 0.007 mm/day

The standard deviation for the GNSS-estimated seasonal amplitude is 0.001 m

The standard deviation for the InSAR-estimated initial height is 1.36 mm

The standard deviation for the InSAR-estimated velocity is 0.006 mm/day

The standard deviation for the InSAR-estimated seasonal amplitude is 0.001 m`
% solution_end

% solution_start

- 1 point for discussing info in covariance matrix and interpretation - should at least mention variance/standard deviations on diagonal, covariance/correlations, and that it gives information about precision/quality/uncertainty (-0.25 per missing item)
- 0.5 points for presenting the correct standard deviations or variances (-0.2 if incorrect but due to small coding error, -0.3 if they mix up standard deviations and variances)
- 0.5 points for discussing the significance (standard deviation in comparison to estimated values) stating that estimated values are relatively large compared to standard deviations

% solution_end

## Part 3

**3. Based on an analysis of the fitted model and residuals and their confidence intervals: do you think the fitted model is correct? (4 pt)**
*To include in your report and answer:*

- *One figure with observations, fitted model and confidence intervals of fitted model ($\hat{y}$)*
- *One figure to support your answer to the next question about distribution of residuals*
- *Is the distribution of the residuals as expected? Why or why not?*
- *What information do the confidence intervals give you?*
- *Why are so many observations outside the confidence interval of the fitted model ($\hat{y}$)?*


% solution_start

The mean value and standard deviation of the InSAR residuals is 0.0 m and 0.016 m.

The mean value and standard deviation of the GNSS residuals is 0.0 m and 0.021 m

The mean is thus close to zero, as it should, which may suggest a good fit. On the other hand, the residual plots clearly show a systematic effect (pattern): the residuals are not 'randomly' fluctuaring around zero, and also the histogram and Q-Q plot show that the residuals are not normally distributed as expected. This indicates that the model is generally not good, and misses some important characteristics in the data. Perhaps we should consider adding a bit of complexity (next week!).

Confidence intervals are a useful way to report uncertainty and are based on an assumed theoretical distribution around a quantity of interest; in this case we assume a Normal distribution about each model prediction, $\hat{y}_i$, as well as each residual, $y_i-\hat{y}_i$. Using the first and second moments (i.e. mean and std. dev.), we can create confidence intervals based on a specific critical value determined by the confidence level $\alpha$. When our sample size is large enough and our assumptions that our random variable is distributed randomly are reasonably correct, we will see that the fraction of data points in our CI is (almost) equal to $1-\alpha$.

The confidence interval is for the fitted model, based on all observations; it represents the uncertainty in the estimated $\hat{y}_i$ not of the observed $y_i$
% solution_end

% solution_start

- 1 point for clear and correct figures of confidence intervals and residuals (with confidence intervals/histogram/q-q plot or similar) (-0.25 if incorrect due to small error in code)
- 0.5 points for clarity of plots, incl. axis labels, legend (-0.2 in case of small issue)
- 1 point for mentioning that distibution should be normal with zero-mean. Indeed the mean is zero, but residual plot/histogram / Q-Q plot shows deviations. (-0.5 if answer is not completely correct, but some of this is contained in the answer)
- 0.5 point for explaining the confidence intervals (-0.25 if confidence level / alpha not mentioned)
- 1 point for explaining that confidence interval is for the fitted model, not for the individual observations (-0.5 if somewhat correct)

% solution_end

## Part 4

**4. Compare the results you found for the InSAR observations and the GNSS observations. Discuss/explain the differences, taking into account the different properties of the datasets. Be quantitative. (1 pt)**

% solution_start
Estimated parameters, hence fitted model, is different. Factors that have an impact:

- Precision of the observations

- Number of observations

Although the quality of the GNSS data is lower compared to InSAR (15 vs 2 mm), the precision of the estimated parameters is similar. Here we see the effect of 'more' data points: the much lower precision of the observations is somewhat compensated by the much higher number of observations.

Also, when reviewing the residuals for both datasets, it seems that the model that we use is maybe too simple since we miss part of the signal.
% solution_end

% solution_start

- 0.5 points for mentioning both factors (precision of observations, number of observations)
- 0.5 points for explaining that precision of estimated parameters with GNSS or InsAR is similar, even though GNSS is less precise 

% solution_end

## Part 5

**5. What would you advise the authorities in terms of long-term monitoring strategy: use GNSS, InSAR, or both? Justify your choice based on the results previous questions. (1 pt)** *To include: how would you change your processing strategy when using both GNSS and InSAR data? (you need to answer this question, even if you recommend to use only of the two)*

% solution_start
GNSS has advantage of higher temporal resolution (more frequent observations), but this seems not to be crucial here since the fluctuations are not on short time scales. Disadvantage is the lower precision. Therefore it seems that InSAR could be sufficient for this monitoring task.

The same reasoning can also be used to conclude that it doesn’t really matter.

An advantage of using both InSAR and GNSS is that you have the advantage of more observations and high temporal resolution.

If using both observations together , we would estimate the unknown parameters using the GNSS and InSAR observations at the same time (in one observation vector), which would result in 365+53 observations, and hence a redundancy of 415. With BLUE we would of course apply proper weights, taking into account the different precisions.
% solution_end

% solution_start

- 0.5 points for mentioning advantage of temporal resolution (or more frequent observations, etc.) of GNSS to detect changes at smaller time scales
OR
- 0.5 points for mentioning in this case InSAR's temporal resolution is sufficient, esp. in combination with higher precision
(both options are correct)

PLUS
- 0.5 points for explaining that both observation types should be used together to estimate the model parameters, providing much higher redundancy (-0.2 if not completely correct)

% solution_end


> By Sandra Verhagen, Delft University of Technology. CC BY 4.0, more info [on the Credits page of Workbook](https://mude.citg.tudelft.nl/workbook-2025/credits.html).