---
title: Kelp et al. (2025) – Prescribed Burning, Burn Severity, and Smoke Emissions
parent: Literature
nav_order: 1
---

# Kelp et al. (2025) – Effect of Recent Prescribed Burning and Land Management on Wildfire Burn Severity and Smoke Emissions in the Western United States

**Date:** 2026-05-11

## Source

**Title:** *Effect of Recent Prescribed Burning and Land Management on Wildfire Burn Severity and Smoke Emissions in the Western United States*  
**Authors:** Makoto Kelp, Marshall Burke, Minghao Qiu, Iván Higuera-Mendieta, Tianjia Liu, and Noah S. Diffenbaugh  
**Journal:** *AGU Advances*  
**DOI:** [10.1029/2025AV001682](https://doi.org/10.1029/2025AV001682)

## Why I read this

I read this paper because it directly asks whether recent prescribed burning actually reduces the severity and smoke emissions of later wildfires, and because it uses a quasi-experimental design that is much closer to causal inference than a simple treated-versus-untreated comparison.

## Core idea

The core logic of the paper is to compare places that were recently treated with prescribed fire to adjacent untreated areas of equal size that later burned in the same 2020 wildfires. The authors use this local comparison to estimate what burn severity and smoke emissions in the treated areas would likely have been if prescribed fire had not occurred.

## Main research questions

This paper asks two main questions:

1. Does prescribed burning reduce the burn severity of later wildfires?
2. Although prescribed burning produces smoke itself, does it reduce later wildfire PM2.5 emissions enough to create a net reduction in total smoke?

The study focuses on the 2020 extreme wildfire season. Treatments occurred from October 2018 to May 2020, and outcomes were measured during the 2020 wildfire season from July to November 2020.

## Spatial and temporal scope

- Burn severity analysis covers the western US.
- Smoke PM2.5 emissions analysis is restricted to California because the WBSE emissions product only covers California fires.
- The paper identifies 186 unique NFPORS treatments intersecting 14 wildfires, with 6 California fires included in the emissions analysis.

## Data and variables

### Treatment / prescribed burn data

The main treatment dataset is NFPORS (National Fire Plan Operations and Reporting System). It records treatment point locations, acreage, whether the treatment occurred in the WUI, and treatment category such as Rx fire or mechanical thinning. Since 2018, the database mainly provides point locations plus acreage rather than exact treatment polygons, so the authors construct circular treatment buffers.

For robustness, the authors also use the CAL FIRE Rx fire perimeter dataset, which contains more precise prescribed burn perimeters but covers fewer treatments.

### Wildfire perimeter data

Wildfire perimeters come from MTBS (Monitoring Trends in Burn Severity), which uses 30 m Landsat imagery to define wildfire perimeters and burn severity for large fires in the western US.

### Burn severity outcome

The main burn severity variable is dNBR, derived from Sentinel-2A Level 2A imagery processed in Google Earth Engine.

The authors:
- use imagery from 2 weeks before and 2 weeks after wildfire occurrence,
- exclude pixels with cloud probability above 65%,
- calculate NBR,
- then compute dNBR = NBR_pre-fire - NBR_post-fire.

Higher dNBR indicates higher burn severity. The final product is resampled to 30 m, and pixels with dNBR less than or equal to 0 are excluded.

### Smoke emissions outcome

Wildfire PM2.5 emissions are estimated using WBSE (Wildfire Burn Severity and Emissions Inventory), a severity-based emissions inventory combining Landsat dNBR, MODIS/VIIRS fire detections, vegetation type, and California-specific emission factors. WBSE provides 30 m event-based emissions estimates for California fires.

Prescribed burn PM2.5 emissions are estimated using a reclassified FINNv2.2 source-specific inventory. This product provides daily 1 km Rx fire emissions across California and is used to estimate net smoke effects after including prescribed burn emissions themselves.

### Control variables

The regressions include controls for:
- WUI status,
- land cover type,
- previous fire history.

Additional datasets include:
- NLCD 2019 for land cover,
- NASADEM for elevation.

## How the causal inference works

The authors do not simply compare all treated areas to all untreated areas. Instead, they use a quasi-experimental local comparison design.

### Step 1: identify treated areas

They select NFPORS Rx fire treatments from October 2018 to May 2020 that later fall within 2020 wildfire perimeters. These are the treated areas.

### Step 2: construct treatment and control buffers

Because NFPORS provides only points plus acreage, the authors construct a circular treatment buffer around each treatment point whose area equals the reported treatment acreage.

They then define a control buffer as a concentric ring outside the treatment circle, also with area equal to the treatment acreage, excluding the treated area itself.

### Step 3: random pixel sampling

Within each treatment buffer and control buffer, the authors generate 1,000 random points and extract dNBR, PM2.5 emissions, and covariates such as land cover and elevation.

### Step 4: regression with fixed effects

They estimate:

y_id = βD_id + λX_id + α_d + ε_id

where:
- y_id is either dNBR or PM2.5 emissions,
- D_id indicates whether the pixel was treated,
- X_id includes controls such as WUI, land cover, and previous fire history,
- α_d is a treatment-area fixed effect for each treatment-control pair.

The fixed effects are crucial because they ensure that comparison happens within each local treated-control pair, rather than comparing treated pixels in one location to control pixels far away.

### Step 5: robustness and placebo tests

The authors test robustness by:
- expanding treatment and control buffers,
- comparing NFPORS circular buffers with CAL FIRE exact perimeters,
- conducting placebo tests with randomly generated fake treatment locations.

## Main results

The headline results are:

- Rx fire-treated areas had about 16% lower burn severity than adjacent untreated controls across the western US.
- In California, Rx fire-treated areas had 101 kg acre⁻¹ lower wildfire PM2.5 emissions on average, though this estimate is statistically weaker.
- After including prescribed burn emissions themselves, the authors estimate an overall net reduction of 14% in PM2.5 emissions.

The paper also finds that:
- Rx fire is more effective than mechanical thinning.
- Treatment effects are stronger outside the WUI.
- Forest treatments reduce burn severity and smoke more clearly than some other land cover types.

## Figure-by-figure notes

### Figure 1 – Study design

Figure 1 illustrates the identification strategy using the Creek Fire. The map shows 30 m dNBR within the Creek Fire perimeter, where darker red indicates more severe burning. Blue dots mark NFPORS Rx fire treatment locations. Insets show the circular treatment buffer and the adjacent equal-area control buffer. The key message is that the comparison is very local.

### Figure 2 – Main estimates and robustness

Figure 2a shows the main treatment effects: Rx fire lowers both burn severity and PM2.5 emissions, with stronger evidence for burn severity than for emissions.

Figure 2b compares three treatment-boundary definitions:
- NFPORS circular buffers,
- CAL FIRE exact perimeters,
- overlap subset of NFPORS within CAL FIRE perimeters.

The CAL FIRE perimeter analysis gives a larger estimated effect, suggesting that the circular-buffer approximation may dilute the true treatment effect.

Figure 2c presents the placebo test. The placebo treatment-effect distribution is centered near zero, while the real estimate lies outside that distribution.

### Figure 3 – Heterogeneity

Figure 3 shows that:
- Rx fire reduces burn severity much more than mechanical thinning.
- Treatment generally lowers PM2.5 emissions too, though with larger uncertainty.
- Rx fire outside the WUI is the most effective combination.

### Figure 4 – Net smoke effect and scaling projection

Figure 4a combines Rx fire emissions and avoided later wildfire emissions for the Creek and Slater Fires and shows a net smoke savings.

Figure 4b accounts for the fact that not every treated area will soon reburn in a wildfire. Even after adjusting for this, net smoke savings remain positive.

Figure 4c scales the results to California’s policy goal of treating 1 million acres and suggests that the resulting net PM2.5 reduction could be very large relative to 2020 wildfire emissions.

## My interpretation

This paper’s causal claim rests on a local counterfactual comparison: within the same 2020 wildfire burn scar, compare a recently treated Rx fire area to an adjacent untreated area of equal size. After controlling for land cover, WUI status, previous fire history, and pair-specific fixed effects, the treated-control difference is interpreted as the effect of prescribed burning.

The main substantive conclusion is that recent prescribed burning appears to reduce later wildfire burn severity in the western US and likely reduce wildfire PM2.5 emissions in California as well. Even when prescribed burn smoke is included, the paper argues that the overall smoke effect remains net beneficial.

## Caveats I want to remember

- The emissions analysis is limited to California because WBSE only covers California fires.
- NFPORS lacks exact treatment polygons, so circular buffers may introduce spatial misclassification.
- PM2.5 results are statistically weaker than burn severity results.
- The net-emissions estimate combines two inventories with different resolutions and methodologies: WBSE for wildfire emissions and reclassified FINNv2.2 for Rx fire emissions.
