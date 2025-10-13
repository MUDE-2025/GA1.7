# Group Assignment 1.7: Modelling surface uplift due to groundwater variations

*[CEGM1000 MUDE](http://mude.citg.tudelft.nl/)*

*Written by: `Sandra Verhagen, Lina Hagenah`*

*Due: Friday, October 17, 2025.*

## Part 1

**1.1 1. Give a short explanation about the data and the models we created. Include brief statements about the data and the differences between the two datasets. (1 pt)**
_Your answer should only be a few sentences long, and be sure to use quantitative information! You do not need to reproduce the model, but at least specify model parameters (physical meaning), observation types, reduncdancy, etc. You can use bullet lists to summarize and state interesting information._

% solution_start
`Two data sets were used. We had heights based on InSAR and GNSS observations (both satellite observations of the ground surface). InSAR- and GNSS-derived heights were used as observations, and for each the functional model was set up.

InSAR has 53 observations and GNSS 365. The standard deviation of each InSAR and GNSS measurement is assumed to be 2 mm and 15 mm, respectively.

The model has three parameters, each of which are linear with respect to the computed displacement of the ground surface:

- initial displacement, $d_0$ m (or mm if you converted the observations to mm as well)

- rate of displacement as a function of time, $v$ m/day (or mm/day)

- amplitude of seasonal (annual) variations (m or mm)`


$$

d = d_0 + vt + A\sin(\frac{2\pi t}{365} - \phi),

$$

Note in particular the differences between each term: $d_0$ in independent of time, the other terms are dependent on time.

To construct the model we need a parameter value for each observation (GNSS/InSAR); this is problematic as we only have 25 groundwater measurements.

% solution_end

## Part 2

**2.1 .	Assess the precision and significance of the estimated parameters. (2 pt)**
_To include in your answer: What information is contained in the covariance matrix? How to interpret the values (given the physical meaning of the parameters)?_ 

% solution_start

The covariance matrix $\Sigma_Y$ contains information on the quality of the observations, where an entry on the diagonal represents the variance of one observation at a particular epoch. If there is an indication that for instance the quality for a particular time interval differs, different $\sigma$ values can be put in the stochastic model for these epochs.

The off-diagonal in the matrix represents the correlation between observations or estimated values. A zero value on the off-diagonal indicates zero correlation.

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

## Part 3

**3. Based on an analysis of the fitted model and residuals and their confidence intervals: do you think the fitted model is correct? (3 pt)**
*To include in your answer:*

- *Is the distribution of the residuals as expected? Why or why not?*

- *What information do the confidence intervals give you?*
- *Why are so many observations outside the confidence interval of the fitted model (y_hat)?*


% solution_start

The mean value and standard deviation of the InSAR residuals is 0.0 m and 0.021 m.

The mean value and standard deviation of the GNSS residuals is 0.0 m and 0.016 m

The mean is thus close to zero, as it should, which may suggest a good fit. On the other hand, the residual plots clearly show a systematic effect (pattern): the residuals are not 'randomly' fluctuaring around zero, and also the histogram and Q-Q plot show that the residuals are not normally distributed as expected. This indicates that the model is generally not good, and misses some important characteristics in the data. Perhaps we should consider adding a bit of complexity (next week!).

Confidence intervals are a useful way to report uncertainty and are based on an assumed theoretical distribution around a quantity of interest; in this case we assume a Normal distribution about each model prediction, $\hat{y}_i$, as well as each residual, $y_i-\hat{y}_i$. Using the first and second moments (i.e. mean and std. dev.), we can create confidence intervals based on a specific critical value determined by the confidence level $\alpha$. When our sample size is large enough and our assumptions that our random variable is distributed randomly are reasonably correct, we will see that the fraction of data points in our CI is (almost) equal to $1-\alpha$.

The confidence interval is for the fitted model, based on all observations; it represents the uncertainty in the estimated $\hat{y}_i$ not of the observed $y_i$
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

## Part 5

**5. What would you advise the authorities in terms of long-term monitoring strategy: use GNSS, InSAR, or both? Justify your choice based on the results previous questions. (1 pt)** *To include: how would you change your processing strategy when using both GNSS and InSAR data? (you need to answer this question, even if you recommend to use only of the two)*

% solution_start
GNSS has advantage of higher temporal resolution (more frequent observations), but this seems not to be crucial here since the fluctuations are not on short time scales. Disadvantage is the lower precision. Therefore it seems that InSAR could be sufficient for this monitoring task.

The same reasoning can also be used to conclude that it doesn’t really matter.

An advantage of using both InSAR and GNSS is that you have the advantage of more observations and high temporal resolution.

If using both observations together , we would estimate the unknown parameters using the GNSS and InSAR observations at the same time (in one observation vector), which would result in 365+53 observations. With BLUE we would of course apply proper weights, taking into account the different precisions.
% solution_end


> By Sandra Verhagen, Delft University of Technology. CC BY 4.0, more info [on the Credits page of Workbook](https://mude.citg.tudelft.nl/workbook-2025/credits.html).

*Copyright 2025 MUDE, TU Delft. This work is licensed under CC BY 4.0 License.*