---
title: "Reading Note: Wind Speed and Large Fire Duration in the Western US"
parent: Literature
nav_order: 3
---
**Date:** 2026-05-19
# Wang et al. (2025) — The Role of Wind Speed in Prolonging Large Fire Durations in the Western US

**Paper:** Wang, S. S.-C., Leung, L. R., & Qian, Y. (2025). *The Role of Wind Speed in Prolonging Large Fire Durations in the Western US*. Geophysical Research Letters, 52, e2024GL112539.  
**Topic:** wildfire duration, wind speed, western US fire trends, fire meteorology, multiple linear regression  
**My keywords:** large fire duration, uncontrolled fire duration, wind speed, VPD, fuel moisture, LAI, western US wildfires, fire-weather feedback

---

## 1. Research Question and Overall Design

This paper asks why large wildfires in the western United States have been lasting longer over recent decades. Specifically, it examines trends in **large fire duration** from 1992 to 2020 and identifies which meteorological, vegetation, and topographical variables best explain the interannual variability and long-term trend.

The study focuses on two major fire seasons:

- **JJA:** June–July–August
- **SON:** September–October–November

The authors define large fires as fires with burned area greater than **400 ha** in the western US, defined as regions west of **103°W**. Fire duration is calculated as the number of days between the discovery date and containment date in the fire record. The authors call this **uncontrolled large fire duration**, because it reflects the time before full containment rather than the physical burning lifetime alone.

The overall design is statistical. The authors first construct annual time series of mean large fire duration for JJA and SON. They then use stepwise multiple linear regression models to identify which predictors best explain the trends and variability of large fire duration.

The central conclusion is that **maximum daily wind speed during large fires** is the most important predictor in the regression models for both seasons. This wording is important: the paper mainly establishes statistical importance within the model, rather than a fully causal relationship.

---

## 2. Data Products, Variables, Time Range, and Spatial Range

### Time Range

The analysis covers **1992–2020**.

### Spatial Range

The spatial domain is the **western United States**, defined as regions west of **103°W**.

### Fire Data

The authors use the **Fire Program Analysis Fire-Occurrence Database (FPA-FOD)**. This database provides fire discovery dates, containment dates, burned area, fire cause, and discovery location.

The key fire variable is:

\[
\text{Fire duration} = \text{containment date} - \text{discovery date}
\]

The study focuses on fires larger than **400 ha**.

### Meteorological Data

The main meteorological predictors come from **gridMET**, at 4-km spatial resolution.

Variables include:

- daily maximum surface temperature,
- daily mean vapor pressure deficit (VPD),
- daily accumulated precipitation,
- daily mean surface wind speed,
- 1000-hr fuel moisture,
- wind speed statistics during the fire period,
- VPD statistics during the fire period,
- meteorological conditions around the discovery date,
- antecedent climate conditions before the fire season.

For each fire, the authors extract predictor values at the grid point closest to the fire discovery location, because the fire database does not provide full fire-spread trajectories.

### Vegetation Data

The authors use monthly **leaf area index (LAI)** from the NOAA Climate Data Record of AVHRR Surface Reflectance. LAI is used as an indicator of vegetation amount and fuel availability.

### Topographical Data

Topographical variables come from **USGS GTOPO30**, including:

- elevation,
- slope,
- terrain variability within the local grid.

### Predictor Aggregation

For each year and season, the authors average fire duration and predictor variables across all large fires in the western US. Therefore, the regression is based on annual seasonal mean values, not individual fire-level samples.

---

## 3. Core Logic of the Method

The target variable is annual mean uncontrolled large fire duration for each season.

The authors use stepwise multiple linear regression:

\[
y = \beta_0 + \sum_{k=1}^{j} \beta_k x_k
\]

where:

- \(y\) is the annual mean large fire duration,
- \(x_k\) are selected meteorological, vegetation, and topographical predictors,
- \(\beta_k\) are regression coefficients.

All predictors are standardized by subtracting the 1992–2020 mean and dividing by the standard deviation. This makes coefficient magnitudes more comparable across predictors.

The model selection uses **Akaike Information Criterion (AIC)**. The best models are selected from the top five models with the lowest AIC values. The authors also check multicollinearity using variance inflation factor and require VIF < 5.

They use leave-one-year-out cross-validation to reduce overfitting concerns. The cross-validated model performance is strong:

- JJA: \(R^2 = 0.94\)
- SON: \(R^2 = 0.82\)

The key modeling result is that maximum wind speed during large fires is selected in both seasonal models and has the largest standardized coefficient. This means it has the strongest statistical relationship with annual mean large fire duration among the selected predictors.

---

## 4. Main Results

### 4.1 Large Fire Duration Has Increased

Large fire duration increased significantly from 1992 to 2020:

- **JJA:** +0.76 days per year
- **SON:** +0.55 days per year

This means that large fires have been taking longer to contain in both summer and fall.

### 4.2 Maximum Wind Speed During Fires Is the Most Important Predictor

The stepwise MLR models identify **maximum daily wind speed during large fires** as the strongest predictor of large fire duration in both seasons.

For JJA, the selected predictors include:

- maximum wind speed during large fires,
- seasonal mean LAI,
- maximum VPD during fires,
- total precipitation from March to May,
- mean VPD in the prior winter,
- maximum 1000-hr fuel moisture within ±7 days of discovery.

For SON, the selected predictors include:

- maximum wind speed during large fires,
- maximum 1000-hr fuel moisture within ±7 days of discovery,
- mean elevation,
- mean VPD during large fires.

The wind coefficient is larger than the coefficients of other variables, suggesting that wind speed has the largest explanatory power in the regression framework.

### 4.3 Maximum Wind Speed During Fires Has Increased

Average maximum daily wind speed during large fires increased significantly:

- **JJA:** +0.031 m s\(^{-1}\) yr\(^{-1}\)
- **SON:** +0.063 m s\(^{-1}\) yr\(^{-1}\)

The standard deviation of daily wind speed during large fires also increased:

- **JJA:** +0.0045 m s\(^{-1}\) yr\(^{-1}\)
- **SON:** +0.0103 m s\(^{-1}\) yr\(^{-1}\)

This suggests that large fires are increasingly associated with stronger wind extremes and greater wind variability.

### 4.4 Background Fire-Season Winds Do Not Show Comparable Trends

The authors compare wind trends during large fires with wind trends across all fire-season days.

They find that average background fire-season winds do not show comparable increases. In JJA, background wind speed generally decreases. In SON, background wind speed increases slightly, but the trend is weaker than the increase in maximum wind speed during large fires.

This contrast suggests that the increasing maximum wind speeds during large fires cannot be explained simply by a broad increase in background wind speed.

### 4.5 Possible Fire-Wind Feedback

The authors hypothesize a possible bidirectional relationship:

1. Strong wind can increase fire spread and make fires harder to contain.
2. Larger and longer-lasting fires may themselves generate stronger local winds through fire-induced heat and circulation.
3. These fire-induced winds may then further prolong fire duration.

This is an important hypothesis, but the paper does not fully prove it. The authors explicitly state that the mechanisms behind increasing maximum wind speeds during large fires remain unclear and require future modeling studies.

---

## 5. Robustness Checks and Uncertainty Analysis

### Alternative Wind Dataset

gridMET wind is interpolated from coarser NLDAS-2 data, so wind uncertainty is a concern. To test robustness, the authors repeat part of the analysis using a 6-km WRF simulation driven by NARR.

The WRF wind speed shows a similarly strong correlation with fire duration, especially in JJA. However, the SON result is less robust: in the WRF-based regression, mean VPD during fires becomes the dominant predictor. This suggests that the wind-duration relationship is more robust in summer than in fall.

### Cross-Validation

The authors use leave-one-year-out cross-validation. The models still perform well, with high cross-validated \(R^2\), suggesting that the regression models are not simply overfitting the full time series.

### Multicollinearity Check

They require the variance inflation factor of each predictor to be less than 5. This reduces the risk that selected predictors only appear important because of strong correlations among predictors.

### Extreme Wind Events

The supporting information tests models using the frequency of extreme wind events, defined by daily wind speed exceeding the 95th percentile of fire-season winds. These models perform similarly to models using maximum wind speed, reinforcing the importance of wind extremes during fires.

### Background Wind Analysis

The authors compare trends in wind during fires with trends in all fire-season days. Since background winds do not show comparable increases, the authors argue that increasing maximum wind during large fires may not be driven by broad fire-season wind trends.

### Important Uncertainties

The study has several important uncertainties:

1. **Fire duration uncertainty:** Discovery and containment dates in FPA-FOD may contain reporting inconsistencies across agencies.
2. **Containment is not purely physical:** Fire duration can be affected by firefighting resources, management strategy, accessibility, and prioritization.
3. **Fire location simplification:** Predictors are extracted at the discovery location, but large fires spread over large areas.
4. **Wind data uncertainty:** Surface wind is difficult to represent, especially in complex terrain and near active fires.
5. **Causality is not fully established:** The study identifies wind speed as the most important predictor, but this does not prove that increasing wind speed alone causes longer fire duration.

---

## 6. Main Message of Each Figure and Table

### Figure 1: Observed and Predicted Large Fire Duration

Figure 1 shows observed and MLR-predicted annual mean large fire duration for JJA and SON. Both seasons show increasing trends from 1992 to 2020. The MLR model captures much of the interannual variability.

My takeaway: large fire duration has increased substantially, and the selected predictors reproduce the observed variability reasonably well.

### Figure 2: Trends in Maximum Wind Speed and VPD During Large Fires

Figure 2 shows that maximum wind speed during large fires increases significantly in both JJA and SON. In contrast, VPD during large fires does not show a comparable increasing trend.

My takeaway: the increasing fire duration is more closely aligned with increasing maximum wind speed during fires than with increasing VPD during fires.

### Figure 3: Background Fire-Season Wind Trends

Figure 3 examines trends in daily mean, maximum, and standard deviation of wind speed across all fire-season days, not only during large fires.

My takeaway: background fire-season winds do not show the same strong increase as maximum wind speed during large fires. This suggests that the wind changes associated with large fires may be distinct from general seasonal wind trends.

### Table 1: Regression Coefficients

Table 1 shows the selected MLR predictors and their coefficients for JJA and SON. Maximum wind speed during large fires has the largest coefficient in both seasons.

My takeaway: within the standardized regression framework, maximum wind speed is the most important predictor of mean large fire duration.

### Table 2: Wind Trends During Fire Season vs. During Large Fires

Table 2 compares wind trends across all fire-season days and during large fires. Maximum wind speed during large fires increases significantly, while background maximum wind speed does not.

My takeaway: the key trend is not a broad increase in all seasonal winds, but a specific increase in maximum wind speed during large fires.

### Supporting Figure S1: Number of Large Fires

Figure S1 shows the number of large fires used in the analysis for JJA and SON.

My takeaway: the number of large fires varies substantially from year to year, which may affect annual mean duration estimates.

### Supporting Figure S2: Distribution of Large Fire Duration

Figure S2 shows annual distributions of large fire duration.

My takeaway: the increase in mean duration is accompanied by changes in the distribution and more long-duration events in later years.

### Supporting Figures S3 and S4: Correlations Between Fire Duration and Selected Predictors

Figures S3 and S4 show scatter plots between fire duration and the selected MLR variables for JJA and SON.

My takeaway: maximum wind speed has the strongest positive correlation with fire duration in both seasons.

### Supporting Figure S5: WRF vs. gridMET Wind Sensitivity

Figure S5 compares fire duration relationships with maximum wind speed from WRF and gridMET.

My takeaway: the wind-fire duration relationship is robust in JJA but less certain in SON.

### Supporting Figures S6–S8: Wind Variability and Strong Wind Events

These figures examine trends in wind variability and strong wind events.

My takeaway: wind variability during large fires has increased, but strong wind-event trends across the whole fire season do not fully explain the increase during fires.

### Supporting Tables S1–S3: Model Selection and Sensitivity

The SI tables summarize the top AIC-selected models and sensitivity tests using extreme wind event frequency and WRF-derived wind.

My takeaway: wind-related variables repeatedly appear in the best-performing models, but fall-season results are more sensitive to wind data choice.

---

## 7. Limitations, Future Directions, and Connections to My Research

### Limitations

This paper is powerful as a statistical attribution study, but it is not a fully causal study. The phrase “maximum wind speed is the most important predictor” should be read as model-based explanatory importance, not definitive causality.

The use of containment date also means that “fire duration” depends not only on fire behavior but also on human management. Fires may last longer because of weather and fuel conditions, but also because of limited firefighting resources, strategic containment decisions, terrain, or access difficulty.

Another limitation is that meteorological predictors are extracted near the discovery location. Large fires may spread over many kilometers and experience different wind, fuel, and terrain conditions across their lifetime.

The wind analysis is also uncertain because near-surface winds are difficult to represent in gridded products, especially in complex terrain and in the presence of fire-atmosphere feedbacks.

### Future Directions

Future work should use coupled fire-atmosphere models to test whether large fires can generate stronger local winds that then feed back on fire spread and duration. Higher-resolution wind observations and simulations would help separate background synoptic winds, terrain-driven winds, and fire-induced winds.

It would also be useful to combine fire progression data, daily burned area, containment records, and suppression effort data to distinguish physical fire duration from management-driven containment duration.

### Connections to My Research on PyroCb, ACI, and Wildfire

This paper is relevant to my research because it highlights the importance of wind during large fires. PyroCb development depends on fire intensity, heat release, plume dynamics, and environmental wind shear. If maximum wind speed during large fires is increasing, this may affect plume organization, fire spread, and the likelihood of intense convective development.

The paper also raises an important feedback idea: large fires may induce local winds, and those winds may further prolong fire duration. This connects naturally to coupled fire-atmosphere modeling. In my WRF-Chem-SFIRE pyroCb simulations, fire-atmosphere coupling, smoke transport, and vertical injection are central. A similar framework could help test whether fire-induced winds modify plume structure, updraft strength, smoke injection height, and pyroCb development.

For aerosol-cloud interaction research, longer fire duration could also mean longer smoke emission periods and more sustained aerosol loading into fire-driven convective clouds. This may influence cloud droplet activation, latent heating, precipitation formation, and smoke injection into the upper troposphere.

This paper therefore helps frame wildfire duration not only as a fire-management metric, but also as a driver of smoke exposure, aerosol emissions, and potentially pyroCb-relevant plume dynamics.

---

## 8. One-Paragraph Summary

Wang et al. (2025) examine why large wildfire duration has increased in the western United States from 1992 to 2020. Using FPA-FOD fire records, gridMET meteorology, AVHRR LAI, topographic data, and stepwise multiple linear regression, they show that mean uncontrolled large fire duration increased by 0.76 days per year in summer and 0.55 days per year in fall. Among meteorological, vegetation, and topographical predictors, maximum daily wind speed during large fires emerges as the strongest predictor of fire-duration trends and variability. This maximum wind speed also increases significantly during large fires, whereas background fire-season winds do not show comparable increases. The authors therefore suggest that longer large-fire durations may be linked to increasing wind extremes during fires, possibly involving fire-induced local wind feedbacks. However, the study remains mainly statistical: wind speed is identified as an important predictor, not as a fully proven causal driver. The work is relevant to wildfire and pyroCb research because stronger winds can affect fire spread, plume dynamics, smoke emissions, and fire-atmosphere coupling.

---

## 9. Additional Notes and Discussion

### 9.1 What Does “Containment” Mean?

In wildfire management, **containment** means that control lines have been established around a fire such that the fire is not expected to spread beyond those boundaries. Therefore, the fire duration used in this paper is not exactly the physical duration of active combustion. It is closer to **time to containment**:

\[
\text{Uncontrolled fire duration} = \text{containment date} - \text{discovery date}
\]

This definition is useful because it reflects how long a fire remained uncontrolled. However, it also means that the outcome can be affected by human factors, including suppression resources, management strategy, terrain accessibility, risk tolerance, and reporting practices. Therefore, “longer fire duration” should not be interpreted purely as “the fire physically burned for longer under natural conditions.”

### 9.2 What Is Stepwise Multiple Linear Regression?

**Multiple linear regression (MLR)** estimates the relationship between one outcome variable and multiple predictors:

\[
y = \beta_0 + \beta_1 x_1 + \beta_2 x_2 + \cdots + \beta_k x_k
\]

In this paper, \(y\) is annual mean large fire duration, and the predictors include wind speed, vapor pressure deficit, fuel moisture, precipitation, LAI, elevation, and other fire-weather or landscape variables.

**Stepwise MLR** is a variable-selection procedure. Instead of manually choosing one fixed set of predictors, the algorithm searches across different combinations of variables. At each step, it may add, remove, or replace predictors, depending on whether the model-selection criterion improves.

A simple intuition is that stepwise regression asks:

> Does including this variable improve the model enough to justify the additional complexity?

It is not necessarily just “adding one variable at a time in one fixed order.” The result can depend on the candidate variable pool, the selection direction, and the model-selection criterion.

### 9.3 What Is AIC?

**AIC** stands for **Akaike Information Criterion**. It is commonly used for model selection.

A simplified expression is:

\[
\mathrm{AIC} = 2k - 2\ln(\hat{L})
\]

where \(k\) is the number of model parameters and \(\hat{L}\) is the maximum likelihood.

The intuition is:

\[
\text{AIC} = \text{lack of fit} + \text{penalty for complexity}
\]

A lower AIC means the model achieves a better balance between fitting the data and avoiding unnecessary complexity. Adding more predictors usually improves the in-sample fit, but AIC penalizes extra parameters. Therefore, a more complex model is preferred only if the improvement in fit is large enough.

In this paper, AIC is used to select among candidate MLR models. This is a model-selection tool, not a causal-identification tool.

### 9.4 Are Regression Coefficients Treatment Effects?

Not necessarily.

A regression coefficient only becomes a **treatment effect** under a specific causal inference framework. For example, if the model is:

\[
Y_i = \alpha + \tau D_i + \gamma X_i + \epsilon_i
\]

where \(D_i\) is a binary treatment variable, then \(\tau\) can be interpreted as a treatment effect only under strong assumptions, such as no unobserved confounding after controlling for \(X_i\). In that case, the coefficient can be understood as the relationship between the residualized outcome and the residualized treatment after removing the variation explained by confounders.

That is not what this paper is doing.

Here, there is no binary treatment variable and no causal identification design. The regression coefficients should be interpreted as **statistical associations** within the selected model. For example, the coefficient on maximum wind speed means:

> Holding the other selected predictors fixed, a one-standard-deviation increase in maximum wind speed during large fires is associated with a certain increase in annual mean large fire duration.

This does not prove that wind speed alone causally increased fire duration. The more careful interpretation is that maximum wind speed is a strong **model predictor** of fire duration trends and variability.

### 9.5 Can Regression Coefficients Tell Us Which Variable Is the “Most Important Predictor”?

They can, but only under certain conditions.

If predictors are not standardized, coefficient magnitudes cannot be directly compared because variables have different units and scales. For example, wind speed may be measured in m/s, precipitation in mm, VPD in kPa, elevation in meters, and LAI as a dimensionless index. Changing the unit of a variable can change the numerical coefficient without changing its physical importance.

To compare coefficient magnitudes more meaningfully, predictors should be standardized:

\[
x^\* = \frac{x - \bar{x}}{\sigma_x}
\]

After standardization, one unit of each predictor means one standard deviation. Then the coefficient measures the change in \(y\) associated with a one-standard-deviation increase in that predictor.

This paper standardizes all predictors before fitting the MLR models. Therefore, the authors can more reasonably compare coefficient magnitudes and state that maximum wind speed during large fires has the largest standardized coefficient.

However, “most important predictor” can mean different things, including:

1. largest standardized regression coefficient,
2. largest decrease in model performance when removed,
3. most frequently selected by AIC-based model selection,
4. largest improvement in out-of-sample prediction,
5. strongest causal effect.

This paper mainly supports the first few meanings, not the fifth.

### 9.6 Different Meanings of “Variable Importance”

It is useful to separate several concepts that are often mixed together.

#### 1. Standardized Regression Coefficient

A standardized coefficient measures how much the outcome changes when a predictor increases by one standard deviation, holding other selected predictors fixed.

This is the interpretation most directly connected to the regression table in this paper. Since the predictors are normalized, the coefficient magnitudes are more comparable.

#### 2. Contribution to Model \(R^2\)

A variable can be considered important if removing it causes a large drop in \(R^2\), meaning the model explains much less variance without it.

This is related to predictive/explanatory contribution. It asks:

> How much does this variable help the model explain the observed variability?

This is not exactly the same as having the largest coefficient. A variable may have a large coefficient but contribute less to \(R^2\) if it overlaps strongly with other predictors or has limited independent variation.

#### 3. Frequency of Selection by Stepwise/AIC Models

A variable may be important if it repeatedly appears in the best AIC-selected models. This suggests that the variable provides useful information even after accounting for model complexity.

In this paper, wind-related variables repeatedly appear in the best models, which strengthens the claim that wind is an important predictor.

#### 4. Out-of-Sample Predictive Importance

A variable can also be important if it improves prediction on data not used to fit the model, such as in cross-validation.

This is different from contribution to \(R^2\) in the fitted model. A variable may improve in-sample \(R^2\) but fail to improve out-of-sample prediction if it mainly captures noise. Out-of-sample importance focuses on generalizability.

The difference between **2** and **4** is important:

- **Contribution to model \(R^2\)** usually refers to how much the variable helps explain the data used in the fitted model.
- **Out-of-sample predictive importance** asks whether the variable helps predict new or withheld data.

Thus, 2 is more about in-sample explanatory power, while 4 is more about predictive robustness.

#### 5. Causal Importance

A variable is causally important if changing that variable would change the outcome, all else equal.

This is the strongest interpretation, but it requires a causal design, natural experiment, intervention, instrumental variable, randomized experiment, or process-based modeling experiment. A statistical regression alone usually cannot establish this.

#### 6. Physical or Mechanistic Importance

A variable may also be important because it has a clear physical mechanism. For fire behavior, wind speed is mechanistically relevant because strong winds can increase fire spread rate, enhance oxygen supply, tilt flames, promote spotting, and make suppression harder.

This mechanistic plausibility makes the statistical relationship more convincing, but it still does not by itself prove causality in the observational regression.

### 9.7 My Interpretation

My interpretation is that this paper provides strong evidence that maximum wind speed during large fires is tightly associated with the observed increase in large fire duration. The result is physically plausible and statistically robust in the main gridMET-based analysis, especially for summer.

However, I should be careful not to overstate the conclusion. The paper does not prove that increasing wind speed is the sole causal driver of longer large-fire duration. Fire duration is measured using containment dates, which are influenced by both fire behavior and human management. Also, the authors themselves suggest that the increase in maximum wind speed during large fires may partly reflect fire-atmosphere feedbacks, where larger or longer fires generate stronger local winds.

A careful summary would be:

> Wang et al. (2025) identify maximum daily wind speed during large fires as the strongest standardized predictor of increasing large-fire duration in the western US. The result suggests an important role for wind extremes and possible fire-atmosphere feedbacks, but the observational regression framework does not by itself establish a causal effect of wind speed on fire duration.
