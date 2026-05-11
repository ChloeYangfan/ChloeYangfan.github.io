title: Kelp et al. (2025) – Prescribed Burning, Burn Severity, and Smoke Emissions
parent: Literature
nav_order: 1

Kelp et al. (2025) – Effect of Recent Prescribed Burning and Land Management on Wildfire Burn Severity and Smoke Emissions in the Western United States

Date: 2026-05-11

Source

Title: Effect of Recent Prescribed Burning and Land Management on Wildfire Burn Severity and Smoke Emissions in the Western United States
Authors: Makoto Kelp, Marshall Burke, Minghao Qiu, Iván Higuera-Mendieta, Tianjia Liu, Noah S. Diffenbaugh
Journal: AGU Advances
DOI: 10.1029/2025AV001682

Why I read this

I read this paper because it directly asks whether recent prescribed burning actually reduces the severity and smoke emissions of later wildfires, and because it uses a quasi-experimental design that is much closer to causal inference than a simple treated-versus-untreated comparison.

Core idea

The core logic of the paper is to compare places that were recently treated with prescribed fire to adjacent untreated areas of equal size that later burned in the same 2020 wildfires. The authors use this local comparison to estimate what burn severity and smoke emissions in the treated areas would likely have been if prescribed fire had not occurred. Their identifying assumption is that, conditional on nearby controls and observed covariates, treated pixels would have behaved like adjacent untreated pixels in the absence of treatment.  ￼  ￼

Main research questions

This paper asks two main questions:

1. Does prescribed burning reduce the burn severity of later wildfires?
2. Although prescribed burning produces smoke itself, does it reduce later wildfire PM2.5 emissions enough to create a net reduction in total smoke?

The study focuses on the 2020 extreme wildfire season. Treatments occurred from October 2018 to May 2020, and outcomes were measured during the 2020 wildfire season (July–November 2020). Burn severity analysis covers the western US, while the smoke PM2.5 emissions analysis is restricted to California because the high-resolution WBSE emissions product is only available there. The paper identifies 186 unique NFPORS treatments intersecting 14 wildfires, with 6 California fires included in the PM2.5 analysis.  ￼  ￼

Data, variables, time range, and spatial range

1. Prescribed burn / treatment data

The main treatment dataset is NFPORS (National Fire Plan Operations and Reporting System). It records treatment point locations, acreage, whether treatment occurred in the WUI, and treatment category such as Rx fire or mechanical thinning. Since 2018, the database mainly provides point locations plus acreage, rather than exact treatment polygons, which is why the authors construct circular treatment buffers themselves.  ￼

For robustness, the authors also use the CAL FIRE Rx fire perimeter dataset, which contains more precise prescribed burn perimeters but covers fewer treatments. For example, inside the Creek Fire perimeter, NFPORS reports 115 unique treatments, whereas CAL FIRE reports 36 treatment perimeters.  ￼

2. Wildfire perimeter / burn area data

Wildfire perimeters come from MTBS (Monitoring Trends in Burn Severity), which uses 30 m Landsat imagery to define final wildfire perimeters and burn severity for large fires in the western US. MTBS is used here mainly to identify which prescribed burn treatments later overlapped with 2020 wildfire perimeters.  ￼

3. Burn severity variable

The main burn severity outcome is dNBR, derived from Sentinel-2A Level 2A imagery in Google Earth Engine. The authors use imagery from 2 weeks before and 2 weeks after wildfire occurrence, mask out pixels with cloud probability above 65%, compute NBR, and then compute:

dNBR = NBR_pre-fire − NBR_post-fire

Higher dNBR means higher burn severity. The final product is resampled to 30 m, and pixels with dNBR ≤ 0 are excluded.  ￼

4. Smoke emissions variable

Wildfire PM2.5 emissions are estimated using WBSE (Wildfire Burn Severity and Emissions Inventory), a severity-based emissions inventory that combines Landsat dNBR, MODIS/VIIRS active fire detections, vegetation type, and California-specific emission factors. WBSE provides 30 m event-based emissions estimates but only for California fires.  ￼

PM2.5 emissions from prescribed burning itself are estimated using a reclassified FINNv2.2 source-specific inventory. This product provides daily 1 km Rx fire emissions across California and is used to calculate the net smoke effect after including prescribed burn emissions themselves.  ￼

5. Control variables

The regressions use controls including:

* WUI indicator
* land cover type
* previous fire history

The land cover and elevation datasets are NLCD 2019 and NASADEM, both at 30 m resolution. Land cover is grouped into forest, shrub, and barren. Past fire history is included to control for legacy effects from earlier burns.  ￼  ￼

How the causal inference works

The most important point is that the authors do not simply compare all treated areas to all untreated areas. Instead, they use a quasi-experimental local comparison.

Step 1: Identify treated areas

They select NFPORS Rx fire treatments from October 2018 to May 2020 that later fall within 2020 wildfire perimeters. So the treated units are places that were treated first and then reburned during the 2020 wildfire season.  ￼

Step 2: Construct treatment and control buffers

Because NFPORS gives points plus acreage rather than exact polygons, the authors construct a circular treatment buffer around each treatment point whose area equals the reported treatment acreage.

They then define a control buffer as a concentric ring outside the treated circle, also with area equal to the treatment acreage, excluding the treated area itself. This means treated and control areas are adjacent and equally sized.  ￼

Step 3: Randomly sample pixels

Within each treatment buffer and control buffer, the authors generate 1,000 random points and extract dNBR, PM2.5 emissions, and covariates such as land cover and elevation.  ￼

Step 4: Estimate treatment effects with fixed effects regression

They estimate

y_id = βD_id + λX_id + α_d + ε_id

where:

* y_id is either dNBR or PM2.5 emissions
* D_id indicates whether the pixel was treated
* X_id includes controls such as WUI, land cover, and previous fire history
* α_d is a treatment-area fixed effect for each treatment-control pair

The fixed effects are crucial because they ensure that comparison happens within each local treated-control pair, rather than comparing treated pixels in one location to control pixels far away. Standard errors are clustered at the treatment level.  ￼

Step 5: Robustness and placebo tests

The authors check robustness by:

* expanding treatment and control buffers by one-third
* comparing their circular-buffer method to more precise CAL FIRE perimeters
* conducting placebo tests with 100 random hypothetical treatment locations per fire

If the real estimate lies well outside the placebo distribution, that suggests the result is unlikely to be caused by random spatial variation within wildfire burn scars.  ￼  ￼  ￼

Main results

The main result is that recent prescribed burning reduced later wildfire impacts.

Across the western US, Rx fire-treated areas had about −16% lower burn severity than adjacent untreated controls. In California, Rx fire-treated areas had −101 kg acre⁻¹ lower wildfire PM2.5 emissions, though the PM2.5 estimate is only marginally significant (p < 0.1). When prescribed burn emissions themselves are included, the authors estimate an overall −14% net reduction in PM2.5 emissions. They further project that treating 1 million acres annually in California could reduce PM2.5 emissions by 655,000 tons over 5 years, about 52% of 2020 wildfire emissions.  ￼  ￼  ￼

The paper also finds that:

* Rx fire is more effective than mechanical thinning
* treatment effects are stronger outside the WUI
* forest treatments reduce both burn severity and smoke more clearly
* WUI treatments are weaker partly because WUI treatments rely more on mechanical thinning and because prescribed burning is more constrained near people and infrastructure.  ￼

Figure-by-figure notes

Figure 1 – Study design

Figure 1 illustrates the identification strategy using the Creek Fire. The main map shows 30 m dNBR within the Creek Fire perimeter, where darker red indicates more severe burning. Blue dots mark NFPORS Rx fire treatment locations. The insets show how the authors construct a circular treatment buffer and an adjacent equal-area control buffer. The key message is that the comparison is very local: treated pixels are compared with nearby untreated pixels immediately outside the treated area, rather than with distant controls. The figure and caption on page 5 make this design especially clear.  ￼

Figure 2 – Main estimates and robustness

Figure 2a gives the headline treatment effects: Rx fire lowers both burn severity and PM2.5 emissions during the 2020 wildfire season, with stronger evidence for burn severity than for emissions.

Figure 2b compares three ways of defining treatment boundaries:

* NFPORS circular buffers
* CAL FIRE exact perimeters
* overlap subset of NFPORS within CAL FIRE perimeters

The CAL FIRE perimeter analysis shows a larger estimated effect, especially for PM2.5, suggesting that the circular-buffer approximation from NFPORS likely dilutes the true treatment effect because it is spatially less precise.

Figure 2c shows the placebo test. The placebo treatment-effect distribution is centered near zero, while the real estimate lies outside that distribution, indicating that the observed effects are unlikely to be explained by random spatial variation within fire scars.  ￼  ￼

Figure 3 – Heterogeneity by treatment type, land cover, and WUI

Figure 3a shows that Rx fire reduces burn severity much more than mechanical thinning.

Figure 3b shows that treatment generally lowers PM2.5 emissions too, though with larger uncertainty.

Figure 3c further breaks results down by treatment type and WUI status. The clearest message is that Rx fire outside the WUI is most effective, while treatment effects inside the WUI are weaker. This is consistent with the fact that treatments inside the WUI rely more heavily on mechanical thinning.  ￼

Figure 4 – Net smoke effect and scaling projection

Figure 4a combines Rx fire emissions and avoided later wildfire emissions for the Creek and Slater Fires. It shows that prescribed burning emits PM2.5 itself, but the reduction in later wildfire smoke is larger, producing a net smoke savings.

Figure 4b addresses the fact that not every treated area will soon reburn in a wildfire. Using the reclassified FINNv2.2 data, the authors estimate that about 75% of treated land later burns within the period they analyze. Even after adjusting for this, net smoke savings remain positive.

Figure 4c scales the estimate to California’s policy goal of treating 1 million acres and concludes that the resulting net PM2.5 reduction could be very large relative to emissions from the 2020 wildfire season.  ￼  ￼

My interpretation

This paper’s causal claim rests on a local counterfactual comparison: within the same 2020 wildfire burn scar, compare a recently treated Rx fire area to an adjacent untreated area of equal size. After controlling for land cover, WUI status, previous fire history, and pair-specific fixed effects, the treated-control difference is interpreted as the effect of prescribed burning.

The key substantive conclusion is that recent prescribed burning appears to reduce later wildfire burn severity in the western US and likely reduce wildfire PM2.5 emissions in California as well. Even when prescribed burn smoke is included, the paper argues that the overall smoke effect is still net beneficial.  ￼  ￼  ￼

Questions / caveats I want to remember

* The emissions analysis is limited to California because WBSE only covers California fires.
* NFPORS lacks exact treatment polygons, so circular buffers may introduce spatial misclassification.
* PM2.5 results are weaker statistically than burn severity results.
* The net-emissions estimate combines two inventories with different resolutions and methodologies: WBSE for wildfire emissions and reclassified FINNv2.2 for Rx fire emissions. The paper explicitly notes this as a limitation.  ￼

