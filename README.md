# econ3916-lab14-ols-diagnostics

# OLS Diagnostics: When the Standard Error Is Lying

## Objective

I examined how heteroskedasticity, model misspecification, and influential observations affect OLS estimates and standard errors, using simulated data and California Housing data.

## Methodology

- I simulated errors whose spread increases with x and compared classical and HC3 robust standard errors for the same regression.
- I ran 400 simulated samples and compared confidence interval coverage with the nominal 95% rate, using Monte Carlo standard errors to assess the gaps.
- I examined four residual plots alongside Breusch-Pagan and Jarque-Bera tests to identify changing variance, missing curvature, and an extreme residual.
- I calculated leverage, standardized residuals, and Cook’s distance, then compared the regression with and without the most influential observation.
- I regressed California district house values on median income, house age, rooms per household, and people per household, comparing classical and HC3 standard errors.
- I wrote hc3_se() to return the HC3 standard error for a selected coefficient and compared its results with and without districts at the value ceiling.

## Key Findings

### Heteroskedasticity and Interval Coverage

I obtained the same slope estimate of 2.0147 with both methods, but the classical standard error was 0.0264 and the HC3 standard error was 0.0290. Changing the standard error method changed the uncertainty around the estimate without changing the estimate itself.

Across 400 simulated samples, the classical 95% interval covered the true slope 91.8% of the time, compared with 93.5% for HC3. The Monte Carlo standard errors were 1.4% and 1.2%, respectively. I found that HC3 coverage was closer to the nominal 95%, although neither method reached it in this simulation.

### Residual Diagnostics and Influence

I found that the residual plots revealed different problems that individual tests could miss. In particular, the missing-curvature model passed Breusch-Pagan despite a clear curved pattern, showing why I need to read the plots alongside the test results.

After deleting one observation out of 600, I found that the slope moved 0.58 of its original standard error, while the standard error fell by 33%. The observation affected the estimated uncertainty much more than the slope.

### California Housing

I estimated an AveRooms coefficient of −0.0273, with an HC3 standard error of 0.0121, which was 5.02 times the classical standard error. The residual plot showed changing spread and a diagonal edge caused by the value ceiling.

My function returned an HC3 standard error of 0.0121 with all districts and 0.0082 without the 965 districts at the 5.0 ceiling. I would disclose that ceiling as a limitation, since the recorded values do not show how far those districts exceeded it. I would not remove valid observations just to obtain a smaller standard error.
